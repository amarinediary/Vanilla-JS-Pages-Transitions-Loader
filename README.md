# Sailor

Sailor is a lightweight, 890 bytes (or boat) Wordpress pages transition loader with no dependencies beside Wordpress jQuery core version or higher.

- View it live @ https://codepen.io/amarinediary/full/ExgRzLV

## Installation

Add the following, to the top of your Wordpress `function.php` file, and paste `sailor.min.js` to you theme's root directory.

```
add_action( 'admin_enqueue_scripts', 'sailor', PHP_INT_MIN );
function sailor() {
  wp_enqueue_script( 'sailor_js', get_template_directory_uri() . '/sailor.min.js', array( 'jquery' ), '1.0.0', true );
  add_filter( 'script_loader_tag', 'data_sailor_js', PHP_INT_MIN, 3 );
  function data_sailor_js( $tag, $handle, $src ) {
    if( $handle === 'sailor_js' ) {
      $tag = str_replace( "<script", "<link rel='preload prefetch' href='" . esc_url( $src ) . "' as='script' /><script", $tag );
    };
    return $tag;
  };
};
```

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.
