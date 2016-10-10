# Alternative webservers

To be a lean, mean, SEO-machine, Fork CMS uses url-rewriting to form a proper url-structure for your website. Fork CMS has been configured to work well with Apache out of the box, but it can run perfectly on other servers as well (such as Lighttpd and Nginx).

## Apache

Although Fork CMS should run fine on Apache without additional configuration, during installation you may receive a warning message. If you do, you should verify that the ".htaccess" file is present in the root of your Fork CMS folder.

The .htaccess-file is the Apache configuration file and is a hidden file on Unix-based systems; as such it may not have been unpacked. Please make sure that the **.htaccess** file is present in your document root and contains [this content](https://github.com/forkcms/forkcms/blob/master/.htaccess#L1). If it is not present, you can manually create it.

Alternatively, it is possible that your webserver does not allow the server's configuration to be overridden through a .htaccess-file. In that case, contact your hosting provider and ask them to change the **AllowOverride** directive. Another common problem is that the **mod_rewrite** module is not enabled on your webserver, in which case you'll also have to turn to your hosting provider to have them enable this Apache module.

If you see an internal server error, it is possible that your webserver does not allow the first 2 directives of the Fork CMS .htaccess to be set. In this case you can simple remove the line that says:

```
Options +FollowSymlinks -Indexes
```

## Lighttpd

On Apache the .htaccess-file instructs all incoming urls to be parsed by index.php. The Lighttpd-config should reflect this. Here's a sample configuration example:

```
server.modules = (
 "mod_rewrite",
 ...
)
...

## Fork-CMS
$HTTP["host"] =~ "(mydomain.com)" {
server.document-root = "/path/to/forkcms"
dir-listing.activate = "disable"
setenv.add-environment = ( "MOD_REWRITE" => "1")

url.rewrite-if-not-file = ( "^/?$" => "$0",
                "^/(backend|install|api(\/\d.\d)?(\/client)?)/(.*)" => "/index.php/$0",
                "^/(?!(backend|install|api(\/\d.\d)?(\/client)?))(.+)/?$" => "/index.php/$0"
               )

}
```

In this sample configuration, Fork CMS needs to rewrite its urls. This rewrite rule is based on the Apache .htaccess-file and should work with the latest lighttpd 1.4.x without causing a redirect loop.

These are the minimal requirements for Fork CMS to function properly with regards to configuring Lighttpd as your webserver.

Additional configuration options can be added to Lighttpd's configuration file to approximate the behaviour under Apache with regards to caching, compression, and so on.

## Nginx

Another popular lightweight webserver is Nginx. The configuration of this server for Fork CMS is similar to the configuration on a Lighttpd server. Below you can find an example configuration.

```
server {
  listen       80;

  server_name mydomain.com;
  server_name_in_redirect off;
  root /path/to/fork;

  index index.html index.php;
  
  location / {
  	try_files $uri $uri/ /index.php?$args;
  }
  
  location ~ ^/(backend|install|api(\/\d.\d)?(\/client)?).*\.php$ {
  	# backend/install/api are existing dirs, but should all pass via the front
  	try_files $uri $uri/ /index.php?$args;
  }
  
  location ~ ^(.+\.php)(.*)$ {
    include fastcgi_params;
    fastcgi_pass 127.0.0.1:9000;
    fastcgi_index index.php;
  }

  # gzip
  gzip on;
  gzip_disable "MSIE [1-6]\.(?!.*SV1)"; # disables gzip compression for browsers that don't support it (in this case MS Internet Explorer before version 6 SV1).
  gzip_http_version 1.1;
  gzip_vary on; # This sets the response header Vary: Accept-Encoding. Some proxies have a bug in that they serve compressed content to browsers that don't support it. By setting the Vary: Accept-Encoding header, you instruct proxies to store both a compressed and uncompressed version of the content.
  gzip_comp_level 6;
  gzip_proxied any;
  gzip_types text/plain text/html text/css application/json application/x-javascript text/xml application/xml application/xml+rss text/javascript application/javascript text/x-js ;
  gzip_buffers 16 8k;

  # client caching
  location ~ \.(css|js|html|htm|rtf|rtx|svg|svgz|txt|xsd|xsl|xml|asf|asx|wax|wmv|wmx|avi|bmp|class|divx|doc|docx|exe|gif|gz|gzip|ico|jpg|jpeg|jpe|mdb|mid|midi|mov|qt|mp3|m4a|mp4|m4v|mpeg|mpg|mpe|mpp|odb|odc|odf|odg|odp|ods|odt|ogg|pdf|png|pot|pps|ppt|pptx|ra|ram|swf|tar|tif|tiff|wav|wma|woff|wri|xla|xls|xlsx|xlt|xlw|zip)$ {
    expires 31d;
    add_header Pragma "public";
    add_header Cache-Control "public, must-revalidate, proxy-revalidate";
  }
  ...
}
```

## Cherokee

To get Fork CMS working properly Cherokee needs to redirect the request made by the users' browsers. To do this one must edit the default rule of the vhost then add two new rules. Instructions:

1. Open Cherokee Admin
2. Open the behavior settings for the vhost
3. Change the handler of the default rule to “Redirection”
4. Click the “Add New RegEx” button
5. Set type to internal, leave regular expression blank, and set substitution to “/index.php”
6. Create two directory rules: /frontend and /backend (both are Final)
7. Set the handlers of those two rules to “List & Send”
8. Make sure the Directory Rules are under the static content and PHP rules
9. Save the configuration then restart the server.
10. All credits to arch_is_awesome.
