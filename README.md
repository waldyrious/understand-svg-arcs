# Understanding SVG arcs

**SVG paths** can be daunting at first,
but upon closer examination,
most of the commands can be understood pretty intuitively.

The syntax of the **arc command**, however, seems to be an exception.
This repo provides some resources that hopefully make its syntax clearer.

See the main **[demo page](http://waldyrious.github.io/understand-svg-arcs)**,
as well as the [links below](#resources) for more in-depth explanations.

## Details

The awkward [syntax of the arc command](https://www.w3.org/TR/SVG/implnote.html#ArcSyntax)
comes out of the desire to unify the syntax of the svg path commands,
so that all path commands end with the coordinates of the new "current point".

However, just like a circle is defined more intuitively
by specifying the center and radius,
an elliptical arc is also best understood
if defined by its center, the minor and major radius,
the starting angle and the angular span it covers.

The best way to think of SVG's "endpoint parametrization"
is as providing parameters to a
**[constraint solver](https://en.wikipedia.org/wiki/Constraint_programming)**:
the arc has to follow an ellipse
with a given width/height ratio (x-radius vs. y-radius),
with a given rotation<sup>†</sup>, and that passes through the start point
given at the end of the preceding path command, and the end point
given at the end of the arc command.

<sup>†</sup>Note that the rotation maintains the start and end points,
whereas a rotation with the transform attribute (outside the path description)
would cause the entire path, including the start and end points, to be rotated.

These restrictions (with a few
[adjustments to prevent unsolvable constraints](https://www.w3.org/TR/SVG/implnote.html#ArcOutOfRangeParameters))
result in two possible ellipses,
and four corresponding elliptical arcs
connecting the two endpoints.
The "large arc" and "sweep" flags then provide disambiguation
between these four arc possibilities,
giving a unique, unambiguous (but highly unintuitive)
arc parametrization.

## Resources

The main example on this repo takes inspiration from the excellent diagram
in the [OReilly Commons wiki](http://commons.oreilly.com/wiki/index.php/SVG_Essentials/Paths#Elliptical_Arc).

The SVG implementation of this diagram was inspired by
[Jakob Jenkov](https://github.com/jjenkov)'s excellent [svg paths tutorial](http://tutorials.jenkov.com/svg/path-element.html#arcs),
with some help from his [svg markers tutorial](http://tutorials.jenkov.com/svg/marker-element.html)
for the arrow heads. He also made a
[video version of the svg paths tutorial](https://youtu.be/k6TWzfLGAKo?t=2m52s)
(content about arcs starts at 2:52), which helps visualize the effects of the arc command parameters.

Another nice video explanation is
[this one](https://youtu.be/Iyb3R_1NkEU?t=10m42s) by [Glenn Howes](https://github.com/grhowes)
(content about arcs starts at 10:42).
[The iOS app used in the video](https://itunes.apple.com/us/app/svg-paths/id690371196)
seems to be an interesting way to experiment with arcs interactively.
