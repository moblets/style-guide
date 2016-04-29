# Moblets' JavaScript Style Guide

## Intro
Code style is very important to simplify the understanding and maintenance of the project in the future. The code needs maintenance, this is a fact, and working with a set of known rules from the begining of the project is the best way to get used to the code style.

In *Moblets*, we follow [Google Javascript Style] in revision 2.93. It's a complete set of rules used by lots of open source projects.

Before start codding for *Moblets*, it's important to read and understand [Google Javascript Style] and follow the instructions to install and use the tools that will help you with these rules.

## Helper Style Tools
To be easier to follow these rules, you should use [ESLint](http://eslint.org/) and [JSDoc](http://usejsdoc.org/). Follow the next instructions to install and use them.

### 1. ESLint global files
You need to **install eslint and jsdoc configurations** using NPM.

    $ npm install -g eslint jsdoc eslint-config-google eslint-plugin-jsdoc

This will make Eslint and JSDoc available to use on your IDE.

### 2. ESLint IDE Plugin
Follow the instructions from [eslint integration](http://eslint.org/docs/user-guide/integrations) to install the plugin in your IDE.

As DocBlockr is only available to [Atom](https://atom.io/), [Sublime Text 2](http://www.sublimetext.com/2) and [Sublime Text 3](https://www.sublimetext.com/3), we recommend the choice of one of these IDEs, but the plugin is also available to other IDEs.

### 3. Dev dependencies
In order to make your IDE use these tools in a project, you need to install some development dependencies. Run this command in the root of your project:

    $ npm install --save-dev eslint@">=2.8 <3" eslint-config-google@">=0.5 < 1" eslint-plugin-jsdoc@">=2.3 < 3" jsdoc@">=3.4 <4"

This will add these dev dependencies to your `package.json` file. You can find an example in the repository.

 #### ESLint configuration file.
You need to create the ESLint configuration file. Just run this command in the root of your project:

    $ eslint --init


Then, choose '**Use a popular style guide**', '**Google**' and choose any language (JavaScript, YAML or  JSON).

![eslint --init](eslint --init.png)

This will create a `.eslintrc.xxx` file in the project root that will be used by your IDE to follow [Google Javascript Style]. In this documentation, we have examples for each language.

### DocBlockr
To create the code documentation, DocBlockr plugins can be found for [Atom](https://atom.io/packages/docblockr) and [Sublime Text](https://packagecontrol.io/packages/DocBlockr).

This plugin will help you to create code documentation that follow [Google Javascript Style]'s rules.

### IDE configuration
You must set your IDE to:

* Use **soft tabs**
* Set soft tabs to **2 spaces**
* **Remove spaces** in the end line on save
* Add a **new line (```\n```)** at the end of the file

### DocBlockr configurations
Use DocBlockr default configurations.

### ESLint configurations
Use ESLint default configurations.

### File names
[Google Javascript Style] has 2 possible interpretations about file names.

In the first case, it says file names should have the **whole file name in lower case**, with no separations, like "`thisisthefilename.js`":

>"In general, use functionNamesLikeThis… …and **filenameslikethis.js**".

After that, they say that **filenames may contain hyphens**, like "`this-is-the-file-name.js`":

>"Filenames should be **all lowercase**… …no punctuation except for - or _ (**prefer - to _**)".

In order to improve the name readability, we will use the second case, so, **Moblets file names should use the hyphen separation style**.

### Suggestions
In Atom, configure your keymap to use `Linter Eslint: Fix File` with an alias.

Add to your `keymap.cson`:

```
'atom-text-editor':
  'ctrl-alt-l': 'linter-eslint:fix-file'
```

## Hook to Git
To always check the edited files with ESLint, add the pre-commit hook on the git repository.

To add this hook, create the file `pre-commit` in `.git/hooks` with the following command:

    $ touch .git/hooks/pre-commit

Then, insert this code on the file:

```
#!/bin/sh
function lintit () {
  filesJsWithDiff=$(git diff --cached --name-only | grep -E '(.js)$')
  file=$(echo $filesJsWithDiff | tr '\n' ' ')
  rootDir=$(git rev-parse --show-toplevel)
  eslintFile=($rootDir/.eslintrc.*)
  e=$(eslint -c $eslintFile $file)
  if [[ "$e" != *"0 problems"* ]]; then
    echo "ERROR: Check eslint hints."
    eslint -c $eslintFile $file
    exit 1 # reject
  fi
}
lintit

```

[Google Javascript Style]: https://google.github.io/styleguide/javascriptguide.xml
