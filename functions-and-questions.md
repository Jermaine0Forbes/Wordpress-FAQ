# Wordpress Functions and Questions


- [bloginfo()][blog-info]
- [esc_attr()][esc-attr]
- [esc_html_()][esc-html]
- [esc_url()][esc-url]
- [get_bloginfo()][get-blog]
- [get_post_format()][get-post-format]
- [get_template_part()][get-template]
- [get_theme_mod()][get-theme]
- [get_query_var()][get-query]
- [has_header_image][has-header-image] 
- [header_image][header-image]
- [home_url()][home-url]
- [is_active_sidebar()][is-active-sidebar]
- [is_front_page()][is-front-page]
- [is_page_template()][is-page-template]
- [post_class()][post-class]

[home]:#wordpress-functions-and-questions
[blog-info]:#bloginfo
[esc-attr]:#esc_attr
[esc-html]:#esc_html_
[esc-url]:#esc_url
[get-blog]:#get_bloginfo
[get-template]:#get_template_part
[get-theme]:#get_theme_mod
[has-header-image]:#has_header_image
[header-image]:#header_image
[home-url]:#home_url
[is-active-sidebar]:#is_active_sidebar
[is-front-page]:#how-to-check-if-you-are-on-the-front-page
[is-page-template]:#is_page_template
[get-post-format]:#get_post_format
[post-class]:#post_class
[get-query]:#get_query_var


### get_query_var()

Retrieve variable in the WP_Query class.

`get_query_var( string $var, mixed $default = '' )`

**reference**
- [wordpress](https://developer.wordpress.org/reference/functions/get_query_var/)

```php
<?php

    $paged = ( get_query_var( 'paged' ) ) ? absint( get_query_var( 'paged' ) ) : 1;
```

[go back home][home]

### post_class()

`post_class( string|array $class = '', int|WP_Post $post_id = null )`

**reference**
- [wordpress](https://developer.wordpress.org/reference/functions/post_class/)

```php
<div id="post-<?php the_ID(); ?>" <?php post_class( 'class-name' ); ?>>

```

[go back home][home]

### get_post_format()

`get_post_format( int|object|null $post = null )`

Retrieve the format slug for a post

**reference**
- [wordpress](https://developer.wordpress.org/reference/functions/get_post_format/)

```php
/*
 * Pull in a different sub-template, depending on the Post Format.
 * 
 * Make sure that there is a default format.php file to fall back to as a default.
 * Name templates format-link.php, format-aside.php, etc.
 *
 * You should use this in the loop.
 */
get_template_part( 'format', get_post_format() );
```

[go back home][home]

### get_template_part()

`get_template_part( string $slug, string $name = null )`

Loads a template part into a template.

**reference**
- [wordpress](https://developer.wordpress.org/reference/functions/get_template_part/)

```php

<?php get_template_part('footer-widget'); ?>
```

[go back home][home]

### is_active_sidebar()

`is_active_sidebar( string|int $index )`

Whether a sidebar is in use.

**reference**
- [wordpress](https://developer.wordpress.org/reference/functions/is_active_sidebar/)

```php
<?php if ( is_active_sidebar( 'left-sidebar' ) ) { ?>
    <ul id="sidebar">
        <?php dynamic_sidebar( 'left-sidebar' ); ?>
    </ul>
<?php } ?>

```

[go back home][home]

### esc_html_()

`esc_html__( string $text, string $domain = 'default' )`

Retrieve the translation of $text and escapes it for safe use in HTML output.

**reference**
- [wordpress](https://developer.wordpress.org/reference/functions/esc_html__/)
- [codex](https://codex.wordpress.org/Function_Reference/esc_html)

```
<h3><?php echo esc_html__( 'Title', 'text-domain' )?></h3>
```

[go back home][home]

### is_page_template()

`is_page_template( string|array $template = '' )`

Whether currently in a page template.

**reference**
- [wordpress](https://developer.wordpress.org/reference/functions/is_page_template/)

```php
<?php

if ( is_page_template( 'about.php' ) ) {
    // about.php is used
} else {
    // about.php is not used
}
```

[go back home][home]

### esc_attr()

`esc_attr( string $text )`

**reference**
- [wordpress](https://developer.wordpress.org/reference/functions/esc_attr/)

```php
<input type="text" name="fname" value="<?php echo esc_attr( $fname ); ?>">
```

[go back home][home]

### get_bloginfo()

`get_bloginfo( string $show = '', string $filter = 'raw' )`

Retrieves information about the current site.

**reference**
- [wordpress](https://developer.wordpress.org/reference/functions/get_bloginfo/)

```php
$site_title = get_bloginfo( 'name' );
```

[go back home][home]

### bloginfo()

**reference**
- [wordpress](https://developer.wordpress.org/reference/functions/bloginfo/)

[go back home][home]

### esc_url()

**reference**
- [wordpress](https://developer.wordpress.org/reference/functions/esc_url/)
- [codex](https://codex.wordpress.org/Function_Reference/esc_url)

[go back home][home]

### home_url()

**reference**
- [wordpress](https://developer.wordpress.org/reference/functions/home_url/)

[go back home][home]

### wp_nav_menu

**reference**
- [wordpress](https://developer.wordpress.org/reference/functions/wp_nav_menu/)

```php
wp_nav_menu(array(
                'theme_location'    => 'primary',
                'container'       => 'div',
                'container_id'    => '',
                'container_class' => 'collapse navbar-collapse justify-content-end',
                'menu_id'         => false,
                'menu_class'      => 'navbar-nav',
                'depth'           => 3,
                'fallback_cb'     => 'wp_bootstrap_navwalker::fallback',
                'walker'          => new wp_bootstrap_navwalker()
                ));
```

[go back home][home]

### The proper way to add styles and scripts in the frontend

`wp_enqueue_style(id name, deps, src, version, media)`
`wp_enqueue_script(id name,deps,src,version, in footer)`

**reference**
- [source](https://codex.wordpress.org/Plugin_API/Action_Reference/wp_enqueue_scripts)
- [wp_enqueue_style(id name, deps, src, version, media)](https://developer.wordpress.org/reference/functions/wp_enqueue_style/)
- [wp_enqueue_script(id name,deps,src,version, in footer)](https://developer.wordpress.org/reference/functions/wp_enqueue_script/)

[go back home][home]

### How to check if you are on a certain page

`is_page( int|string|array $page = '' )`

**reference**
- [source](https://developer.wordpress.org/reference/functions/is_page/)

```php


```

[go back home][home]

### How to check if you are on  home page

`is_home()`

**reference**
- [source](https://developer.wordpress.org/reference/functions/is_home/)


```php


```

[go back home][home]

### How to check if you are on front page

`is_front_page()` 

**reference**
- [source](https://codex.wordpress.org/Function_Reference/is_front_page)


```php


```

[go back home][home]

### How to include files/templates in wordpress

`get_template_part( string $slug, string $name = null )`

**reference**
- [konstantin](https://konstantin.blog/2013/get_template_part/)
- [wordpress](https://developer.wordpress.org/reference/functions/get_template_part/)

```php


```

[go back home][home]

### How to create a child theme


**reference**
- [wordpress](https://codex.wordpress.org/Child_Themes)

```php


```

[go back home][home]

### What is the Template Hierarchy

**reference**
- [source](https://developer.wordpress.org/themes/basics/template-hierarchy/)

```php


```

[go back home][home]
