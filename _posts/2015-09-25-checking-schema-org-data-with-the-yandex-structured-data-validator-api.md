---
id: 145
title: 'Checking schema.org data with the Yandex structured data validator API'
date: '2015-09-25T13:05:15+01:00'
author: 'Phil Barker'
excerpt: 'I have been writing examples of LRMI metadata for schema.org. Of course I want these to be valid, so I have been hitting various online validators quite frequently. This was getting tedious. Fortunately, the Yandex structured data validator has an API, so I could write a python script to automate the testing. Here it is &hellip; <a href="http://blogs.pjjk.net/phil/checking-schema-org-data-with-the-yandex-structured-data-validator-api/">Continue reading <span>Checking schema.org data with the Yandex structured data validator API</span> <span>&rarr;</span></a>'
layout: post
guid: 'http://blogs.pjjk.net/phil/?p=1534'
permalink: 'http://blogs.pjjk.net/phil/checking-schema-org-data-with-the-yandex-structured-data-validator-api/'
enclosure:
    - "\n\n"
syndication_source:
    - 'Sharing and learning'
syndication_source_uri:
    - 'http://blogs.pjjk.net/phil'
syndication_source_id:
    - 'http://blogs.pjjk.net/phil/feed/'
syndication_feed:
    - 'http://blogs.pjjk.net/phil/feed/'
syndication_feed_id:
    - '2'
syndication_permalink:
    - 'http://blogs.pjjk.net/phil/checking-schema-org-data-with-the-yandex-structured-data-validator-api/'
syndication_item_hash:
    - a099d1f79f5f5996424648ccb4ae0ce2
    - 589c533c06c336c7fe196c995c7b7f9e
    - e6e292cb0001c8e78bd0a31e08e75c93
    - e6e292cb0001c8e78bd0a31e08e75c93
    - f44d0a9b99a0b6a7e23351bb5948a8f7
categories:
    - LRMI
    - python
    - schema.org
---

I have been writing [examples of LRMI metadata](http://blogs.pjjk.net/phil/lrmi-examples-for-schema-org/) for schema.org. Of course I want these to be valid, so I have been hitting [various online validators](http://blogs.pjjk.net/phil/lrmi-schema-org-validation/) quite frequently. This was getting tedious. Fortunately, the [Yandex structured data validator has an API](https://tech.yandex.com/validator/), so I could write a python script to automate the testing.

Here it is

```
<pre class="brush: python; title: ; notranslate">
#!/usr/bin/python
import httplib, urllib, json, sys 
from html2text import html2text
from sys import argv

noerror = False

def errhunt(key, responses):                 # a key and a dictionary,  
    print "Checking %s object" % key         # we're going on an err hunt
    if (responses[key]):
        for s in responses[key]:             
            for object_key in s.keys(): 
                if (object_key == "@error"):              
                    print "Errors in ", key
                    for error in s['@error']:
                        print "tError code:    ", error['error_code'][0]
                        print "tError message: ", html2text(error['message'][0]).replace('n',' ')
                        noerror = False
                elif (s[object_key] != ''):
                    errhunt(object_key, s)
                else:
                    print "No errors in %s object" % key
    else:
        print "No %s objects" % key

try:
    script, file_name = argv 
except:
    print "tError: Missing argument, name of file to check.ntUsage: yandexvalidator.py filename"
    sys.exit(0)

try:
    file = open( file_name, 'r' )
except:
    print "tError: Could not open file ", file_name, " to read"
    sys.exit(0)

content = file.read()

try:
    validator_url = "validator-api.semweb.yandex.ru"
    key = "12345-1234-1234-1234-123456789abc"
    params = urllib.urlencode({'apikey': key, 
                               'lang': 'en', 
                               'pretty': 'true', 
                               'only_errors': 'true' 
                             })
    validator_path = "/v1.0/document_parser?"+params
    headers = {"Content-type": "application/x-www-form-urlencoded",
               "Accept": "*/*"}
    validator_connection = httplib.HTTPSConnection( validator_url )
except:
    print "tError: something went wrong connecting to the Yandex validator." 

try:
    validator_connection.request("POST", validator_path, content, headers)
    response = validator_connection.getresponse()
    if (response.status == 204):
        noerror= True
        response_data = response.read()   # to clear for next connection
    else:
        response_data = json.load(response)
    validator_connection.close()
except:
    print "tError: something went wrong getting data from the Yandex validator by API." 
    print "tcontent:n", content
    print "tresponse: ", response.read()
    print "tstatus: ", response.status
    print "tmessage: ", response.msg 
    print "treason: ", response.reason 
    print "n"

    raise
    sys.exit(0)

if noerror :
    print "No errors found."
else:
    for k in response_data.keys():
        errhunt(k, response_data)
```

Usage:

```
<pre class="brush: plain; title: ; notranslate">
$ ./yandexvalidator.py test.html
No errors found.
$ ./yandexvalidator.py test2.html
Checking json-ld object
No json-ld objects
Checking rdfa object
No rdfa objects
Checking id object
No id objects
Checking microformat object
No microformat objects
Checking microdata object
Checking http://schema.org/audience object
Checking http://schema.org/educationalAlignment object
Checking http://schema.org/video object
Errors in  http://schema.org/video
	Error code:     missing_empty
	Error message:  WARNING: Не выполнено обязательное условие для передачи данных в Яндекс.Видео: **isFamilyFriendly** field missing or empty  
	Error code:     missing_empty
	Error message:  WARNING: Не выполнено обязательное условие для передачи данных в Яндекс.Видео: **thumbnail** field missing or empty  
$ 
```

Points to note:

- I’m no software engineer. I’ve tested this against valid and invalid files. You’re welcome to use this, but it might not work for you. (You’ll need your own API key). If you see something needs fixing, drop me a line.
- Line 51: has to be an HTTPS connection.
- Line 58: we ask for errors only (at line 46) so no news is good news.
- The function errhunt does most of the work, recursively.

The response from the API is a json object (and json objects are converted into python dictionary objects by line 62), the keys of which are the “id” you sent and each of the structured data formats that are checked. For each of these there is an array/list of objects, and these objects are either simple key-value pairs or the value may be an array/list of objects. If there is an error in any of the objects, the value for the key “@error” gives the details, as a list of Error\_code and Error\_message key-value pairs. errhunt iterates and recurses through these lists of objects with embedded lists of objects.