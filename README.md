# Moblets JavaScript Style Guide

## Intro

The code style is very, very important, to simplify the understanding and maintenance of the project in the future. The code needs maintenance, this is a fact, and working with a set of known rules from the begin of project is the best way to get used to the code style.

In Moblets, we follow the style of [Google Javascript Style](https://google.github.io/styleguide/javascriptguide.xml) because it's complete and used by lots of open source projects.

## Code Style Tools

To follow the best practices, we use:
- [ESLint](http://eslint.org/) with code style set to `google`
- [JSDoc](http://usejsdoc.org/) style to comments

To install the `eslint` with `google` and `jsdoc`, run this command in your terminal:

    $ npm install -g eslint jsdoc eslint-config-google eslint-plugin-jsdoc


### IDE Plugins

#### ESLint

To help us with the code style, we use the [eslint integration](http://eslint.org/docs/user-guide/integrations) plugin in our IDEs.

#### DocBlockr
 To the comments, we use DocBlockr plugins, that can be found for [Sublime Text](https://packagecontrol.io/packages/DocBlockr) and  [Atom](https://atom.io/packages/docblockr).

#### Suggestions
In Atom, configure your keymap to use `Linter Eslint: Fix File` with alias.

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
