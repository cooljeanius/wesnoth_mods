.. vim:ft=rst:

====================
Terrain Graphics WML
====================

.. contents:: Table of Contents

Tutorial documentation
======================

The [terrain_graphics] tags describes a terrain graphics rule, which associates
a set of images to a given terrain configuration. Those are used to define how
to translate a map into a set of bitmap images which will be displayed to the
user.

[terrain_graphics] WML tags may be either top-level tags, or defined as direct
children of scenarios.

Defining a rule
---------------

To define a terrain graphics rule, just add one [terrain_graphics] element. The
simplest terrain_graphics rule looks like this::

  [terrain_graphics]
  [/terrain_graphics]

Of course, this rule does absolutely nothing, so it is completely useless.

Adding constraints to rules
---------------------------

For rules to do anything useful, one must first add some conditions which will
specify where they will match. This is done using the [tile] WML tag.
[tile] WML elements define what we will name, in the rest of this document, a
"constraint".

For example, the following WML code adds a constraint to our empty rule::

  [terrain_graphics]
     [tile]
        x=0
        y=0
        type=g
     [/tile]
  [/terrain_graphics]

Let's describe the elements defined inside this WML tag:

* x and y define the /offset/ of the constraint.
* type defines the type of the terrain which will be matched.

Supposed, the terrain map is the following one (the letter inside the hexes
representing the terrain type)::

   __    __
  /g \__/g \
  \__/m \__/
  /g \__/c \
  \__/c \__/
  /c \__/c \
  \__/  \__/

The rule we defined will match on each terrains marked "g"

What is the use of those "offsets", then? Those allow for a rule to match, a
combination of terrains and not a single terrain. Suppose, for example, we want
the rule to match the following terrain configuration::

   __ 
  /g \__
  \__/c \
     \__/

To achieve this, we will define the rule like this::

  [terrain_graphics]
     [tile]
        x=0
        y=0
        type=g
     [/tile]
     [tile]
        x=1
        y=0
        type=c
     [/tile]
  [/terrain_graphics]

Here, this rule has 2 constraints:

* The first one which specifies that the terrain at the offset (0, 0), should
  be of type "g"
* The second one which specifies that the terrain at the offset (1, 0) should
  be of type "c"

The hex coordinate system
-------------------------

To reference hexes with a system of 2 coordinates, the Wesnoth map model is
used. The top-left hex is numbered (0, 0), then the hex immediately to its SE
side is numbered (1, 0), then the hex immediately to its NE side is numbered
(2, 0), etc. The hex immediately behind the hex numbered (0, 0) is (1, 0), and
so on. Here is a picture representing coordinates of hexes::

    ____        ____        ____        ____
   /    \      /    \      /    \      /    \
  / 0,0  \____/ 2,0  \____/ 4,0  \____/ 6,0  \
  \      /    \      /    \      /    \      /
   \____/ 1,0  \____/ 3,0  \____/ 5,0  \____/
   /    \      /    \      /    \      /    \
  / 0,1  \____/ 2,1  \____/ 4,1  \____/ 6,1  \
  \      /    \      /    \      /    \      /
   \____/ 1,1  \____/ 3,1  \____/ 5,1  \____/
   /    \      /    \      /    \      /    \
  / 0,2  \____/ 2,2  \____/ 4,2  \____/ 6,2  \
  \      /    \      /    \      /    \      /
   \____/ 1,2  \____/ 3,2  \____/ 5,2  \____/
   /    \      /    \      /    \      /    \
  / 0,3  \____/ 2,3  \____/ 4,3  \____/ 6,3  \
  \      /    \      /    \      /    \      /
   \____/ 1,3  \____/ 3,3  \____/ 5,3  \____/
        \      /    \      /    \      /    
         \____/      \____/      \____/

When we talk about an offset OF (xo, yo) FROM (xf, yf), we talk about the point
which would be at the position  (xo, yo) if (xf, yf) was (0, 0). This is *not*
always the sum of coordinates! For example, the offset (1,0) from (2,0) is (3,
0), but the offset (1, 0) from (3, 0) is (4, 1)

Type strings
------------

