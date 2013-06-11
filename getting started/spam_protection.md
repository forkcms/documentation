# Spam protection

When you installed a blog or another module that allows comments you have to install an anti-spam service too. Not only is spam irritating for visitors, Google will [reward quality](http://googlewebmastercentral.blogspot.be/2012/04/another-step-to-reward-high-quality.html) content that doesn't contain webspam.

The built-in spam protection of Fork CMS uses the very popular [Akismet](http://akismet.com/), they monitor millions of websites and your website can benefit from their knowledge. It is free for personal use and [affordable](https://akismet.com/signup/) for business usage.

> Akismet is a hosted web service that saves you time by automatically detecting comment and trackback spam.

### Step 1: Get your Akismet key

The installation is rather simpel, first go to [http://akismet.com/signup](http://akismet.com/signup) and go through the steps. 

Select your plan

![Select Akismet plan](https://raw.github.com/forkcms/documentation/master/getting%20started/assets/akismet_step1.png)

Create a wordpress.com account, the email that is used for that account will be used to send you the api key.

![Create wordpress.com account](https://raw.github.com/forkcms/documentation/master/getting%20started/assets/akismet_step2.png)

As last step fill in the account details and select the amount you want to pay for the service.

![Fill in account details](https://raw.github.com/forkcms/documentation/master/getting%20started/assets/akismet_step3.png)

The Akismet api key will be send by mail, threat your key as a password and keep it private.

![The api key](https://raw.github.com/forkcms/documentation/master/getting%20started/assets/akismet_step4.png)

### Step 2: Enter your key

In the private section of Fork CMS, go to *Settings* and enter the api key on the *General* page.

![Enter the key](https://raw.github.com/forkcms/documentation/master/getting%20started/assets/akismet_final.png)

The largest amount of spam will be taken care of by Akismet, check out the [user guide](#todo) to learn how to manually assign comments as spam.