# Version Control

## GitHub

Instead of downloading an archive you could clone the source code from [GitHub](https://github.com/forkcms/forkcms). There are a few advantages; First of all, in this way you will always have the latest bugfixes, even before they are available in a release.

Secondly, version control makes it easy to upgrade your code, even when you made some custom changes in the core of Fork CMS. Only database changes can not be handled (yet).

If you're not familiar with git or github yet, here are some good resources to get you started:

* [The Git documentation](http://git-scm.com/doc)
* [The GitHub help](https://help.github.com/)
* [Git Workflows](http://documentup.com/skwp/git-workflows-book)
* [Learn Git Branching](http://pcottle.github.io/learnGitBranching/)

Specially check out the guide about [forking a project](https://help.github.com/articles/fork-a-repo). ([Fork](http://en.wikipedia.org/wiki/Fork_(software_development) in this context has nothing to do with our name.)


## Composer

Instead of copying all code from other repositories, [Composer](http://getcomposer.org) is used to manage the dependencies. Make sure Composer is [installed](http://getcomposer.org/doc/00-intro.md#installation-nix) on your machine.

In Terminal on Mac OS X or in Command Prompt on Windows, go to the root of your project folder and execute the command:

```
composer install
```

All dependencies are now installed in the *vendors* folder.

Go through the [upgrading guide](upgrading.md) to find out how you can keep your setup up-to-date with Git.