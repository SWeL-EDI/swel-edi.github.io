---
id: 499
title: 'Shared WordPress archive for different post types'
date: '2017-03-23T16:27:02+00:00'
author: 'Phil Barker'
excerpt: "<p>In a WordPress plugin I have&nbsp;custom post types for different types of publication: books, chapters, papers, presentations, reports. I want one single archive of all of these publications. I know that the theme template hierarchy allows templates with the pattern archive-$posttype.php, so&nbsp; I tried setting the slug for all the custom post types to &lsquo;presentations&rsquo;.&nbsp;WordPress &hellip; <a href=\"https://blogs.pjjk.net/phil/shared-wordpress-archive-different-post-types/\">Continue reading <span>Shared WordPress archive for different post types</span> <span>&rarr;</span></a></p>\n<p>The post <a rel=\"nofollow\" href=\"https://blogs.pjjk.net/phil/shared-wordpress-archive-different-post-types/\">Shared WordPress archive for different post types</a> appeared first on <a rel=\"nofollow\" href=\"https://blogs.pjjk.net/phil\">Sharing and learning</a>.</p>"
layout: post
guid: 'https://blogs.pjjk.net/phil/?p=1738'
permalink: 'https://blogs.pjjk.net/phil/shared-wordpress-archive-different-post-types/'
enclosure:
    - "\n\n"
syndication_source:
    - 'Sharing and learning'
syndication_source_uri:
    - 'https://blogs.pjjk.net/phil'
syndication_source_id:
    - 'http://blogs.pjjk.net/phil/feed/'
'rss:comments':
    - 'https://blogs.pjjk.net/phil/shared-wordpress-archive-different-post-types/#respond'
'wfw:commentRSS':
    - 'https://blogs.pjjk.net/phil/shared-wordpress-archive-different-post-types/feed/'
syndication_feed:
    - 'http://blogs.pjjk.net/phil/feed/'
syndication_feed_id:
    - '2'
syndication_permalink:
    - 'https://blogs.pjjk.net/phil/shared-wordpress-archive-different-post-types/'
syndication_item_hash:
    - bd0958d05903f8a372766f082b5b2e64
categories:
    - Other
    - WordPress
---

In a WordPress plugin I have custom post types for different types of publication: books, chapters, papers, presentations, reports. I want one single archive of all of these publications.

I know that the [theme template hierarchy](https://developer.wordpress.org/themes/basics/template-hierarchy/) allows templates with the pattern `archive-$posttype.php, so` I tried setting the slug for all the custom post types to ‘presentations’. WordPress doesn’t like that. So what I did was set the slug for one of the publication custom post types to ‘presentations’, that gives me a /presentations/ archive for that custom post type<sup>(1)</sup>. I then edited the `archive.php` file to [use a different template parts](https://developer.wordpress.org/reference/functions/get_template_part/) for custom post types<sup>(2)</sup>:

```
<pre class="brush: php; title: ; notranslate">
<?php $cpargs = array('_builtin' => False,
				  'exclude_from_search' => False);
	$custom_post_types = get_post_types( $cpargs, 'names', 'and' );
	if ( is_post_type_archive( $custom_post_types ) ) {
		get_template_part( 'archive-publication' );
	} else {
		get_template_part( 'archive-default' );
	}  
?>
```

See anything wrong with this approach? Any comments on how better to do this would be welcome.

##### Notes:

1. 1 could edit the .htaccess file to redirect the /books/, /chapters/ …etc archives to /publications/, which would be neater in some ways but would make setting up the theme a bit of a faff.
2. Yes, the code gives all the custom post types with an archive the same archive. That’s fixable if you make the array of post types for which you want a shared archive manually.

The post [Shared WordPress archive for different post types](https://blogs.pjjk.net/phil/shared-wordpress-archive-different-post-types/) appeared first on [Sharing and learning](https://blogs.pjjk.net/phil).