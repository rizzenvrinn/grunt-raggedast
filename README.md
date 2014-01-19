# grunt-raggedast

> Adjust the text rag of your documents for better readability.

## Overview

This task was inspired by an [article](http://24ways.org/2013/run-ragged) by Mark Boulton and based on [plugin](https://github.com/nathanford/ragadjust) by Nathan Ford. In case you want to process your documents dynamically, you should take a look at that plugin. Raggedast is for those who care about typography and readability but are concerned about layout reflows and JavaScript regex performance during the critical phase of document loading. Raggedast will process static files generated by Jekyll or any similar solution.

### Why the stupid name?

Meet [Raggedast](http://upload.wikimedia.org/wikipedia/commons/a/a0/New_granite_sculpture_of_Radegast.jpg), the god of beer and finely ragged chunks of text.

## Getting Started
This plugin requires Grunt `~0.4.2`

If you haven't used [Grunt](http://gruntjs.com/) before, be sure to check out the [Getting Started](http://gruntjs.com/getting-started) guide, as it explains how to create a [Gruntfile](http://gruntjs.com/sample-gruntfile) as well as install and use Grunt plugins. Once you're familiar with that process, you may install this plugin with this command:

```shell
npm install grunt-raggedast --save-dev
```

Once the plugin has been installed, it may be enabled inside your Gruntfile with this line of JavaScript:

```js
grunt.loadNpmTasks('grunt-raggedast');
```

## Raggedast

_Run this task with the `grunt raggedast` command._

### Options

#### options.selector
Type: `String`
Default value: `'p'`

Target elements that should be processed by Raggedast. Use whatever CSS selector you like.

#### options.space
Type: `String`
Default value: `'&#160;'`

The character that is put in place of simple spaces, if for some reason you need to change it to something else.

#### options.words
Type: `Boolean`
Default value: `true`

Whether or not Raggedast tries to find and adjust words that shouldn't end up last on the line, i.e. prepositions, articles and conjunctions. Note that the words are predefined ([see the code](http://github.com/rizzenvrinn/grunt-raggedast/blob/master/tasks/raggedast.js#L17)) and only English is supported as of the moment. The option to serve your own list of words to Raggedast is on its way.

#### options.symbols
Type: `Boolean`
Default value: `true`

Targets basic mathematical symbols and spaced en or em dashed (if spaced is the way you like them).

#### options.units
Type: `Boolean`
Default value: `true`

Looks for a combination of number and some unit of measurement. As before, the units are predefined ([see the code](http://github.com/rizzenvrinn/grunt-raggedast/blob/master/tasks/raggedast.js#L19)) and the list is by no means exhaustive.

#### options.numbers
Type: `Boolean`
Default value: `true`

Tries to find numbers separated into groups of thousands for better readability and glue them together by hard spaces.

#### options.emphasis
Type: `Boolean`
Default value: `true`

Searches for short emphasized phrases. Short means two to three words long, emphasized suggests the use of either `strong`, `em`, `b` or `i`.

#### options.quotes
Type: `Boolean`
Default value: `true`

Looks for short quotations or phrases enclosed in quotation marks. Short means the same thing as before.

#### options.shortWords
Type: `Integer`
Default value: `2`

Allows you to fill the gaps and find the rest of the words that you consider poor candidates for being at the end of the line. The words are targeted by their length, the default 2 matching words such as "I" or "he". By setting the number too high, this method can obviously become very greedy. On the other hand, setting this options to zero turns it off entirely.

#### options.limit
Type: `Integer`
Default value: `0`

This option should come in handy in case you want to tame the hard spaces a little after all the processing. The number implies the longest allowed row of words stuck together by hard spaces. For example, with `shortWords` set to 3, the sentence "It showed a lady fitted out with a fur hat and fur boa who sat upright." would end up with eleven words transformed into a non-breakable string, starting with the word "out". But if you set `limit` to 6, it would split that string into two by removing the hard space after the word "and". Obviously, it is always better to do these alterations by hand but in case you process a lot of text, it is not always viable. The default 0 suggests leaving the strings as they are.

### Usage Examples

#### Default Options
In this example, the default options are used to process the files generated by Jekyll.

```js
grunt.initConfig({
   raggedast: {
         options: {
         selector: 'p',
         space: '&#160;',
         words: true, 
         symbols: true,
         units: true,
         numbers: true,
         emphasis: true,
         quotes: true,
         shortWords: 2,
         limit: 0
      },
      files: [{
         expand: true,
         cwd: '_site',
         src: ['*.html']
      }],
   },
});
```

## Release History

* 2014-01-19   v0.0.1   Raggedast released.

## Release History

MIT © Adam Havel