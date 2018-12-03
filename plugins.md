
# Plugins

## Useful Plugins
- Simply Show Hooks
- Yoast SEO
- Smush
- W3 total cache

## Functions
- add_action
- [add_filter][add-filter]
- [add_menu_page][add-menu-page]
- [add_options_page][add-options-page]
- [add_settings_field][add-settings-field]
- [add_settings_section][add-settings-section]
- [add_submenu_page][add-submenu-page]
- array_key_exists
- checked
- current_user_can
- [do_settings_sections][do-settings-sections]
- esc_html
- esc_attr
- esc_url
- get_admin_page_title
- get_option
- plugin_dir_path
- [plugins_url][plugins-url]
- [register_setting][register-setting] 
- sanitize_text_field
- selected
- [settings_fields][settings-field]
- [stripslashes_deep][stripslashes-deep]
- submit_button
- [update_option][update-option]
- [wp_create_nonce][wp-create-nonce]
- [wp_kses][wp-kses]
- wp_kses_allowed_html
- wp_kses_post
- wp_update_user

## Sanitization
- [how to sanitize text fields][sanitize-text]

## How to
- [make a basic plugin][basic-plugin]
- [how to add js files to your plugin][js-plugin]
- [how to add css files to your plugin][css-plugin]
- [basic plugin creation][basic-plugin-create]

[sanitize-text]:#how-to-sanitize-text-fields
[css-plugin]:#how-to-add-css-files-to-your-plugin
[js-plugin]:#how-to-add-js-files-to-your-plugin
[settings-field]:#settings_fields
[plugins-url]:#plugins_url
[basic-plugin-create]:#basic-plugin-creation
[do-settings-section]:#do_settings_sections
[wp-create-nonce]:#wp_create_nonce
[stripslashes-deep]:#stripslashes_deep
[add-submenu-page]:#add_submenu_page
[add-menu-page]:#add_menu_page
[update-option]:#update_option
[add-filter]:#add_filter
[basic-plugin]:#make-a-basic-plugin
[add-settings-section]:#add_settings_section
[home]:#plugins
[add-settings-field]:#add_settings_field
[add-options-page]:#add_options_page
[register-setting]:#register_setting


### how to sanitize text fields
<details>
  <summary>
  View Content
  </summary>

If you are using the **register_setting** function,
this is how you sanitize the text fields

1. create a function that will validate all the input fields in the form

```php

// the input variable will be the option name of the input
function validate_icecream($input){

	if(isset($input["type"])){
		// $input["type"] = sanitize_text_field($input["type"]);
		$input["type"] = "cherry";
	}
	if(isset($input["date"])){
		$input["date"] = sanitize_text_field($input["date"]);

	}
	if(isset($input["weight"])){
		$input["weight"] = sanitize_text_field($input["weight"]);
	}

//make sure you hit return
	return $input;
}
```

2. now you have to add the function into another function called register_setting

```php
register_setting("icecream_plugin", "icecream_option",
array("type"=>"string","sanitize_callback" => "validate_icecream" ));
```
</details>

[go back :house:][home]


### how to add css files to your plugin
<details>
  <summary>
  View Content
  </summary>

