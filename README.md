# WP Setting Media #

WP drop-in to add media attachments to settings

## Description ##

> This WordPress drop-in requires at least [WordPress](https://wordpress.org) 4.7.

Adding attachments to settings through the Media Library is simplified through this drop-in class. Use this in your plugin or theme to add media selection in your settings workflow. 

## Usage ##

To include this drop-in in your project, do the following:

1. Put the drop-in class file and `assets` folder in your project
2. Require the `class-wp-setting-media.php` class file in your main project file
3. Register a setting media item with the `wp_setting_media()` function, generally at the 'init' action
4. Use the `wp_setting_media_field()` template tag in the your settings admin page where you want to have the selector field - usually in the settings field callback.
5. You're done!

```php
// 2. In your main project file
require( $path_to_file . 'class-wp-setting-media.php' );

// 3. When hooking in 'init'
wp_setting_media(
	__FILE__,       // Location where the assets folder was placed
	'setting-name', // Setting key/name
	array(
		'mime_type'  => 'image', // Mime type of selectable attachments. Can be 'image', 'video', 'audio', or any mime type in wp_get_mime_types(). Defaults to 'image'.
		'image_size' => array( 50, 50 ), // For images, the size to add when it does not exist yet. Can be image size name or array with dimensions.
		'labels'     => array(           // Labels for the Media Library
			'setSettingMedia'    => __( 'Set Setting Attachment',    'your-textdomain' ),
			'settingMediaTitle'  => __( 'Setting Attachment',        'your-textdomain' ),
			'removeSettingMedia' => __( 'Remove Setting Attachment', 'your-textdomain' ),
		),
	)
);

// 4. In your settings field callback
wp_setting_media_field( array(
	'setting'     => 'setting-name', // The setting key/name
	'description' => esc_html__( 'Field description', 'your-textdomain' ) // Optional field description, wrapped in `<p class="description"></p>`
) );
```

## Contributing ##

You can contribute to the development of this drop-in by [opening a new issue](https://github.com/lmoffereins/wp-setting-media/issues/) to report a bug or request a feature in the drop-in's GitHub repository.

## Related ##

See also the [`WP_Post_Media`](https://github.com/lmoffereins/wp-post-media/) and [`WP_Term_Media`](https://github.com/lmoffereins/wp-term-media/) drop-ins, to select media attachments for posts and terms respectively.