What if we want a constraint to be able to match several terrain types? To do
this, just put the list of types we want to match in the ``type=`` element of
the [tile] tag. For example, the following rule will match any terrain with is
either grassland (g), or dirt (r)::

  [terrain_graphics]
     [tile]
        x=0
        y=0
        type=gr
     [/tile]
  [/terrain_graphics]

The following characters are also possible:

* The ``*`` character means 'any terrain'. Any constraint with the 
  ``type=*`` element will match any possible terrain type. We'll see below for
  actual uses of such constraints.
* The ``!`` character inverts the meaning of the terrain type list. Instead of
  matching terrains which are in the list, the constraint will match terrains
  which are not in the list.

Adding images to terrains
-------------------------

Now that we have "rules" which can "match", we need to make the do something
useful, that is, adding new images to terrains. This is done using the
``[image]`` tag. The basic syntax for ``[image]`` tags is the following one::

  [image]
     name=<name>
  [/image]

Where <name> is to be replaced by the base filename of the image. The string
"terrain/" will be prepended to this name, and the string ".png" will be
appended to it, to generate the actual filename of the image.

Image tags may appear into constraints, or into rules; those have slightly
different meanings.

[image] tags into constraints
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

When [image] tags are placed into constraints, they must specify a single-hex
image (currently, that means the ipmage must be 72x72). When the rule which
contains the given contraint matches (that is, when all the rule's constraint
match,) the image will be added to the hex corresponding to the constraint. For
example, if our rule looks like this::

  [terrain_graphics]
     [tile]
        x=0
        y=0
        type=g
     [/tile]
     [tile]
        x=1
        y=0
        type=c
        [image]
           name=foobar
        [/image]
     [/tile]
  [/terrain_graphics]

And if the terrain looks like this::

   __    __
  /g \__/g \
  \__/m \__/
  /g \__/c \
  \__/c*\__/
  /c \__/c \
  \__/  \__/

Then the tile at coordinate (1,1) (the one marked with a star) will get the
image "terrains/foobar.png". The other tiles will get nothing from this rule,
even the tile at the coordinates (0,1), which corresponds to the first
constraint of this rule.

Several images may appear in a single constraint. Images may appear each
constraint of a rule.

[image] tags directly into the rule
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

When [image] tags are directly placed into a rule, they may specify a multi-hex
image. The image will be split into sub-images the size of a hex, and each of
those sub-images will be added to the corresponding hex, if the rule contains a
constraint in that position.

For example, consider the following rule::

  [terrain_graphics]
     [tile]
        x=0
        y=0
        type=g
     [/tile]
     [tile]
        x=1
        y=0
        type=c
     [/tile]
     [image]
        name=foobar
     [/image]
  [/terrain_graphics]

The foobar image being a 126x108 image which looks like this::

 ________________
 | /    \       |
 |/  A   \____  |
 |\ (0,0)/    \ |
 | \____/  B   \|
 |      \ (1,0)/| 
 |_______\____/_|

The terrain, still is the same map::

   __    __
  /g \__/g \
  \__/m \__/
  /g+\__/c \
  \__/c*\__/
  /c \__/c \
  \__/  \__/

Here, the part marked "A" of the image will be applied to the hex marked with a
+, whereas the part marked "B" of the image will be added to the hex marked
with a \*.

However, suppose we wish to define a village which casts a shadow on nearby
tiles. We draw a 126x144 image like the following one [*]_::

 ________________
 |              |
 |        ____  |
 |       /    \ |
 |  ____/  V   \|
 | /    \ (1,0)/| 
 |/shadow\____/ |
 |\ (0,1)/      |
 |_\____/_______|

.. [*] Notice that, when maps are cut, the top-left part of the map always is a
       full hex, namely the hex marked (0,0), even if it doesn't correspond to
       anything on the map.

The rule only matches villages, so we should be tempted to write something like
that (assuming B is the village tile)::

  [terrain_graphics]
     [tile]
        x=1
        y=0
        type=B
     [/tile]
     [image]
        name=shadow-village
     [/image]
  [/terrain_graphics]

