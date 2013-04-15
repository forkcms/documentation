# Minimum requirements

These are the minimum requirements to run Fork CMS:

* PHP 5.3.3 or higher
* The following PHP extensions should be installed and enabled: [cURL](http://php.net/curl), [libxml](http://php.net/libxml), [DOM](http://php.net/dom), [SimpleXML](http://php.net/simplexml), [SPL](http://php.net/manual/en/book.spl.php), [PDO](http://php.net/pdo) (with MySQL driver), [mb_string](http://php.net/mb_string), [iconv](http://php.net/iconv), [GD2 graphics library](http://php.net/manual/en/book.image.php), [json](http://php.net/json), [PCRE](http://php.net/pcre).
* MySQL 5.0 or higher
* Apache 2.0 with .htaccess, mod_rewrite, mod_expires (optional but recommended), mod_deflate (optional) enabled.

If you're uncertain if your server matches these requirements you can execute the [`php_info()`](http://php.net/phpinfo) function.

> Please note that Fork can not be installed in subdirectories.

> A guide for alternative webserver is also available.