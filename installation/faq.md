# FAQ

## Why is Fork not installable into subfolders?

We think developers should try to keep the differences between the server and local machine as little as possible.

If you are developing with an url like http://localhost/projectname/ all your references will be relative, which is a hell when something changes. If you use an url like http://projectname.dev (can be done using virtual host setup on your local web server) you don't have to think about all those references, so you can use / as a starting point.


## I got redirected to /install and get a 500 Forbidden error

Check if your .htaccess file is uploaded correctly. Some operating systems or ftp clients hide this file by default.
