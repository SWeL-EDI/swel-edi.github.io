---
id: 457
title: 'Cloning WordPress sites for development'
date: '2017-01-12T11:48:30+00:00'
author: 'Phil Barker'
excerpt: "<p>I do just enough theme and plugin development on WordPress to need an alternative to using a live WordPress site for development and testing, but at the same time I want to be testing on site as similar to the live site as possible. So I set up clones&nbsp;of WordPress sites either on my local &hellip; <a href=\"https://blogs.pjjk.net/phil/cloning-wordpress/\">Continue reading <span>Cloning WordPress sites for development</span> <span>&rarr;</span></a></p>\n<p>The post <a rel=\"nofollow\" href=\"https://blogs.pjjk.net/phil/cloning-wordpress/\">Cloning WordPress sites for development</a> appeared first on <a rel=\"nofollow\" href=\"https://blogs.pjjk.net/phil\">Sharing and learning</a>.</p>"
layout: post
guid: 'https://blogs.pjjk.net/phil/?p=1703'
permalink: 'https://blogs.pjjk.net/phil/cloning-wordpress/'
enclosure:
    - "\n\n"
syndication_source:
    - 'Sharing and learning'
syndication_source_uri:
    - 'https://blogs.pjjk.net/phil'
syndication_source_id:
    - 'http://blogs.pjjk.net/phil/feed/'
'rss:comments':
    - 'https://blogs.pjjk.net/phil/cloning-wordpress/#respond'
'wfw:commentRSS':
    - 'https://blogs.pjjk.net/phil/cloning-wordpress/feed/'
syndication_feed:
    - 'http://blogs.pjjk.net/phil/feed/'
syndication_feed_id:
    - '2'
syndication_permalink:
    - 'https://blogs.pjjk.net/phil/cloning-wordpress/'
syndication_item_hash:
    - 4c7b35f8dcd6d3384b91531954ff74ed
categories:
    - Other
    - WordPress
---

