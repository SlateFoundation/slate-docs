## Overview
Server-side components are primarily implemented via PHP classes stored within the `php-classes` tree. Following the 
[PSR-4 autoloader](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md) standard, each file
must contain exactly one PHP class, with the filename exactly matching the class name, suffixed with a `.php` extension. The
directory structure between `php-classes` and the class file must exactly match the declared namespace for the class.

PHP classes are put to use by request-handling scripts within [`site-root`](site-root), and their public static properties
can be configured by corresponding files in [`php-config`](php-config).

## Creating a simple class
In this example, we create a class that provides a wrapper for instantiating the official Facebook API class, with settings
configurable via public static properties in `php-classes/RemoteSystems/FacebookApp.php`:

```language-php
<?php

namespace RemoteSystems;

use Facebook;

class FacebookApp
{
    public static $apiAppId;
    public static $apiSecret;
    protected static $_instance;

    public static function getApi()
    {
        if (!isset(static::$_instance)) {
            static::$_instance = new Facebook(array(
                'appId'  => static::$apiAppId,
                'secret' => static::$apiSecret,
                'cookie' => true
            ));
        }

        return static::$_instance;
    }
}
```

Now, you can create a separate file under [`php-config`](php-config) to store the actual app ID and secret key, allowing them to be
overridden from inheriting sites and kept separate from the code in `php-config/RemoteSystems/FacebookApp.config.php`:

```language-php
<?php

RemoteSystems\FacebookApp::$apiAppId  = '1234567890987654321';
RemoteSystems\FacebookApp::$apiSecret = 'aBcDeFgHiJkLmNoPqRsTuVwXyZ1234567890';
```

## Creating a record model
Model classes allow you to define an object that can be persisted in a database table. The PHP class contains everything needed
to generate the schema of the table, and comes with basic methods for storing, retrieving, and manipulating database records by
implementing the common [active record pattern](https://en.wikipedia.org/wiki/Active_record_pattern).

In this example, we create a class to keep track of projector requests and store it in `php-classes/MySchool/Requests/Projector.php`:

```language-php
<?php

namespace MySchool\Requests;

class Projector extends \ActiveRecord
{
    // ActiveRecord configuration
    public static $tableName       = 'requests-projector';
    public static $singularNoun    = 'projector request';
    public static $pluralNoun      = 'projector requests';
    public static $collectionRoute = '/requests/projectors';

    public static $fields = array(
        'Status' => array(
            'type'    => 'enum',
            'values'  => array('Requested', 'Scheduled', 'Denied'),
            'default' => 'Requested'
        ),
        'RequestorID' => 'uint',
        'LocationID'  => 'uint',
        'StartTime'   => 'timestamp',
        'EndTime'     => 'timestamp'
    );

    public static $validators = array(
        'RequestorID' => array(
            'validator'    => 'number',
            'min'          => 0,
            'errorMessage' => 'ID of requesting person required'
        ),
        'LocationID' => array(
            'validator'    => 'number',
            'min'          => 0,
            'errorMessage' => 'ID of requested location required'
        ),
        'StartTime' => array(
            'validator'    => 'datetime',
            'errorMessage' => 'Requested starting time required'
        ),
        'EndTime' => array(
            'validator'    => 'datetime',
            'errorMessage' => 'Requested starting time required'
        )
    );

    public static $relationships = array(
        'Requestor' => array(
            'type'  => 'one-one',
            'class' => 'Person'
        ),
        'Location' => array(
            'type'  => 'one-one',
            'class' => 'Emergence\\Locations\\Location'
        )
    );
}
```

The table for this class will be automatically created the first time you attempt to persist a record to the database. Until then,
all fetch records will silently return an empty result set. To examine the generated table structure or manually trigger the
creation of the table, visit `/table_manager` in your browser.