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
- [wp_list_pages()][list-pages]

[list-pages]:#wp_list_pages
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


### wp_list_pages()

`wp_list_pages( array|string $args = '' )`

**wordpress definition:** Retrieve or display list of pages (or hierarchical post type items) in list (li) format.

**my definition:** I think it retrives all the pages/posts that you want in a list format

**reference**
- [wordpress](https://developer.wordpress.org/reference/functions/wp_list_pages/)

```

$args

    (array|string) (Optional) Array or string of arguments. Optional.

        'child_of'
        (int) Display only the sub-pages of a single page by ID. Default 0 (all pages).
        'authors'
        (string) Comma-separated list of author IDs. Default empty (all authors).
        'date_format'
        (string) PHP date format to use for the listed pages. Relies on the 'show_date' parameter. Default is the value of 'date_format' option.
        'depth'
        (int) Number of levels in the hierarchy of pages to include in the generated list. Accepts -1 (any depth), 0 (all pages), 1 (top-level pages only), and n (pages to the given n depth). Default 0.
        'echo'
        (bool) Whether or not to echo the list of pages. Default true.
        'exclude'
        (string) Comma-separated list of page IDs to exclude.
        'include'
        (array) Comma-separated list of page IDs to include.
        'link_after'
        (string) Text or HTML to follow the page link label. Default null.
        'link_before'
        (string) Text or HTML to precede the page link label. Default null.
        'post_type'
        (string) Post type to query for. Default 'page'.
        'post_status'
        (string|array) Comma-separated list or array of post statuses to include. Default 'publish'.
        'show_date'
        (string) Whether to display the page publish or modified date for each page. Accepts 'modified' or any other value. An empty value hides the date.
        'sort_column'
        (string) Comma-separated list of column names to sort the pages by. Accepts 'post_author', 'post_date', 'post_title', 'post_name', 'post_modified', 'post_modified_gmt', 'menu_order', 'post_parent', 'ID', 'rand', or 'comment_count'. Default 'post_title'.
        'title_li'
        (string) List heading. Passing a null or empty value will result in no heading, and the list will not be wrapped with unordered list <ul> tags. Default 'Pages'.
        'item_spacing'
        (string) Whether to preserve whitespace within the menu's HTML. Accepts 'preserve' or 'discard'. Default 'preserve'.
        'walker'
        (Walker) Walker instance to use for listing pages. Default empty (Walker_Page).

    Default value: ''

```


[go back home][home]

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

`bloginfo( string $show = '' )`

Displays information about the current site.

**reference**
- [wordpress](https://developer.wordpress.org/reference/functions/bloginfo/)

```php
//Display your blog's title in a tag.
<h1><?php bloginfo( 'name' ); ?></h1>
```

[go back home][home]

### esc_url()

`esc_url( string $url, array $protocols = null, string $_context = 'display' )`

Checks and cleans a URL.

**reference**
- [wordpress](https://developer.wordpress.org/reference/functions/esc_url/)
- [codex](https://codex.wordpress.org/Function_Reference/esc_url)

```php

<a href="<?php echo esc_url( home_url( '/' ) ); ?>">Home</a>
```

[go back home][home]

### home_url()

`home_url( string $path = '', string|null $scheme = null )`

Retrieves the URL for the current site where the front end is accessible.

**reference**
- [wordpress](https://developer.wordpress.org/reference/functions/home_url/)

```php

$url = home_url();
echo $url;
```

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

**Adding css**
`wp_enqueue_style(id name, deps, src, version, media)`

**Adding js**
`wp_enqueue_script(id name,deps,src,version, in footer)`

**reference**
- [source](https://codex.wordpress.org/Plugin_API/Action_Reference/wp_enqueue_scripts)
- [wp_enqueue_style(id name, deps, src, version, media)](https://developer.wordpress.org/reference/functions/wp_enqueue_style/)
- [wp_enqueue_script(id name,deps,src,version, in footer)](https://developer.wordpress.org/reference/functions/wp_enqueue_script/)

```php
function my_theme_enqueue_scripts() {
    wp_enqueue_script( 'js-stick', get_theme_file_uri().'/js/scrollfix.js');
    wp_enqueue_script( 'js-style', get_theme_file_uri().'/js/index.js');
    wp_enqueue_style('master-css', get_theme_file_uri().'/css/master.css');

}


add_action( 'wp_enqueue_scripts', 'my_theme_enqueue_scripts' );
```

[go back home][home]

### How to check if you are on a certain page

`is_page( int|string|array $page = '' )`

Is the query for an existing single page?

**reference**
- [source](https://developer.wordpress.org/reference/functions/is_page/)

```php

// When any single Page is being displayed.
is_page();
 
// When Page 42 (ID) is being displayed.
is_page( 42 );
 
// When the Page with a post_title of "Contact" is being displayed.
is_page( 'Contact' );
```

[go back home][home]

### How to check if you are on  home page

`is_home()`

Checks to see if you are on the home page

**reference**
- [wordpress](https://developer.wordpress.org/reference/functions/is_home/)


```php
if ( is_home() ) {
    // This is the blog posts index
    get_sidebar( 'blog' );
} else {
    // This is not the blog posts index
    get_sidebar();
}

```

[go back home][home]

### How to check if you are on front page

`is_front_page()` 

Checks to see if it is the front page

**reference**
- [codex](https://codex.wordpress.org/Function_Reference/is_front_page)


```php

<?php if(is_front_page()) {?>

    // Do something 

<?php  } ?>

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

