# Logs



## 11/29/18

###  Things to learn from  wordpress plugin development
-  create a php class to for a plugin
-  create a submenu in the menu of your custom plugin
- create a custom post type

## 9/20/18

### How to add a php plugin to the dashboard menu

```php
// exit if file is called directly
if ( ! defined( 'ABSPATH' ) ) {

	exit;

}

// display the plugin settings page
function simple_example_display_settings_page() {

	// check if user is allowed access
	if ( ! current_user_can( 'manage_options' ) ) return;

	?>

	<div class="wrap">
		<h1><?php echo esc_html( get_admin_page_title() ); ?></h1>
		<form action="options.php" method="post">

			<?php

			// output security fields
			settings_fields( 'simple-example_options' );

			// output setting sections
			do_settings_sections( 'simple-example' );

			// submit button
			submit_button();

			?>

		</form>
	</div>


<?php
}
  // add top-level administrative menu
function myplugin_add_toplevel_menu() {

	/*
		add_menu_page(
			string   $page_title,
			string   $menu_title,
			string   $capability,
			string   $menu_slug,
			callable $function = '',
			string   $icon_url = '',
			int      $position = null
		)
	*/

	add_menu_page(
		'Simple Example Settings',
		'Simple',
		'manage_options',
		'simple-example',
		'simple_example_display_settings_page',
		'dashicons-admin-generic',
		null
	);

}
add_action( 'admin_menu', 'myplugin_add_toplevel_menu' );



```

## 9/14/18

### Validation Functions
- is_email : checks if email is valid
- term_exists: checks if term exists
- username_exists

### Sanitization functions
- sanitize_emal
- sanitize_text_field
- sanitize_user

### Reseaerch what the fuck is "Nonces"

also look it this/these functions
- wp_nonce_field
- wp_verify_nonce

### Look into wordpress boilerplates to get started coding plugins
It should go without saying to search for these keywords on the internet

- wordpress plugin boilerplate
- wp skeleton plugin

## 9/13/18

### Add into functions
- register_uninstall_hook
- register_deactivate_hook
- register_activation_hook
- add_option
- delete_option

### Look into pluggable functions

I believe they are wordpress functions that you can override and add to your plugins


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