**reference**
- [stackoverflow](https://stackoverflow.com/questions/3760222/how-to-include-css-and-jquery-in-my-wordpress-plugin)

```php
function register_styles(){
  wp_register_style("icecream",plugins_url("/css/icecream_style.css",__FILE__));
  wp_enqueue_style("icecream");


}

add_action("admin_enqueue_scripts","register_styles");


```
</details>

[go back :house:][home]


### how to add js files to your plugin
<details>
  <summary>
  View Content
  </summary>

  **reference**
  - [stackoverflow](https://stackoverflow.com/questions/3760222/how-to-include-css-and-jquery-in-my-wordpress-plugin)

```php
function register_script(){

  wp_enqueue_script("icecream-js",plugins_url("/js/icecream_script.js",__FILE__));
}

add_action("admin_enqueue_scripts","register_script");
```
</details>

[go back :house:][home]



### plugins_url
<details>
  <summary>
  View Content
  </summary>

**reference**
- [wordpress](https://codex.wordpress.org/Function_Reference/plugins_url)

**Parameters**

` <?php plugins_url( $path, $plugin ); ?> `

```php
echo '<img src="' . plugins_url( 'images/wordpress.png', __FILE__ ) . '" > ';
```
</details>

[go back :house:][home]


### basic plugin creation
<details>
  <summary>
  View Content
  </summary>

1.  create a name of a plugin in the plugins folder and name the folder and file the same

```
   mkdir icecream-plugin
   touch icecream-plugin/icecream-plugin.php
```

2. inside the file create add the plugin information and the code to prevent people
  from accessing  it

```php
/*

Plugin Name: Icecream Plugin
Plugin URI: https:w.jermaineforbes.com/plugins/icecream_plugin
Author: Jermaine Forbes
Description: This is just a basic plugin for wordpress
Author URI: www.jforbes.site
License: GPL 2.0+
Text Domain: icecream_plugin
*/


// exit if file is called directly
if ( ! defined( 'ABSPATH' ) ) {

	exit;

}
```

3. Add the code that will be shown in settings page of the plugin, then add the
action hook to include in the admin menu

```

// This will be the settings page of the plugin
function display_icecream_page(){

  ?>
  <div class="wrap">
    <h2>Something </h2>
    <form  action="options.php" method="post">

      <?php

        // this will be the hidden fields of the form
        settings_fields("icecream_plugin");

        //this will show all sections and fields that is going to be in the plugin
        do_settings_sections("icecream_plugin");

        // this is obviously a submit button
        submit_button("save the icecream");
        ?>
    </form>
  </div>

  <?php
}

// this is the function that will add the plugin menu to the admin menu
function add_icecream_menu(){

  add_menu_page(
    "Ice Cream Plugin",// this will show up as the title page when you visit the plugin setting page
    "Ice Cream",// this will show up as the name in the admin menu
    "manage_options",// I'm pretty sure you're always supposed to add this
    "icecream_plugin",//This should be the text domain name of the plugin
    "display_icecream_page", // this is function that is supposed show the setting page
    "dashicons-lightbulb" // this is the icon that will show up next to the plugin menu name


  );

}



// this is the hook that will add all of this shit to admin page
add_action("admin_menu", "add_icecream_menu");

```

4. Now, to add fields and sections to the settings page do this

```php
function add_icecream_settings(){

  add_settings_section(
    "icecream_section",// this is the id for section
    "Icecream Section", // This print out the name for the section
    "icecream_section_cb",// this is a function that will output information at the top of the section
    "icecream_plugin");// This is for the text domain

  add_settings_field(
  "icecream_type", // this is the id for the field
  "Icecream Type", // the name for the field
   "icecream_type_cb",//this function  will output the html to the form
   "icecream_plugin",//this is for the text domain
   "icecream_section",//this is where you will hook the field to the specific section
   array("label_for" =>"icecream_type","class" => "icecream_type"));//adds classes, that's all you need to know

  add_settings_field(
    "icecream_weight",
    "Icecream Weight(kg)",
    "icecream_weight_cb",
    "icecream_plugin",
    "icecream_section");

  add_settings_field(
    "icecream_date",
    "When did you eat the Icecream",
    "icecream_date_cb",
    "icecream_plugin",
    "icecream_section");

  register_setting(
    "icecream_plugin", //I think you're supposed to add the text-domain here
    "icecream_option");//This is the name of the option that will be saved in the database

}

//hooks all the shit up
add_action("admin_init","add_icecream_settings");
```

5. Now you have to add the actual sections/fields for the data

```
function icecream_section_cb(){
  echo "This is some expensive icecream";
}

function icecream_type_cb(){



  ?>
  <input type="text" name="icecream_option[type]" value="<?php echo get_option('icecream_option')['type']; ?>">

  <?php
}

function icecream_weight_cb(){
  ?>
    <input type="number" name="icecream_option[weight]" value="<?php echo get_option('icecream_option')['weight']; ?>">
  <?php
}

function icecream_date_cb(){
  ?>
    <input type="date" name="icecream_option[date]" value="<?php echo get_option('icecream_option')['date']; ?>">
  <?php
}
```

6. Now this is what you do to deactivate and remove data from the database... I think

```php
// remove options on uninstall
function icecream_on_uninstall() {

	if ( ! current_user_can( 'activate_plugins' ) ) return;

	delete_option( 'icecream_option' );

}
register_uninstall_hook( __FILE__, 'icecream_on_uninstall' );
```

7. And that my friends is the basic way to create plugin

</details>

[go back :house:][home]


### do_settings_sections
<details>
  <summary>
  View Content
  </summary>

**reference**
- [wordpress](https://developer.wordpress.org/reference/functions/do_settings_sections/)

**Parameter**

`do_settings_sections( string $page )`


</details>

[go back :house:][home]

### settings_fields
<details>
  <summary>
  View Content
  </summary>

**reference**
- [wordpress](https://developer.wordpress.org/reference/functions/settings_fields/)

**Parameters**

`settings_fields( string $option_group )`

**Options**

```
$option_group
(string) (Required) A settings group name. This should match the group name used in register_setting().
```

**Example**

```php
echo '<form method="post" action="options.php">';
settings_fields( 'wpdocs-plugin-settings-group' );
```
</details>

[go back :house:][home]



### wp_create_nonce
<details>
  <summary>
  View Content
  </summary>

**reference**
- [wordpress](https://developer.wordpress.org/reference/functions/wp_create_nonce/)
- [tipsandtricks](https://www.tipsandtricks-hq.com/introduction-to-wordpress-nonces-5357)

**My definition:** I really don't know what the fuck this thing is about. Apparently
it is used identifying the user id?

```php
$my_nonce = wp_create_nonce('delete_my_rec');
?>
<a href='admin.php?page=mypluginpage&action=delete&recid=1&_wpnonce=<?php echo $my_nonce ?>'>Delete Me</a>

```
</details>

[go back :house:][home]



### stripslashes_deep
<details>
  <summary>
  View Content
  </summary>

**reference**
- [wordpress](https://codex.wordpress.org/Function_Reference/stripslashes_deep)

**Wordpress Definition:** Navigates through an array and removes slashes from the values.

```php
$my_post = stripslashes_deep($_POST);
$my_value = $my_post['value'];
```
</details>

[go back :house:][home]




### wp_kses
<details>
  <summary>
  View Content
  </summary>

**reference**
- [wordpress](https://developer.wordpress.org/reference/functions/wp_kses/)

  `wp_kses( string $string, array $allowed_html, array $allowed_protocols = array() )`

**Options**
```
$string
(string) (Required) Content to filter through kses

$allowed_html
(array) (Required) List of allowed HTML elements

$allowed_protocols
(array) (Optional) Allowed protocol in links.

Default value: array()
```
</details>

[go back :house:][home]

### add_submenu_page
<details>
  <summary>
  View Content
  </summary>

**reference**
- [wordpress](https://developer.wordpress.org/reference/functions/add_submenu_page/)

`add_submenu_page( string $parent_slug, string $page_title, string $menu_title, string $capability, string $menu_slug, callable $function = '' )`

**Options**
```
$parent_slug
(string) (Required) The slug name for the parent menu (or the file name of a standard WordPress admin page).

$page_title
(string) (Required) The text to be displayed in the title tags of the page when the menu is selected.

$menu_title
(string) (Required) The text to be used for the menu.

$capability
(string) (Required) The capability required for this menu to be displayed to the user.

$menu_slug
(string) (Required) The slug name to refer to this menu by. Should be unique for this menu and only include lowercase alphanumeric, dashes, and underscores characters to be compatible with sanitize_key().

$function
(callable) (Optional) The function to be called to output the content for this page.

Default value: ''

```


**Example**
```php
/**
 * Adds a submenu page under a custom post type parent.
 */
function books_register_ref_page() {
    add_submenu_page(
        'edit.php?post_type=book',
        __( 'Books Shortcode Reference', 'textdomain' ),
        __( 'Shortcode Reference', 'textdomain' ),
        'manage_options',
        'books-shortcode-ref',
        'books_ref_page_callback'
    );
}

/**
 * Display callback for the submenu page.
 */
function books_ref_page_callback() {
    ?>
    <div class="wrap">
        <h1><?php _e( 'Books Shortcode Reference', 'textdomain' ); ?></h1>
        <p><?php _e( 'Helpful stuff here', 'textdomain' ); ?></p>
    </div>
    <?php
}
```
</details>

[go back :house:][home]


### add_menu_page
<details>
  <summary>
  View Content
  </summary>

**reference**
- [wordpress](https://developer.wordpress.org/reference/functions/add_menu_page/)

`add_menu_page( string $page_title, string $menu_title, string $capability, string $menu_slug, callable $function = '', string $icon_url = '', int $position = null )`


```
$page_title
(string) (Required) The text to be displayed in the title tags of the page when the menu is selected.

$menu_title
(string) (Required) The text to be used for the menu.

$capability
(string) (Required) The capability required for this menu to be displayed to the user.

$menu_slug
(string) (Required) The slug name to refer to this menu by. Should be unique for this menu page and only include lowercase alphanumeric, dashes, and underscores characters to be compatible with sanitize_key().

$function
(callable) (Optional) The function to be called to output the content for this page.

Default value: ''

$icon_url
(string) (Optional) The URL to the icon to be used for this menu.
* Pass a base64-encoded SVG using a data URI, which will be colored to match the color scheme. This should begin with 'data:image/svg+xml;base64,'.
* Pass the name of a Dashicons helper class to use a font icon, e.g. 'dashicons-chart-pie'.
* Pass 'none' to leave div.wp-menu-image empty so an icon can be added via CSS.

Default value: ''

$position
(int) (Optional) The position in the menu order this one should appear.

Default value: null



```

```php
/**
 * Register a custom menu page.
 */
function wpdocs_register_my_custom_menu_page() {
    add_menu_page(
        __( 'Custom Menu Title', 'textdomain' ),
        'custom menu',
        'manage_options',
        'myplugin/myplugin-admin.php',
        '',
        plugins_url( 'myplugin/images/icon.png' ),
        6
    );
}
add_action( 'admin_menu', 'wpdocs_register_my_custom_menu_page' );
```
</details>

[go back :house:][home]


### update_option
<details>
  <summary>
  View Content
  </summary>

  **reference**
  - [wordpress](https://developer.wordpress.org/reference/functions/update_option/)


  `update_option( string $option, mixed $value, string|bool $autoload = null )`

  **My defintion:** updates the value of the option, if the option does not exist
   it will create the option for you

```php
$option_name = 'my_custom_color_option' ;
$new_value = 'red';

if ( get_option( $option_name ) !== false ) {

    // The option already exists, so update it.
    update_option( $option_name, $new_value );

} else {

    // The option hasn't been created yet, so add it with $autoload set to 'no'.
    $deprecated = null;
    $autoload = 'no';
    add_option( $option_name, $new_value, $deprecated, $autoload );
}
```
</details>

[go back :house:][home]




### add_filter
<details>
  <summary>
  View Content
  </summary>

  **reference**
  - [wordpress](https://developer.wordpress.org/reference/functions/add_filter/)

  **My definition:** I think it grabs data from a specific hook and you are able to
  manipulate it and return the modified value

  `add_filter( string $tag, callable $function_to_add, int $priority = 10, int $accepted_args = 1 )`

```php
// returns six sections from the front page of the website

add_filter( 'twentyseventeen_front_page_sections', 'prefix_custom_front_page_sections' );

function prefix_custom_front_page_sections( $num_sections )
{
        return 6;
}



```
</details>

[go back :house:][home]


### make a basic plugin
<details>
  <summary>
  View Content
  </summary>

  **reference**
  - [WordPress Settings API Tutorial with Examples](http://qnimate.com/wordpress-settings-api-a-comprehensive-developers-guide/)

```

```
</details>

[go back :house:][home]


### add_settings_section
<details>
  <summary>
  View Content
  </summary>

**reference**
- [wordpress](https://developer.wordpress.org/reference/functions/add_settings_section/)

**Parameters**
`add_settings_section( string $id, string $title, callable $callback, string $page )`

**Options**
```
Parameters #Parameters
$id
(string) (Required) Slug-name to identify the section. Used in the 'id' attribute of tags.

$title
(string) (Required) Formatted title of the section. Shown as the heading for the section.

$callback
(callable) (Required) Function that echos out any content at the top of the section (between heading and fields).

$page
(string) (Required) The slug-name of the settings page on which to show the section. Built-in pages include 'general', 'reading', 'writing', 'discussion', 'media', etc. Create your own using add_options_page();
```

```php
add_settings_section(
    'eg_setting_section',
    __( 'Example settings section in reading', 'textdomain' ),
    'wpdocs_setting_section_callback_function',
    'reading'
);

/**
 * Settings section display callback.
 *
 * @param array $args Display arguments.
 */
function wpdocs_setting_section_callback_function( $args ) {
    // echo section intro text here
    echo '<p>id: ' . esc_html( $args['id'] ) . '</p>';                         // id: eg_setting_section
    echo '<p>title: ' . apply_filters( 'the_title', $args['title'] ) . '</p>'; // title: Example settings section in reading
    echo '<p>callback: ' . esc_html( $args['callback'] ) . '</p>';             // callback: eg_setting_section_callback_function
}
```
</details>

[go back :house:][home]

### add_settings_field
<details>
  <summary>
  View Content
  </summary>

**reference**  
- [wordpress](https://developer.wordpress.org/reference/functions/add_settings_field/)

**Parameters**
`add_settings_field( string $id, string $title, callable $callback, string $page, string $section = 'default', array $args = array() )`

**Options**
```
$id
(string) (Required) Slug-name to identify the field. Used in the 'id' attribute of tags.

$title
(string) (Required) Formatted title of the field. Shown as the label for the field during output.

$callback
(callable) (Required) Function that fills the field with the desired form inputs. The function should echo its output.

$page
(string) (Required) The slug-name of the settings page on which to show the section (general, reading, writing, ...).

$section
(string) (Optional) The slug-name of the section of the settings page in which to show the box.

Default value: 'default'

$args
(array) (Optional) Extra arguments used when outputting the field.

'label_for'
(string) When supplied, the setting title will be wrapped in a <label> element, its for attribute populated with this value.
'class'
(string) CSS Class to be added to the <tr> element when the field is output.
Default value: array()
```

```php
add_settings_field( 'myprefix_setting-id',
    'This is the setting title',
    'myprefix_setting_callback_function',
    'general',
    'myprefix_settings-section-name',
    array( 'label_for' => 'myprefix_setting-id' ) );
```
</details>

[go back :house:][home]



### register_setting
<details>
  <summary>
  View Content
  </summary>

**reference**
- [wordpress](https://developer.wordpress.org/reference/functions/register_setting/)


**Parameters**
`register_setting( string $option_group, string $option_name, array $args = array() )`


**Options**
```
$option_group
(string) (Required) A settings group name. Should correspond to a whitelisted option key name. Default whitelisted option key names include "general," "discussion," and "reading," among others.

$option_name
(string) (Required) The name of an option to sanitize and save.

$args
(array) (Optional) Data used to describe the setting when registered.

'type'
(string) The type of data associated with this setting. Valid values are 'string', 'boolean', 'integer', and 'number'.
'description'
(string) A description of the data attached to this setting.
'sanitize_callback'
(callable) A callback function that sanitizes the option's value.
'show_in_rest'
(bool) Whether data associated with this setting should be included in the REST API.
'default'
(mixed) Default value when calling get_option().
Default value: array()
```

```php
/**
* Registers a text field setting for Wordpress 4.7 and higher.
**/
function register_my_setting() {
    $args = array(
            'type' => 'string',
            'sanitize_callback' => 'sanitize_text_field',
            'default' => NULL,
            );
    register_setting( 'my_options_group', 'my_option_name', $args );
}
add_action( 'admin_init', 'register_my_setting' );
```
</details>

[go back :house:][home]

### add_options_page

<details>
  <summary>
  View Content
  </summary>

**reference**
- [wordpress](https://developer.wordpress.org/reference/functions/add_options_page/)

```

```
</details>

[go back :house:][home]