However, this will **not** work: the village will be displayed, but not the
shadow! Remember what was written before: *those sub-images will be added to
the corresponding hex, if the rule contains a constraint in that position.* As
there is no constraint at the location (0,1), there will be no image either.

So, the solution is to add a match-all constraint, like this::

  [terrain_graphics]
     [tile]
        x=1
        y=0
        type=B
     [/tile]
     [tile]
        x=0
        y=1
        type=*
     [/tile]
     [image]
        name=shadow-village
     [/image]
  [/terrain_graphics]

Here, everything will work correctly.

Using flags
-----------

Rules may also set flags upon matching, and check for the absence, or presence,
of flags, before being applied. This allows, for example, to make some
mutually-exclusive rules. Flags are character strings whicy may be added to
each hex of the map. Flags are not visible to the user, and only are used for
the purpose of calculating terrain graphics.

Setting flags
~~~~~~~~~~~~~

A [tile] tag may have the ``set_flag`` element present, followed by a
comma-separated list of flags. This specifies that, when the rule which
contains this constraint does match, the following flags are to be set to the
terrain corrsponding to this constraint.

Testing for flags
~~~~~~~~~~~~~~~~~

A [tile] tag may have the ``has_flag`` element present, followed by a
comma-separated list of flags. This specifies that this constraint will only
match if the corresponding hex has *each* of the flags present in the list.
Those flags may have been set be previous rules.

A [tile] tag may have the ``no_flag`` element present, followed by a
comma-separated list of flags. This specifies that this constraint will only
match if *none* of the flags present in the list are present on the
corresponding hex.

Flags under [terrain_graphics]
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

``set_flag``, ``has_flag`` and ``no_flag`` may also be defined as children of
[terrain_graphics] WML elements. Doing this is equivalent to defining those
same flags in each constraint.

A common use for flags is to make mutually-exclusive rules. For example, if we
have one rule which defines a 2-hex grassland tile, and another rule which
defines a 1-hex grassland tile, we do not want both to appear on the same hex.
So, the rules may be defined like that::

  [terrain_graphics]
     [tile]
        x=0
        y=0
        type=g
     [/tile]
     [tile]
        x=0
        y=1
        type=g
     [/tile]
     [image]
        name=2-tile-grassland
     [/image]
     set_flag=base
  [/terrain_graphics]

  [terrain_graphics]
     [tile]
        x=0
        y=0
        type=g
     [/tile]
     [image]
        name=1-tile-grassland
     [/image]
     no_flag=base
  [/terrain_graphics]

Here, the first rule, regarding the 2-tile grassland, will be checked first. If
it does match, it will set, on both hexes, the flag "base". Hence, the second
rule won't match on any of those hexes, because it has "no_flag=base".

It is quite common to add, in the same rule, ``set_flag=flag`` and
``no_flag=flag``. This allows to define a set of mutually-exclusive rules,
irrespectively of the order in which they will be applied.

Using map-strings
-----------------

Defining large multi-hex terrains may be rather confusing when the number of
tiles increase. To make this simpler, a shortcut notation was introduced:
map-strings. Map strings are defined by adding a ``map`` element under a
``terrain_graphics`` tag.

Map string format
~~~~~~~~~~~~~~~~~

Map strings are stings, generally multi-line, which are parsed the following
way:

* Starting empty lines are discarded.
* If the first non-empty line starts with a space, it is given the line number
  "1". Else, it is given the line-number "0"
* If the line is odd-numbered, its first 2 characters are discarded
* The rest of the line is split into 4-character chunks (or smaller if less
  characters are left in the current line.)
* For each of those 4-character chunks:

  + If the chunk consists in a dot, it is ignored.
  + If the chunk consists a combination of any characters except digits, a new
    rule is created.
  + If the chunk consists in digits, a new anchor_ is created (see below.)
  + The column-number is increased by one.

A rule created by a map will be the exact equivalent of the following WML::

  [tile]
     x=<x>
     y=<y>
     type=<type>
  [/time]

Where <type> is the 4-character string of the current chunk, and where x and y
are given by the following formula:

x = (lineno % 2) + colno * 2
y = lineno / 2

"%" being the modulus operator, and "/" the integer division operator.

For example, the following notations will be equivalent.

