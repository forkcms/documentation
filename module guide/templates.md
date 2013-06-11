# Templates

## Variables

To make our different pages visible on our website we need to write a template file for every action. As said before, a template file is a html-file containing placeholders for the data that we will parse into that template-file.

Let's first have a look at the detail-page, in the default Fork CMS-theme, in the browser:

![Detail](assets/detail.png)

The code that was used in the .tpl-file you find below. As you can see it's regular html-code, but with a lot of data between { and }. We'll discuss the different types of placeholders one by one.

```
<div id="blogDetail">
 <article class="mod article">
 <div class="inner">
 <header class="hd">
 <h1>{$item.title}</h1>
 <ul>
 <li>{$msgWrittenBy|ucfirst|sprintf:{$item.user_id|usersetting:'nickname'}} {$lblOn} {$item.edited|date:{$dateFormatLong}:{$LANGUAGE}}</li>
 </ul>
 </header>
 <div class="bd content">
 {$item.introduction}
 </div>
 <div class="bd content">
 {$item.text}
 </div>
 <div class="awesome" id="awesome{$item.id}">
 <span class="counter">{$item.awesomeness}</span>
 {$lblPeopleThinkThisPostIsAwesome}
 <span class="bar">|</span>
 <a class="add" rel="{$item.id}">{$lblIThinkThisIsAwesome}</a>
 <span style="display:none;" class="added">{$lblIThinkThisIsAwesome}</span>
 </div>
 <footer class="ft">
 <ul class="pageNavigation">
 {option:navigation.previous}
 <li class="previousLink">
 <a href="{$navigation.previous.url}" rel="prev">{$lblPreviousArticle|ucfirst}: {$navigation.previous.title}</a>
 </li>
 {/option:navigation.previous}
 {option:navigation.next}
 <li class="nextLink">
 <a href="{$navigation.next.url}" rel="next">{$lblNextArticle|ucfirst}: {$navigation.next.title}</a>
 </li>
 {/option:navigation.next}
 </ul>
 </footer>
 </div>
 </article>
</div> 
```

When we discussed the detail.php file we came across the following line:

```
$this->tpl->assign('item', $this->record); 
```

With this code, the array in `$this->record`, containing our article, is parsed into the template as the array item. The syntax for reading elements from an array in a template is the dot-syntax, preceding the variable name with an $. On the sixth line your see `{$item.title}`. This does nothing more than echoing the value in the field 'title' of our array 'item'.

In some cases, you'll have array's in array's, in array's, in ... you'll write them next to each other as in our example: `{$navigation.previous.title}`

> **Plain simple vars**
> Not everything needs to be an array. A normal variable is possible too:
> `$articleTitle = 'Finding Little Nemo in Slumberland';
> $this->tpl->assign('title', $articleTitle);`
> You can echo it in your template like this:
> `{$title}`

## Locale

When you're developing a module you'd better don't write plain English, Dutch, French, ... in your templates. Instead you use locale which will be replaced by the right translation. You see a couple of locale in our example:

* `{$msgWrittenBy}`
* `{$lblOn}`
* `{$lblPeopleThinkThisPostIsAwesome}`

Everything what applies to normal data applies to labels as well. They stand between { and }, are preceded by $ and can be used in combination with modifiers (see next chapter). There are two differences. The first is that you don't have to parse them in the template yourself, this happens automatically.

The second is that labels always begin with lbl, msg, act or err. More about this, you'll find in the next chapter.

## Modifiers

Because plain simple translations or only echoing data is not always what we need, you can add modifiers to an echo of data or a label. Take this example:

```
{$item.edited|date:{$dateFormatLong}:{$LANGUAGE}}
```

The variable {$item.edited}, echoed without modifiers would look something like:

```
1303481726
```

... a UNIX-timestamp.

We put a pipe next to the variable name, followed by the modifier name and next you'll find two arguments, separated by colons. {$dateFormatLong} and {$LANGUAGE}, two other variables automatically parsed into the template by Fork. The result of this expression becomes

```
Friday 22 April 2011
```

It's possible to send the result of one modifier to another modifier, just add a pipe and write the next modifier.

> **modifiers**
> There a lots of modifiers available, some with arguments (f.e. sprintf, substring, ...), others without, (ucfirst, nl2br, ...). Also check our [cheatsheet](http://www.fork-cms.be/frontend/files/userfiles/files/cheatsheet_2_05_2011.pdf).

## Commenting

Templates have other possibilities too. To illustrate these we'll use the template of the recents_posts widget.

As you see on the first 4 lines, we added some comments. When you're working with different people on a website it might be a good idea to provide on overview of which variables are parsed into the template.

```
{*
 variables that are available:
 - {$widgetMiniBlogRecentPosts}
*}
<section id="blogRecentCommentsWidget" class="mod">
 <div class="inner">
 <header class="hd">
 <h3>{$lblRecentArticles|ucfirst}</h3>
 </header>
 <div class="bd content">
 {option:widgetMiniBlogRecentPosts}
 <ul>
 {iteration:widgetMiniBlogRecentPosts}
 <li>
 <a href="{$widgetMiniBlogRecentPosts.full_url}">{$widgetMiniBlogRecentPosts.title}</a>
 {$msgWrittenBy|ucfirst|sprintf: {$widgetMiniBlogRecentPosts.user_id|usersetting:'nickname'}} {$lblOn}
 {$widgetMiniBlogRecentPosts.edited|date:{$dateFormatShort}:{$LANGUAGE}}
 </li>
 {/iteration:widgetMiniBlogRecentPosts}
 </ul>
 {/option:widgetMiniBlogRecentPosts}
 {option:!widgetMiniBlogRecentPosts}
 {$msgThereAreNoRecentItemsYet}
 {/option:!widgetMiniBlogRecentPosts}
 </div>
 </div>
</section>
```

## Options

Templates have two programming techniques. The first are options. They work just the same as an if-statement, except the only thing you can check is: Is a variable set, or not set.

In our example above we check if the variable widgetMiniBlogRecentPosts isset. If so, the code between the options is show. Else, it's not shown!

You add the “Else” yourself by reversing the same option with an exclamation mark. This way you can add some kind of error message.

> **!isset()**
> The evaluation of an option doesn't work the same as the “isset” function in php. An option is FALSE when the variable is:
> an empty string, 0 (string or integer), NULL, FALSE (boolean), an empty array.

## Iterations

The second programming technique your can use in templates are iterations. With iterations, you can walk all the items of an array. This example prints all the title fields of an array.

```
{iteration:widgetMiniBlogRecentPosts}
 {$widgetMiniBlogRecentPosts.title}
{/iteration:widgetMiniBlogRecentPosts}
```

There are a lot of other things you should know about iterations, such as nesting iterations, the first- and last-option, cycle, ... You'll find everything about these on the Cheatsheet.

> **No $**
> Mind that in neither in options nor iterations, the variable name is preceded by the dollar-sign.

## Includes

Another nice thing about templates is that you can include other templates, just like you do in .php.

E.g. in the backend, you will add the following lines to every action template so all pages start with the same header:

```
{include:{$BACKEND_CORE_PATH}/layout/templates/head.tpl}
{include:{$BACKEND_CORE_PATH}/layout/templates/structure_start_module.tpl}
```

The same way, you can add your own pieces of code that perhaps often return on other pages, without it's necessary to create a widget. E.g. a collection of "Share on twitter, facebook, netlog, myspace, ..." buttons.