# Logs

## 7/30/18


### Shortcodes with WooCommerce 

[Shortcodes included with WooCommerce](https://docs.woocommerce.com/document/woocommerce-shortcodes/)

### What the hell is call_user_func 

[PHP call_user_func vs. just calling function](https://stackoverflow.com/questions/1596221/php-call-user-func-vs-just-calling-function)

### WooCommerce Product Filter  

[WC Product Filter Tour](https://www.youtube.com/watch?v=Z7My8WsG11w)

## 7/27/18

### adding custom logo 

[wordpress](https://developer.wordpress.org/themes/functionality/custom-logo/)


### how to change custom logo 

[answer](https://wordpress.stackexchange.com/questions/229905/how-to-add-css-class-to-custom-logo)

```php
add_filter( 'get_custom_logo', 'change_logo_class' );


function change_logo_class( $html ) {

    $html = str_replace( 'custom-logo', 'your-custom-class', $html );
    $html = str_replace( 'custom-logo-link', 'your-custom-class', $html );

    return $html;
}
```


## 7/26/18

### If you want to build your own theme

Then go to choose starter theme from underscores, 
or watch the lynda video "Wordpress: building themes from scratch using underscores"

### Things I need to look into 
- yoast seo
- simply wordpress hooks : a plugin to be able to see what hooks are being used
- look into post format : learn how to change post structure 
- woocommerce colors : helps gets the colors ... i dont know
- better font awesome: basically  a font awesome plugin


### Actions I need to look into
- woocommerce_sections_
- woocommerce_settings_
- woocommerce_settings_tabs_
- woocommerce_update_options
- wp
- woocommerce_product_data_panels

### Functions I need to look into
- apply_filters(): applies a function to a filter hook
- get_option()
- in_array()
-  woocommerce_admin_fields()
- woocommerce_update_options
- is_checkout() : checks if you are on the checkout page
- wp_safe_redirect() : redirects a page based on the url
- get_permalink(): returns the url by the id of the page
- woocommerce_wp_text_input(): creates text input for product page tab
- woocommerce_wp_select(): creates a selection where you can add different options
- add_theme_support(): adds support for different functionality  
- remove_action()



### Filters I need to look into
- active_plugins
- woocommerce_settings_tabs_array
- woocommerce-opening-hours
- woocommerce_product_data_tabs