Map notation::

  [terrain_graphics]
    map="
  g   !c
    mh
  gd"
  [/terrain_graphics]

Classic notation::

  [terrain_graphics]
     [tile]
        x=0
        y=0
        type=g
     [/tile]
     [tile]
        x=1
        y=0
        type=mh
     [/tile]
     [tile]
        x=2
        y=0
        type=!c
     [/tile]
     [tile]
        x=0
        y=1
        type=gd
     [/tile]
  [/terrain_graphics]

Anchors
~~~~~~~

.. _anchor:

As was stated before, maps may, instead of specifying terrains, may also
specify "anchors". Anchors do not define actual rules. However, when an anchor
is set, any [tile] WML child tag may use, instead of ``x`` and ``y``, the WML
element ``pos=<anchor>``, where anchor is the index of the anchor, from 0 to 9.
This will define a rule as normal, except that its offset will be the offset of
the anchor.

An useful feature is that a same anchor may be specified multiple times. When a
[tile] tag uses this anchor, this will create several rules at once! For
example: the following notations are equivalent::

  [terrain_graphics]
     map="
    1
  1   1
    2
  1   1
    1"
     [tile]
        pos=1
        type=m
        set_flag=adjacent_to_foo
     [tile]
     [tile]
        pos=2
        type=m
        no_flag=adjacent_to_foo
        [image]
           name=foo
        [/image]
     [/tile]
  [/terrain_graphics]

And::

  [terrain_graphics]
     [tile]
        x=1
        y=0
        type=m
        set_flag=adjacent_to_foo
     [/tile]
     [tile]
        x=0
        y=1
        type=m
        set_flag=adjacent_to_foo
     [/tile]
     [tile]
        x=1
        y=1
        no_flag=adjacent_to_foo
        [image]
           name=foo
        [/image]
     [/tile]
     [tile]
        x=2
        y=1
        type=m
        set_flag=adjacent_to_foo
     [/tile]
     [tile]
        x=0
        y=2
        type=m
        set_flag=adjacent_to_foo
     [/tile]
     [tile]
        x=1
        y=2
        type=m
        set_flag=adjacent_to_foo
     [/tile]
     [tile]
        x=1
        y=3
        type=m
        set_flag=adjacent_to_foo
     [/tile]
  [/terrain_graphics]

Rule parameters
---------------

The 2 elements ``probability``, and ``precedence``, and the ``x`` and ``y``
couple, may be added directly under the [terrain_graphics] WML tag. Those
affect the rule as a whole, and have the following meaning:

Position: x and y
~~~~~~~~~~~~~~~~~

If a rule defines the ``x`` and ``y`` elements, it may only match on this
position of the screen (provided all other conditions are met). May be useful
for some scenario-specific terrains that only may appear at one given position.

Probability
~~~~~~~~~~~

The ``probability`` element defines the probability of a rule to match, when
all other conditions are met. It is a number from 0 to 100, 0 meaning "this
rule will never match", and 100 "this rules always matches, provided all other
conditions are met."

Precedence
~~~~~~~~~~

Usually, rules do not define any precedence, and are executed in the order they
are defined. rules with a lower precedence will always be executed before rules
with a higher precedence. This allows for custom scenario to define custom
rules and to choose whether they have to be defined before, or after generic
rules.

Layering images
---------------

When images are defined like what was explained above, without any layering
information, they will be displayed on-screen in a first-to-last way, that is,
images which are added first go into the background, and images which are added
last go into the foreground. This may not be what we expect; so, in general,
some "layering"-related elements are added to the images, directly into the
[image] WML tags.

2 layering models exist; an image can use either model. The two layering models
are the horizontal model, and the vertical model. Model is selected with the
``position`` element.

Horizontal-layered images
~~~~~~~~~~~~~~~~~~~~~~~~~

The simplest, default layering model is called the "horizontal" model. Images
are set to usie the horizontal model by either specifying
``position=horizontal`` in the [image] tag, or by not specifying a position at
all.

The horizontal layering model is pretty simple: each image may define, using
the ``layer`` element, which layer it is in. The layer index is an integer
number going from -1000 (most background) to +1000 (most foreground) (actually,
using higher and lower number should work, but this may change.) Images which
have negative layeris are displayed behind unit graphics; images which have
positive layers are displayed in front of unit graphics.

