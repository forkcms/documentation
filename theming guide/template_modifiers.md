# Template-modifiers

## Native Spoon Library modifiers

### addslashes

Syntax: `{$var|addslashes}`

Will escape all characters in the given string. So
`Is your name O'reilly?` will be converted into
`Is your name O\'reilly?`. You'll use this modifier mostly in JS-files.

### createhtmllinks

Syntax: `{$var|createhtmllinks[:nofollow]}`

#### Parameters

-   **<small>(bool) optional</small> nofollow**: Should a rel="nofollow"
    be added into the link-markup.

Will detect links in the given text and replace the with valid
HTML-markup.

### date

Syntax: `{$var|date[:format[:language]]}`

#### Parameters

* **<small>(string) optional</small> format**: The format that should be
applied on the date, see the [php documentation](http://be.php.net/manual/en/function.date.php)[] for the possible formats, default is Y-m-d H:i:s.
* <small>(string) optional</small> language: **The language to use, default is en**.

Format the given timestamp in the given format for aspecific language.

### htmlentities

Syntax: `{$var|htmlentities}`

Apply the htmlentities function on the given string.

### lowercase

Syntax: `{$var|lowercase}`

Will convert the variable to lowercase.

### ltrim

Syntax: `{$var|ltrim}`

Will strip the whitespace from the beginning of the variable.

### nl2br

Syntax: `{$var|nl2br}`

Will insert \<br\> before each newline in the variable.

### repeat

Syntax: `{$var|repeat:multiplier}`

#### Parameters

* **<small>(int) </small> multiplier**: Number of times the string should be repeated.

Repeat a string.

### rtrim

Syntax: `{$var|rtrim}`

Will strip the whitespace from the end of the variable.

### shuffle

Syntax: `{$var|shuffle}`

Shuffle the variable.

### sprintf

Syntax: `{$var|sprintf:var1[:var2[:var3[:...]]]}`

#### Parameters

* **<small>(mixed) </small> var*x***: The variables that should be parsed into the variable.

Parse the given variables into the variable. You should use
\$\<numeric-position\>%s in the variable.

### stripslashes

Syntax: `{$var|stripslashes}`

Un-escapes a string.

### substring

Syntax: `{$var|substring:start[:length]}`

#### Parameters

* **<small>(int) </small> start**: The index to start from, start count from 0.
* **<small>(int) optional</small> length**: The numbers of characters to return.

Returns a portion of the variable.

### trim

Syntax: `{$var|trim}`

Strip whitespace from the beginning and end of a string.

### ucfirst

Syntax: `{$var|ucfirst}`

Uppercase the first charater of the variable.

### ucwords

Syntax: `{$var|ucwords}`

Uppercase the first character of each word in the variable.

### uppercase

Syntax: `{$var|uppercase}`

Will convert the variable to uppercase.

## Available througout Fork CMS

### camelcase

Syntax: `{$var|camelcase[:separator[:lcfirst[:charset]]]}`

#### Parameters

* **<small>(string) optional</small> separator**: The string to use as a word-separator, default is \_.
* **<small>(bool) optional</small> lcfirst**: Should the first character be lowercase, default is false.

Will camelCase the given string.

### dump

Syntax: `{$var|dump}`

Will dump the data inside the var, this is the template variant of
Spoon::dump.

### formatfloat

Syntax: `{$var|formatfloat[:decimals]}`

#### Parameters

* **<small>(int) optional</small> decimals**: The maximum number of decimals to show, default is 2.

Will format the given floating point number according to the user's
preferences.

### formatnumber

Syntax: `{$var|formatnumber}`

Will format the goven number according to the user's preferences.

### rand

Syntax: `{$var|rand:minimum:maximum}`

#### Parameters

* **<small>(int)</small> minimum**: The minimum as a number.
* **<small>(int)</small> maximum**: The maximum as a number.

Generates a random number between the given minimum and the given
maximum

### stripnewlines

Syntax: `{$var|stripnewlines}`

Will remove all newlines from the given string.

### truncate

Syntax: `{$var|truncate:max-length[:append-hellip]}`

#### Parameters

* **<small>(int)</small> max-length**: The maximum length as number.
* **<small>(bool) optional</small> append-hellip**: Should a hellip be appended if the lenth exceeds the requested length?

Will truncate the given string. If you pass true for the optional
append-hellip-parameter it will appeend a hellip (…) to the truncated
string, but only if it exceeds the maximum length.

## Only available in the frontend

### cleanupplaintext {#cleanupplainttext}

Syntax: `{$var|cleanupPlainText}`

Formats plain text as HTML, links will be detected, paragraphs will be
inserted.

### formatcurrency {#formatcurrence}

Syntax: `{$var|formatcurrency[:currency[:decimals]]}`

#### Parameters

* **<small>(string) optional</small> currency**: The currency to will be used to format the number.
* **<small>(int) optional</small> decimals**: The number of decimals to show.

Format a number as currency.

### getnavigation

Syntax:
`{$var|getnavigation[:type[:parentId[:depth[:excludeIds-splitted-by-dash]]]]}`

#### Parameters

* **<small>(string) optional</small> type**: The type of navigation, possible values are: page, footer.
* **<small>(int) optional</small> parentId**: The parent wherefore the navigation should be build.
* **<small>(int) optional</small> depth**: The maximum depth that has to be build.
* **<small>(string) optional</small> excludeIds**: Which pageIds should be excluded (split them by -).

Get the navigation html

### getpageinfo

Syntax: `{$var|getpageinfo:pageId[:field[:language]]}`

#### Parameters

* **<small>(int)</small> pageId**: The id of the page to build the URL for.
* **<small>(string) optional</small> field**: The field to get.
* **<small>(string) optional</small> language**: The language to use, if not provided we will use the loaded language.

Get a given field for a page-record

### getpath

Syntax: `{$var|getpath:file}`

#### Parameters

* **<small>(string)</small> \$file**: The base path.

Fetch the path for an include (theme file if available, core file otherwise)

### getsubnavigation

Syntax:
`{$var|getsubnavigation[:type[:parentId[:startdepth[:enddepth[:'excludeIds-splitted-by-dash']]]]]}`

#### Parameters

* **<small>(string) optional</small> type**: The type of navigation, possible values are: page, footer.
* **<small>(int) optional</small> pageId**: The parent wherefore the navigation should be build.
* **<small>(int) optional</small> startDepth**: The depth to strat from.
* **<small>(int) optional</small> endDepth**: The maximum depth that has to be build.
* **<small>(string) optional</small> excludeIds**: Which pageIds should be excluded (split them by -).

Get the subnavigation html, when supplying more than 1 ID to exclude,
the single quotes around the dash-separated list are mandatory.

### geturl

Syntax: `{$var|geturl:pageId[:language]}`

#### Parameters

* **<small>(int)</small> pageId**: The id of the page to build the URL for.
* **<small>(string) optional</small> language**: The language to use, if not provided we will use the loaded language.

Get the URL for a given pageId & language

### geturlforblock

Syntax: `{$var|geturlforblock:module[:action[:language]]}`

#### Parameters

* **<small>(string)</small> module**: The module wherefor the URL should be build.
* **<small>(string) optional</small> action**: A specific action wherefor the URL should be build, otherwise the default will be used.
* **<small>(string) optional</small> language**: The language to use, if not provided we will use the loaded language.

Get the URL for a give module & action combination

### geturlforextraid

Syntax: `{$var|geturlforextraid:extraId[:language]}`

#### Parameters

* **<small>(int)</small> extraId**: The id of the extra.
* **<small>(string) optional)</small> language**: The language to use, if not provided we will use the loaded language.

