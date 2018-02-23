# Wordpress Reference


## Installation
- [how to change siteurl from old domain to new domain][change-domain]
- [how to install wordpress for the first time][install]
- [how install a new wordpress][new-installation]

## References
- [Wordpress Function Reference][function-ref]
- [Post Reference][post-ref]
- [what does the template hierarchy look like][hierarchy]
- [the List of WP_Query arguments][query-arguments]
- [Standard post loops][standard-loop]

## Child theme
- [how to  create a child theme][child]

## Customization
- [how to customize a sidebar][sidebar]
- [How to customize login form][customize-form]

## Post/Page
- [how to get src of  feature imaged post][image-post]
- [how to get the parent category of a child category while looping through $query->have_posts()][parent-child]
- [how to get all posts from category][all-category]
- [Template Tags to use for your blog template OR while looping through a post][template-tags]
- [How to remove “Powered by Wordpress” in footer][remove-footer]
- [how to get posts with get_posts()][get-posts]
- [how to create a page template][page-temp]

## Functions
- [how to add css/js files][css]
- [how to use add_action and do_action][add-action]
- [how to add scripts from different urls][add-script]
- [how to make jquery work][jquery-work]
- [how to get the current theme's root folder][theme-root]
- [how to add pagination to blog][add-pagination]

## Plugins
- [how to allow installation of plugins/themes][allow-install]
- [how to set placeholder text in contact form 7][form-place]

## Settings
- [How to turn on wordpress debug messages][debug]

[new-installation]:#how-to-install-a-new-wordpress
[add-pagination]:#how-to-add-pagination-to-blog
[theme-root]:#how-to-get-the-current-theme-folder
[standard-loop]:#standard-post-loops
[jquery-work]:#how-to-make-jquery-work
[form-place]:#how-to-set-placeholder-text-in-contact-form-7
[add-script]:#how-to-add-scripts-from-different-urls
[post-ref]:#post-reference
[function-ref]:#wordpress-function-reference
[customize-form]:#how-to-customize-login-form
[remove-footer]:#how-to-remove-powered-by-wordpress-in-footer
[debug]:#how-to-turn-on-wordpress-debug-messages
[template-tags]:#template-tags-to-use-for-your-blog-template-or-while-looping-through-a-post
[all-category]:#how-to-get-all-posts-from-category
[parent-child]:#how-to-get-the-parent-category-of-a-child-category-while-looping-through-have_posts
[query-arguments]:#the-list-of-wp_query-arguments
[image-post]:#how-to-get-src-of-feature-imaged-post
[add-action]:#how-to-use-add_action-and-do_action
[get-posts]:#how-to-get-posts-with-get_posts
[page-temp]:#how-to-create-a-page-template
[change-domain]:#how-to-change-siteurl-from-old-domain
[hierarchy]:#what-does-the-template-hierarchy-look-like
[allow-install]:#how-to-allow-installation-of-pluginsthemes
[home]:#wordpress-reference
[css]:#how-to-add-cssjs-files
[child]:#how-to-create-a-child-theme
[install]:#how-to-install-wordpress
[sidebar]:#how-to-customize-a-sidebar

---


### How to install a new wordpress 

1. create a database 

```sql
CREATE DATABASE wordpress DEFAULT CHARACTER SET utf8 COLLATE utf8_unicode_ci;
```
2. update linux 

```
sudo apt-get update
```

3. create a conf for your wordpress site

```
sudo nano /etc/apache2/wordpress.conf

	// add this into the file

	<Directory /var/www/html/>
    	AllowOverride All
	</Directory>
```

4. activate the conf file and restart apache 

```
sudo a2ensite wordpress.conf ; sudo service apache2 reload; sudo service apache2 restart;
```

5. encrypt the address with Let's Encrypt 

```
sudo certbot --apache -d example.com
```

6. copy wordpress files to new location 

```
sudo cp -a /tmp/wordpress/. /var/www/html
```

7. configure wordpress 
```
	sudo chown -R yourName:www-data /var/www/html;
	sudo find /var/www/html -type d -exec chmod g+s {} \;
	sudo chmod g+w /var/www/html/wp-content;
	sudo chmod -R g+w /var/www/html/wp-content/themes;
	sudo chmod -R g+w /var/www/html/wp-content/plugins;
```

8. now, create the keys and passwords

```
// copy the printed keys
	curl -s https://api.wordpress.org/secret-key/1.1/salt/

	sudo nano /var/www/html/wp-config.php

	// place the printed keys in the file
	// and add in the database information  like this

	define('DB_NAME', 'wordpress');

	/** MySQL database username */
	define('DB_USER', 'wordpressuser');

	/** MySQL database password */
	define('DB_PASSWORD', 'password');

	. . .

	define('FS_METHOD', 'direct');
```

[go back home][home]

### How to add pagination to blog

` echo paginate_links(array("total" => $the_query->max_num_pages));`

**reference**
- [WordPress Pagination Tutorial (Custom Query & Template Integration)](https://www.youtube.com/watch?v=HMscydyViZw)
- [paginate_links](https://developer.wordpress.org/reference/functions/paginate_links/)

**paginate_links()**
```php
    <?php

    $paged = ( get_query_var( 'paged' ) ) ? absint( get_query_var( 'paged' ) ) : 1;
    $args = array(
   'post_type' => 'post', //must use tag id for this field
   'posts_per_page' => 3,
   "paged" => $paged,

 ); //get all posts


 // the query
 $the_query = new WP_Query( $args ); ?>

 <?php if ( $the_query->have_posts() ) : ?>

 	<!-- pagination here -->

 	<!-- the loop -->
 	<?php while ( $the_query->have_posts() ) : $the_query->the_post(); ?>
        <div class="border border-bottom-0 text-center">
            <h2><?php the_title(); ?></h2>
            <p><?php the_content(); ?></p>
        </div>

 	<?php endwhile; ?>
 	<!-- end of the loop -->

 	<!-- pagination here -->
    <?php

        //previous_posts_link();
       echo paginate_links(array(
           "total" => $the_query->max_num_pages
       ));
        //next_posts_link("Next post", $the_query->max_num_pages);

     ?>

 	<?php wp_reset_postdata(); ?>



 <?php else : ?>
 	<p><?php esc_html_e( 'Sorry, no posts matched your criteria.' ); ?></p>
 <?php
    endif;
 ?>

```

**next_posts_link()**
```php
<?php

//If you want to only next and previous arrow links then
//this is how you do it

        previous_posts_link();
       
        next_posts_link("Next post", $the_query->max_num_pages);

     ?>
```

[go back home][home]

### How to get the current theme folder

`get_theme_file_uri( string $file = '' )`

This method essential if you are trying to get root folder or your 
child theme, in order to retrieve a js or css file

**reference**
- [wordpress](https://developer.wordpress.org/reference/functions/get_theme_file_uri/)

```php
//in functions.php

function my_theme_enqueue_scripts() {
    wp_enqueue_script( 'js-stick', get_theme_file_uri().'/js/scrollfix.js');
    wp_enqueue_script( 'js-style', get_theme_file_uri().'/js/index.js');


}


add_action( 'wp_enqueue_scripts', 'my_theme_enqueue_scripts' );

```


[go back home][home]

### Standard Post loops

Here are the typical ways to query posts/pages from the **WP_Query** class

**reference**
- [codex](https://codex.wordpress.org/Class_Reference/WP_Query)

#### Standard Loop

```php

<?php

// The Query
$the_query = new WP_Query( $args );

// The Loop
if ( $the_query->have_posts() ) {
	echo '<ul>';
	while ( $the_query->have_posts() ) {
		$the_query->the_post();
		echo '<li>' . get_the_title() . '</li>';
	}
	echo '</ul>';
	/* Restore original Post Data */
	wp_reset_postdata();
} else {
	// no posts found
}
```

#### Standard Loop 2

```php
<?php 
// the query
$the_query = new WP_Query( $args ); ?>

<?php if ( $the_query->have_posts() ) : ?>

	<!-- pagination here -->

	<!-- the loop -->
	<?php while ( $the_query->have_posts() ) : $the_query->the_post(); ?>
		<h2><?php the_title(); ?></h2>
	<?php endwhile; ?>
	<!-- end of the loop -->

	<!-- pagination here -->

	<?php wp_reset_postdata(); ?>

<?php else : ?>
	<p><?php esc_html_e( 'Sorry, no posts matched your criteria.' ); ?></p>
<?php endif; ?>

```

#### Standard Loop 3 

```php

    <?php
    global $wp_query;
    $paged = ( get_query_var( 'paged' ) ) ? absint( get_query_var( 'paged' ) ) : 1;
    $args = array(
   'post_type' => 'post', //must use tag id for this field
   'posts_per_page' => 3,
   "paged" => $paged,

 ); //get all posts

    $posts = get_posts($args);

     ?>

     <?php
     foreach ($posts as $post) :
         //$post->the_post();
      ?>

      <div class=" border border-bottom-0 row justify-content-center">
          <div class="col text-center">

              <h4><?php echo $post->post_title; ?></h4>
              <p><?php echo $post->post_content;  ?></p>
          </div>
      </div>
        
 <?php
 endforeach;
 
   ?>
```

#### Multiple Loops

```php
<?php

// The Query
$query1 = new WP_Query( $args );

if ( $query1->have_posts() ) {
	// The Loop
	while ( $query1->have_posts() ) {
		$query1->the_post();
		echo '<li>' . get_the_title() . '</li>';
	}
	
	/* Restore original Post Data 
	 * NB: Because we are using new WP_Query we aren't stomping on the 
	 * original $wp_query and it does not need to be reset with 
	 * wp_reset_query(). We just need to set the post data back up with
	 * wp_reset_postdata().
	 */
	wp_reset_postdata();
}

/* The 2nd Query (without global var) */
$query2 = new WP_Query( $args2 );

if ( $query2->have_posts() ) {
	// The 2nd Loop
	while ( $query2->have_posts() ) {
		$query2->the_post();
		echo '<li>' . get_the_title( $query2->post->ID ) . '</li>';
	}

	// Restore original Post Data
	wp_reset_postdata();
}

?>

```


[go back home][home]

### How to make JQuery work

**reference**
- [TypeError: $ is not a function Wordpress](https://stackoverflow.com/questions/12258282/typeerror-is-not-a-function-wordpress)

```js
jQuery( document ).ready(function( $ ) {
// Code that uses jQuery's $ can follow here.
$('.site-title').css('background-color','red');
});
```

**Note:** make sure in `functions.php` you add jquery in the wp_enqueue_script parameter

```php
<?php

add_action( 'wp_enqueue_scripts', 'my_theme_enqueue_scripts' );

function my_theme_enqueue_scripts() {
    wp_enqueue_script( 'js-style', get_theme_file_uri().'/js/main.js', array("jquery") );

}
```

[go back home][home]

### How to set placeholder text in contact form 7

**reference**
- [contact form 7](https://contactform7.com/setting-placeholder-text/)

```php
[text your-name placeholder "Enter Name"]
```

[go back home][home]

### How to add scripts from different urls

**reference**
- [tutplus](https://code.tutsplus.com/articles/how-to-include-javascript-and-css-in-your-wordpress-themes-and-plugins--wp-24321)

```php
function wptuts_scripts_load_cdn()
{
    // Deregister the included library
    wp_deregister_script( 'jquery' );
     
    // Register the library again from Google's CDN
    wp_register_script( 'jquery', 'http://ajax.googleapis.com/ajax/libs/jquery/1.7.1/jquery.min.js', array(), null, false );
     
    // Register the script like this for a plugin:
    wp_register_script( 'custom-script', plugins_url( '/js/custom-script.js', __FILE__ ), array( 'jquery' ) );
    // or
    // Register the script like this for a theme:
    wp_register_script( 'custom-script', get_template_directory_uri() . '/js/custom-script.js', array( 'jquery' ) );
 
    // For either a plugin or a theme, you can then enqueue the script:
    wp_enqueue_script( 'custom-script' );
}
add_action( 'wp_enqueue_scripts', 'wptuts_scripts_load_cdn' );

```

[go back home][home]

### Post Reference 

**reference**
- [codex](https://codex.wordpress.org/Class_Reference/WP_Post)

Member Variable|Variable Type|Notes
-|-|-
ID|int|The ID of the post 
post_author|string|The post author's user ID (numeric string)  
post_name|string|The post's slug   
post_type|string|[post types](https://codex.wordpress.org/Post_Types)  
post_title|string|The title of the post  
post_date|string|Format: 0000-00-00 00:00:00  
post_date_gmt|string|Format: 0000-00-00 00:00:00  
post_content|string| The full content of the post   
post_excerpt|string| User-defined post excerpt   
post_status|string|[get_post_status](https://codex.wordpress.org/Function_Reference/get_post_status)  


[go back home][home]

### Wordpress function reference

There are a lot of functions in this bitch, so I am only going to 
focus on **Post, Custom Post Type, Page, Attachment and Bookmarks Functions**

**reference**
-  [wordpress](https://codex.wordpress.org/Function_Reference)

**Posts**

- [get_adjacent_post]()
- [get_boundary_post]()
- [get_children]()
- [get_extended]()
- [get_next_post]()
- [get_next_posts_link]()
- [next_posts_link]()
- [get_permalink]()
- [the_permalink]()
- [get_the_excerpt]()
- [the_excerpt]()
- [get_the_post_thumbnail]()
- [get_post]()
- [get_post_field]()
- [get_post_ancestors]()
- [get_post_mime_type]()
- [get_post_status]()
- [get_post_format]()
- [set_post_format]()
- [get_edit_post_link]()
- [get_delete_post_link]()
- [get_previous_post]()
- [get_previous_posts_link]()
- [previous_posts_link]()
- [get_posts]()
- [have_posts]()
- [is_single]()
- [is_sticky]()
- [get_the_ID]()
- [the_ID]()
- [the_post]()
- [wp_get_recent_posts]()
- [has_post_thumbnail]()
- [has_excerpt]()
- [has_post_format]()

[go back home][home]

### How to use add_action and do_action

Actions are the hooks that the WordPress core launches at specific points during execution, or when specific events occur. Plugins can specify that one or more of its PHP functions are executed at these points, using the Action API.

`add_action( string $tag, callable $function_to_add, int $priority = 10, int $accepted_args = 1 )`

**reference**
- [wordpress](https://developer.wordpress.org/reference/functions/add_action/)
- [understanding do_action annd add_action](http://frumph.net/2010/06/14/understanding-do_action-and-add_action/)
- [best practice way to implement custom sections into a wordpress](http://wordpress.stackexchange.com/questions/99952/best-practice-way-to-implement-custom-sections-into-a-wordpress-theme/99958#99958)

```php

add_action( 'save_post', 'wpdocs_my_save_post', 10, 3 );
```

[go back home][home]

### How to get src of  feature imaged post

**reference**
- [source](https://codex.wordpress.org/Function_Reference/the_post_thumbnail_url)

```php
<?php if ( has_post_thumbnail() ) : ?>
	<a href="<?php the_permalink(); ?>" title="<?php the_title_attribute(); ?>">
	<img src="<?php the_post_thumbnail_url(); ?>"/>
	</a>
<?php endif; ?>


```

[go back home][home]

### The List of WP_Query arguments

**reference**
- [source](http://www.billerickson.net/code/wp_query-arguments/)

```php

<?php
/**
* WordPress Query Comprehensive Reference
* Compiled by luetkemj - luetkemj.com
*
* CODEX: http://codex.wordpress.org/Class_Reference/WP_Query
* Source: http://core.trac.wordpress.org/browser/tags/3.3.1/wp-includes/query.php
*/
 
$args = array( 
  
//////Author Parameters - Show posts associated with certain author.
    'author' => 1,2,3,                        //(int) - use author id [use minus (-) to exclude authors by ID ex. 'author' => -1,-2,-3,]
    'author_name' => 'luetkemj',              //(string) - use 'user_nicename' (NOT name)
  
//////Category Parameters - Show posts associated with certain categories.
    'cat' => 5,//(int) - use category id.
    'category_name' => 'staff', 'news',       //(string) - use category slug (NOT name).
    'category__and' => array( 2, 6 ),         //(array) - use category id.
    'category__in' => array( 2, 6 ),          //(array) - use category id.
    'category__not_in' => array( 2, 6 ),      //(array) - use category id.
     
//////Tag Parameters - Show posts associated with certain tags.
    'tag' => 'cooking',                       //(string) - use tag slug.
    'tag_id' => 5,                            //(int) - use tag id.
    'tag__and' => array( 2, 6),               //(array) - use tag ids.
    'tag__in' => array( 2, 6),                //(array) - use tag ids.
    'tag__not_in' => array( 2, 6),            //(array) - use tag ids.
    'tag_slug__and' => array( 'red', 'blue'), //(array) - use tag slugs.
    'tag_slug__in' => array( 'red', 'blue'),  //(array) - use tag slugs.
  
//////Taxonomy Parameters - Show posts associated with certain taxonomy.
  //Important Note: tax_query takes an array of tax query arguments arrays (it takes an array of arrays)
  //This construct allows you to query multiple taxonomies by using the relation parameter in the first (outer) array to describe the boolean relationship between the taxonomy queries.
    'tax_query' => array(                     //(array) - use taxonomy parameters (available with Version 3.1).
    'relation' => 'AND',                      //(string) - Possible values are 'AND' or 'OR' and is the equivalent of ruuning a JOIN for each taxonomy
      array(
        'taxonomy' => 'color',                //(string) - Taxonomy.
        'field' => 'slug',                    //(string) - Select taxonomy term by ('id' or 'slug')
        'terms' => array( 'red', 'blue' ),    //(int/string/array) - Taxonomy term(s).
        'include_children' => true,           //(bool) - Whether or not to include children for hierarchical taxonomies. Defaults to true.
        'operator' => 'IN'                    //(string) - Operator to test. Possible values are 'IN', 'NOT IN', 'AND'.
      ),
      array(
        'taxonomy' => 'actor',
        'field' => 'id',
        'terms' => array( 103, 115, 206 ),
        'include_children' => false,
        'operator' => 'NOT IN'
      )
    ),
//////Post & Page Parameters - Display content based on post and page parameters.
    'p' => 1,                               //(int) - use post id.
    'name' => 'hello-world',                //(string) - use post slug.
    'page_id' => 1,                         //(int) - use page id.
    'pagename' => 'sample-page',            //(string) - use page slug.
    'pagename' => 'contact_us/canada',      //(string) - Display child page using the slug of the parent and the child page, separated ba slash
    'post_parent' => 1,                     //(int) - use page id. Return just the child Pages.
    'post__in' => array(1,2,3),             //(array) - use post ids. Specify posts to retrieve.
    'post__not_in' => array(1,2,3),         //(array) - use post ids. Specify post NOT to retrieve.
    //NOTE: you cannot combine 'post__in' and 'post__not_in' in the same query
//////Type & Status Parameters - Show posts associated with certain type or status.
    'post_type' => array(                   //(string / array) - use post types. Retrieves posts by Post Types, default value is 'post';
            'post',                         // - a post.
            'page',                         // - a page.
            'revision',                     // - a revision.
            'attachment',                   // - an attachment. The default WP_Query sets 'post_status'=>'published', but atchments default to 'post_status'=>'inherit' so you'll need to set the status to 'inherit' or 'any'.
            'my-post-type',                 // - Custom Post Types (e.g. movies)
            ),  
    'post_status' => array(                 //(string / array) - use post status. Retrieves posts by Post Status, default value i'publish'.         
            'publish',                      // - a published post or page.
            'pending',                      // - post is pending review.
            'draft',                        // - a post in draft status.
            'auto-draft',                   // - a newly created post, with no content.
            'future',                       // - a post to publish in the future.
            'private',                      // - not visible to users who are not logged in.
            'inherit',                      // - a revision. see get_children.
            'trash'                         // - post is in trashbin (available with Version 2.9).
            ),
    //NOTE: The 'any' keyword available to both post_type and post_status queries cannot be used within an array. 
    'post_type' => 'any',                    // - retrieves any type except revisions and types with 'exclude_from_search' set to true.
    'post_status' => 'any',                  // - retrieves any status except those from post types with 'exclude_from_search' set to true.
    
//////Pagination Parameters
    'posts_per_page' => 10,                 //(int) - number of post to show per page (available with Version 2.1). Use 'posts_per_page'=-1 to show all posts. Note if the query is in a feed, wordpress overwrites this parameter with the stored 'posts_per_rss' option. Treimpose the limit, try using the 'post_limits' filter, or filter 'pre_option_posts_per_rss' and return -1
    'posts_per_archive_page' => 10,         //(int) - number of posts to show per page - on archive pages only. Over-rides showposts anposts_per_page on pages where is_archive() or is_search() would be true
    'nopaging' => false,                    //(bool) - show all posts or use pagination. Default value is 'false', use paging.
    'paged' => get_query_var('page'),       //(int) - number of page. Show the posts that would normally show up just on page X when usinthe "Older Entries" link.
    //NOTE: You should set get_query_var( 'page' ); if you want your query to work with pagination. Since Wordpress 3.0.2, you dget_query_var( 'page' ) instead of get_query_var( 'paged' ). The pagination parameter 'paged' for WP_Query() remains the same.
//////Offset Parameter
    'offset' => 3,                          //(int) - number of post to displace or pass over.
//////Order & Orderby Parameters - Sort retrieved posts.
    'order' => 'DESC',                      //(string) - Designates the ascending or descending order of the 'orderby' parameter. Defaultto 'DESC'.
                                              //Possible Values:
                                              //'ASC' - ascending order from lowest to highest values (1, 2, 3; a, b, c).
                                              //'DESC' - descending order from highest to lowest values (3, 2, 1; c, b, a).
    'orderby' => 'date',                    //(string) - Sort retrieved posts by parameter. Defaults to 'date'.
                                              //Possible Values://
                                              //'none' - No order (available with Version 2.8).
                                              //'ID' - Order by post id. Note the captialization.
                                              //'author' - Order by author.
                                              //'title' - Order by title.
                                              //'date' - Order by date.
                                              //'modified' - Order by last modified date.
                                              //'parent' - Order by post/page parent id.
                                              //'rand' - Random order.
                                              //'comment_count' - Order by number of comments (available with Version 2.9).
                                              //'menu_order' - Order by Page Order. Used most often for Pages (Order field in the EdiPage Attributes box) and for Attachments (the integer fields in the Insert / Upload MediGallery dialog), but could be used for any post type with distinct 'menu_order' values (theall default to 0).
                                              //'meta_value' - Note that a 'meta_key=keyname' must also be present in the query. Note alsthat the sorting will be alphabetical which is fine for strings (i.e. words), but can bunexpected for numbers (e.g. 1, 3, 34, 4, 56, 6, etc, rather than 1, 3, 4, 6, 34, 56 as yomight naturally expect).
                                              //'meta_value_num' - Order by numeric meta value (available with Version 2.8). Also notthat a 'meta_key=keyname' must also be present in the query. This value allows for numericasorting as noted above in 'meta_value'.
                                              //'post__in' - Preserve post ID order given in the post__in array (available with Version 3.5).
																							 
																							 
//////Sticky Post Parameters - Show Sticky Posts or ignore them.
    'ignore_sticky_posts' => false,         //(bool) - ignore sticky posts or not. Default value is false, don't ignore. Ignore/excludsticky posts being included at the beginning of posts returned, but the sticky post will still be returned in the natural order othat list of posts returned.
    //NOTE: For more info on sticky post queries see: http://codex.wordpress.org/Class_Reference/WP_Query#Sticky_Post_Parameters
																							 
																							 
//////Time Parameters - Show posts associated with a certain time period.
    'year' => 2012,                         //(int) - 4 digit year (e.g. 2011).
    'monthnum' => 3,                        //(int) - Month number (from 1 to 12).
    'w' =>  25,                             //(int) - Week of the year (from 0 to 53). Uses the MySQL WEEK command. The mode is dependenon the "start_of_week" option.
    'day' => 17,                            //(int) - Day of the month (from 1 to 31).
    'hour' => 13,                           //(int) - Hour (from 0 to 23).
    'minute' => 19,                         //(int) - Minute (from 0 to 60).
    'second' => 30,                         //(int) - Second (0 to 60).
//////Custom Field Parameters - Show posts associated with a certain custom field.
    'meta_key' => 'key',                    //(string) - Custom field key.
    'meta_value' => 'value',                //(string) - Custom field value.
    'meta_value_num' => 10,                 //(number) - Custom field value.
    'meta_compare' => '=',                  //(string) - Operator to test the 'meta_value'. Possible values are '!=', '>', '>=', '<', or ='. Default value is '='.
    'meta_query' => array(                  //(array) - Custom field parameters (available with Version 3.1).
       array(
         'key' => 'color',                  //(string) - Custom field key.
         'value' => 'blue',                 //(string/array) - Custom field value (Note: Array support is limited to a compare value of 'IN', 'NOT IN', 'BETWEEN', or 'NOT BETWEEN')
         'type' => 'CHAR',                  //(string) - Custom field type. Possible values are 'NUMERIC', 'BINARY', 'CHAR', 'DATE', 'DATETIME', 'DECIMAL', 'SIGNED', 'TIME', 'UNSIGNED'. Default value is 'CHAR'.
         'compare' => '=',                  //(string) - Operator to test. Possible values are '=', '!=', '>', '>=', '<', '<=', 'LIKE', 'NOT LIKE', 'IN', 'NOT IN', 'BETWEEN', 'NOT BETWEEN'. Default value is '='.
       ),
       array(
         'key' => 'price',
         'value' => array( 1,200 ),
         'compare' => 'NOT LIKE'
       )
         
//////Permission Parameters - Display published posts, as well as private posts, if the user has the appropriate capability:
    'perm' => 'readable'                    //(string) Possible values are 'readable', 'editable' (possible more ie all capabilitiealthough I have not tested)
//////Parameters relating to caching
    'no_found_rows' => false,               //(bool) Default is false. WordPress uses SQL_CALC_FOUND_ROWS in most queries in order timplement pagination. Even when you donâ€™t need pagination at all. By Setting this parameter to true you are telling wordPress not tcount the total rows and reducing load on the DB. Pagination will NOT WORK when this parameter is set to true. For more informatiosee: http://flavio.tordini.org/speed-up-wordpress-get_posts-and-query_posts-functions
    'cache_results' => true,                //(bool) Default is true
    'update_post_term_cache' => true,       //(bool) Default is true
    'update_post_meta_cache' => true,       //(bool) Default is true
    //NOTE Caching is a good thing. Setting these to false is generally not advised. For more info on usage see: http://codex.wordpresorg/Class_Reference/WP_Query#Permission_Parameters
//////Search Parameter
    's' => $s,                              //(string) - Passes along the query string variable from a search. For example usage see: http://www.wprecipes.com/how-to-display-the-number-of-results-in-wordpress-search 
    'exact' => true                         //(bool) - flag to make it only match whole titles/posts - Default value is false. For more information see: https://gist.github.com/2023628#gistcomment-285118
    'sentence' => true                      //(bool) - flag to make it do a phrase search - Default value is false. For more information see: https://gist.github.com/2023628#gistcomment-285118
//////Post Field Parameters
    //Not sure what these do. For more info see: http://codex.wordpress.org/Class_Reference/WP_Query#Post_Field_Parameters
//////Filters
    //For more information on available Filters see: http://codex.wordpress.org/Class_Reference/WP_Query#Filters
);
$the_query = new WP_Query( $args );
// The Loop
if ( $the_query->have_posts() ) :
while ( $the_query->have_posts() ) : $the_query->the_post();
  // Do Stuff
endwhile;
endif;
// Reset Post Data
wp_reset_postdata();
?>
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

**Getting the category by ID**
```php
global $wp_query;
        $args = array(
        'cat' => '2', // gets the category by the id
        'posts_per_page' => -1); //get all posts

$posts = get_posts($args);
        foreach ($posts as $post) :
  //do stuff 
     endforeach;

```

**Getting the categories by slug name**
```php
global $wp_query;
        $args = array(
        'category_name' => 'diet, news', // gets the category by the slug names
        'posts_per_page' => -1); //get all posts

$posts = get_posts($args);
        foreach ($posts as $post) :
  //do stuff 
     endforeach;

```

[go back home][home]

### Template Tags to use for your blog template OR while looping through a post

**reference**
- [codex](https://codex.wordpress.org/Template_Tags)


```php
<?php $args = array(
	'posts_per_page'   => 5,
	'offset'           => 0,
	'category'         => '',
	'category_name'    => '',
	'orderby'          => 'date',
	'order'            => 'DESC',
	'include'          => '',
	'exclude'          => '',
	'meta_key'         => '',
	'meta_value'       => '',
	'post_type'        => 'post',
	'post_mime_type'   => '',
	'post_parent'      => '',
	'author'	   => '',
	'author_name'	   => '',
	'post_status'      => 'publish',
	'suppress_filters' => true 
);
$posts_array = get_posts( $args ); ?>

```

[go back home][home]

### How to turn on wordpress debug messages

In the wp-config.php file, add this code

**reference**
- [source](https://codex.wordpress.org/Debugging_in_WordPress)



```php
define( 'WP_DEBUG', true );

```

[go back home][home]

### How to remove “Powered by Wordpress” in footer

**reference**
- [source](http://www.wpbeginner.com/wp-themes/how-to-remove-the-powered-by-wordpress-footer-links/)
 

1. Go to **footer.php** and comment out the `get_template_part()` that  has footer

```php
// get_template_part(‘template-parts/footer/site’, ‘info’);

```

[go back home][home]

### How to customize login form

If you want to change the style of the wordpress login form here 
are a couple of ways of doing it.

**reference**
- [source](https://codex.wordpress.org/Customizing_the_Login_Form)

**To create an inline style sheet to change login**
```php
function my_login_logo() { ?>
    <style type="text/css">
        #login h1 a, .login h1 a {
            background-image: url(<?php echo get_stylesheet_directory_uri(); ?>/images/site-login-logo.png);
		height:65px;
		width:320px;
		background-size: 320px 65px;
		background-repeat: no-repeat;
        	padding-bottom: 30px;
        }
    </style>
<?php }
add_action( 'login_enqueue_scripts', 'my_login_logo' );

```

**To have a style sheet to change login**
```php

function my_login_stylesheet() {
    wp_enqueue_style( 'custom-login', get_stylesheet_directory_uri() . '/style-login.css' );
    wp_enqueue_script( 'custom-login', get_stylesheet_directory_uri() . '/style-login.js' );
}
add_action( 'login_enqueue_scripts', 'my_login_stylesheet' );
```

[go back home][home]

### How to get posts with get_posts

**reference**
- [source](https://codex.wordpress.org/Template_Tags/get_posts)


```php


```

[go back home][home]


### how to create a page template 

**reference**
- [wordpress](https://developer.wordpress.org/themes/template-files-section/page-template-files/)

**Inside your page template add this**
```php

<?php /* Template Name: Example Template */ ?>
```

[go back home][home]

### how to change siteurl from old domain

**reference**
- [Redirecting to old domain after migration](https://wordpress.stackexchange.com/questions/187574/redirecting-to-old-domain-after-migration)

#### Option 1: change siteurl in MySQL

1. Log into your mysql account and access your wordpress database

2. select wp_options table and update the `siteurl` and `home` columns

```sql

update wp_options set option_value = "yourNewDomain.com" where option_name = "siteurl";

update wp_options set option_value = "yourNewDomain.com" where option_name = "home"; 

```
3. Once you change the names to your domain, everything will be all good.

[go back home][home]

### how to customize a sidebar
**reference**
- [customizing sidebars](https://codex.wordpress.org/Customizing_Your_Sidebar)
- [Sidebars](https://developer.wordpress.org/themes/functionality/sidebars/)

```


```
[go back home][home]

### what does the template hierarchy look like

**reference**
- [interactive hierarchy map](https://wphierarchy.com/)
- [template-hierarchy](https://developer.wordpress.org/themes/basics/template-hierarchy/)

![idk](https://developer.wordpress.org/files/2014/10/wp-hierarchy.png)

[go back home][home]

### how to allow installation of plugins/themes

**reference**
- [How do I enable Wordpress to update itself through its back end?](https://www.digitalocean.com/community/questions/how-do-i-enable-wordpress-to-update-itself-through-its-back-end)

#### Option 1

you can either write this in the terminal

```
 sudo chown www-data:www-data ./
```

#### Option 2

second option is to change the group to www-data and give permissions to them,
and then add FS_METHOD

```
// in terminal
sudo chgrp -R www-data /var/www/sitename.com
sudo chmod -R g+w /var/www/sitename.com
find /var/www/sitename.com -type d -exec chmod g+s {} \;
```

```
// in wp-config.php add this

define( 'FS_METHOD', 'direct' );
```

[go back home][home]

### how to add css/js files


**To add css**
```
wp_enqueue_style( string $handle, string $src = '', array $deps = array(), string|bool|null $ver = false, string $media = 'all' )
```

**To add js**
```
wp_enqueue_script( string $handle, string $src = '', array $deps = array(), string|bool|null $ver = false, bool $in_footer = false )
```

**reference**
- [enqueue scripts](https://codex.wordpress.org/Plugin_API/Action_Reference/wp_enqueue_scripts)


**This gets the parent theme**
```php
// in functions.php add this

add_action( 'wp_enqueue_scripts', 'my_theme_enqueue_styles' );
function my_theme_enqueue_styles() {
    wp_enqueue_style( 'parent-style', get_template_directory_uri() . '/style.css' );

}


```
**This gets the child theme**
```php
// in functions.php add this

<?php

add_action( 'wp_enqueue_scripts', 'my_theme_enqueue_scripts' );

function my_theme_enqueue_scripts() {
    wp_enqueue_script( 'js-style', get_theme_file_uri().'/js/index.js' );

}


```
[go back home][home]


### how to create a child theme

**reference**
- [child theme](https://codex.wordpress.org/Child_Themes)

1. Go to the folder that the parent theme is located and open the style.css

```css
/* copy the style header that looks like this*/

/*
Theme Name: Twenty Seventeen
Theme URI: https://wordpress.org/themes/twentyseventeen/
Author: the WordPress team
Author URI: https://wordpress.org/
Description: Twenty Seventeen brings your site to life with header video and immersive featured images. With a focus on business sites, it features multiple sections on the front page as well as widgets, navigation and social menus, a logo, and more. Personalize its asymmetrical grid with a custom color scheme and showcase your multimedia content with post formats. Our default theme for 2017 works great in many languages, for any abilities, and on any device.
Version: 1.3
License: GNU General Public License v2 or later
License URI: http://www.gnu.org/licenses/gpl-2.0.html
Text Domain: twentyseventeen
Tags: one-column, two-columns, right-sidebar, flexible-header, accessibility-ready, custom-colors, custom-header, custom-menu, custom-logo, editor-style, featured-images, footer-widgets, post-formats, rtl-language-support, sticky-post, theme-options, threaded-comments, translation-ready

This theme, like WordPress, is licensed under the GPL.
Use it to make something cool, have fun, and share what you've learned with others.
*/


```
2. Now create the folder for the child theme

```
mkdir <insert child theme folder name>

touch functions.php style.css

```
3. open the style.css inside the child theme

```css
//paste parent header content

/*
Theme Name: Twenty Seventeen Child
Theme URI: https://wordpress.org/themes/twentyseventeen/
Author: the WordPress team
Author URI: https://wordpress.org/
Description: Twenty Seventeen brings your site to life with header video and immersive featured images. With a focus on business sites, it features multiple sections on the front page as well as widgets, navigation and social menus, a logo, and more. Personalize its asymmetrical grid with a custom color scheme and showcase your multimedia content with post formats. Our default theme for 2017 works great in many languages, for any abilities, and on any device.
Version: 1.3
License: GNU General Public License v2 or later
License URI: http://www.gnu.org/licenses/gpl-2.0.html
Text Domain: twentyseventeen
Tags: one-column, two-columns, right-sidebar, flexible-header, accessibility-ready, custom-colors, custom-header, custom-menu, custom-logo, editor-style, featured-images, footer-widgets, post-formats, rtl-language-support, sticky-post, theme-options, threaded-comments, translation-ready

This theme, like WordPress, is licensed under the GPL.
Use it to make something cool, have fun, and share what you've learned with others.
*/


```

4. now add the template property to header content

```css

// copy folder name of the parent theme and put it inside template
// you can also change the name of the child by changing the *Theme Name*

/*
Template : twentyseventeen
Theme Name: Twenty Seventeen Child
Theme URI: https://wordpress.org/themes/twentyseventeen/
Author: the WordPress team
Author URI: https://wordpress.org/
Description: Twenty Seventeen brings your site to life with header video and immersive featured images. With a focus on business sites, it features multiple sections on the front page as well as widgets, navigation and social menus, a logo, and more. Personalize its asymmetrical grid with a custom color scheme and showcase your multimedia content with post formats. Our default theme for 2017 works great in many languages, for any abilities, and on any device.
Version: 1.3
License: GNU General Public License v2 or later
License URI: http://www.gnu.org/licenses/gpl-2.0.html
Text Domain: twentyseventeen
Tags: one-column, two-columns, right-sidebar, flexible-header, accessibility-ready, custom-colors, custom-header, custom-menu, custom-logo, editor-style, featured-images, footer-widgets, post-formats, rtl-language-support, sticky-post, theme-options, threaded-comments, translation-ready

This theme, like WordPress, is licensed under the GPL.
Use it to make something cool, have fun, and share what you've learned with others.
*/
```
5. now go to the dashboard and click on themes


6. and then activate the child theme

[go back home][home]


### how to install wordpress

1. log into mysql and type this into the terminal

```mysql
	CREATE DATABASE wordpress DEFAULT CHARACTER SET utf8 COLLATE utf8_unicode_ci;
```
2. create a user specifically for wordpress and type

```mysql
	GRANT ALL ON wordpress.* TO 'wordpressuser'@'localhost' IDENTIFIED BY 'password';
	FLUSH PRIVILEGES;
	EXIT;
```
3. install the additional php extensions

```
	sudo apt-get update
	sudo apt-get install php-curl php-gd php-mbstring php-mcrypt php-xml php-xmlrpc
	sudo systemctl restart apache2
```
4. go into apache2.conf file to allow htaccess overrides

```
	sudo nano /etc/apache2/apache2.conf

	// add this into the file

	<Directory /var/www/html/>
    	AllowOverride All
	</Directory>
```
5. enable the changes and restart apache2

```
	sudo a2enmod rewrite
	sudo apache2ctl configtest
	sudo systemctl restart apache2
```
6. download wordpress and unzip it

```
	cd /tmp
	curl -O https://wordpress.org/latest.tar.gz
	tar xzvf latest.tar.gz
```
7.  do some shit with wordpress

```
	touch /tmp/wordpress/.htaccess
	chmod 660 /tmp/wordpress/.htaccess
	cp /tmp/wordpress/wp-config-sample.php /tmp/wordpress/wp-config.php
	mkdir /tmp/wordpress/wp-content/upgrade
	sudo cp -a /tmp/wordpress/. /var/www/html
```
8. configure wordpress

```
	sudo chown -R yourName:www-data /var/www/html
	sudo find /var/www/html -type d -exec chmod g+s {} \;
	sudo chmod g+w /var/www/html/wp-content
	sudo chmod -R g+w /var/www/html/wp-content/themes
	sudo chmod -R g+w /var/www/html/wp-content/plugins
```

9. creating keys and passwords
```
	// copy the printed keys
	curl -s https://api.wordpress.org/secret-key/1.1/salt/

	sudo nano /var/www/html/wp-config.php

	// place the printed keys in the file
	// and add in the database information  like this

	define('DB_NAME', 'wordpress');

	/** MySQL database username */
	define('DB_USER', 'wordpressuser');

	/** MySQL database password */
	define('DB_PASSWORD', 'password');

	. . .

	define('FS_METHOD', 'direct');
```
10. Setup the apache server to host the wordpress, and then you are done

[go back home][home]
