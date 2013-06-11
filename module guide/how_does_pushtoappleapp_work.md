# How does pushToAppleApp() work

If you browse through the code you will see we have methods that notify the admin. One of the methods that is called is pushtToAppleApp().

This method enables you to push notifications to the Fork Pocket App. This application is just a proof of concept, but it demonstrates Fork CMS is able to push data to the application.

## How does it work?

Because we can't publish an application in the Appstore for every Fork install we need a central system that is allowed to push notifications.

That central system is called the Fork CMS API (our API in the image). This part communicates with the Apple-servers.

![How does pushToAppleApp work](https://raw.github.com/forkcms/documentation/master/module%20guide/assets/how_apple_push_works.png)

When you install the Fork Pocket-application it will ask the credentials of your site, as soon as you submit the form it will make a request to your website (1) and will add the ID of your iPhone/iPad/i... in the database.

When someone add a comment on one of your blog-articles the method pushToAppleApp() will be called, in this method we will look for al registered devices. For each device we make a call to our API (2).

Our API will push all queued notification to the Apple Servers (3). Apple will then notify all devices (4). Apple will return the devices that are marked as invalid to us and we will send it back to your website, as the return of the call (5).

When you open up the app it will communicate (6 & 7) with your website, directly, so nothing happens through the Fork CMS API.