Fetch an URL based on an extraId

### highlight

Syntax: `{$var|highlight}`

Highlights all strings in \<code\> tags.

### striptags

Syntax: `{$var|}`

### timeago

Syntax: `{$var|timeago}`

Formats a timestamp as a string that indicates the time ago.

### urlencode

Syntax: `{$var|}`

### usersetting

Syntax: `{$var|usersetting:setting[:userId]}`

#### Parameters

* **<small>(string)</small> setting**: The name of the setting you want.
* **<small>(int) optional</small> userId**: The userId, if not set by \$var.

Get the value for a user-setting.

### profilesetting {#profilesettings}

Syntax: `{$var|profilesetting:setting}`

#### Parameters

* **<small>(string)</small> setting**: The name of the setting you want.

Get the value for a profile-setting.

## Only available in the backend

### formatdate

Syntax: `{$var|formatdate}`

Will format the given timestamp as a date according to the user's
preferences.

### formatdatetime

Syntax: `{$var|formatdatetime}`

Will format the given timestamp as a full date according to the user's
preferences.

### formattime

Syntax: `{$var|formattime}`

Will format the given timestamp as a time according to the user's
preferences.

### getmainnavigation

Syntax: `{$var|getmainnavigation}`

Will convert the variable in the main navigation HTML.

### getnavigation

Syntax: `{$var|getnavigation:startdepth[:enddepth]}`

#### Parameters

* **<small>(int)</small> startdepth**: The startdepth of the navigation.
* **<small>(int) optional</small> enddepth**: The ending depth of the navigation.

Convert a var into navigation HTML.

### geturl

Syntax: `{$var|geturl:action[:module[:suffix]]}`

#### Parameters

* **<small>(string)</small> action**: The action to build the URL for.
* **<small>(string) optional</small> module**: The module to build the url for.
* **<small>(string) optional</small> suffix**: A string that will be appended to the generated url.

Will convert the variable into an url to an action (and module). If you
don't pass a module the current module will be used.

### tolabel

Syntax: `{$var|tolabel}`

Will convert the given string in a label. For instance if you pass
`choose_an_application` it will be replaced by the value of the label
ChooseAnApplication. (Seperate words by a underscore: \_)