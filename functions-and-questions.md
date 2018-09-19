# Wordpress Functions and Questions

- [_e()][e]
- [add_action()][add-action]
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
- [is_email()][is-email]
- [is_page_template()][is-page-template]
- [is_user_logged_in][logged-in]
- [post_class()][post-class]
- [remove_action][remove-action]
- [term_exists()][term-exists]
- [username_exists()][username-exists]
- [wp_list_pages()][list-pages]
- [wp_list_categories()][list-categories]
- [wp_nav_menu()][wp-nav-menu]

[term-exists]:#term_exists
[is-email]:#is_email
[logged-in]:#is_user_logged_in
[wp-nav-menu]:#wp_nav_menu
[remove-action]:#remove_action
[add-action]:#add_action
[list-categories]:#wp_list_categories
[e]:#_e
[list-categories]:#wp_list_categories
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


### username_exists
<details>
  <summary>
  View Content
  </summary>

  Returns the user ID if the user exists or false if the user doesn't exist.

```php
<?php username_exists( $username ); ?>
```
</details>

[go back :house:][home]

### term_exists
<details>
  <summary>
  View Content
  </summary>

  Check if a given term exists and return the term ID, a term array, or 0 (false) if the term doesn't exist.

```php
<?php term_exists( $term, $taxonomy, $parent ) ?>
```
</details>

[go back :house:][home]

### is_email

<details>
<summary>
View Content
</summary>
Verifies that an email is valid.

```php

<?php is_email( $email ) ?>

```
</details>

[go back :house:][home]


### is_user_logged_in

<details>
<summary>
View Content
</summary>
Checks if the current visitor is a logged in user.

```
is_user_logged_in()
```
</details>

[go back :house:][home]

### wp_nav_menu

<details>
<summary>
View Content
</summary>

**reference**
- [codex](https://developer.wordpress.org/reference/functions/wp_nav_menu/)

**My definition:**  adds a nav menu that you created in the backend

```php
<?php wp_nav_menu( array $args = array() ); ?>
```
</details>

[go back :house:][home]

### remove_action

<details>
<summary>
View Content
</summary>

**reference**
- [codex](https://codex.wordpress.org/Function_Reference/remove_action)

**My definition:** removes content from a specific action section

```php
<?php remove_action( $tag, $function_to_remove, $priority ); ?>
```
</details>

[go back :house:][home]

### add_action

<details>
<summary>
View Content
</summary>

**reference**
- [wordpress](https://developer.wordpress.org/reference/functions/add_action/)

```php
add_action( string $tag, callable $function_to_add, int $priority = 10, int $accepted_args = 1 )
```
</details>

[go back :house:][home]

### _e()

`_e( string $text, string $domain = 'default' )`

**wordpress definition:** Display translated text.

**reference**
- [wordpress](https://developer.wordpress.org/reference/functions/_e/)

```


```

[go back home][home]

### wp_list_categories()

`wp_list_categories( string|array $args = '' )`

**wordpress definition:** Display or retrieve the HTML list of categories.

**reference**
- [wordpress](https://developer.wordpress.org/reference/functions/wp_list_categories/)

**arguments**
- **child_of** (int)
- **current_directory** (int|array)
- **depth** (int)
- **echo** (bool|int)
- **exclude** (array|string)
- **exclude_tree** (array|string)
- **feed** (string)
- **feed_image** (string)
- **feed_type** (string)
- **hide_empty** (boo|int)
- **hide_title_if_empty** (bool)
- **hierarchical** (bool)
- **order** (string)
- **orderby** (string)
- **seperator** (string)
- **show_count** (bool|int)
- **show_option_all** (string)
- **show_option_none** (string)
- **style** (string)
- **taxonomy** (string)
- **title_li** (string)
- **use_desc_for_title** (bool|int)

```php
//This will display all the categories
    <ul>
<?php wp_list_categories(); ?>
    </ul>
```

[go back home][home]

### wp_list_pages()

`wp_list_pages( array|string $args = '' )`

**wordpress definition:** Retrieve or display list of pages (or hierarchical post type items) in list (li) format.

**my definition:** I think it retrives all the pages/posts that you want in a <li> format

**reference**
- [wordpress](https://developer.wordpress.org/reference/functions/wp_list_pages/)

```php
<ul>
<?php wp_list_pages( array(

    //This displays the Pages with the id of 5,9,23
    'include'  => array( 5, 9, 23 ),

    // This displays a title of Poetry before generating the list
    'title_li' => '<h2>' . __('Poetry') . '</h2>'
) ); ?>
</ul>
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
