# Minimum requirements

## Server

* PHP 5.3.3 or higher
* The following PHP extensions should be installed and enabled: [cURL](http://php.net/curl), [libxml](http://php.net/libxml), [DOM](http://php.net/dom), [SimpleXML](http://php.net/simplexml), [SPL](http://php.net/manual/en/book.spl.php), [PDO](http://php.net/pdo) (with MySQL driver), [mb_string](http://php.net/mb_string), [iconv](http://php.net/iconv), [GD2 graphics library](http://php.net/manual/en/book.image.php), [json](http://php.net/json), [PCRE](http://php.net/pcre).
* MySQL 5.0 or higher
* Apache 2.0 with .htaccess, mod_rewrite, mod_expires (optional but recommended), mod_deflate (optional) enabled. A guide for alternative webservers is also [available](webservers).

If you're uncertain if your server matches these requirements you can execute the [`php_info()`](http://php.net/phpinfo) function by creating a file with the following content:
```php
<?php
phpinfo();
?>
```
When pointing your browser to that file, you will see what extensions which are enabled.


> Please note that Fork can not be installed in [subdirectories](faq).


## Browser versions

The administration interface of Fork CMS is compatible with Internet Explorer 8 and later. Chrome, Firefox, Opera and Safari have an automatic update system. Therefore we only support the latest versions for those browsers.

The browser support for the frontend is depending on the theme you choose. We ask theme developers to document known issues for browsers in the description of their theme.
