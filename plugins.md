
# Plugins

## Useful Plugins
- Simply Show Hooks
- Yoast SEO

## Functions
- add_action
- add_filter
- add_menu_page
- [add_options_page][add-options-page]
- [add_settings_field][add-settings-field]
- add_settings_section
- add_submenu_page
- current_user_can
- do_settings_sections
- esc_html
- esc_url
- get_admin_page_title
- get_option
- [register_setting][register-setting] 
- sanitize_text_field
- settings_fields
- submit_button
- wp_kses_post
- wp_update_user

## How to


[home]:#plugins
[add-settings-field]:#add_settings_field
[add-options-page]:#add_options_page
[register-setting]:#register_setting

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
