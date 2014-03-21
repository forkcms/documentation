# Configuring Cronjobs

Cronjobs are scripts that are designed to be called periodically, in Fork CMS they are mainly used to go through queued items like for example queued e-mails. They can be excuted either through commandline as well as over your webserver.

Without additional modules has Fork CMS two cronjobs:

Commandline: 

```
php http://mydomain.com/backend/cronjob.php?module=core&action=process_queued_hooks

php http://mydomain.com/backend/cronjob.php?module=core&action=send_queued_emails
```

Webserver: 

```
/usr/bin/wget -O - --quiet --timeout=1440 "http://mydomain.com/backend/cronjob.php?module=core&action=process_queued_hooks"
/usr/bin/wget -O - --quiet --timeout=1440 "http://mydomain.com/backend/cronjob.php?module=core&action=send_queued_emails"
```

Some additional modules need extra cronjobs, check the details page on your modules overview to see which cronjobs need to be set for the module.

![Cronjobs from Analytics module](https://raw.github.com/forkcms/documentation/master/getting%20started/assets/cronjobs_analytics.png)

When setting cronjobs on servers with several Fork CMS installation try to spread the execution by changing the minutes parameter.
