# Cronjobs

If a certain action needs to be executed at a certain interval (ones a day, hour, …) you'll be defining a cronjob. The first thing you have to do is write a cronjob action. For our example we want an action that sends the administrator, ones a week, the overview of the most awesome blog_posts. (ok, a bit far fetched, ...)

## Action

Just as with an Ajax-action, you'll make an action file but located in the cronjobs folder of your module. Mind that in contrast to ajax-files, this is *always* in the modules folder in the backend!
The name of our class is, `ApplicationModuleCronjobAction`, which extends `BackendBaseCronjob`. Very similar to the Ajax-actions indeed.

```
class BackendMiniBlogCronjobSendMostAwesome extends BackendBaseCronjob
{
	public function execute()
	{

		$this->setBusyFile();

		$items = BackendMiniBlogModel::getTopAwesome();

		$str = '';

		foreach((array) $items as $item)
		{
			$str .= '<p><a href="' . SITE_URL . $item['full_url'] . '">' .
							$item['title'] . ' (' . $item['awesomeness'] . ')</a></p>';
		}

		$variables['data'] = $str;

		BackendMailer::addEmail(
			ucfirst(BL::getMessage('AwesomenessTopFive')), 
			BACKEND_MODULES_PATH . '/mini_blog/layout/templates/mails/send_top_awesome.tpl', 
			$variables, 
			BackendModel::getModuleSetting('core', 'admin_email', 'mail@fork-cms.com')
		);

		$this->clearBusyFile();
	}
}
```

### Busy?

The first line of code you'll see is the `setBusyFile` method. This creates a temporary file that exists as long as the action is executing. At the end of the executing the action, the file is deleted with the `clearBusyFile` method.

You'll use cronjob often for quite intensive tasks that might take a while. To avoid a action being executed while the previous execution is not yet finished, the busy file is used as a check.

> **Not executing anymore?**
> When you're developing sometimes, you'll probably write code that generates an error. When this happens while testing a cronjob action, the busy file is created but never deleted because the clearBusyFile-line is never reached. This causes all further executions of the cronjob to fail because setBusyFile thinks that the previous run of the file is not completed yet.
>To solve this problem, go to /backend/cache/cronjobs/ and delete the existing busy-files.

## Executing

Before you install the action as a cronjob you'll want to test it manually. You'll do this by calling the following url:

```
/backend/cronjob.php?module=MODULENAME&action=ACTIONNAME
```

## How to install the action as a cronjob

Add a line to your crontab that executes a following command

```
/usr/bin/wget -O - --quiet --timeout=1440 "http://domain.tld/backend/cronjob.php?module=MODULENAME&action=ACTIONNAME&id=NR"
```

As you see we use wget to call the cronjob. Note that we supply an extra parameter id in the URL. This id should by unique for every cronjob you define. It's used to name the busy-file.

> **Security**
> It might be a good idea to secure the cronjob.php with a password because anyone(who knows the address to the file) could execute the cronjobs.
> You can do this by putting a .htaccess and a .htpasswd file in the backend directory where the cronjob.php file is located. Note that the call to the your action in the crontab changes somewhat.
http://HTUSERNAME:HTPASSWORD@domain.tld/backend/cronjob.php?module=MODULENAME&action=ACTIONNAME&id=NR

## Problems when coding

When coding cronjobs you should not use one of the following functions, because they are going to break your cronjob:
- BL::getWorkingLanguage()
- BackendModel::createURLForAction()

This comes because the cronjob doesn't know what the language is and these functions use that language.