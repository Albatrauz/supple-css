# Supple CSS | composition.mesh

Mesh makes use of `grid` & Custom Properties to provide for a flexible, fluid & extensible grid system. In a declaritive way you can create a variety of different grid systems for every need.

If you want to arrange items over 1 dimension (horizontal) I recommend using [composition.layout](../layout).

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
* Fluid grid system.
* Intelligent cell wrapping.
* Evenly fill cell spacing.
* Fluid width columns that break into more or less columns as space is available.
* Masonry layout


## Use

A simple mesh is easy to create. A mesh container can have any number of child cells.

**Note** `.c-mesh` only accepts `.c-mesh__cell` as direct descendants. This keeps our layout nicely separated from other components.

```html
<div class="c-mesh  c-mesh--gap-base">
  <div class="c-mesh__cell"><!-- content --></div>
  <div class="c-mesh__cell"><!-- content --></div>
  <div class="c-mesh__cell"><!-- content --></div>
  <div class="c-mesh__cell"><!-- content --></div>
</div>
```

For more granular control over mesh make use of modifiers, custom properties or sizing utilities.

### Modifiers on `c-mesh`

```html
<div class="c-mesh  [c-mesh--flow  |  c-mesh--dense  |  c-mesh--gap-base]">
  <div class="c-mesh__cell"></div>
  <div class="c-mesh__cell"></div>
  <div class="c-mesh__cell"></div>
  <div class="c-mesh__cell"></div>
</div>
```

### Modifiers on `c-mesh__cell`

```html
<div class="c-mesh">
  <div class="c-mesh__cell  c-mesh__cell--row">Spans a full row</div>
</div>
```

### Works with `u-colspan-X` & `u-colstart-X` on `c-mesh__cell`

```html
<div class="c-mesh">
  <div class="c-mesh__cell  u-colspan-5  u-colstart-2">Spans 5 of 12 columns and starts at column 2</div>
</div>
```

### Custom properties

```html
<div class="c-mesh" style="--columns: 10; --gap: 3rem;">
  <div class="c-mesh__cell" style="--colspan: 4;">
    Spans 4 of 10 columns
  </div>

  <div class="c-mesh__cell" style="--colspan: 1;  --colstart: 5;">
    Spans 1 of 10 columns starts at column 5
  </div>

  <div class="c-mesh__cell" style="--colspan: 3;">
    Spans 3 of 10 columns
  </div>

  <div class="c-mesh__cell" style="--colspan: 2;">
    Spans 2 of 10 columns
  </div>
</div>
```

**Note** Of course this specific use of custom properties(through inline styles) is pure for example purposes. It is advised to overwrite the custom properties in your own components instead of inline styles.

### Nesting

You can nest mesh in any context. Keep in mind that the dimensions will be relative to the width of `c-mesh`, and not the width of the whole application.

```html
<div class="c-mesh">
  <div class="[ c-mesh__cell  c-mesh ]  [ u-colspan-X ]">
    <div class="[ c-mesh__cell ]  [ u-colspan-X ]">
    </div>
  </div>
</div>
```

### responsive modifiers
When you set breakpoints in `$row-in-breakpoint` you can use it like this:

```html
<div class="c-mesh">
  <div class="c-mesh__cell  c-mesh__cell--row@from-lap">
    spans 1 column and from lap breakpoint it will span 12 columns (full row).
  </div>
</div>
```


## Available classes

**On the `.c-mesh` block**

* `.c-mesh`: core mesh block
* `.c-mesh--flow`: Fluid width columns that break into more or less columns as space is available, with no media queries.
* `.c-mesh--dense`: Attempt to fill in holes earlier in the grid if smaller items come up later.
* `.c-mesh--gap-base`: adds a base gutter between cells

**On the `.c-mesh__cell` element**
* `.c-mesh__cell`: Core mesh cell element
* `.c-mesh__cell--row`: Spans a full row
* `.c-mesh__cell--row@[from|until]-[BREAKPOINT-NAME]`: Spans full row on a certain breakpoint (available in `$row-in-breakpoint` SCSS setting)


## Configurable variables
There are multiple ways to configure the mesh composition. The Custom properties are calculated at run-time, the SCSS variables will allow you to change things at build-time.

### Custom properties

**On the `.c-mesh` block**

* `--columns`: The number of columns you want to have, defaults to `12`
* `--gap`: The width of the gutter applied between the cells, defaults to `0`
* `--block-gap`: The space of the gutter applied between the cells on the block axis, defaults to `--gap`
* `--inline-gap`: The space of the gutter applied between the cells on the inline axis, defaults to `--gap`

**On the `.c-mesh--flow` modifier**

* `--min-inline-size`: minimum size that a cell needs to have

**On the `.c-mesh__cell` element**

* `--colspan`: The amount of columns this cell will span, defaults to `--columns`
* `--colstart`: Startpoint of the cell

### SCSS variables

* `$gaps`: a list of gaps where possible `.c-mesh--gap-X` are generated from, defaults to `('base': defaults.$space-base)`
* `$row-in-breakpoint`: a list of breakpoints where `c-mesh__cell--row` is generated for,  defaults to `()`

You can overwrite the SCSS variables the following ways:

```scss
// in your manifest file, eg. `styles.scss`
@use '~supple/lib/composition/mesh' with (
  $row-in-breakpoint: (lap, desk),
  $gaps: (
    'base': defaults.$space-base,
    'tiny': defaults.$space-tiny,
  ),
);
```
or
```scss
// in your own variable file, eg. `_vars.scss`
@use '~supple/lib/composition/mesh/variables' with (
  $row-in-breakpoint: (lap, desk),
  $gaps: (
    'tiny': defaults.$space-tiny,
    'huge': defaults.$space-huge,
  ),
);

// in your manifest file, eg. `styles.scss`
@use '~supple/lib/composition/mesh';
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
