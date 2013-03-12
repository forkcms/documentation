# Making a basic theme

The first step of making a theme is creating a design. The second step is slicing this into basic HTML - CSS. This tutorial doesn't give information about these steps but assumes you did them both. The slice of day 02:

![Day 02 theme](assets/daytwo.jpg)

The easiest way to start making a theme is copying the triton theme folder located in fork_folder/frontend/themes. We have to  rename the copied theme folder to the name you want to see in the backend, which is in this example "daytwo". This will make sure we're able to install the theme in the backend. See Theme contents.

## info.xml

The next thing you should do is open up your info.xml file. It's located directly in the theme folder and contains some basic information about the theme, your templates and your positions. You should change the content of the name tag, the description tag, and the author tag. If you want to use special characters in the description, don't forget to add CDATA tags ("<![CDATA[" and "]]>"). These tags make sure the text data won't be parsed by the XML parser ([more info about CDATA](http://en.wikipedia.org/wiki/CDATA)). If you want to give the tumbnail file another name, you can also change the thumbnail tag.

Every theme contains templates which contain positions. Every theme needs at least a default.tpl template. Most themes also contain a home.tpl and can contain as much templates as you want to. In day two we need two templates: home.tpl: a two column layout for the home and blog page and default.tpl: a three column layout for the other pages. These layouts contain positions. The footer and header template don't need to be included in the info.xml since they'll be loaded from the home and default templates. 

A position is a place where a user can put modules, widgets or editor content. The home.tpl has two positions, since there are two columns to be filled. We call them main and right. The default.tpl contains three positions: left, main and right. Try to use names that describe the position like top, left, right, main,... When you change a fork theme, it tries to reallocate all the blocks to positions with the same name, for example: Fork will try to put the blog index in the main position of the blog page. 

In the picture you see the main templates: home and in it header. The footer isn't visible but is also included in the home template. The grey parts are the positions.

![Structure](assets/structure.jpg)

Templates also contain a format tag. They are a visual representation of the template, to be used in the pages-module. You can see this representation when you edit or create a page in the cms backend.

To add a row, you'll need square brackets: [ ]. The positions are added with the position name. All rows and positions are separated by comma's. If you want to add an empty place, you can add a slash: /. In our example, these formats are really basic. Just one row with two (home) and three (default) columns. The home format looks like: [left,main,main,right] and the default format looks like [main,main,right]. In this example, main is used two times side by side. In the pages-module, the width of the main block will be two times the width of the right (and left) block.

The xml:

```
<?xml version="1.0" encoding="UTF-8"?>
<theme>
	<name>daytwo</name>
	<version>1.0.0</version>
	<requirements>
		<minimum_version>3.0.0</minimum_version>
	</requirements>
	<thumbnail>thumbnail.png</thumbnail>
	<description>
		<![CDATA[
			DAY 02 is a grid-based sci-fi/space theme for Fork CMS.
			It includes styles for: main navigation, slideshow, blog (category, archives, comments, comment form, widgets), contact form and search.
		]]>
	</description>
	<authors>
		<author>
			<name>Wouter Sioen</name>
			<url>http://www.woutersioen.be</url>
		</author>
	</authors>
	<metanavigation supported="false" />
	<templates>
		<template label="Default" path="core/layout/templates/default.tpl">
			<positions>
				<position name="main" />
				<position name="left" />
				<position name="right" />
			</positions>
			<format>
				[left,main,main,right]
			</format>
		</template>
		<template label="Home" path="core/layout/templates/home.tpl">
			<positions>
				<position name="main" />
				<position name="right" />
			</positions>
			<format>
				[main,main,right]
			</format>
		</template>
	</templates>
</theme>
```

It's also worth mentioning it's possible to put a default widget or module in a position. In the next example, we have a top position containing the search form widget. This isn't necessary in the daytwo info.xml.

```
<position name="top" >
	<defaults>
		<widget module="search" action="form" />
	</defaults>
</position>
```

If the info.xml isn't a valid XML file, your theme won't work and won't show up in the themes install page! If you haven't installed your theme yet, now is the right time, even though the frontend will contain some strange stuff caused by non-existing positions.

## The templates

The next step is updating the copied templates (theme_folder/core/layout/templates) to make sure they contain the right positions. You can delete the positions that don't exist, add new positions or change the names of the positions in the file to the names of the positions in your info.xml. You'll probably need to remove and add some html tags to make sure the structure of your template is the same as the structure of your sliced html without the content. For the day two example, some divs where added (divs with id mainColumn, column, clas sidebar,..) and a lot of overhead was removed.

### Positions

For adding positions you need to use iteration tags. This example shows the position Main with a lot of comments to explain how it works. Comments are put in between the {* and *} tags. Multiline comments are allowed.

```
{* iteration:positionMain loops through all the blocks in this position:
it does everything in this iteration for every block *}
{iteration:positionMain}
	{* This option (blockIsHTML) checks if the block is editor content *}
	{option:positionMain.blockIsHTML}
		{* Everything within this option will be added around the blockcontent *}
		<article class="article content">
			{* The actual block content, in this case an editor block *}
			{$positionMain.blockContent}
		</article>
	{* end of the option *}
	{/option:positionMain.blockIsHTML}
	{* This option (blockIsHTML) checks if the block is a module or a widget *}
	{option:!positionMain.blockIsHTML}
		{* The actual block content in this case a widget or a module *}
		{$positionMain.blockContent}
	{* end of the second option *}
	{/option:!positionMain.blockIsHTML}
{* end of the iteration *}
{/iteration:positionMain}
```

