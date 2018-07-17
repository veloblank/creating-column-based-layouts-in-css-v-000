# Creating Column-based Layouts in CSS

## Problem Statement

There are a number of ways to create columns and layouts using CSS. You can create layouts
that emulate print with little to no added markup that can adapt beyond a fixed canvas. With
the right combination of properties, building columns with CSS create a responsive-friendly
layout option that degrades gracefully.

## Objectives

1. Explain how to create column layouts using `float`
2. Explain how to create column layouts using "flexbox"
3. Explain how to create column layouts using `grid`
4. Explain how to create column layouts with CSS columns

## Explain how to Create Column Layouts Using `float`

Floats can be used to create entire web layouts. Floats were used to create column layouts
before the arrival of newer layout methods, so you'll likely run into this method in older
code bases. This method worked by setting fixed widths to containers, and setting them to
float next to one another. Manipulation of the percentage or fixed sizes of these floated
containers with appropriately calculated padding or margin would create the grid effect.

```html
<div class="container">
  <div class="col col-1">
     Main Content
  </div>
  <div class="col col-2">
     Sidebar
  </div>
</div>
```
```css
.col {
    float: left;
}
.col-1 {
  width: 66.66%;
}
.col-2 {
  width: 33.33%;
}
```
In this basic example, we float `.col` left and and apply widths to classes that define 2
different column types. This would cause the content to span edge to edge with no space or
gutter in between. In order to apply padding or other properties without having to adjust
width properties, we can apply the `border-box` box-sizing model for all elements and
psuedo-elements:

```css
*, *:before, *:after {
  box-sizing: border-box;
}
```

Using this "universal box-sizing" is a good way to work. The width you set is the width you get,
padding, borders, etc. included, without having to calculate math and manage the complexity that
come from varying widths that compound from multiple properties, and change the size of the container.

There are many ways to set up a CSS column structure using floats. Some of the
most common methods come in the form of CSS frameworks such as [Bootstrap 3][https://getbootstrap.com/docs/3.3], built with floating elements, fixed margins, and a 12-column grid system. You can read about a
responsive-friendly column layout with CSS `float` [here][https://webdesign.tutsplus.com/tutorials/quick-tip-building-responsive-layouts-with-floats--cms-25625].

This method is not recommended for new development, however, it will likely remain in
existing sites for some time. Therefore, if you come across a design where almost everything
seems to be floated, you will understand how to work within it.

## Explain how to Create Column Layouts Using "flexbox"

The main idea behind the flex layout is to give the container the ability to alter its items' width/height (and order) to best fill the available space (mostly to accommodate to all kind
of display devices and screen sizes). A flex container expands items to fill available free
space, or shrinks them to prevent overflow. It is designed for one-dimensional layout, meaning
a single row or column, such as with mobile layouts. To use "flexbox", set your container's
property `display: flex`.

```html
<div class="row">
  <div class="col"></div>
  <div class="col"></div>
  <div class="col"></div>
</div>
```
```css
.row {
  display: flex;
}
.col {
  flex: 1;
}
```

This will support any number of columns will automatically be equal widths and flexible.
If you need gutters, you can add margins and padding to the columns. You can use `justify-content`
to create the columns, like so:

```css
.row-thirds {
  display: flex;
  justify-content: space-between;
}
.row-thirds .col {
  width: 32%;
}
```
If you go the "flexbox" route, you have the ability to change the order of columns as needed,
which can be great for switching up and refactoring content hierarchy.


**NOTE: There are many edge cases and browser support issues that you may run into if you 
start using more niche flexbox features.**

## Explain how to Create Column Layouts Using `grid`

Grid is for layout of items in two dimensions – rows _and_ columns. As with "flexbox", Grid Layout
is a value of the `display` property. Start with `display: grid` on your container, and then set up
columns and/or rows using the `grid-template-columns` and `grid-template-rows` properties.

```css
.container {
    display: grid;
    grid-template-columns: 200px 200px 200px;
    grid-template-rows: 200px 200px;
}
```

You can use any length unit or a percentage, but you can also use the new `fr` unit--a unit created for
Grid Layout. The `fr` unit is a flex unit, and can distribute space for you; you don’t need to calculate
percentages to ensure elements fit into a container. 

```css
.container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-gap: 20px;
}
```
Using `grid-gap` specifies the gaps (gutters) between rows and columns.

A simpler way way to position elements in the grid is with line-based positioning. We can place an item
from column line 1 to column line 3, and row line 1 to row line 3. It will then cover four grid cells in total, spanning two column tracks and two column rows.

```css
.item {
    grid-column-start: 1;
    grid-column-end: 3;
    grid-row-start: 1;
    grid-row-end: 3;
}
```
_or_
```css
.item {
    grid-column: 1 / 3;
    grid-row: 1 / 3;
}
```

For more resources, you can visi [More on CSS Grid Layout][https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout/Box_Alignment_in_CSS_Grid_Layout] or check
out the links in the resources section.

## Explain how to Create Column Layouts with CSS Columns

CSS has the ability to organize content into columns and with vendor prefixes, you can get support
across most browsers. The main use case for CSS columns is to break long sections of text into
several columns, similar to in print media like newspapers and magazines. The great thing about CSS
columns is that the columns are defined with CSS only, and they don’t require any additional markup. 

However, with CSS columns, you can combine a grid system with a column layout! Grid supports fragmentation,
which means that a grid will also flow into a multiple column layout. 

```css
.columns {
  column-width: 200px;
  max-width: 800px;
  margin: 0 auto;
}
.grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-auto-rows: 2em;
  grid-gap: .5em;
}
```

<iframe width="100%" height="300" src="//jsfiddle.net/web_curriculum_kellye/g1jd8hLn/4/embedded/html,css,result/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>


In the previous example, you can see the difference in the top container with only the Grid Layout setup,
and the Grid Layout set up wrapped in CSS columns.

## Conclusion

There are many ways to format columns. We've provided the groundwork for understanding how side-by-side elements interact on the page, and how a number of different properties can affect the flow. Understanding these properties will be useful as you become familiar with "fluid" versus "responsive" layouts.

<p data-visibility='hidden'>View <a href='https://learn.co/lessons/column-structure' title='Column Structure'>Column Structure</a> on Learn.co and start learning to code for free.</p>

## Resources
[The New Layout Standard For The Web: CSS Grid, Flexbox And Box Alignment][https://www.smashingmagazine.com/2016/11/css-grids-flexbox-box-alignment-new-layout-standard/]
[Box Alignment Cheatsheet][https://rachelandrew.co.uk/css/cheatsheets/box-alignment]
[A Complete Guide to Grid][https://css-tricks.com/snippets/css/complete-guide-grid/]
[Grid by Example][https://gridbyexample.com/examples/]
