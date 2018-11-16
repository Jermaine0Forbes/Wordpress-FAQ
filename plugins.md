
# Plugins

## Useful Plugins
- Simply Show Hooks
- Yoast SEO
- Smush
- W3 total cache

## Functions
- add_action
- [add_filter][add-filter]
- add_menu_page
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


[update-option]:#update_option
[add-filter]:#add_filter
[basic-plugin]:#make-a-basic-plugin
[add-settings-section]:#add_settings_section
[home]:#plugins
[add-settings-field]:#add_settings_field
[add-options-page]:#add_options_page
[register-setting]:#register_setting


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
