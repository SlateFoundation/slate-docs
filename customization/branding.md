## Overview
You can change the logo and slogan shown in the site's header without overriding any of Slate's
[HTML templates](../developing/html-templates) or [Sass stylesheets](../developing/site-root#sass).

## Logo {#logo}
Create a file named `logo.png` and upload it to the `site-root/img` directory.

## Slogan, name, and abbreviation {#config}
The school's name will, by default, reflect the name of the site you created, and the abbreviation will default to all the capital
letters from the school name (e.g., "MyTown High" and "MTH"). If you want to change the school slogan and/or override the
default name or abbreviation, you can do this by editing the file `php-config/Slate.config.php`. If you haven't previously customized
this file, find the default version under `_parent/php-config/Slate.config.php` and open that to start. When you save your changes,
a new copy will be created in your local `php-config` directory.

Uncomment any settings you want to change by removing the `//` symbols from the front of the line. In the example below, the slogan has been customized:

```language-php
<?php

//Slate::$schoolName = 'MyTown High';
//Slate::$schoolAbbr = 'MTH';
Slate::$siteSlogan = 'School is cool!';
```

## Colors {#theme}
Before working on the Slate theme, visit `/sass/compile` at least once first to recompile the stock theme. This pulls down all the source
files for the stock theme from the parent site to give you an easy framework to explore and start overriding aspects of it. Be sure to refresh
the `site-root` folder if you've already expanded it after running `/sass/compile`.

The colors and basic style settings used throughout Slate can be customized by setting [Sass](../developing/site-root#sass) variables in
`site-root/sass/_customizations.scss` and then recompiling the site's Sass to CSS. Look at `site-root/sass/slate/_defaults.scss` for a
list of the Sass variables available and their default values.

For example, at the top of `site-root/sass/slate/_defaults.scss` we see:
```language-scss
$base-color:     #008cc1 !default; // Slate blue
$contrast-color: #e8910c !default; // orange
$warning-color:  red     !default;
```

To change the base color to orange and the contrast to blue (swapping their default values), you could add the following lines to `site-root/sass/_customizations.scss`:
```language-scss
$base-color:     #e8910c; // orange
$contrast-color: #008cc1; // Slate blue
```

Finally, visit `/sass/compile` in your browser to compile your Sass source files into CSS. The page will take a few moments to load
while the compilation happens. If you see <samp>CMD finished: exitCode=0</samp> in the output, then compilation was successful.

## Screencast
<iframe width="640" height="360" src="//www.youtube.com/embed/CQP-rKC_h1o?rel=0" frameborder="0" allowfullscreen></iframe>