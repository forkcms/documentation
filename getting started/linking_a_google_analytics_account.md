# Settings: Linking a Google Analytics account

The [analytics module](http://www.fork-cms.com/extensions/detail/analytics) requires you to link a Google Analytics account to Fork. This article will guide you through the process of setting up the analytics module.

## Register domain

A detailed guide can be found on the official google [documentation](https://developers.google.com/accounts/docs/RegistrationForWebAppsAuto).

### Add your domain

On the [Manage Your Domains](https://accounts.google.com/ManageDomains) page, enter the url of your website and click on the *Add Domain* button.

![Add Domain](https://raw.github.com/forkcms/documentation/master/getting%20started/assets/settings_analytics_add_domain.png)

### Verify your domain

The easiest way to verify your domain is by uploading the html file through (s)ftp.

### Provide domain information

The target URL path prefix is just your domain because Fork CMS isn't installable in subdirectories.

![Target URL path prefix](https://raw.github.com/forkcms/documentation/master/getting%20started/assets/settings_analytics_urlpathprefix.png)

## API

### Creating an API key

Go to the [Google API's console](https://code.google.com/apis/console/). If it is the first time, you will need to create a project.

![Start using the Google APIs console](https://raw.github.com/forkcms/documentation/master/getting%20started/assets/settings_analytics_create_project.png)

Go to the *Services* page and activate the *Analytics API* by changing the status to "ON". You might need to agree with the terms of service.

![Google APIs activate service](https://raw.github.com/forkcms/documentation/master/getting%20started/assets/settings_analytics_activate_service.png)

After activating the service go the *API access* page. Under *Simple API Access* click on *Create new Browser key…*.

![Google APIs create API key](https://raw.github.com/forkcms/documentation/master/getting%20started/assets/settings_analytics_create_key.png)

This will open up a dialog, asking you to specify which URL's can use this API key. Leave this empty, this will allow the API key to be used by any domain.

![Google APIs configure API key](https://raw.github.com/forkcms/documentation/master/getting%20started/assets/settings_analytics_configure_api.png)

After creating, the API key will be available on the API Access page under "Simple API Access".

![Google APIs copy API key](https://raw.github.com/forkcms/documentation/master/getting%20started/assets/settings_analytics_key.png)

### Link to the analytics module

Login in to your Fork and go to *Settings -> Modules -> Analytics*. You should see a text field asking you for an API key. Fill in the API key created in the previous step.

![Analytics API key](https://raw.github.com/forkcms/documentation/master/getting%20started/assets/settings_analytics_api_key.png)

After clicking *Link your Google account*, you will be redirected to a Google accounts page asking you to grant access to your Google account. Click *Grant Access*.

![Analytics grant access](https://raw.github.com/forkcms/documentation/master/getting%20started/assets/settings_analytics_grant_access.png)

After granting access you will be redirected back to Fork. You will now be asked to select a profile. This is the profile for which the analytics module will be fetch results.

![Select profile](https://raw.github.com/forkcms/documentation/master/getting%20started/assets/settings_analytics_link_profile.png)

Thats it! After linking a profile you will be able to see statistics in the analytics module.

![Google Analytics is linked](https://raw.github.com/forkcms/documentation/master/getting%20started/assets/settings_analytics_profile_linked.png)

### Known issue: No profiles found

Sometimes your profiles won't show, even if your account is connected succesfully. Google stops sending profiles through their API when one property (web or app) has no specific profile but instead uses All Web Site Data. So make sure that all your properties have profiles.

![All website data](https://raw.github.com/forkcms/documentation/master/getting%20started/assets/settings_analytics_allwebsitedata.png)