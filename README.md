# Supple (S)CSS framework <img src="https://supple-css.github.io/supple/supple-logo.svg" alt="supple Logo" width="90" height="90" align="right">

[![npm (scoped)](https://img.shields.io/npm/v/supple.svg)](https://github.com/supple-css/supple/releases) [![npm](https://img.shields.io/npm/l/supple.svg)](https://github.com/supple-css/supple/blob/master/LICENSE) [![changelog](https://img.shields.io/badge/changelog-md-blue.svg)](https://github.com/supple-css/supple/blob/master/CHANGELOG.md)

## Introduction
Supple CSS is a reliable and testable [Sass](https://sass-lang.com/) framework in its truest sense. It's based on the [CUBE CSS](https://cube.fyi) methodology and is suited very well for **component-based UI development**. Supple CSS plays well with React, Angular, Vue, Svelte and every other component-based approach to UI development.

## Table of contents

* [Why use Supple](#why-use-supple)
* [Features](#features)
* [CUBE CSS](#cube-css)
* [Browser support](#browser-support)
* [Installation](#installation)
* [Getting started](#getting-started)

## Why use supple:
> It is a small but powerfull (S)CSS framework designed specially with the latest browsers in mind. The framework is made with an eye on the future. It uses utilises new [CSS webstandards](https://cssdb.org/) like custom properties, Grid layout, Flexbox, logical properties, .

Supple provides little to no design wich means no undoing other peoples design decisions.

## Features
A grasp of Supple's featureset:

* Built with the [CUBE CSS](https://cube.fyi) methodology.
* Sensible, powerfull reset for web applications.
* Suite of functions and mixins for speedy development.
* CSS Grid & Flexbox objects  for creating layouts.
* Objects for reusable solutions to common features.
* Variety of utility classes for the most common problems like visually hiding, spacing and more.

### CUBE CSS
<img src="https://piccalilli.imgix.net/images/cube/logo.svg" alt="The CUBE CSS logo which is navy type wrapping a pink cube with dashed inner lines" loading="lazy" width="200">

[CUBE CSS](https://cube.fyi) is a CSS methodology that’s orientated towards simplicity, pragmatism and consistency. It’s designed to work **with** the medium that you’re working in—often the browser—rather than against it.

### Size

The framework including all modules weighs less than **1.5kB**. With this small payload you have the power to build an entire website without even writing a single line of CSS. You can reduce the payload even further by only including the modules you need, and configure those modules to your needs.

### Browser support
Supple supports all major browsers which can render the following features:

* [custom properties](https://caniuse.com/#feat=css-variables)
* [logical properties](https://caniuse.com/#feat=css-logical-props)
* [CSS Grid Layout](https://caniuse.com/#feat=css-grid)
* [CSS Flexible Box Layout(flexbox)](https://caniuse.com/#feat=flexbox)

Basically that comes down to:

* Google Chrome (latest)
* Opera (latest)
* Firefox (latest)
* Safari (latest)
* Edge (latest chromium based)
* iOS (latest)


## Installation

### Prerequisites
Supple is built with the latest version of [Sass](https://sass-lang.com/) so your build-pipeline must be equipped with [Dart Sass](https://sass-lang.com/dart-sass).

### Install

* npm: `npm install supple --save`


## Getting started
The framework is very design-free. this means that the style and design of your site is left entirely up to you. Because Supple gives you lots of customisable foundations you only need to add the final layer: **UI**.

Supple is built using the [Sass module system](https://css-tricks.com/introducing-sass-modules/) and it is advised to structure your application the same way.

Below are some examples on how to use and structure the framework:

### With 1 manifest file, eg. `styles.scss`

```scss
// styles.scss
@use 'settings/your-own-vars';
@use 'node-modules/supple/lib/composition/mesh';
@use 'node-modules/supple/lib/utility/colspan';
@use 'block/your-own-block';
```

```scss
// settings/_your-own-vars.scss
@use 'node-modules/supple/lib/settings/defaults' with (
  $font-size: 20px,
  $columns: 10,
  $breakpoints: (
    lap: 320px,
    desk: 960px,
  ),
);

@use 'node-modules/supple/lib/composition/mesh/variables' with (
  $columns: 24,
);
```

```scss
// block/_your-own-block.scss
@use 'node-modules/supple/lib/settings/defaults';
@use 'settings/your-own-vars';
@use 'node-modules/supple/lib/tools/mixins';

.your-own-block {
  @include tools.mixins-rem(margin-inline-start, defaults.$space-base);
  transition-timing-function: your-own-vars.$animation-timing-function;
}
```

### In a component based setup like React, Vue, Svelte etc.

```scss
// settings/_your-own-vars.scss
@use 'node-modules/supple/lib/settings/defaults' with (
  $font-size: 20px,
  $columns: 10,
  $breakpoints: (
    lap: 320px,
    desk: 960px,
  ),
);
```

```javascript
// components/your-own-component/index.js
import './index.scss';

// rest of your javascript code
```

```scss
// block/index.scss
@use 'settings/your-own-vars';
@use 'node-modules/supple/lib/settings/defaults';
@use 'node-modules/supple/lib/tools/mixins';

.your-own-block {
  @include tools.mixins-rem(margin-inline-start, defaults.$space-base);
  transition-timing-function: your-own-vars.$animation-timing-function;
}

```


## Available modules
All Supple's modules are created based on the [CUBE CSS](https://cube.fyi) methodology.

**Note** every module has its own readme on how to use the module. In the below list you can click through to the connected documentation.

### Settings
This layer is the first layer and holds any global settings for your project. It should only house settings that need to be accessed from anywhere.

* [settings/defaults](lib/settings/defaults), supples core settings.

**NOTE**: Any variable that does not need to be accessed globally should belong in the module to which it relates.

### Tools
The tools layer houses your globally available tooling, mixins and functions.

* [tools](lib/tools).

**NOTE**: Any mixin or function that does not need to be accessed globally should belong in the module template to which it relates.

### Generic
Its CUBE's CSS layer, only element selectors here.

* [generic/reset](lib/generic/reset), A reset of sensible defaults suitable for web applications.
* **[generic/_headings.scss](lib/generic/_headings.scss), a simple heading level structure**.


### Composition
The composition layer’s job is to create flexible, component-agnostic layout systems that support as many variants of content as possible.

* [composition/layout](lib/composition/layout), arrange items horizontally on the inline-axis with flexbox.
* [composition/mesh](lib/composition/mesh), fluid & extensible grid system based on CSS grid.

All Compositions are prefixed with `c-`.

### Utilities
A utility, in the context of CUBE CSS, is a CSS class that does one job and does that one job well.

* [utility/list-clean](lib/utility/list-clean), strip appearance from lists by removing their bullets and indents
* [utility/retain](lib/utility/retain), page-level constraining and wrapping elements
* [utility/aspect-ratio](lib/utility/aspect-ratio), retain a specific aspect ratio but adapt to elements of variable widths
* [utilities/colspan](lib/utilities/colspan), provides a colspan custom property for use in objects or components.
* [utilities/colstart](lib/utilities/colstart), provides a column start custom property for use in objects or components.
* [utilities/clearfix](lib/utilities/clearfix), Clears floats.
* [utilities/flow](lib/utilities/flow), Create flow and rhythm between elements.
* [utilities/spacing](lib/utilities/spacing), utility classes to put specific spacing values onto elements.
* [utilities/visually-hidden](lib/utilities/visually-hidden), hides an element visually while still allowing the content to be accessible.
* [utilities/hidden](lib/utilities/hidden), completely remove from the flow and hide it from screenreaders.

All Utilities are prefixed with `u-`.

### Block
A block is a skeletal component or organisational structure. To compare it to common user interface elements: it is a card element or a button element.

All Components are prefixed with `b-`.

**NOTE**: Because supple is a design-free framework this layer is completely empty. You can add your own blocks to your project.

## Exception
Usually, an exception is related to a state change. For example: you might have a “reversed” state or an “inactive” state.

By default this layer is empty, because it is advised to code your exceptions inside your compositions or blocks.

## Browserstack
Every feature in Supple is extensively tested in browserstack:

[<img src="https://supple-css.github.io/supple/browserstack-logo.png" alt="browserstack logo" width="152" height="80">](https://www.browserstack.com/)


## Credits

Supple is derived by the ideas of many other developers:

* [Andy Bell](https://hankchizljaw.com/) for his awesome ideas with CUBE CSS and numerous other front-end stuff.
* [Harry Roberts](https://twitter.com/csswizardry) for his awesome work on ITCSS and other CSS stuff.
* [Nicole Sullivan](https://twitter.com/stubbornella) for her work on OOCSS.
* [Jonathan Snook](https://twitter.com/snookca) for his work on SMACSS.
* [Nicolas Gallagher](https://twitter.com/necolas) for his work on numerous CSS things.
* [Machiel Hulsbosch](http://www.hulsbos.ch/) for the supple logo.

And probably more…
