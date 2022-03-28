---
id: 155
title: 'WordPress as a semantic web platform?'
date: '2015-08-12T08:53:00+01:00'
author: 'Phil Barker'
excerpt: 'For&nbsp;the work we&rsquo;ve been doing on semantic description of courses we needed a platform for creating and editing instance data flexibly&nbsp;and easily. We looked at callimachus&nbsp;and Semantic MediaWiki; in the end we went with the latter because of JAVA version incompatibility problems with the other, but it has been a bit of a struggle. I&rsquo;ve &hellip; <a href="http://blogs.pjjk.net/phil/wordpress-as-a-semantic-web-platform/">Continue reading <span>WordPress as a semantic web platform?</span> <span>&rarr;</span></a>'
layout: post
guid: 'http://blogs.pjjk.net/phil/?p=1450'
permalink: 'http://blogs.pjjk.net/phil/wordpress-as-a-semantic-web-platform/'
enclosure:
    - "\n\n"
syndication_source:
    - 'Sharing and learning'
syndication_source_uri:
    - 'http://blogs.pjjk.net/phil'
syndication_source_id:
    - 'http://blogs.pjjk.net/phil/feed/'
'rss:comments':
    - 'http://blogs.pjjk.net/phil/wordpress-as-a-semantic-web-platform/#comments'
'wfw:commentRSS':
    - 'http://blogs.pjjk.net/phil/wordpress-as-a-semantic-web-platform/feed/'
syndication_feed:
    - 'http://blogs.pjjk.net/phil/feed/'
syndication_feed_id:
    - '2'
syndication_permalink:
    - 'http://blogs.pjjk.net/phil/wordpress-as-a-semantic-web-platform/'
syndication_item_hash:
    - 31ee33eb7bb51ddfc565446fb40837f0
    - c4e84916df53c764484083e422f2f845
    - ad382f657f0c80675b39db64c9f6cef2
    - ad382f657f0c80675b39db64c9f6cef2
    - 29a993412ad21efd856eb49a7255279a
    - 29a993412ad21efd856eb49a7255279a
    - 00dac428b03fa3b6c47ac2ce169dc2f8
    - 0f393048b313614fdb94ca7b444fac51
    - 3535e8fe9df1373acdd3300212c31138
categories:
    - cetis
    - WordPress
---

