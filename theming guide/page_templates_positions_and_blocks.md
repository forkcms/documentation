# Page templates, positions & blocks

Page templates contain the content of the website. A default template (default.tpl) will be used when the publisher creates a new page. Next to the default template, you can create additional page templates. After defining them in the backend, they'll become available in de Pages-module.

To define different areas within the page template, we use **positions** (e.g. top, main, bottom,...). In the backend, it is possible to add **blocks** (editor content or widgets) to these positions to define the template for the publisher. That way we have a simple system that is flexible enough to avoid a huge load of unnecessary template files.

![Template](https://raw.github.com/forkcms/documentation/master/theming%20guide/assets/template.jpg)

## Code

In your page templates, you'll create well-defined area's within the HTML that may receive content. E.g. you can create a left column, where some widgets or may be added, and a main column, where the important content will be added.

Inside these containers, you'll have to put our template syntax to work to actually fill them up with real data, powered by Fork CMS. Below, you'll find an example that demonstrates the main column.

![Code positions](https://raw.github.com/forkcms/documentation/master/theming%20guide/assets/position_code.jpg)

What this will do is pretty straightforward. We start of by opening the iteration tag, in which we define our main position (positionMain). The code inside this iteration will then automatically be parsed for every block (editor content, widget or module) that has been added to this position through the CMS. The actual edit content or the parsed content of the widget or module will be assigned to `{$positionMain.blockContent}`.

Because we may want to create a distinction between whether a block is editor content or rather a module, there's also an option. The first part (inbetween the blockIsHTML option) becomes visible when the block is editor content and de second part (inbetween the !blockIsHTML option) when the block is a widget or module.