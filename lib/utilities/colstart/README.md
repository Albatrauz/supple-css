# Supple CSS | utilities.colstart

Utility which provides a colstart custom property for use in objects or components which can handle those colstarts eg. `object.layout` and `object.mesh`.

Read more about [Supple CSS](https://github.com/supple-css/supple).

## Table of contents

* [Features](#features)
* [Use](#use)
* [Available classes](#available-classes)
* [Configurable variables](#configurable-variables)
* [Installation](#installation)
* [Browser support](#browser-support)

## Features

* Easy & flexible column starts in your objects & components
* Works nicely with `objects.layout` and `objects.mesh`

## Use

```html
<div class="o-mesh">
  <div class="o-mesh__cell  u-colstart-3">
    starts a column 3
  </div>
  <div class="o-mesh__cell  u-colstart-7">
    starts a column 7
  </div>
</div>
```


## Available classes
By default we generate classes for 12 columns but it can be configured with the `$columns` setting.

* `.u-colstart-X`, spans over the designated number of columns
* `.u-colstart-X[from|until]-[BREAKPOINT-NAME]`: applies colstart at the given breakpoint. (available in `$in-breakpoint` SCSS setting)


## Configurable variables


### SCSS variables

* `$columns`, number of columns we generate classes for, defaults to `defaults.$columns`
* `$in-breakpoint`: a list of breakpoints where `.u-colstart-X@[from|until]-[BREAKPOINT-NAME]` is generated for, defaults to: `()`

You can overwrite the SCSS variables the following ways:

```scss
// in your manifest file, eg. `styles.scss`
@use '~supple/lib/utilities/colstart' with (
  $columns: 10,
  $fit-in-breakpoint: (lap, desk),
);
```
or
```scss
// in your own variable file, eg. `_vars.scss`
@use '~supple/lib/utilities/colstart/variables' with (
  $fit-in-breakpoint: (lap, desk),
);

// in your manifest file, eg. `styles.scss`
@use '~supple/lib/utilities/colstart';
```


## Installation
Make sure you've installed/downloaded the Supple CSS library:

* [npm](https://www.npmjs.com/package/supple): `npm install supple`
* Download: [zip](https://github.com/supple-css/supple/releases/latest)


## Browser support

* Google Chrome (latest)
* Opera (latest)
* Firefox (latest)
* Safari (latest)
* Edge (latest chromium based)
* iOS (latest)