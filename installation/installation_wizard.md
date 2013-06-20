# Installation Wizard

## Step 1: Check library

First of all the library gets checked if it's is located properly and is accessible. If no errors were found, this step will not be displayed.


## Step 2: Check requirements

Before we start installing something we want to make sure everything is configured right. The wizard goes through all [Minimum Requirements](minimum-requirements) like PHP Version, subfolder restriction, PHP Extensions, PHP ini-settings, PHP functions and webserver configuration.

![Installation step 2](https://raw.github.com/forkcms/documentation/master/installation/assets/installation_step2.png)

At last, the filesystem got checked. Some directories need write priveleges in order to create cache files or to upload assets. You can use your ftp-client or `chmod` on systems were you got ssh access to set the proper rights.

![Installation step 2 - Filesystem check](https://raw.github.com/forkcms/documentation/master/installation/assets/installation_step2_filesystem.png)


## Step 3: Languages

One of the most remarkable features of Fork CMS is the built-in support for multilingual setups. In this step the languages are chosen for both front- as backend. The default language that you select in this step is shown when the *locale* module couldn't determine the browser's language.

![Installation step 3](https://raw.github.com/forkcms/documentation/master/installation/assets/installation_step3.png)


## Step 4: Modules & Debug mode

It is recommended to only install modules that are necessary for the initial version of the website, after the installation it requires just a click to add the extra modules. Enable debug module to prevent caching while developing the website.

![Installation step 4](https://raw.github.com/forkcms/documentation/master/installation/assets/installation_step4.png)


## Step 5: Database

Enter your MySQL credentials.

![Installation step 5](https://raw.github.com/forkcms/documentation/master/installation/assets/installation_step5.png)


## Step 6: God

The user that you create here during the installation has a god status (and will have an avatar of Chuck Norris by default!), which means he has all rights. Make sure you have decent password for this almighty power.

![Installation step 6](https://raw.github.com/forkcms/documentation/master/installation/assets/installation_step6.png)


## Step 7: Finishing

Finally all necessary files get created in the background and your success message is displayed.

![Installation step 7](https://raw.github.com/forkcms/documentation/master/installation/assets/installation_step7.png)

If the installation is finished you can [start configuring](../getting-started/index) your website and tools.