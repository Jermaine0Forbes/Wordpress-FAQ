# Wordpress Functions and Questions

**The proper way to add styles and scripts in the frontend**
- [source](https://codex.wordpress.org/Plugin_API/Action_Reference/wp_enqueue_scripts)
- [wp_enqueue_style(id name, deps, src, version, media)](https://developer.wordpress.org/reference/functions/wp_enqueue_style/)
- [wp_enqueue_script(id name,deps,src,version, in footer)](https://developer.wordpress.org/reference/functions/wp_enqueue_script/)

**How to check if you are on a certain page**
- [source](https://developer.wordpress.org/reference/functions/is_page/)
- `is_page( int|string|array $page = '' )`

**How to check if you are on  home page**
- [source](https://developer.wordpress.org/reference/functions/is_home/)
- `is_home()`

**How to check if you are on front page**
- [source](https://codex.wordpress.org/Function_Reference/is_front_page)
- `is_front_page()`

**How to include files/templates in wordpress**
- [source](https://konstantin.blog/2013/get_template_part/)
- [get_template_part( string $slug, string $name = null )](https://developer.wordpress.org/reference/functions/get_template_part/)

**How to create a child theme**
- [source](https://codex.wordpress.org/Child_Themes)

**What is the Template Hierarchy**
- [source](https://developer.wordpress.org/themes/basics/template-hierarchy/)

**How to use add_action and do_action**
- [source](https://developer.wordpress.org/reference/functions/add_action/)
- [second reference](http://frumph.net/2010/06/14/understanding-do_action-and-add_action/)
- [third reference](http://wordpress.stackexchange.com/questions/99952/best-practice-way-to-implement-custom-sections-into-a-wordpress-theme/99958#99958)

**How to get src of  feature imaged post**
- [source](https://codex.wordpress.org/Function_Reference/the_post_thumbnail_url)

**The List of WP_Query arguments**
- [source](http://www.billerickson.net/code/wp_query-arguments/)

**How to get the parent category of a child category while looping through $query->have_posts()**
- [source](http://www.wpbeginner.com/wp-themes/how-to-display-only-parent-category-in-your-wordpress-post-loop/)

**How to get all posts from category**
- [source](http://wordpress.stackexchange.com/questions/4201/how-to-query-posts-by-category-and-tag)

**Template Tags to use for your blog template OR while looping through a post**
- [source](https://codex.wordpress.org/Template_Tags)

**How to turn on wordpress debug messages**
- [source](https://codex.wordpress.org/Debugging_in_WordPress)

**How to remove “Powered by Wordpress” in footer**
- [source](http://www.wpbeginner.com/wp-themes/how-to-remove-the-powered-by-wordpress-footer-links/)
- Go to footer and comment or remove get_template_part(‘template-parts/footer/site’, ‘info’);

**How to customize login form**
- [source](https://codex.wordpress.org/Customizing_the_Login_Form)

**How to get posts with get_posts**
- [source](https://codex.wordpress.org/Template_Tags/get_posts)
