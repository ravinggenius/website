---
title: Pink() Notes For 2012-08-02: Breakpoint
created_at: 2012-08-02 23:22:52 UTC
---

https://github.com/lesjames/Breakpoint

## Pain Points

* Fluid Layouts
* Floats
* Media Queries
* Internet Explorer
* _something else was mentioned here..._
* Additional Markup
* Grid Complexity
* Many Different Resolutions
* Print
* Teams

## Breakpoint Philosophies

* fluid *and* fixed
  * fluid at low resolutions
  * snaps into one or more fixed layouts at higher resolutions
* columns
  * once you go fixed, columns remain the same size
  * frameless grid - more screen equals more columns, but columns stay the same width
* mobile first
  * start designing for low resolution devices first, then work up
* uses inline-block to work magic
  * griddle
  * everything works nicer (than using float)
* classes
  * non-semantic class names suck (.col-6 et cetera)
  * only three class names for grids (wrapper, grid, grid-cell)
* stays out of your way
  * doesn't limit design, tries to get out of the way
  * tries to not make every site built with it look the same
* internet explorer
  * non-javascript fallback
* media query management
  * breakpoint calculates and writes all media queries for you
* play nice with javascript
  * hooks for javascript to tell javascript which layout is active for responsive images

## Class Names

* .wrapper
  * snaps into fixed width layouts
  * centers itself on page
* .grid
  * 100% fluid inside .wrapper
  * uses negative letter-spacing to remove extra space between .grid-cell
* .grid-cell
  * must be only child of .grid (to compensate for negative letter-spacing)
* .responsive-image
  * %img.responsive-image{:src => 'data-uri for 1x1 transparent gif', :data-mobile => '', :data-desktop => ''}
  * use %noscript for non-javascript fallback
  * use 1x1 transparent gif as initial source; [data-uri](http://en.wikipedia.org/wiki/Data_URI_scheme) may work to prevent additional requests

## Example

    // _setup.sass
    // internet explorer gets the nine column layout
    //$ie-support: 9

    // _structure.sass
    @include breakpoint(6)
      .content
      .sub-content
    // $label sets font-family on %head (used for responsive image feature)
    @include breakpoint(9, $label: desktop)
      .content
        // percentage based width
        width: fluid(6)
        // em based width
        //width: fixed(6)
      .sub-content
        width: fluid(3)
      .feature
        width: fluid(3)