For the work we’ve been doing on [semantic description of courses](http://blogs.pjjk.net/phil/two-projects-about-describing-courses/) we needed a platform for creating and editing instance data flexibly and easily. We looked at [callimachus](http://callimachusproject.org/) and [Semantic MediaWiki](https://semantic-mediawiki.org/); in the end we went with the latter because of JAVA version incompatibility problems with the other, but it has been a bit of a struggle. I’ve used WordPress for publishing information about resources on a couple of projects, for [Cetis publications](http://blogs.pjjk.net/phil/cetis-publications-now-on-wordpress/) and for [learning resources](https://deloresoer.wordpress.com/2011/08/11/wordpress-for-hosting-and-describing-learning-resources/), and have been very happy with it. WordPress handles the general task of publishing stuff on the web really well, it is easily extensible through plugins and themes, I have nearly always found plugins that allow me to do what I want and themes that with a little customization allow me to present the information how I want. As a piece of open source software it is used on a massive scale (about a [quarter of all web domains](http://w3techs.com/technologies/overview/content_management/all) use it) and has the development effort and user support to match. For the previous projects my approach was to have a post for each resource I wanted to describe and to set the title, publication date and author to be those for the resource, I used the main body of the post for a description and used tags and categories for classification, e.g. by topic or resource type; other metadata could be added using WordPress’s [Custom Fields](https://codex.wordpress.org/Custom_Fields), more or less as free text name-value pairs. While I had modified themes so that the semantics of some of this information was marked up with microdata or RDFa embedded in the HTML, I was aware that WordPress allowed for more than I was doing.

The possibility of using WordPress for creating and publishing semantic data hinges on two capabilities that I hadn’t used before: firstly the ability to create custom post types so that for each resource type there can be a corresponding post type; secondly the ability to create custom metadata fields that go beyond free text. I used these in conjunction with a theme which is a child theme of the current default, TwentyFifteen, which sets up the required custom types and displays them. Because I am familiar with it and it is quite general purpose, I chose the schema.org ontology to implement, but I think the ideas in this post would be applicable to any RDF vocabulary. When creating examples I had in mind a dataset describing the books that I own and the authors I am interested in.

I started by using a plugin, [Custom Post Type UI](https://wordpress.org/plugins/custom-post-type-ui/), to create the post types I wanted but eventually was doing enough in php as a theme extensions (see below) that it made sense just to add a function to create the the post types. This drops the dependency on the plugin (though it’s a good one) and means the theme works from the outset without requiring custom types to be set up manually.

```
<pre class="brush: php; title: ; notranslate">
add_action( 'init', 'create_creativework_type' );
function create_creativework_type() {
  register_post_type( 'creativework',
    array(
      'labels' => array(
        'name' => __( 'Creative Works' ),
        'singular_name' => __( 'Creative Work' )
      ),
      'public' => true,
      'has_archive' => true,
      'rewrite' => array('slug' => 'creativework'),
      'supports' => array('title', 'thumbnail', 'revisions' )
    )
  );
}
```

The key call here is to the WP function [register\_post\_type()](https://codex.wordpress.org/Function_Reference/register_post_type) which is used to create a post type with the same name as the schema.org resource type / class; so I have one of these for each of the schema.org types I use (so far Thing, CreativeWork, Book and Person). This is hooked into the WordPress init process so it is done by the time you need those post types.

I do use a plugin to help create the custom metadata fields for every property except the name property (for which I use the title of the post). [Meta Box](https://wordpress.org/plugins/meta-box/) extends the WordPress API with some functions that make creating metadata fields in php much easier. These metadata fields can be tailored for particular data types, e.g. text, dates, numbers, urls and, crucially, links to other posts. That last one gives you what you need for to create relationships between the resources you describe in WordPress, which can expressed as triples. Several of these custom fields can be grouped together into a “meta box” and attached as a group to specific post types so that they are displayed when editing posts of those types. Here’s what declaring a custom metadata field for the author relationship between a CreativeWork and a Person looks like with MetaBox (for simplicity I’ve omitted the code I have for declaring the other properties of a Creative Work and some of the optional parameters). I’m using the author property as an example because a repeatable link to another resource is about as complicated a property as you get.

```
<pre class="brush: php; title: ; notranslate">
function semwp_register_creativework_meta_boxes( $meta_boxes )
{
    $prefix = 'semwp_creativework_';

    // 1st meta box
    $meta_boxes[] = array(
        'id'         => 'main_creativework_info',
        'title'      => __( 'Main properties of a schema.org Creative Work', 'semwp_creativework_' ),
        // attach this box to the following post types
        'post_types' => array('creativework', 'book' ),

	// List of meta fields
	'fields'     => array(
            // Author
            // Link to posts of type Person.
            array(
                'name'        => __( 'Author (person)', 'semwp_creativework_' ),
                'id'          => "{$prefix}authors",
                'type'        => 'post',
                'post_type'   => 'person',
                'placeholder' => __( 'Select an Item', 'semwp_creativework_' ),
            // set clone to true for repeatable fields
            'clone' => true
            ),
        ),
    );
    return $meta_boxes;
}

```

What this gives when editing a post of type book is this:

[![semwpeditshot](http://blogs.pjjk.net/phil/content/uploads/semwpeditshot-411x480.png)](http://blogs.pjjk.net/phil/content/uploads/semwpeditshot.png)

WordPress uses a series of nested templates to display content, which are defined in the theme and can either be specific to a post type or generic, the generic ones being used as a fall back if a more specific one does not exist. As I mentioned I use a child theme of TwentyFifteen which means that I only have to include those files that I change from the parent. To display the main content of posts of type book I need a file called content-book.php (the rest of the page is common to all types of post), which looks like this

```
<pre class="brush: xml; title: ; notranslate">

<article resource="?<?php the_ID() ; ?>#id" id="?<?php the_ID(); ?>" <?php post_class(); ?> vocab="http://schema.org/" typeof="Book">

<header class="entry-header">
    <?php
        if ( is_single() ) :
            the_title( '<h1 class="entry-title" property="name">', '</h1>' );
        else :
            the_title( sprintf( '<h2 class="entry-title"><;a href="%s" rel="bookmark">', esc_url( get_permalink() ) ), '</a></h2>;' );
        endif;
    ?>
</header>
<div class="entry-content">
    <?php semwp_print_creativework_author(); ?>
    <?php semwp_print_book_bookEdition(); ?>
    <?php semwp_print_book_numberOfPages(); ?>
    <?php semwp_print_book_isbn(); ?>
    <?php semwp_print_book_illustrator(); ?>
    <?php semwp_print_creativework_datePublished(); ?>
    <?php semwp_print_book_bookFormat(); ?>
    <?php semwp_print_creativework_sameAs(); ?></div>
<footer class="entry-footer">
    <?php twentyfifteen_entry_meta(); ?>
    <?php edit_post_link( __( 'Edit', 'twentyfifteen' ), '<span class="edit-link">', '</span>' ); ?>
    <?php semwp_print_extract_rdf_links(); ?>
</footer>

</article>

```

Note the RDFa in some of the html tags, for example the &lt;article&gt; tag includes

```
resource= [url]#id vocab="http://schema.org/" typeof="Book"
```

and the title is output in an &lt;h1&gt; tag with the

```
property="name"
```

attribute. Exposing semantic data as RDFa is one (good) thing, but what about other formats? A useful web service called [RDF Translator](http://rdf-translator.appspot.com/) helps here. It has an API which allowed me to put a link at the foot of each resource page to the semantic data from that page in formats such as RDF/XML, N3 and JSON-LD; it’s quite not what you would want for fully fledged semantic data publishing but it does show the different views of the data that can be extracted from what is published.

Also note that most of the content is printed through calls to php functions that I defined for each property, semwp\_print\_creativework\_author() looks like this (again a repeatable link to another resource is about as complex as it gets:

```
<pre class="brush: php; title: ; notranslate">
function semwp_print_alink($id) {
     if (get_the_title($id))       //it's a object with a title
     {
         echo sprintf('<a property="url" href="%s"><span property="name">%s</span></a>', esc_url(get_permalink($id)), get_the_title($id) );
     }
     else                          //treat it as a url
     {
         echo sprintf('<a href="%s">%s</a>', esc_url($id), $id );
     }
}
function semwp_print_creativework_author()
{
    if ( rwmb_meta( 'semwp_creativework_authors' ) )
    {
	echo '

By: ';
	$authors = rwmb_meta( 'semwp_creativework_authors' );
        foreach ( $authors as $author )
        {
               echo '<span property="author" typeof="Person">';
               semwp_print_alink($author);
               echo '</span>';
        }
        echo '

';
    }
}
```

So in summary, for each resource type I have two files of php/html code: one which sets up a custom post type, custom metadata fields for the properties of that type (and any other types which inherit them) and includes some functions that facilitate the output of instance data as HTML with RDFa; and another file which is the WordPress template for presenting that data. Apart from a few generally useful functions related to output as HTML and modifications to other theme files (mostly to remove embedded data which I found distracting) that’s all that is required.

The result looks like this:

<figure class="wp-caption aligncenter" id="attachment_1474" style="width: 640px">[![Note, this image is linked to the page on wordpress that is shows, click on it if you want to explore the little data that there is there, but please do be aware that it is a development site which won't always be working properly.](http://blogs.pjjk.net/phil/content/uploads/semwp_page_shot-640x480.png)](http://www.pjjk.net/semanticwp/book/the-day-of-the-triffids)<figcaption class="wp-caption-text">Note, this image is linked to the page on my WordPress install that it shows, click on it if you want to explore the little data that there is there, but please do be aware that it is a development site which won’t always be working properly.</figcaption></figure>And here’s the N3 rendering of the data in that page as converted by RDF Translator:

```
<span class="k">@prefix </span><span class="nv">rdf: </span><span class="nn"><http://www.w3.org/1999/02/22-rdf-syntax-ns#> .</span>
<span class="k">@prefix </span><span class="nv">rdfa: </span><span class="nn"><http://www.w3.org/ns/rdfa#> .</span>
<span class="k">@prefix </span><span class="nv">rdfs: </span><span class="nn"><http://www.w3.org/2000/01/rdf-schema#> .</span>
<span class="k">@prefix </span><span class="nv">schema: </span><span class="nn"><http://schema.org/> .</span>
<span class="k">@prefix </span><span class="nv">xml: </span><span class="nn"><http://www.w3.org/XML/1998/namespace> .</span>
<span class="k">@prefix </span><span class="nv">xsd: </span><span class="nn"><http://www.w3.org/2001/XMLSchema#> .</span>

<span class="nc"><http://www.pjjk.net/semanticwp/book/the-day-of-the-triffids></span><span class="o"> rdfa:usesVocabulary </span><span class="na">schema: </span>.

<span class="nc"><http://www.pjjk.net/semanticwp/book/the-day-of-the-triffids?36#id></span><span class="o"> a </span><span class="na">schema:Book </span>;
    <span class="o">schema:author </span>[<span class="o"> a </span><span class="na">schema:Person </span>;
            <span class="o">schema:name </span><span class="s">"John Wyndham"</span><span class="err">@</span><span class="na">en-gb </span>;
            <span class="o">schema:url </span><span class="na"><http://www.pjjk.net/semanticwp/person/john-wyndham></span> ] ;
    <span class="o">schema:bookEdition </span><span class="s">"Popular penguins (2011)"</span><span class="err">@</span><span class="na">en-gb </span>;
    <span class="o">schema:bookFormat </span><span class="err">""@</span><span class="na">en-gb </span>;
    <span class="o">schema:datePublished </span><span class="s">"2011-09-01"^^xsd:date </span>;
    <span class="o">schema:illustrator </span>[<span class="o"> a </span><span class="na">schema:Person </span>;
            <span class="o">schema:name </span><span class="s">"John Griffiths"</span><span class="err">@</span><span class="na">en-gb </span>;
            <span class="o">schema:url </span><span class="na"><http://www.pjjk.net/semanticwp/person/john-griffiths></span> ] ;
    <span class="o">schema:isbn </span><span class="s">"0143566539"</span><span class="err">@</span><span class="na">en-gb </span>;
    <span class="o">schema:name </span><span class="s">"The day of the triffids"</span><span class="err">@</span><span class="na">en-gb </span>;
    <span class="o">schema:numberOfPages </span><span class="na">256 </span>;
    <span class="o">schema:sameAs </span><span class="s">"http://www.amazon.co.uk/Day-Triffids-Popular-Penguins/dp/0143566539/"</span><span class="err">@</span><span class="na">en-gb</span><span class="err">,</span>
<span class="s">        "https://books.google.co.uk/books?id=zlqAZwEACAAJ"</span><span class="err">@</span><span class="na">en-gb </span>.
```

## Further work: Ideas and a Problem

There’s a ton of other stuff that I can think of that could be done with this, from the simple, e.g. extend the range of types supported, to the challenging, e.g. exploring ways of importing data or facilitating / automating the creation of new post types from known ontologies, output in other formats, providing a SPARQL end point &amp;c &amp;c… Also, I suspect that much of what I have implemented in a theme would be better done as a plugin.

<del datetime="2015-10-12T17:22:33+00:00">There is one big problem that I only vaguely see a way around, and that is illustrated above in the screenshot of the editing interface for the ‘about’ property. The schema.org/about property has an expected type of schema.org/Thing; schema.org types are hierarchical, which means the value for about can be a Thing or any subtype of Thing (which is to say of any type). This sort of thing isn’t unique to schema.org. However, the MetaBox plugin I use will only allow links to be made to posts of one specific type, and I suspect that reflects something about how WordPress organises posts of different custom types. I don’t think there is any way of asking it to show posts from a range of different types and I don’t think there is any way of saying that posts of type person are also of type thing and so on. In practice this means that at the moment I can only enter data that shows books as being about unspecific Things; I cannot, for example, say that a biography is a book about a Person. I can only see clunky ways around this.</del>   
**Update:** I noticed that you ***can*** pass an array of post types so that selection can be made from any one of them.

\[Aside: the big consumers of schema data (Google, Bing, Yahoo, Yandex) will also permit text values for most properties and try to make what sense of it they can, so you could say that for any property either a string literal or a link to another resource should be permitted. This, I think, is a peculiarity of schema.org. The screenshot above of the data input form shows that the about field is repeated to provide the option of a text-only value, an approach hinting at one of the clunky unscalable solutions to the general problem described above.\]

What next? I might set a student project around addressing some of these extensions. If you know a way around the selecting different type problem please do drop me a line. Other than that I can see myself extending this work slowly if it proves useful for other stuff, like creating examples of pages with schema.org or LRMI data in them. If anyone is really interested in the source code I could put it on github.

**Update** 02 Sep 2015:

I refactored the code so that most of the new php for creating new custom post types and setting up the forms to edit their properties is in plugin, and all the theme does is display the data entered with embedded RDFa.

The [code is now on GitHub](https://github.com/philbarker/semwp).

I did set a student project around extending it, waiting to see if any student opts for it.