# Moblets' JavaScript Style Guide

## Table of contents

1. [Introduction](#introduction)
1. [Helper Style Tools](#helper-style-tools)
1. [ESLint IDE Plugin](#eslint-ide-plugin)
1. [IDE Plugins](#ide-plugins)
1. [IDE configuration](#ide-configuration)
1. [API documentation](#api-documentation)
1. [Points of attention](#-points-of-attention)


## Introduction
Code style is very important to simplify the understanding and maintenance of the project in the future. The code needs maintenance, this is a fact, and working with a set of known rules from the begining of the project is the best way to get used to the code style.

In *Moblets*, we follow [Google JavaScript Style] in revision 2.93. It's a complete set of rules used by lots of open source projects.

As we are migrating to ECMA Script 6, we adopted [Airbnb JavaScript Style Guide].

Before start codding for *Moblets*, it's important to read and understand [Google JavaScript Style] (for projects using ECMA Script 5) OR [Airbnb JavaScript Style Guide] (for new projects using ECMA Script 6) and follow the instructions to install and use the tools that will help you with these rules.

## Helper Style Tools
To be easier to follow these rules, you should use [ESLint](http://eslint.org/) and [JSDoc](http://usejsdoc.org/). Follow the next instructions to install and use them.

### Configuration

#### ESLint global files
You need to **install eslint and jsdoc configurations** using NPM.

```
npm install -g eslint jsdoc
```

This will make Eslint and JSDoc available to use on your IDE.

In order to make your IDE use these tools in a project, you need to install some development dependencies. They differ from ECMA 5 and ECMA 6 projects.

#### ECMA Script 5

Run this command in the root of your project:

```
npm install --save-dev eslint eslint-config-google eslint-plugin-jsdoc jsdoc
```

This will add these dev dependencies to your `package.json` file that should look like this:

```json
"devDependencies": {
    "eslint": "^3.8.1",
    "eslint-config-google": "^0.5.0",
    "eslint-plugin-jsdoc": "^2.3.1",
    "jsdoc": "^3.4.2"
  }
```

Create a file called **.eslintrc.yml** in your project root and add the following content:

```yml
extends: google
```

This file will be used by your IDE to follow [Google JavaScript Style].

#### ECMA Script 6

Run these commands in the root of your project:

```
(
  export PKG=eslint-config-airbnb-base;
  npm info "$PKG@latest" peerDependencies --json | command sed 's/[\{\},]//g ; s/: /@/g' | xargs npm install --save-dev "$PKG@latest"
)
npm install --save-dev eslint-plugin-jsdoc jsdoc babel-eslint
```

This will add these dev dependencies to your `package.json` file that should look like this:

```json
"devDependencies": {
    "babel-eslint": "^7.0.0",
    "eslint": "^3.8.1",
    "eslint-config-airbnb-base": "^9.0.0",
    "eslint-plugin-import": "^2.0.1",
    "eslint-plugin-jsdoc": "^2.3.1",
    "jsdoc": "^3.4.2"
  }
```

Create a file called **.eslintrc.yml** in your project root and add the following content:

```yml
extends: airbnb/base
```

## IDE Plugins

### ESLint 
Follow the instructions from [eslint integration](http://eslint.org/docs/user-guide/integrations) to install the plugin in your IDE.

As DocBlockr is only available to [Atom](https://atom.io/), [Sublime Text 2](http://www.sublimetext.com/2) and [Sublime Text 3](https://www.sublimetext.com/3), we recommend the choice of one of these IDEs, but the plugin is also available to other IDEs.

### DocBlockr
To create the code documentation, DocBlockr plugins can be found for [Atom](https://atom.io/packages/docblockr) and [Sublime Text](https://packagecontrol.io/packages/DocBlockr).

This plugin will help you to create code documentation that follow [Google JavaScript Style]'s rules.

## IDE configuration
You must set your IDE to:

* Use **soft tabs**
* Set soft tabs to **2 spaces**
* **Remove spaces** in the end line on save
* Add a **new line (```\n```)** at the end of the file

### DocBlockr configurations
Use DocBlockr default configurations.

### ESLint configurations
Use ESLint default configurations.

### Suggestions
In Atom, configure your keymap to use `Linter Eslint: Fix File` with an alias.

Add to your `keymap.cson`:

```
'atom-text-editor':
  'ctrl-alt-l': 'linter-eslint:fix-file'
```

## API documentation
In order to create API documentations, we use [Documentation](https://github.com/documentationjs/documentation) tool.

## Points of attention

### Files and folders names
[Google JavaScript Style] has 2 possible interpretations about [file names](https://google.github.io/styleguide/javascriptguide.xml?showone=Naming#Naming).

In the first case, it says file names should have the **whole file name in lower case**, with no separations, like "`thisisthefilename.js`":

>"In general, use functionNamesLikeThis… …and **filenameslikethis.js**".

After that, they say that **filenames may contain hyphens**, like "`this-is-the-file-name.js`":

>"Filenames should be **all lowercase**… …no punctuation except for - or _ (**prefer - to _**)".

In order to improve the name readability, we will use the second case, so, **Moblets file names should use the hyphen separation style**.

In *Moblets* wi'll use this rule to **files** and **folders**.

### Iterate over arrays using 'for-in'
The use of '[for-in](https://google.github.io/styleguide/javascriptguide.xml?showone=for-in_loop#for-in_loop)' – for (var key in object) – must be used only to iterate objects, never to iterate arrays.

### Properties and methods [names](https://google.github.io/styleguide/javascriptguide.xml?showone=Naming#Naming)
Private properties and methods should be named with a trailing underscore.

Protected properties and methods should be named without a trailing underscore (like public ones).

### Parentheses
Never use [parentheses](https://google.github.io/styleguide/javascriptguide.xml?showone=Parentheses#Parentheses) for unary operators such as delete, *typeof* and void or after keywords such as *return*, throw as well as others (case, in or new).

### Strings
Prefer single-quotes (') than double quotes ("") for [strings](https://google.github.io/styleguide/javascriptguide.xml?showone=Strings#Strings).

This is helpful when creating strings that include HTML.

### JavaScript Types
[Types](https://google.github.io/styleguide/javascriptguide.xml?showone=JavaScript_Types#JavaScript_Types)


[Google JavaScript Style]: https://google.github.io/styleguide/javascriptguide.xml

[Airbnb JavaScript Style Guide]: https://github.com/airbnb/javascript
