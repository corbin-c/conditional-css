# conditional-css

This repo is just a demonstration of the possibility to perform boolean tests using
CSS vars.

The idea comes from this stackoverflow answer: https://stackoverflow.com/a/64322555/8086209

Sometimes you have one component that should behave differently based on its
size (or its container's), but CSS doesn't provide a way to handle this simply
(just like media queries to handle viewport size). The container query is
supposed to be implemented soon, but as I write these lines, it's still an
experimental feature, so this is a workaround.

The idea is to perform operations on a CSS variable so it outputs 0 or 1.

We would declare a `--width` & a `--threshold` var, and then do:

  * `--result = calc(var(--width) - var(--treshold))` : this outputs a negative number if width is inferior to threshold
  * `--positive = max(var(--result), 0)` : outputs the above result if positive, otherwise 0
  * `--boolean = min(1, --positive)` : outputs 1 or 0

So the shorthand for this would be :

`--boolean = min(1, max(var(--width) - var(--threshold), 0))`

Then this value can be used to trigger animations states using the `step` property.
When `--boolean` equals 0, the animation won't be triggered so the element will
get the default properties, otherwise the `to` keyframe will override them:

`animation: element-if-true steps(var(--boolean)) forwards;`

All animatables properties can be changed conditionnally using this technique.

The complete process can be seen in the [`style.css` file](./style.css) & the
result is shown here: https://corbin-c.github.io/conditional-css/
