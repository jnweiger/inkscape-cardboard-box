
=========================
Unfinished. Idea only. No code here
=========================


inkscape-cardboard-box
======================

An inkscape extension featuring parametric design of cardboard boxes. Faltschachtel in German. And yes, parametric!

how it works
------------

Parametric design needs arithmetic terms for many of its dimensions.
These terms compute the dimension from parameters like 
width, height, depth and thickness.

We use a layer called 'parameters' for all the parametric meta information.
This layer should contain

* arrows with one head, and text "near" the other end. This text is either a pythonic tuple of terms, or a single term.

** arrows pointing horizontally (left or right, identical effect) define an x-coordinate, and should have single term.
** arrows pointing vertically (up or down) define an y-coordinate, and should have a single term.
** arrows pointing at any slanted angle define an (x,y) coordinate pair.

** the x=0 and y=0 coordinates must be defined exactly once, either as a pair, or by two separate arrows.

* python statements (that are not near any arrow). These python statements must 
  initialize all variable parameters, and should also contain assert() statements
  to define sane conditions for the parameters.
  They are executed from top to bottom, before any of the arrow terms are evaluated.

how to use
----------

Draw your design with typical dimensions.  If possible align edges parallel to the x and y axis, and use a snap grid.

Then define the parameters. The most common parameters for a simple cardboard
box would be width, height, depth, and perhaps material thickness, if it
matters. Extra parameters could be radii of corners, or cut outs.

Write down these parameter names and their value so that they match the typical
dimensions drawn.

Define the (x=0, y=0) origin of the design. 
Add as many arrows to label all major coordinates. If possible use a snap grid
for the arrow points.

* The numerical term of an horizontal arrow applies to all x-coordinates of line segment endpoints that visually align on the same x-position.
* The numerical term of a vertical arrow applies to all y-coordinates of line
segment endpoints that visually align on the same y-position.  
* The numerical
term values of a slanted arrow apply to the x,y position of all line segent end
points that are directly at the arrows point.

A small fudge value (typically 1/1000 of the page diagonale) is allowed while finding matching coordinates.
All coordinates that do not have matching arrows are interpolated using the two nearest arrows on opposite sides of the coordinate.
Take care to always put arrows on the extreme left, extreme right, extrem top
and extreme bottom of your design. It is an error if these are missing. No
extrapolation is done.

You may use horizontal guides to properly align your vertical arrows with the corners of your design. And vertical guides for aligning horizontal arrows.
Take care to have only one arrow per guide. Multiple (non-identical) terms at the same guide are an error.

Take care that independant edges and corners do not align. If they happen to
align when constructed correctly, you are free to give them a (small) offset in
one direction, so that independant arrows can be used.
Correct to scale construction of the design is not important for the computation. 
Only alignment with arrows matters. 