Images which are in the same layer are ordered the classic way, in the order
they are defined. If an image does not specify a layer, it will be assumed to
be in layer 0.

For example, suppose the two following rules::

  [terrain_graphics]
     [tile]
        x=0
        y=0
        type=t
        [image]
           position=horizontal
           layer=-500
           name=village_foreground
        [/image]
     [/tile]
  [/terrain_graphics]

  [terrain_graphics]
     [tile]
        x=0
        y=0
        type=t
        [image]
           position=horizontal
           layer=-1000
           name=village_background
        [/image]
     [/tile]
  [/terrain_graphics]

In this case, village_background will be drawn behind village_foreground, even
if it is defined after it.

Vertical-layered images
~~~~~~~~~~~~~~~~~~~~~~~

Images may also specify ``position=vertical`` in the [image] tag, so they use
the "vertical" model. Vertical-layered images are not disposed in flat, stacked
layers, but are instead assumed, when they are rendered, to have an (x, y)
position on the screen. They are, then, drawn according the rule which states
that objects in the bottom are hidden by objects in the front.

To use the vertical model, [image] tags should contain the ``base`` element,
like this::

  base=x,y

Where x, and y, are the coordinates, in pixels, of the base of the image (that
is, the virtual point at which the image would be in contact of the ground).
Those coordinates are relative to the top-left-corner of the image. 

If the image is a single-hex image, this means that the ``base`` coordinates
are relative to the top-left corner of the smallest square containing the tile
hex.

If the image is a multi-hex image (see the `[image] tags directly into the rule`_
section for more info,) this means that the ``base`` coordinates are relative
to the top-left corner of the multi-hex image. Please note that, when using
multi-hex images, the top-left hex of the image always is assumed to ihave hex
coordinates (0,0) (see above). The coordinates of ``base`` will always be
relative to the top-left of  **this hex**, even if the rules contains no
constraint regarding (0, 0).

**Note**: for positioning purposes, units are supposed to be in the position
(36,54) relative to the top-left corner of the square containing their hex.
This means that any image in front of this may hide units.

**Note**: vertical-layered images are always drawn in front of
horizontal-layered images which have a negative layer, whatever their
respective layers and base coordinates may otherwise be. Vertical-layered
images are always drawn behind horizontal-layered images which have a positive
layer. [*]_

.. [*] However, this may be broken in wesnoth up to 0.8.11

Using rotation templates
------------------------

Rules sometimes are rotated versions of other, similar rules. To simplify the
definition of such rules, the notion of "rotation templates" was introduced.
Those are [terrain_graphics] definitions which do not define one rule, but may
define up to 6 rules, each one rotated by a Pi/3 [*]_ angle.

To define a rotation template, defines a [terrain_graphics] rule, as usual,
except that this rule should contain the ``rotations`` element, followed by a
list of 6 comma-separated strings (usually short ones.)

The image names and flag names of the rule and of its constraints may contain
template strings of the form ``@Rn``, n being a number from 0 to 5.
   
A template rule will generate 6 rules, which are similar to the template,
except that:
   
* The map of constraints of this rule will be rotated by an angle, from 0 to 5
  pi / 6. Note that the relative positions of the constraints will be rotated,
  too; and so will the "base" of images whose position is set to "vertical". 

  After being rotated, each set of constraint will be translated, so that:
  
  + There is no constraint with negative coordinates
  + There is at least one constraint which has x=0
  + There is at least one constraint which has y=0

  This is important, because, for example, rules about multi-hex images will
  then apply as usual, using the modified set of constraints
   
* On the rule which is rotated to 0rad, the template strings @R0, @R1, @R2,
  @R3, @R4, @R5, will be replaced by the corresponding r0, r1, r2, r3, r4, r5
  variables given in the rotations= element.
   
* On the rule which is rotated to pi/3 rad, the template strings @R0, @R1, @R2
  etc. will be replaced by the corresponding *r1, r2, r3, r4, r5, r0* (note the
  shift in indices).
   
