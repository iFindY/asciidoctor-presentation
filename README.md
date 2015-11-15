# Asciidoctor Presentation Gradle Plugin

A plugin to try to make it a little easier to make a standalone Asciidoctor presentation. The plugin automatically clones the deck.js infrastructure for you, so you don't have to fuss with finding the right projects and installing them as submodules. It adds less support and implies a standard template build file that lets you insert your content and go.

## Presentation Directory Structure

Your project will look something like this.

```
.
├── README.md
├── build.gradle
└── src
    ├── framework
    │   ├── asciidoctor-deck.js
    │   └── deck.js
    ├── images
    │   ├── something.jpg
    │   └── whatever.jpg
    ├── styles
    │   ├── cojorado-mixins.less
    │   ├── cojorado.less
    │   ├── fonts.less
    │   └── reset.css
    └── slides
        ├── intro.adoc
        ├── body.adoc
        └── slides.adoc
```

Some notes on this structure:

* Your less files are entirely customizable. You can also ignore less and just put CSS in there.
* The directories under `src/framework` should be in `.gitignore`, since they are automatically cloned by the plugin.
* `src/slies/slides.adoc` is autogenerated, and should also be `.gitignore`
* You can download a presentation template [here](https://github.com/tlberglund/asciidoctor-presentation/template).

## Example Presentation Build File

You'll have to customize your modules, theme, title and author, but otherwise this is it:

```groovy
plugins {
  id 'com.timberglund.presentation.plugin' version '0.1'
}

apply plugin: 'com.timberglund.presentation.plugin'

presentation {
  modules {
    opening {
      title = 'Getting Warmed Up'
      file = 'intro.adoc'
    }
    meat {
      title = 'Delivering the Goods'
      file = 'body.adoc'
    }
  }
}

slides {
  header = [
    deckjs_transition: 'fade',
    deckjs_theme: 'cojorado',
    navigation: '',
    menu: '',
    goto: '',
    split: ''
  ]
  title = 'Super Compelling Presentation Title'
  author = 'Tim Berglund'
}
```