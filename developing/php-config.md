## Overview
Files placed in the `php-config` directory should correspond one-to-one with files in `php-classes`, matching them in path and name.
Whenever a PHP class within `php-classes` is loaded, a corresponding file ending in `.config.php` is checked for under `php-config`
and, if found, is executed before the PHP class is used at all. The config script can modify any of the class' public static
properties and has access to details of the current request, including the currently logged-in user (if available).

Slate's PHP classes are designed to expose their configurable options in this way, and those based on Emergence's ActiveRecord
base class -- used to define and interface with database tables -- expose their fields, relationships, and validation to be modified
and extended in this fashion.

## Examples

### Changing the school name, abbreviation, or slogan
See [&rarr;&nbsp;Slogan, name, and abbreviation](../customization/branding#config)

### Adding a field to the courses table
For example, suppose you want to add an additional field to your courses table, to map courses to district-issued course codes.

The courses table is defined by the PHP class `Slate\Courses\Course`, which is loaded from the file
`php-classes/Slate/Courses/Course.php` and can be configured by a file saved to `php-config/Slate/Courses/Course.config.php`:

```language-php
Slate\Courses\Course::$fields['DistrictCode'] = array(
    'type'    => 'string',
    'notnull' => false
);
```

### Add a field to the users table
Similarly, to keep track of which campus a student attends, we can add a field to the users table by creating a config file
for the `Slate\Student` class at `php-config/Slate/Student.config.php`:

```language-php
Slate\Student::$fields['Campus'] = array(
    'type'    => 'enum',
    'values'  => array(1, 2, 3),
    'notnull' => false
);
```

### Integrate with different Canvas accounts based on user's campus
Building on the example above, and the fact that config files are scripts with access to information about the current request and user,
we can do something more advanced, like varying our settings for connecting to another system based on the current user:

```language-php
<?php

RemoteSystems\Canvas::$canvasHost = 'myschool.instructure.com';
RemoteSystems\Canvas::$apiToken   = 'aBcDeFgHiJkLmNoPqRsTuVwXyZ12345';

if ($GLOBALS['Session']->Person &&
    $GLOBALS['Session']->Person->Campus) {
    // user is logged in and has a campus set
    RemoteSystems\Canvas::$accountID = $GLOBALS['Session']->Person->Campus;
} else {
    // default to account 1
    RemoteSystems\Canvas::$accountID = 1;
}
```