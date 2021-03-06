[![Packagist](https://img.shields.io/packagist/l/doctrine/orm.svg)]()
[![Maintenance](https://img.shields.io/maintenance/yes/2018.svg)]()
[![npm](https://img.shields.io/badge/npm-%3E4.1-blue.svg)]()
[![php](https://img.shields.io/badge/php->5.4-green.svg)]()
[![php](https://img.shields.io/badge/php-7.x-green.svg)]()
[![CocoaPods](https://img.shields.io/badge/docs-60%25-yellow.svg)]()


# PHP Auto Include AutoLoadOne Generator
AutoloadOne is a program that generates an autoload class (Auto Include) for PHP that is project specific. This class is useful to use classes on code without calling each "include" manually.
Contrary to other alternatives, it supports the easiest way to autoload classes using PHP without sacrifice performance.  How it works?. AutoLoadOne pre-calculates every class of a project and generates a single autoload.php file that it's ready to use.  You don't need a specific folder, structure or rule to use it. Just generate the autoload class, include and you are ready to load any class (even classes without a namespace, classes in the namespace in different folders, multiple classes defined in a single file...).  

AutoLoadOne is a replacement to Composer's Autoload, rendering obsolete the use of psr-0 or psr-4.  

**Last Update September 5, 2018**

> "Universal Autoloading classes in PHP, any class, any time!"

## How it Works?

:one:  
 Run AutoLoadOne.php as CLI or as Web.  
:two:  
 AutoLoadOne will generate a single file called autoload.php based in your project. For the record, it takes mere 1.5 seconds to scan Wordpress and yes, it is compatible with Wordpress.  
:three:  
 Include autoload.php in your project code and start using it.  

## When i should re-run AutoLoadOne?

You don't need to run it again if you are adding a new class with the same namespace in the same folder.

Also, you could edit autoload.php manually by adding more classes and namespaces.

Or you could run AutoLoadOne.php again and replace the old autoload.php

## Composer Autoload features:
:black_square_button: One class per file  
:black_square_button: One Namespace per file.  
:black_square_button: The file must have a namespace.  
:black_square_button: It requires composer.  
:black_square_button: It validates the file each file the class is loaded per user.  
:black_square_button: The structure of the folders should be pre-defined.  
:white_check_mark: Support CLI  

## AutoLoadOne extended features:
:white_check_mark: One or Many classes per file.  
:white_check_mark: One or many namespaces per file.  
:white_check_mark: The file could contain optionally a namespace.  
:white_check_mark: It only requires PHP  
:white_check_mark: The folder structure and classes are validated once.  
:white_check_mark: If you add a class that shares a previous folder and uses the previous namespace, then you don't need to run the generator.  
:white_check_mark: You could use any structure of folder. It's recommended to use the same folder for the same namespace but it's not a requisite.  
:white_check_mark: Support CLI and Web-UI.  
:white_check_mark: It doesn't require APCU, lock files or cache.  
:white_check_mark: It´s compatible with practically any project, including a project that uses Composer's autoload.  
:white_check_mark: PSR-0, PSR-4, and practically  any specification, since you don't need to use any special configuration or standard.  

## Usage (generate code via Web)

:one:  
 Copy the file **autoloadone.php** somewhere.

:two:  
 For security, you couldedit the first lines of the class **autoloadone.php**. Change the user, password and autoloadenter if it's required.

```php
<?php
define("_AUTOLOAD_USER","autoloadone");
define("_AUTOLOAD_PASSWORD","autoloadone");
define("_AUTOLOAD_ENTER",true); // if you want to autoload (no user or password) then set to true
?>
```
:three:  
   Start the browser

Enter your user and password.  If _AUTOLOAD_ENTER is true then you are logged automatically.

![autoloadone login](https://github.com/EFTEC/AutoLoadOne/blob/master/doc/login.jpg "Autoloadone logon")


:four:  
 Select the folder to scan, then select the file to generate and finally press the button GENERATE.

![autoloadone screen](https://github.com/EFTEC/AutoLoadOne/blob/master/doc/screen.jpg "Autoloadone screen")

* Root Folder : The folder to scan.
* Generated File: The full path (local) of the autoload.php.  Even if you are not using the generation of file, you must specify it, because the program uses for determine the relative path.
* Save File: If you check it, then generate file will be generated.  If PHP doesn't have access to save the file, then you could copy the code manually (screen Result)
* Excluded Namespace : Namespace excluded of mapping.
* Excluded Map : Paths excluded to scan (they are not recursives)



:five:  
 The result should looks this:

![autoloadone screen2](https://raw.githubusercontent.com/EFTEC/AutoLoadOne/master/doc/screen2.jpg "Autoloadone screen2")

## Usage (via cli)

![autoloadone cli](https://raw.githubusercontent.com/EFTEC/AutoLoadOne/master/doc/cli1.jpg)

In the shell, browser to the folder where you want to generate the code and run the next command

Commands available :  

* current (scan and generates files from the current folder)  
* folder (folder to scan)  
* filegen (folder where autoload.php will be generate)  
* save yes/no (save the file to generate).This option is required.
* excludens (namespace excluded)  
* excludepath (path excluded)  


> Example: php autoloadone.php -folder folder\scan -filegen folder\whereautoload\ -save yes


```
php folder/located/autoloadone.php -current
```



## Usage of the generated file autoload.php

:one:  
include the generated file by the previous step. ex: autoload.php

```php
<?php
define("_AUTOLOAD_ONEDEBUG",true); // this line is optional. By default, the DEBUG is off. The debug mode is used for find errors.
include "autoload.php"; // it could be an absolute or relative path.
?>
```
and that's it!.

In the /test folder you could find some example to try.

> Note:Finally, you could delete the file autoloadone.php if you wish for.

## Note

> If you want to exclude a class, you could add the namespace to the exclude list, or you could skip a folder.  
> Also, if a class has the next comment, it's excluded automatically:

```php
<?php
// @noautoload
?>
```
> If you find the error: Parse error: syntax error, <message> in on line 000. Then some of the php files scanned have some syntax error. The solution is to fix the problem or to exclude the whole folder.  
> How to find the file with error? You could run the page with the debug flag: autoloadone.php?debug=1  

## Benchmark

PHP 7.1.18 + Windows 10 + SSD.

![autoloadone benchmark](https://github.com/EFTEC/AutoLoadOne/blob/master/doc/speed.jpg "Autoloadone benchmarj")  

_More is better._


> I did a synthetic benchmark by loading different classes and reading the performance of it. Since my machine has a SSD disk then, the impact of the disk is minimum in comparison with a mechanical hard disk.
> This chart compares the performance against INCLUDE.

## Security

> :heavy_exclamation_mark: While the program has a build-in-security measure, however I suggest to protect adding new layers of security such as locating the AutoLoadOne.php file outside of the public/web folder.

> AutoLoadOne.php is not safe (because it writes a generate file), it doesn't have access to the database, neither it allows to write any content to the file but, it could overwrite an exist code and put down a system.

> However, the generate file is safe (autoload.php) and you could expose to the net.

* Change the user and password and set _AUTOLOAD_ENTER to false.
* Or, Don't put this file in your public website.
* Or, change the filename.
* Or, you could block the access to the file using .htaccess or similar.  

```
RewriteEngine On
RewriteBase /

<Files "AutoLoadOne.php">
Order Allow,Deny
Deny from all
</Files>
```

* Or you could restrict the access to PHP and it's the behaviour by default on Linux (it runs under Apache's account, most of the time as user NOBODY)

## Version
* 1.5 2018-09-05 Now the interface open automatically by default. This file must be delete or restricted if it's used publicity.
* 1.4 2018-08-25 Some example. Now the interface doesn't open automatically by default. It's for security.
* 1.3 2018-07-05 Now it works with interface and it fixes a problem with some specific file.  It also fixes a problem with linux vs windows folder.
* 1.2 2018-07-01 Lots of changes. Modified exclusion.  Title and icons for the web ui.  It also allows to disable the web.
* 1.1 2018-06-26 Some fixes. 
* 1.0 2018-06-24 First version  

## Todo
* Save configuration
* CLI (more commands)
* Clean the code.
* ~~Convert to a single class.~~
* External folder/library (relative or absolute path)
* The generation fails if a php file has an error.
* Specify the extensions. By default it scans only .php files.