I do just enough theme and plugin development on WordPress to need an alternative to using a live WordPress site for development and testing, but at the same time I want to be testing on site as similar to the live site as possible. So I set up clones of WordPress sites either on my local machine or a server for development and testing. (Normally I have clones on the localhost server of couple of machines I use for development and another clone on a web accessible testing or staging server for other people to look at.) I don’t do this very often, but each time I do it I spend as much time trying to remember what it is I need to do as it actually takes to do it. So here, as much as an aide-memoire for myself as anything, else I’ve gathered it all in one place. What I do is largely based on the [Moving WordPress](https://codex.wordpress.org/Moving_WordPress) information in the codex, but there are a couple of things that doesn’t cover and a couple of things I find it easier to do differently.

Assuming that the [pre-requisites for WordPress](https://wordpress.org/about/requirements/) are in place (i.e. MySQL, webserver, PHP), there are three stages to creating a clone. A. copy the WordPress files to the development site; B. clone the database; C. fix the links between WordPress and the database for the new site. A and B are basically creating backup copies of your site, but you will want to make sure that whatever routine backups you use are up to date and ready to restore in case something goes wrong. Also, this assumes that you are notwant to clone just one site on a WordPress Multisite installation.

## Copying the WordPress files

Simply copy all the files from the folder you have WordPress installed in, and all the sub-folders to where you want the new site to be. This will mean that all the themes, plugins and uploaded media will be the same on both sites. Depending on whether the development site is on the same server as the main site I do this either with file manager or by making a compressed archive and ftp. Make sure the web server can read the files on the dev site (and write to the relevant folders if that is how you upload media, plugins and themes).

## Cloning the database

First I create a new, blank database on for the new site, either from the command line or using something like [MySQL Database Wizard](https://documentation.cpanel.net/display/ALD/MySQL+Database+Wizard) which my hosting provider has on CPanel. I create a new user with full access to that data base–the username and password for this user will be needed to configure WordPress with access to this database. If you have complete control of over the database name and user name then use the same name username and password as is in the [wp-config.php](https://codex.wordpress.org/Editing_wp-config.php) file of the site you are cloning. Otherwise you can change these later.

Second, I use [PHP MyAdmin](https://www.phpmyadmin.net/) to export the data base from the original site and import it to the one on which you are making a clone.

![phpMyAdmin Export screen](https://blogs.pjjk.net/phil/content/uploads/phpMyAdminExport-640x286.png)

## Fix all the bits that break

All that remains is to reconnect the PHP files to the database and fix a few other things that break. This is where it get fiddly. Also, from now on be really careful about which site you are working on: they look the same and you really don’t want to set up your public site as a development server. Make all these changes on the new development site.

In [wp-config.html](https://codex.wordpress.org/Editing_wp-config.php) (it’s in the top of the WordPress folder hierarchy) find the following lines and change the values to be those for your new development server and database.

```
define( 'WP_CONTENT_URL', 'http://example.org/blog' );
define( 'WP_CONTENT_DIR', 'path/to/wp-content' );

define('DB_NAME', 'databaseName');

/** MySQL database username */
define('DB_USER', 'databaseUserName');

/** MySQL database password */
define('DB_PASSWORD', 'password');
```

You might also need to change the value for DB\_HOST

Then you need to change the options that WordPress stores in the database. Normally you do this through the WordPress admin interface, but this is not yet available on your new site. There are [various ways you can do this](https://codex.wordpress.org/Changing_The_Site_URL), I [change the url directly in the data base](https://codex.wordpress.org/Changing_The_Site_URL#Changing_the_URL_directly_in_the_database) with PHPMyAdmin, either by direct editing as described in the codex page or from the command line [as described here](https://www.liberiangeek.net/2014/08/change-wordpress-home-site-url-via-mysql-database-servers/).

```
mysql -u root -p

USE databaseName
SELECT * FROM wp_options WHERE option_name = 'home';
UPDATE wp_options SET option_value="http://example.org/blog" WHERE option_name = "home";
SELECT * FROM wp_options WHERE option_name = 'siteurl';
UPDATE wp_options SET option_value="http://example.org/blog" WHERE option_name = "siteurl";
```

You should now have access to the new cloned site, though some things will still be misbehaving.

You will probably have the old site’s URL in various posts and GUIDs. I use the [better search replace](https://en-gb.wordpress.org/plugins/better-search-replace/) plugin to fix these.

iesiesIf you do any fancy redirects with .htaccess, make sure that these are written in such a way that works for the new URL.

If you are using Jetpack you will need to use it in [safe mode](https://jetpack.com/support/safe-mode/) if the development server is connected to the web or [development mode](https://jetpack.com/support/development-mode/) if running on localhost. (This is a bit of a pain if you want to test Jetpack settings.)

On a development site you’ll probably want to add this to wp-config.php:

```
define('WP_DEBUG', true);
```

If you are running a development or testing server on a web accessible site you probably want to restrict who has access to it. I use the [My private site](https://wordpress.org/plugins-wp/jonradio-private-site/) plugin so that only site admins have access.

## Keeping in sync

While it’s not entirely necessary that a development or testing site be kept completely in sync with the main one, it is worth keeping them close so that you don’t get unexpected issues on the main site. You can manually update the plugins and themes, and use the wordpress export / import plugins to transfer new content from the live site to the clone. Every now and again you might want to re-clone the site afresh. Something I find useful for development and testing of new plugins and themes is to have the plugin or theme directory that I am developing in set up as a git repository linked to github and keep files in sync with git push and git pull.

## Anything else?

I think that is it. If I have forgotten anything or if you have tips on making any of this easier please leave a comment.

The post [Cloning WordPress sites for development](https://blogs.pjjk.net/phil/cloning-wordpress/) appeared first on [Sharing and learning](https://blogs.pjjk.net/phil).