* On the rule rotated 2pi/3, those will be replaced by r2, r3, r4, r5, r0, r1
  and so on.

For example, the following notations are equivalent

The compact template-based rotation::

  [terrain_graphics]
      map="
  1
    g"
      [tile]
         pos=1
         image=bar-@R0-@R3
      [/tile]
      rotations=se,s,sw,nw,n,ne
  [/terrain_graphics]

And the quite verbose classic notation::

  [terrain_graphics]
      map="
  1
    g"
      [tile]
         pos=1
         image=bar-se-nw
      [/tile]
  [/terrain_graphics]
  [terrain_graphics]
      map="
  1
  
  g"
      [tile]
         pos=1
         image=bar-s-n
      [/tile]
  [/terrain_graphics]
  [terrain_graphics]
      map="
    1
  g"
      [tile]
         pos=1
         image=bar-sw-ne
      [/tile]
  [/terrain_graphics]
  [terrain_graphics]
      map="
  g
    1"
      [tile]
         pos=1
         image=bar-nw-se
      [/tile]
  [/terrain_graphics]
  [terrain_graphics]
      map="
    g

    1"
      [tile]
         pos=1
         image=bar-n-s
      [/tile]
  [/terrain_graphics]
  [terrain_graphics]
      map="
    g
  1"
      [tile]
         pos=1
         image=bar-ne-sw
      [/tile]
  [/terrain_graphics]

.. [*] All angles will here be expressed in radians.

Animating images
----------------

Images may may be animated instead of being static. To do this, specify a list
of comma-separated images in the ``name`` element of the ``image`` tag. This
will generate an animation, each frame being displayed during 100ms.

The duration of each frame may be specified, to have a different value than the
default 100 ms, by adding, after the image name, a colon (:), followed by a
number representing a time in milliseconds.

For example, take the following declaration::

  [image]
     name=frame1,frame2,frame3:300,frame4:200,frame5
  [/image]

It will define an animation composed of the following 5 frames:

Image  Duration
====== ========
frame1 100 ms
frame2 100 ms
frame3 300 ms
frame4 200 ms
frame5 100 ms

Time-of-day-specific variants of images
---------------------------------------

It is possible, for images, to have several variants; the actual variant
displayed being selected according to the current time-of-day. The notation
introduced above, using the ``name`` attribute to define the image used,
actually defines the default variant of the image; that is, the variant that
will be used, either if there is no time-of-day (for example, in the editor,)
or if the current time-of-day is not specified in another variant.

Variants may be defined by adding the [variant] child tag to the [image] tag.
[variant] child tags have 2 elements:

