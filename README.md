# dat-atomic SCSS

A scss library for rapid and readable templating.

Its aim is to be able to quickly position elements, style grids and texts.

By no means you should use this lib on its own, and I highly recommand writting scss components for your project's design.

Although, you should re-use dat-atomic variables as much as it is justified to do so.

## Installation

```
npm install dat-atomic
```
or
```
yarn add dat-atomic
```

## Import
You can load in different ways :
```
// Import all in one
@import "~dat-atomic";

// Import variables and resets separately.
@import "~dat-atomic/variables";
@import "~dat-atomic/static";
@import "~dat-atomic/resets";

// Import each module separately
@import "~dat-atomic/variables";
@import "/path/to/my/variables"; // <= custom variables values go here
@import "~dat-atomic/static/functions";
@import "~dat-atomic/static/fonts";
@import "~dat-atomic/static/spacing";
@import "~dat-atomic/static/flex-grid";
@import "~dat-atomic/static/utils";
@import "~dat-atomic/resets";
```
Don't hesitate to ignore the resets file, overwrite the variables, or even entirely replace the variables file with your own (don't forget any variable if you do though).

## Flex/grid

```
<div id="first-container" data-flex>...</div>
<div id="second-container" data-grid>...</div>
```
*equals to :*
```
#first-container {
    display: flex;
}
#second-container {
    display: grid;
}
```
But I want to set it to ``display: inline-grid;`` !  
No big deal :
```
<div id="first-container" data-flex="inline">...</div>
<div id="second-container" data-grid="inline">...</div>
```
*equals to :*
```
#first-container {
    display: inline-flex;
}
#second-container {
    display: inline-grid;
}
```
### Flex/grid flow :
Values for `flex-direction` are :
- column
- row
- column-reverse
- row-reverse
```
<div id="first-container" data-flex="row-reverse">...</div>
<div id="second-container" data-flex="column">...</div>
```
*equals to :*
```
#first-container {
    display: flex;
    flex-direction: row-reverse;
}
#second-container {
    display: flex;
    flex-direction: column;
}
```
Values for `grid-auto-flow` are :
- column
- row
- dense
- row-dense
- column-dense
```
<div id="first-container" data-grid="dense">...</div>
<div id="second-container" data-grid="column-dense">...</div>
```
*equals to :*
```
#first-container {
    display: grid;
    grid-auto-flow: dense;
}
#second-container {
    display: grid;
    grid-auto-flow: column dense;
}
```
### Flex wrapping
```
<div id="first-container" data-flex="wrap">...</div>
<div id="second-container" data-flex="nowrap">...</div>
<div id="third-container" data-flex="wrap-reverse">...</div>
```
*equals to :*
```
#first-container {
    display: flex;
    flex-wrap: wrap;
}
#second-container {
    display: flex;
    flex-wrap: nowrap;
}
#third-container {
    display: flex;
    flex-wrap: wrap-reverse;
}
```

### Justifying & aligning :
Alignement and justification properties are defined with the prefixes :
- ``justify-content`` : ``juco-``
- ``justify-items`` : ``juit-`` *(Warning : ``justify-items`` is NOT a valid property of the flex layout, it'll only effect the grid layout)*
- ``align-content`` : ``alco-``
- ``align-items`` : ``alit-``

Followed by the wanted value :
- ``flex-start`` : ``start``
- ``flex-end`` : ``end``
- ``center`` : ``center``
- ``stretch`` : ``stretch`` *(Warning : ``stretch`` is NOT a valid value for ``justify-content`` and ``align-content`` in the flex layout, it'll only effect the grid layout)*
```
<div id="first-container" data-flex="juco-center alit-center alco-center">...</div>
<div id="second-container" data-grid="juit-end juco-end alco-stretch alit-center">...</div>
```
*equals to :*
```
#first-container {
    display: flex;
    justify-content: center;
    align-items: center;
    align-content: start;
}
#second-container {
    display: grid;
    justify-items: flex-end;
    justify-content: flex-end;
    align-content: stretch;
    align-items: center;
}
```
## Flex/grid children
Flex and grid children properties can be defined in ``data-child``.
```
<div id="first-child" data-child="alse-center shrink">...</div>
<div id="second-child" data-child="alse-end no-grow">...</div>
<div id="third-child" data-child="grow">...</div>
```
*equals to :*
```
#first-child {
    align-self: center;
    flex-shrink: 1;
}
#second-child {
    align-self: flex-end;
    flex-grow: 0;
}
#third-child {
    flex-grow: 1;
}
```

### Self justifying & aligning :
Self alignement and justification properties are defined with the prefixes :
- ``align-self`` : ``alse-``
- ``justify-self`` : ``juse-`` *(Warning : ``justify-self`` is NOT a valid property of the flex layout, it'll only effect the grid layout)*

Followed by the wanted value :
- ``flex-start`` : ``start``
- ``flex-end`` : ``end``
- ``center`` : ``center``
- ``stretch`` : ``stretch``

### Grow and Shrink
