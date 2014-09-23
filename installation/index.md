## Step 1: Download

PHP Developers using composer could use this command to install the latest stable release for Fork from the command line:

    composer create-project forkcms/forkcms .

Alternatively, you can install Fork CMS by downloading it from the website.
Before downloading, check if your server meets the [minimum requirements](minimum-requirements) for
Fork CMS. If it does, create a MySQL database and remember the credentials. Next,
[download](http://www.fork-cms.com/download) the lastest release and
[unpack](http://en.wikipedia.org/wiki/Tar_%28file_format%29) the folder.

![Download started](https://raw.github.com/forkcms/documentation/master/installation/assets/started_download.jpg)

## Step 2: Upload

Use an FTP Program like [Transmit](http://www.panic.com/transmit/) (Mac) or [Smart FTP](http://www.smartftp.com/)
(PC) to upload the contents of the folder to the root of the server that will host your website.

Upload the unpacked files into the document_root of your webserver. Make sure you've also copied the
**.htaccess** file, as it may be hidden on certain fileservers.

![Upload started](https://raw.github.com/forkcms/documentation/master/installation/assets/started_upload.jpg)

## Step 3: Installation

Use your browser to surf to your domain (this should forward you to the Fork CMS installer).
[Follow the steps](installation-wizard) and you're done!

![Installation started](https://raw.github.com/forkcms/documentation/master/installation/assets/started_install.jpg)

> Don't panic if you experience problems during the installation. Start by taking a look in our
[Frequently Asked Questions](faq).
