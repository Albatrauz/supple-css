# Supple CSS | composition.layout

Layout makes use of `flexbox` & Custom Properties to provide for a flexible, fluid & extensible layout system. You can horizontally(on the inline axis) arrange items or even use it as a full fledged  traditional grid system.

If you want to arrange items over 2 dimensions (horizontal & vertical) we recommend using [composition.mesh](../mesh).

Read more about [Supple CSS](https://github.com/supple-css/supple).

## Table of contents

* [Features](#features)
* [Use](#use)
* [Available classes](#available-classes)
* [Configurable variables](#configurable-variables)
* [Installation](#installation)
* [Testing](#testing)
* [Browser support](#browser-support)

## Features

* Configurable with custom properties.
* Fluid layout.
* Intelligent cell wrapping.
* Evenly fill cell spacing.
* Equal height columns.
* Horizontal/vertical centering of cells.
* Cell width is controlled independently of layout gap.
* Infinite nesting.


## Use

A simple layout is easy to create. A layout container can have any number of child cells. When used with `.c-layout--fill` space is evenly distributed without need for `--colspan` or sizing utilities.

**Note** `.c-layout` only accepts `.c-layout__cell` as direct descendants. This keeps our layout nicely separated from other components.

```html
<div class="c-layout  c-layout--fill  c-layout--gap-base">
  <div class="c-layout__cell"><!-- content --></div>
  <div class="c-layout__cell"><!-- content --></div>
  <div class="c-layout__cell"><!-- content --></div>
  <div class="c-layout__cell"><!-- content --></div>
</div>
```

For more granular control over layout make use of modifiers, custom properties or sizing utilities.

### Modifiers on `c-layout`

```html
<div class="c-layout  [c-layout--align-inline-center  |  c-layout--align-inline-end  |  c-layout--align-block-center  |  c-layout--align-block-end  |  c-layout--fill  |  c-layout--fit  |  c-layout--equal-block-size  |  c-layout--gap-base]">
  <div class="c-layout__cell"></div>
  <div class="c-layout__cell"></div>
  <div class="c-layout__cell"></div>
  <div class="c-layout__cell"></div>
</div>
```

### Modifiers on `c-layout__cell`

```html
<div class="c-layout">
  <div class="c-layout__cell  c-layout__cell--fit">Fit to content</div>
  <div class="c-layout__cell  c-layout__cell--fill">Take up remaining space</div>
  <div class="c-layout__cell  c-layout__cell--align-inline-center">Center align a single cell</div>
</div>
```

### Works with `u-colspan-X` on `c-layout__cell`

```html
<div class="c-layout">
  <div class="c-layout__cell  u-colspan-5">Spans 5 of 12 columns</div>
</div>
```

### Custom properties

```html
<div class="c-layout" style="--columns: 10; --gap: 3rem;">
  <div class="c-layout__cell" style="--colspan: 4;">
    Spans 4 of 10 columns
  </div>

  <div class="c-layout__cell" style="--colspan: 1;">
    Spans 1 of 10 columns
  </div>

  <div class="c-layout__cell" style="--colspan: 3;">
    Spans 3 of 10 columns
  </div>

  <div class="c-layout__cell" style="--colspan: 2;">
    Spans 2 of 10 columns
  </div>
</div>
```

**Note** Of course this specific use of custom properties(through inline styles) is pure for example purposes. It is advised to overwrite the custom properties in your own components instead of inline styles.

### Nesting

You can nest layouts in any context. Keep in mind that the dimensions will be relative to the width of `c-layout`, and not the width of the whole application.

```html
<div class="c-layout">
  <div class="c-layout__cell  c-layout__cell--fit">
    <div class="c-layout">
      <div class="c-layout__cell">
      </div>
    </div>
  </div>
</div>
```

### responsive modifiers
When you set breakpoints in `$fill-in-breakpoint` or `$fit-in-breakpoint` you can use them like this:

```html
<div class="c-layout">
  <div class="c-layout__cell  c-layout__cell--fit@from-lap">
    100% and from lap breakpoint it will fit to content
  </div>
  <div class="c-layout__cell  c-layout__cell--fill@from-lap">
    100% and from lap breakpoint it will fill remaining space
  </div>
</div>
```


## Available classes

**On the `.c-layout` block**

* `.c-layout`: core layout block
* `.c-layout--align-inline-center`: center align _all_ layout cells over the inline axis
* `.c-layout--align-inline-end`: align all layout cells to the end of the inline axis
* `.c-layout--align-block-center`: center-align layout cells on the block axis
* `.c-layout--align-block-end`: end-align layout cells on the block axis
* `.c-layout--reverse`: reverse all cells in order
* `.c-layout--fill`: evenly distribute space amongst all child cells
* `.c-layout--fit`: fit all cells to their content
* `.c-layout--equal-block-size`: All cells match the size of tallest cell in a row on the block axis
* `.c-layout--gap-base`: adds a base gutter between cells

**On the `.c-layout__cell` element**
* `.c-layout__cell`: Core layout cell element
* `.c-layout__cell--align-inline-center`: Center one cell on the inline axis
* `.c-layout__cell--fit`: Make a cell shrink wrap its content
* `.c-layout__cell--fill`: Make a cell fill the remaining space.
* `.c-layout__cell--[fit|fill]@[from|until]-[BREAKPOINT-NAME]`: applies `fit` or `fill` at the given breakpoint. (available in `$[fit|fill]-in-breakpoint` SCSS setting)


## Configurable variables
There are multiple ways to configure the layout composition. The Custom properties are calculated at run-time, the SCSS variables will allow you to change things at build-time.

### Custom properties

**On the `.c-layout` block**

* `--columns`: The number of columns you want to have, defaults to `12`
* `--gap`: The width of the gutter applied between the cells, defaults to `0`

**On the `.c-layout__cell` element**

* `--colspan`: The amount of columns this cell will span, defaults to `--columns`

### SCSS variables

* `$gaps`: a list of gaps where possible `.c-layout--gap-X` are generated from, defaults to `('base': defaults.$space-base)`
* `$fit-in-breakpoint`: a list of breakpoints where `c-layout__cell--fit` is generated for,  defaults to `()`
* `$fill-in-breakpoint`: a list of breakpoints where `c-layout__cell--fill` is generated for,  defaults to `()`

You can overwrite the SCSS variables the following ways:

```scss
// in your manifest file, eg. `styles.scss`
@use '~supple/lib/composition/layout' with (
  $fit-in-breakpoint: (lap, desk),
  $gaps: (
    'base': defaults.$space-base,
    'tiny': defaults.$space-tiny,
  ),
);
```
or
```scss
// in your own variable file, eg. `_vars.scss`
@use '~supple/lib/composition/layout/variables' with (
  $fit-in-breakpoint: (lap, desk),
  $gaps: (
    'tiny': defaults.$space-tiny,
    'huge': defaults.$space-huge,
  ),
);

// in your manifest file, eg. `styles.scss`
@use '~supple/lib/composition/layout';
```


## Installation
Make sure you've installed/downloaded the Supple CSS library:

* [npm](https://www.npmjs.com/package/supple): `npm install supple`
* Download: [zip](https://github.com/supple-css/supple/releases/latest)


## Testing
Basic visual tests are in [test.html](./test.html).


## Browser support

* Google Chrome (latest)
* Opera (latest)
* Firefox (latest)
* Safari (latest)
* Edge (latest chromium based)
* iOS (latest)
