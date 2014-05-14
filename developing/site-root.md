## Overview
Files placed in the `site-root` root directory will be available publicly via URLs on your Slate site matching their path and filename
within `site-root`. Every file in this directory, except those ending in `.php`, will be available for download by anyone with regular
internet access to your web server. You can host files here, or assets like images and stylesheets you want to embed in the Slate
website.

While possible, it is recommended not to use your Slate site as a general file repository or a relay for one-off file sharing -- there
are better services for that purpose. If your site accumulates large files unnecessary to its operation, regular maintenance and backup
operations will become slower and more expensive.

Most files necessary for the operation of Slate will be housed in special directories and not directly in `site-root`.

## Standard directories
Slate uses these directories to organize the files it comes with. You should use the same directories, when applicable, for consistency
and compatibility with built-in optimization tools.

### The `css` directory {#css}
CSS files that style your Slate site should be kept here, optionally organized into subdirectories. Within HTML templates, the
`{cssmin}` plugin is available for optimally serving files from this directory. For example, to include `site-root/css/myschool.css` in
an [HTML template](html-templates), you could simply write `{cssmin "myschool.css"}`; not only would the `<link>` tag to include the
CSS file be generated for you, but the file will also be "minified" and optimized for browser caching automatically. You can even
include multiple CSS files at the same time with wildcards (`*`) and/or plus (`+`) symbols, e.g., `{cssmin "myschool.css+about/*"}`.

### The `js` directory {#javascript}
Javascript files that add interactive behaviors to your Slate site should be kept here, optionally organized into subdirectories. As
with the `css` directory, a `{jsmin}` plugin is available for use within HTML templates to optimally serve files from this directory.
For example, to include `site-root/js/myschool.js` in an [HTML template](html-templates), you could simply write
`{jsmin "myschool.css"`; not only would the `<script>` tag to include the JS file be generated for you, but the file will also be
"minified" and optimized for browser caching automatically. You can even include multiple JS files at the same time with wildcards (`*`)
and/or plus (`+`) symbols: `{jsmin "myschool.js+widgets/*"}`

### The `img` directory {#images}
There's nothing special about this directory, but it's a good place to put images for your site. Organize with subfolders as needed.

### The `sass` directory {#sass}
Slate's CSS is not written directly, but with a *preprocessor* language called [Sass](http://sass-lang.com/). Sass makes it easier to
organize and customize stylesheets for an application like Slate.

If you want to make changes to any of Slate's default styling, try to limit yourself to only overriding `_customizations.scss` and/or
`_overrides.scss` as these files are already plugged into the main Slate stylesheet, primed for site-specific customizations. You can
override other .scss files and create new ones as well, but keep in mind that if you override any of Slate's .scss files you will need
to handle merging any future enhancements to that file from the parent Slate site into your local copy. By limiting your changes to the
`_customizations.scss` and `_overrides.scss` placeholders, you can count on improved compatibility with future enhancements to Slate's
stylesheets.

To compile the .scss files in the `sass` directory to CSS files in the `css` directory, open the URL <kbd>/sass/compile</kbd> on your
site in your browser and wait for the page to finish loading to see the compile status of your Sass.

For more information on editing Sass files to make basic changes to your site's theme, see
[Changing school logo, slogan, and colors](../customization/branding).

## Creating dynamic pages with PHP
To create a dynamic page, or just a page that uses Slate's master design template, you will need to create a file ending in `.php`
within `site-root`. These pages can be accessed from users' web browsers with or without the `.php` extension. It is recommended to omit
the `.php` extension when linking to pages on your Slate site to create friendly and meaningful URLs. For example, if you create the
file `site-root/about/faculty.php`, the URL for viewing it should be <kbd>http://example.com/about/faculty</kbd>.

### A bare-bones PHP script that only renders a template

Saving the following script at `site-root/about/faculty.php` would render the [HTML template](html-templates)
`html-templates/about/faculty.tpl` when a viewer visits <kbd>http://example.com/about/faculty</kbd>:

```language-php
<?php

RequestHandler::respond('faculty');
```