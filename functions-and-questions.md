# Wordpress Functions and Questions

[home]:#wordpress-functions-and-questions

### The proper way to add styles and scripts in the frontend

**reference**
- [source](https://codex.wordpress.org/Plugin_API/Action_Reference/wp_enqueue_scripts)
- [wp_enqueue_style(id name, deps, src, version, media)](https://developer.wordpress.org/reference/functions/wp_enqueue_style/)
- [wp_enqueue_script(id name,deps,src,version, in footer)](https://developer.wordpress.org/reference/functions/wp_enqueue_script/)

### How to check if you are on a certain page

`is_page( int|string|array $page = '' )`

**reference**
- [source](https://developer.wordpress.org/reference/functions/is_page/)

```php


```

[go back home][home]

### How to check if you are on  home page

- `is_home()`

**reference**
- [source](https://developer.wordpress.org/reference/functions/is_home/)


```php


```

[go back home][home]

### How to check if you are on front page

- `is_front_page()` 

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

### How to use add_action and do_action

**reference**
- [source](https://developer.wordpress.org/reference/functions/add_action/)
- [second reference](http://frumph.net/2010/06/14/understanding-do_action-and-add_action/)
- [third reference](http://wordpress.stackexchange.com/questions/99952/best-practice-way-to-implement-custom-sections-into-a-wordpress-theme/99958#99958)

```php


```

[go back home][home]

### How to get src of  feature imaged post

**reference**
- [source](https://codex.wordpress.org/Function_Reference/the_post_thumbnail_url)

```php


```

[go back home][home]

### The List of WP_Query arguments

**reference**
- [source](http://www.billerickson.net/code/wp_query-arguments/)

```php


```

[go back home][home]

### How to get the parent category of a child category while looping through $query->have_posts()

**reference**
- [source](http://www.wpbeginner.com/wp-themes/how-to-display-only-parent-category-in-your-wordpress-post-loop/)

```php


```

[go back home][home]

### How to get all posts from category

**reference**
- [source](http://wordpress.stackexchange.com/questions/4201/how-to-query-posts-by-category-and-tag)

```php


```

[go back home][home]

### Template Tags to use for your blog template OR while looping through a post

**reference**
- [source](https://codex.wordpress.org/Template_Tags)


```php


```

[go back home][home]

### How to turn on wordpress debug messages

**reference**
- [source](https://codex.wordpress.org/Debugging_in_WordPress)


```php


```

[go back home][home]

### How to remove “Powered by Wordpress” in footer

**reference**
- [source](http://www.wpbeginner.com/wp-themes/how-to-remove-the-powered-by-wordpress-footer-links/)
- Go to footer and comment or remove get_template_part(‘template-parts/footer/site’, ‘info’);


```php


```

[go back home][home]

### How to customize login form

**reference**
- [source](https://codex.wordpress.org/Customizing_the_Login_Form)


```php


```

[go back home][home]

### How to get posts with get_posts

**reference**
- [source](https://codex.wordpress.org/Template_Tags/get_posts)


```php


```

[go back home][home]