* The ``tod`` elements which specifies the time-of-day this variant applies to
  (see the file data/schedules.cfg for the list of times-of-day.
* The ``name`` element which has the same exact meaning as the ``name`` element
  of the [image] tag (and may, for example, carry animations etc), which will
  be used in place of the default ``name`` when the time-of-day matches.

For example, the following WML code specifies a village which has smoke when it
is the night::

  [terrain_graphics]
     [tile]
        x=0
        y=0
        type=t
        [image]
           name=village
           [variant]
              tod=first_watch
              name=village-dusk,village-dusk2,village-dusk3,village-dusk4
           [/variant]
           [variant]
              tod=second_watch
              name=village-dusk,village-dusk2,village-dusk3,village-dusk4
           [/variant]
        [/image]
     [/tile]
  [/terrain_graphics]

Using macros
------------

Macros for base terrains
~~~~~~~~~~~~~~~~~~~~~~~~

Macros for adjacent terrains
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Macros for castles
~~~~~~~~~~~~~~~~~

Macros for canyons
~~~~~~~~~~~~~~~~~~

Macros for bridges
~~~~~~~~~~~~~~~~~~

Reference documentation
=======================

Rule structure synopsis
-----------------------

::
  
  +--------------------------+
  | Rule                     |
  |  +--------------------+  |
  |  | Constraint         |  |
  |  |                    |  |
  |  | * offset           |  |
  |  | * typestring       |  |
  |  | * has_flags        |  |
  |  | * set_flags        |  |
  |  | * no_flags         |  |
  |  |                    |  |
  |  |  +--------------+  |  |
  |  |  | Image        |  |  |
  |  |  +--------------+  |  |
  |  |  | Image        |  |  |
  |  |  | ...          |  |  |
  |  |  +--------------+  |  |
  |  +--------------------+  |
  |  | Constraint         |  |
  |  | ...                |  |
  |  +--------------------+  |
  |                          |
  | * position               |
  | * probability            |
  | * precedence             |
  |                          |
  |  +--------------+        | 
  |  | Image        |        |
  |  +--------------+        |
  |  | Image        |        |
  |  | ...          |        |
  |  +--------------+        |
  +--------------------------+

Rule matching algorithm
-----------------------

Each rule will be tested against each hex of the map. For a rule to match on a
given hex (let name this hex H), the following conditions have to be met:

* Some random, 1 to 100 number must be inferior to the rule "probability"
* If the rule has a position set, it may only match on this very location.
* All constraints of the rule must match.

For a constraint of the rule to match, the following conditions have to be met:

* The hex corresponding to this constraint must have a type which matches the
  constraint's typestring:

  + We define the "hex corresponding to this constraint" as the hex, on the
    map, whose location is the hex H + ofs, ofs being the offset of the
    constraint.
  + The hex matches the constraint's typestring if any of those is true.

    - The typestring contains the metacharacter \*.
    - The typestring does not start with the character '!', and the hex's
      terrain character is included in the typestring.
    - The typestring starts with the character '!', and the hex's terrain
      character is *not* included in the typestring.

* The hex corresponding to this constraint must not have any flag in the
  constraint's "no_flag" list.
* The hex corresponding to this contraint must have all the flags present in
  the constraint's "has_flag" list.

WML Reference
=============

[terrain_graphics]
------------------

The [terrain_graphics] tag represents a terrain graphics rule. It may contain
the following child tags:

`[image]`_
    when an image is defined in a [terrain_graphics] tag, it defines a
    multi-hex image which will be applied over all tiles of the rule.

`[tile]`_
    adds one (or several) constraints to the rule.

Additionnaly, the [terrain_graphics] tag may have the following elements:

``x`` and ``y``
    format: <number>

    Specifies the coordinates at which this rule can match. A rule which has
    x-y coordinates may only match at this position in the map, and nowhere
    else.

``probability``
    format: <number> 

    A number from 0 to 100. Means that this rule will only match, when all
    other conditions are met, if a random number from 0 to 100 is inferior to
    the ``probability`` value. Obviously, 0 means this rule will never match,
    and 100 means this rule will always match if all other conditions are met.

``precedence``
    format: <number>

    An optional tag which allows to specify in which order rules are to be
    tested. Generally, rules are tested in the order they are defined. However,
    rules with a lower precedence will always de tested before rules with
    higher precedence.

``map``
    format: see below

    A string, generally a multi-line one, graphically representing the
    constraints of this rule. Maps are a shorthand notation to defining several
    constraints using the `[tile]`_ element. Those have a special structure; see
    below (`Map Format`_.)

``set_flag``
    Defining a ``set_flag`` element in a rule is identical to defining it on
    each constraint of this rule.

``has_flag``
    Defining a ``has_flag`` element in a rule is identical to defining it on
    each constraint of this rule.

``no_flag``
    Defining a ``no_flag`` element in a rule is identical to defining it on
    each constraint of this rule.

``rotations``
    format: <r0> "," <r1> "," <r2> "," <r3> "," <r4> "," <r5>

    <r0> to <r5> being (usually short) strings.

    Specifies that this [terrain_graphics] element does not define an actual
    rule, but will serve as a template for creating up to 6 rotated rules.

    Template rules are defined like normal rules, except that flags and image
    filenames may contain template strings of the form ``@Rn``, n being a
    number from 0 to 5.
   
    A template rule will generate 6 rules, which are similar to the
    template, except that:
   
    * The map of constraints of this rule will be rotated by an angle, of 0 to
      5 pi / 6
   
    * On the rule which is rotated to 0rad, the template strings @R0, @R1, @R2,
      @R3, @R4, @R5, will be replaced by the corresponding r0, r1, r2, r3, r4,
      r5 variables given in the rotations= element.
   
    * On the rule which is rotated to pi/3 rad, the template strings @R0, @R1,
      @R2 etc. will be replaced by the corresponding *r1, r2, r3, r4,
      r5, r0* (note the shift in indices).
   
    * On the rule rotated 2pi/3, those will be replaced by r2, r3, r4, r5, r0,
      r1 and so on.

[tile]
------

The [tile] element, in a [terrain_graphics] rule, adds one (or more) new
constraints to a rule. It may contain the following child tags:

`[image]`_
    Defining an [image] element inside of a [tile] element will define a
    single-hex image which will only be applied to the tile the constraint
    applies to.

Additionally, the [tile] tag may contain the following elements:

``x`` and ``y``
    format: <number>

    Specify the offset of the constraint.

``loc``
    format: <number>, <number>

    An alternative notation for specifying the offset of the constraint.

``pos``
    format: <number>

    Specifies that this [tile] tag does not define a single constraint, but
    instead, acts as a template for all constraints defined, on the map, with
    an anchor of the same number (See `Map format`_.)

    Only meaningful if the [terrain_graphics] parent tag contains a ``map``
    element.

``type``
    format: <string>

    Defines the typestring for this constraint. This value represents a list of
    characters. For the constraint to match, the corresponding terrain tile's
    type must be one of those characters.

    This string may contain the metacharacter "*" meaning "all terrains", and
    the metacharacter "!", meaning "all terrains except those present in the
    list."

``set_flag``
    format: <flag> [ "," <flag> ] +

    Specifies that, if the rule which contains this constraint matches, the
    given flags will be applied to the corresponding terrain tile.

``has_flag``
    format: <flag> [ "," <flag> ] +

    Specifies that this constraint will only match if the corresponding terrain
    tile already has all the given flags.

``no_flag``
    format: <flag> [ "," <flag> ] +

    Specifies that this constraint will only match if the corresponding terrain
    tile does *not* have any of the given flags.

[image]
-------

The [image] element, in the [terrain_graphics] element, or in a [tile]
elements, specify an image which will be added on the terrain, if the
corresponding rule does match.

It may contain the following child tags:

`[variant]`_
    A time-of-day specific variant of the image.

Images may contain the following elements:

``name``
    format: <timed_image> ( "," <timed_image> ) +

    <timed_image> ::= <image_name> [ ":" <timing> ]

    If the name only contains one timed_image, it will be used as a base to
    build the filename of the image corresponding to this [image] tag, with
    "images/terrain/" prepended, and ".png" appended.

    If the name contains several timed_images, it will correspond to an
    animated image, each timed_image being a frame of the animation. For each
    frame of the animation the <image_name> part corresponds to the base of the
    filename, which will be built as shown above, and the <timing> part will
    correspond to the duration, in milliseconds, of this frame.

``position``
    format: "horizontal" | "vertical"

    The type of layering this image will use. If set to "horizontal", it will
    use a layer-based stack model. If set to vertical, images will be assumed
    to have an (x,y) position on the screen, and will be layered according to
    their coordinates.

``layer``
    format: <number>    

    Only meaningful if the ``position`` tag was set to ``horizontal``. Images
    with an horizontal position will be drawn, lower layer to upper layer,
    without taking their position into account.

``base``
    format: <number> "," <number>

    Only meaningful if the ``position`` tag was set to ``vertical``. Specifies
    the coordinates of the "base" of the image, which is, the imaginary pixel
    at which the image reaches the "floor", relative either to the top-left
    corner of the rule, or to the top-left corner of the constraint hex,
    depending on whether the image applies to a rule, or to a constraint.

[variant]
---------

[variant] tags represent a time-of-day-specific version of an image. Variants
may contain the following elements:

``tod``
    format: <string>

    The identifier of the time-of-day this variant applies to. When the turn's
    top is equal to this, the "name" element of this variant will replace the
    "name" element of the parent image.

``name``
    format: <timed_image> ( "," <timed_image> ) +

    <timed_image> ::= <image_name> [ ":" <timing> ]

    The image string, which will replace the "name" element of the parent image
    on the right time-of-day.

Map format
----------