More info about template syntax can be found in this nice cheat sheet: [Fork Template Syntax cheat sheet](http://www.fork-cms.com/frontend/files/userfiles/files/cheatsheet_2_05_2011.pdf). This cheat sheet will be useful when styling the module templates too.

### Modifiers

A lot of variables can use modifiers. They modify a variable and are used with the syntax {$variable|modifier}. Some modifiers also need extra parameters. For a list of all modifiers check the cheat sheet. The modifier you'll need most in the main templates is the ucfirst modifier. This modifier makes sure a label or string starts with a capital letter.

When this is done, you shouldn't see iteration and option tags appearing in the frontend anymore. If they still appear, there's probably a position in your template with a wrong name. Don't forget to create all needed templates and to edit or create footer.tpl and header.tpl if you use them.

### More variables

Note: Don't forget to add the {$siteHTMLHeader} and {$siteHTMLFooter}.

They make you able to add extra scripts with the backend. In the settings tab you'll have the textboxes '<head> script(s)' and 'End of <body> script(s)'. Scripts like google analytics can be pasted there. These script(s) will be added where the siteHTMLHeader/siteHTMLFooter tag is placed, so place it right before the end of the </head> and </body>  tag.

```
{* Site wide HTML *}
	{$siteHTMLHeader}
</head>

{* Site wide HTML *}
	{$siteHTMLFooter}
</body>
```

Another thing you should include in the head is the {$meta} and {$metaCustom} tags. They load the overal meta tags and the page specific meta tags. The links to the favicon and apple touch icon are placed in the head too. 

```
{* Meta *}
<meta charset="utf-8" />
<meta name="generator" content="Fork CMS" />
{$meta}
{$metaCustom}

<title>{$pageTitle}</title>

{* Favicon and Apple touch icon *}
<link rel="shortcut icon" href="{$THEME_URL}/favicon.ico" />
<link rel="apple-touch-icon" href="{$THEME_URL}/apple-touch-icon.png" />
```

## The CSS

When you have these templates ready, it's time for the styles! This is easy, just copy paste the css of your slice to the core css folder of your theme (theme_folder/core/layout/css) and rename it to screen.css. If you have multiple css files, it is easiest to combine them all in one file. The link to the screen.css file is added in a template with:

```
{iteration:cssFiles}
	<link rel="stylesheet" href="{$cssFiles.file}" />
{/iteration:cssFiles}
```

If you don't want to combine them in one file, you should make an imports folder in the css folder and use the @import tag in your screen.css file. 

## Images, fonts and javascript

The images, fonts and javascript should go in the folders theme_folder/core/layout/images, theme_folder/core/layout/fonts and theme_folder/core/js. When you used another folder structure for the slice, you'll need to change paths in the css file for background-images and @font-face.

You can include scripts in your templates with the variable THEME_URL.

```
<script src="{$THEME_URL}/core/js/html5.js"></script>
```

Include the following code in your template to use the core js files (including jQuery, necessary for some things to work):

```
{* This loads all frontend core javascript files (fork_folder/frontend/core/js/
Don't add your specific js files in this folder *}
{iteration:jsFiles}
	<script src="{$jsFiles.file}"></script>
{/iteration:jsFiles}
```

When this is done, the basic layout of your website should be ok. If the modules don't look the way you want them, it may be possible to style them with css. Sometimes you'll need to change the template files of the modules.

## Modules

If you want to change the structure of a module, you'll need to add a modules folder directly in your theme folder. If you copied the Triton theme, this folder is already present. Everything in this folder should follow the same structure as the frontend/modules folder. The files in your theme modules folder will overwrite the file in the exact same position in the frontend/modules folder. If you want to change the index page for the blog module, you'll need to add "blog/layout/templates/index.tpl" in your modules folder. This is the same for every module/widget you want to style. It's easiest to copy the core files you want to overwrite in your own folder and edit them. This way you start from a working module that hasa basic structure. You'll also see all the variables that where already used. 

When changing module themes, a very useful modifier is dump. This modifier shows all the children of a variable. In the blog index the code {$items|dump} gives this:

![Dump](assets/dump.jpg)

With this modifier you're able to have a representation of all the different variables available.

While creating module templates, you'll probably need more than just iterations and options. Creating nested iterations, checking if it's the first/last item of an iteration and cycles ar some things available to help you. More info in the [cheat sheet](http://www.fork-cms.com/frontend/files/userfiles/files/cheatsheet_2_05_2011.pdf).

## Finishing the theme

Before your theme is finished you'd better check if everything is styled the right way. Some things are easy to forget like pagination, form validation,... You should test the theme carefully by changing settings in the backend, adding content, placing widgets and modules in other positions, testing every page in the frontend,...
With all these steps, you should be able to create a Fork CMS theme without writing one single line of php! Isn't that wonderful?