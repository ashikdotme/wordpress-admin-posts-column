# wordpress-admin-posts-column


// Add the thumbnail column
add_filter('manage_gallery_posts_columns', 'add_gallery_thumbnail_column');
function add_gallery_thumbnail_column($columns) {
    $columns['thumbnail'] = __('Thumbnail');
    return $columns;
}

// Display the thumbnail in the column
add_action('manage_gallery_posts_custom_column', 'display_gallery_thumbnail_column', 10, 2);
function display_gallery_thumbnail_column($column, $post_id) {
    if ($column === 'thumbnail') {
        echo get_the_post_thumbnail($post_id, array(80, 80)); // Set the size of the thumbnail
    }
}

// Add the custom author column to the Testimonials custom post type
add_filter('manage_testimonials_posts_columns', 'add_testimonial_author_column');
function add_testimonial_author_column($columns) {
    $columns['testimonials_author'] = __('Author'); // Add the 'Author' column for ACF field
    return $columns;
}

// Display the custom author field value in the 'Author' column
add_action('manage_testimonials_posts_custom_column', 'display_testimonial_author_column', 10, 2);
function display_testimonial_author_column($column, $post_id) {
    if ($column === 'testimonials_author') {
        // Retrieve the custom author field using ACF
        $custom_author = get_field('testimonials_author', $post_id); // 'testimonials_author' is the ACF field name

        // Display the custom author value
        if (!empty($custom_author)) {
            echo esc_html($custom_author); // Display the author from the ACF field
        } else {
            echo __('No author specified');
        }
    }
}
