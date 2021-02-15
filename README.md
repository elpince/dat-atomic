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
You can load all of dat-atomic with :
```
@import "node-modules/dat-atomic";
```
## Flex & grid

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
## Justifying & aligning :
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
<div id="first-container" data-flex="inline">...</div>
<div id="second-container" data-grid="inline">...</div>
```
*equals to :*
```
#some-id {
    display: flex;
    flex-direction: column;
    flex-wrap: nowrap;
    justify-content: center;
    align-items: center;
    align-content: start;
}
```
#### Customize flex children (col attribute) :
Syntax for column size value is {breakpoint}{column-width}.

**{breakpoint}** can be :
- xs
- sm
- md
- lg
- xl

It corresponds to breakpoints set in "_variables.scss", xs being the default (min-width: 0) value.

**{column-width}** is an integer from 1 to 12 that defines column width as width: 100% / 12 * {column-width}.
```
<div id="some-id"
     flex="column nowrap justify-center items-center content-start">
    <div id="some-child"
         col="md6 xs12 end grow">
    <div>
</div>
```
*equals to :*
```
#some-child {
    align-self: flex-end;
    flex-grow: 1;
    width: 100%;
    flex-basis: 100%;
    
    @media screen and (min-width: $md-breakpoint) {
        width: 50%;
        flex-basis: 50%;
    }
}
```
***see "_flex.scss" file for complete list of values for "flex" and "col" attributes.***

## Spacing
Spacing values are all based on the $space variable defined in "_variables.scss" (default value is 1rem)

Syntax for spacing value is {type}{direction}{size}.

**{type}** can be :
 - m (for margin)
 - p (for padding)

**{direction}** can be :
 - t (for top)
 - r (for right)
 - b (for bottom)
 - l (for left)
 - x (for left and right)
 - y (for top and bottom)
 - a (for all 4 directions)
 
**{size}** is an integer from 1 to 6 and corresponds, each of them corresponding to a multiplier :
 - 1 is ( $space x 0.5 )
 - 2 is ( $space x 1 )
 - 3 is ( $space x 2 )
 - 4 is ( $space x 4 )
 - 5 is ( $space x 6 )
 - 6 is ( $space x 10 )

#### Customize spacing attribute :
```
<div id="some-id" spacing="mt1 mb3 mx4 pa2">
    ...
</div>
```
*equals to :*
```
#some-id {
    padding: 1rem;
    margin-right: 4rem;
    margin-left: 4rem;
    margin-top: .5rem;
    margin-bottom: 2rem;
}
```
##### note that direction a gets overridden by x and y which get overridden by t, r, b and l :
```
<div id="some-id" spacing="pa4 px2 pt1 pr6">
    ...
</div>
```
*equals to :*
```
#some-id {
    padding: 4rem;
    padding-right: 1rem;
    padding-left: 1rem;
    padding-top: .5rem;
    padding-right: 10rem;
}
```
*which results in :*
```
#some-id {
    padding-bottom: 4rem;
    padding-left: 1rem;
    padding-top: .5rem;
    padding-right: 10rem;
}
```
## Hidden
Apply ***display: none;*** to an element depending on screen width.

Values given to ***hide-from*** attribute determine a range from one breakpoint (included) to 0 or infinite,
depending on given direction.

Syntax for hidden range value is {breakpoint}-{direction}

**{breakpoint}** can be :
- xs
- sm
- md
- lg
- xl

**{direction}** can be :
- up
- down

#### Customize hide-from attribute :
```
<div id="some-id" hide-from="sm-down lg-up">
    ...
</div>
```
*equals to :*
```
#some-id {
    @media screen and (max-width: $md-breakpoint - 1) {
        display: none !important;
    }
    @media screen and (min-width: $lg-breakpoint) {
        display: none !important;
    }
}
```
## Grid
###### WARNING : grid library is not supported by IE

##### Add grid
```
<div id="some-id" grid>
    ...
</div>
```
*equals to :*
```
#some-id {
    display: grid;
}
```
#### Customize grid container (grid attribute) :

Syntax for grid values is {breakpoint}{nb-columns}

**{breakpoint}** can be :
- xs
- sm
- md
- lg
- xl

**{nb-columns}** is an integer from 1 to 16, defining the number of columns in your grid

```
<div id="some-id"
     grid="xs2 md4 xl10">
    ...
</div>
```
*equals to :*
```
#some-id {
    grid template-columns: 1fr 1fr;

    @media screen and (min-width: $md-breakpoint) {
        grid template-columns: 1fr 1fr 1fr 1fr;
    }
    @media screen and (min-width: $xl-breakpoint) {
        grid template-columns: 1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr;
    }
}
```

#### Customize grid children (cell attribute) :

Syntax for cell values is {direction}{span}

**{direction}** can be :
- col
- row

**{span}** is an integer from 1 to 16, defining the child's column span

```
<div id="some-id"
     grid="xs2 md4 xl10">
    <div id="child-id"
         cell="col10 row2">
    </div>
</div>
```
*equals to :*
```
#child-id {
    grid-column: 10 span;
    grid-row: 2 span;
}
```
