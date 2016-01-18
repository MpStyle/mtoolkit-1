MToolkit
========

#Summary
- [Intro](#into)
- [Some good features](#some_good_features)
- [Install](#install)
- [MToolkit modules](#mtoolkit_modules)
- [Software using MToolkit](#software_using_mtoolkit)
- [Let's start](#lets_start)

#<a name="intro"></a>Intro

MToolkit is a simple PHP toolkit, it is compliant with the PSR-0 Standard:
- A fully-qualified namespace and class must have the following structure \\\<Vendor Name>\\\(\<Namespace\>)*\\\<Class Name>.
- Each namespace must have a top-level namespace ("Vendor Name"). (Missing)
- Each namespace can have as many sub-namespaces as it wishes.
- Each namespace separator is converted to a DIRECTORY_SEPARATOR when loading from the file system.
- Each underscore in the class name is converted to a DIRECTORY_SEPARATOR. The underscore has no special meaning in the namespace.
- The fully-qualified namespace and class is suffixed with .php when loading from the file system.
- Alphabetic characters in vendor names, namespaces, and class names may be of any combination of lower case and upper case.

It was born from a requirement: develop a website quickly and powerfully.

I know, someone can say "Use Zend Framwork, CakePHP!", but I could reply: "They are very good toolkits, but they aren't the toolkit that I want!" :P

The development model of MToolkit is *rolling release*. I search some people (developer or not) to increase and modify this strategy: my goal is to manage the versioning of this framework. 


The experiences with other toolkits in different platforms have led me to create this toolkit.

MToolkit was born like a mash-up of two frameworks: .NET and Qt. o_O

Yes, the framework of the evil and the desktop framework for excellence.

#<a name="install"></a>Install
To have a full installation of the framework, add into your composer.json file:
```json
{
    "require": {
        "mtoolkit/mtoolkit": "0.1.*"
    }
}
```
Or run the console command:
```
composer require mpstyle/mtoolkit
```

#<a name="some_good_features"></a>Some good features
- Completely Object Oriented
- Autoload of classes (PSR-0 Standard)
- Autorun of pages and of [RPC Json web services](https://github.com/MpStyle/MToolkit/tree/master/Network/RPC/Json) from controller classes
- Javascript frameworks compatibility (jQuery, Bootstrap, etc)
- Master page concept (http://msdn.microsoft.com/it-it/library/system.web.ui.masterpage.aspx)
- Decoupling between business logic and graphics
- Fluent setters

#<a name="mtoolkit_module"></a>MToolkit module
Like Qt, MToolkit has a lot of modules, one for every type of usage.
Here you are the list:
- [Core](https://github.com/mtoolkit/mtoolkit-core)
- [Network](https://github.com/mtoolkit/mtoolkit-network)
- [Model](https://github.com/mtoolkit/mtoolkit-model)
- [Controller](https://github.com/mtoolkit/mtoolkit-controller)
- [View](https://github.com/mtoolkit/mtoolkit-view)
- [Cache](https://github.com/mtoolkit/mtoolkit-cache)
- [Entity](https://github.com/mtoolkit/mtoolkit-entity)

#<a name="software_using_mtoolkit"></a>Software using MToolkit
- [Back-end of TVGuide](https://play.google.com/store/apps/details?id=net.micene.minigroup.palimpsests.lite)
- [Notification Manager](https://github.com/MpStyle/NotificationManager)
- [TV Guide web site](http://tvguide.micene.net/)

#<a name="lets_start"></a>Let's start

Create a folder for your project.

Download the latest version of MToolkit in the project folder, we suggest you using Composer.

On the root of your project create a new file (*Settings.php*) with this content:

```php

<?php
require_once __DIR__.'/MToolkit/Core/MCore.php';

use MToolkit\Core\MApplication;

class Settings
{
    public static function run()
    {
        // Set the root path of the project
        MApplication::setApplicationDirPath(__DIR__);
    }
}

Settings::run();

```

This file sets the root of your project and now you have no longer to use *require*, *require_once*, *include*, *include_once* directives. 

**This file must be included in every entry page of your project.**

##Entry page

An entry page is the page loaded at start time.
Now, we will see how to create the controller of the entry page and his html code.

Controller (Index.php):

```php
<?php

require_once __DIR__ . '/Settings.php';

use \MToolkit\Controller\MAbstractPageController;

class Index extends MAbstractPageController
{
    private $masterPage;

    public function __construct()
    {
        parent::__construct(__DIR__.'/Index.view');
    }

    public function helloWorld()
    {
        return "Hello World";
    }
} 

        
        
```

And the *view* file. Every view file must contain the meta tag, with the correct *content-type*:
```html
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
```
*Index.view*:

```php
<?php /* @var $this Index */ ?>
<html>
    <head>
        <title>Entry page</title>
        <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    </head>
    <body>
        <b><?php echo $this->helloWorld(); ?></b>
    </body>
</html>
```

##Using Composer
*composer.json*:
```json
{
  "require": {
    "mpstyle/mtoolkit": "dev-master"
  }
}
```

On the root of your project create a new file (*Settings.php*) with this content:

```php

<?php
require_once __DIR__ . '/vendor/autoload.php';

use MToolkit\Core\MApplication;

class Settings
{
    public static function run()
    {
        // Set the root path of the project
        MApplication::setApplicationDirPath(__DIR__);
    }
}

Settings::run();

```

And now you can create your web app.
