
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
- add_submenu_page
- array_key_exists
- checked
- current_user_can
- do_settings_sections
- esc_html
- esc_attr
- esc_url
- get_admin_page_title
- get_option
- plugin_dir_path
- [register_setting][register-setting] 
- sanitize_text_field
- selected
- settings_fields
- stripslashes_deep
- submit_button
- [update_option][update-option]
- wp_kses
- wp_kses_allowed_html
- wp_kses_post
- wp_update_user



## How to
- [make a basic plugin][basic-plugin]

[add-menu-page]:#add_menu_page
[update-option]:#update_option
[add-filter]:#add_filter
[basic-plugin]:#make-a-basic-plugin
[add-settings-section]:#add_settings_section
[home]:#plugins
[add-settings-field]:#add_settings_field
[add-options-page]:#add_options_page
[register-setting]:#register_setting


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
