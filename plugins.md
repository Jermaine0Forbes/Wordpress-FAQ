
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



## How to
- [make a basic plugin][basic-plugin]

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


### do_settings_sections
<details>
  <summary>
  View Content
  </summary>

**reference**
- [wordpress](https://developer.wordpress.org/reference/functions/do_settings_sections/)

**Parameter**

`do_settings_sections( string $page )`



```

```
</details>

[go back :house:][home]

### settings-fields
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
