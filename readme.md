# Wordpress Reference

- [Wordpress Function Reference][function-ref]
- [Post Reference][post-ref]
- [how to create a page template][page-temp]
- [how to change siteurl from old domain to new domain][change-domain]
- [how to allow installation of plugins/themes][allow-install]
- [how to add css/js files][css]
- [how to  create a child theme][child]
- [how to install wordpress][install]
- [how to customize a sidebar][sidebar]
- [what does the template hierarchy look like][hierarchy]
- [how to use add_action and do_action][add-action]
- [how to get src of  feature imaged post][image-post]
- [the List of WP_Query arguments][query-arguments]
- [how to get the parent category of a child category while looping through $query->have_posts()][parent-child]
- [how to get all posts from category][all-category]
- [Template Tags to use for your blog template OR while looping through a post][template-tags]
- [How to turn on wordpress debug messages][debug]
- [How to remove “Powered by Wordpress” in footer][remove-footer]
- [How to customize login form][customize-form]
- [how to get posts with get_posts()][get-posts]
- [how to add scripts from different urls][add-script]

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

### How to add scripts from different urls

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

[go back home][home]

### Wordpress function reference

**reference**
-  [wordpress](https://codex.wordpress.org/Function_Reference)

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


### how to create a page template 

**reference**
- [wordpress][https://developer.wordpress.org/themes/template-files-section/page-template-files/]

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
`wp_enqueue_style( string $handle, string $src = '', array $deps = array(), string|bool|null $ver = false, string $media = 'all' )`

**To add js**
`wp_enqueue_script( string $handle, string $src = '', array $deps = array(), string|bool|null $ver = false, bool $in_footer = false )`

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
