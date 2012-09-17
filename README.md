tidy-tag-cloud
=================

Nicer lightweight WP tag cloud without inline style and better configurability such as custom css classes, return objects instead of strings and more.

Installation
------------

Place tidy-tag-cloud.php in your plugins folder and activate it.

Usage
-----

Instead of wp_tag_cloud(), use tidy_tag_cloud(). It accepts the same parameters as wp_tag_cloud plus:

```
array(
	'tag_class' => '',	// css class for each individual tag, use '' for no class
	'list_class' => 'wp-tag-cloud',	// css class for the ul list, use '' for no class
	'show_default_tag_class' => false,	// show or hide the default tag class (tag-link-x)
	'show_title' => true	// show or hide link title
)
```

If the format parameter is set to array, an array of tag objects will be returned:

```
$tag = (object)array(
	'id' => 0,
	'link' => '',
	'name' => '',
	'size' => 0,
	'title' => '',
	'count' => 0,
	'css_class' => ''
)
```

### Filters

Remember to add the last parameters 10, 2.

```
// called for each individual tag
add_filter('tidy_tag_cloud_tag', function($tag, $args) {
	// modify $tag properties, no need to return anything
	$tag->title = 'Custom title';
}, 10, 2);

// called for the complete output
add_filter('tidy_tag_cloud_output', function($output, $args) {
	// modify and return $output
	$output = 'Replace the whole output';
	return $output;
}, 10, 2);
```

### Example

```
tidy_tag_cloud(array(
	'smallest' => 9,
	'largest' => 22,
	'unit' => 'px',
	'format' => 'flat',
	'tag_class' => 'tag',
	'show_default_tag_class' => false,
	'show_title' => false
));

// output:
<a href="http://your-blog.com/tags/tag-name" class="tag size-10">Tag name</a>
...

$tags = tidy_tag_cloud(array(
	'smallest' => 9,
	'largest' => 22,
	'unit' => 'px',
	'format' => 'array',
	'tag_class' => 'tag',
	'show_default_tag_class' => false,
	'show_title' => false
));

foreach ($tags as $tag)
	echo 'Tag: ' . $tag->name;

// output:
Tag: Tag name
```

Changelog
---------

### 1.0.0

* Initial release