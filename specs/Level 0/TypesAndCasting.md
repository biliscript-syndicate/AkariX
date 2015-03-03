Types
=====

Brush
-----

* width : Number

    Considered when used as a stroke.

* caps : String

    Defaults to `round`. Considered when used as a stroke.

    * `none`
    * `round`
    * `square`

* joints : String

    Defaults to `round`. Considered when used as a stroke.

    * `bevel`
    * `miter`
    * `round`

* miterLimit : Number

    Considered when used as a stroke and `joints` equal `miter`. Indicates the limit at which a miter is cut off. Defaults to 3.

* type : string

    * `none`

        Indicates no fill or stroke.

    * `flat`

        Indicates solid or gradient fill as dictated by the `colors` field.

    * `texture`

        Indicates flat fill with texture data.

* texture : Signal

    Considered when `type` equals `texture`.

* colors : Vector<Color>

    When `type` equals `flat`: If the Vector has only one member, solid fill. Otherwise a gradient fill.

    When `type` equals `texture`: The first member is used as a tint color (multiplication) for the texture.

* ratios : Vector<Number>

    Considered when `type` equals `flat` and length of `colors` larger than 1. Position of stops in the gradient. Numbers correspond to colors and reside in the range 0~1.

* spreadMethod : string

    Considered when `type` equals `flat` or `texture`.

    * `pad`

        Repeat edge pixels when out of range.

    * `repeat`

        Repeat the pattern when out of range.

    * `reflect`

        Reflect the pattern when out of range.

* matrix : Matrix

    Considered when `type` equals `flat` or `texture`. Transforms the gradiant or texture before applying.

* polar : bool

    Indicates a radial gradient.

* focalPointRatio : Number

    Offsets gradient center when `polar` is `true`. -1~1 range.

Transform
---------

* position : Vector<Number>

    3-dimensional translation.

* anchor : Vector<Number>

    3-dimensional anchor point.

* rotation : Vector<Number>

    3-dimensional rotation in radians.

* scale : Vector<Number>

    3-dimensional scale. 1.0 being the original scale.

Drawable
--------

A Drawable is an array of the following struct:

* type : String

    Determines the type of the primitive.

    * `Signal`

        `vertices` is ignored. `fill` should be of type `signal`, which will get layered on existing content. `transform` is ignored with this kind of primitive.

    * `Polyline`

        n-dimensional polyline. `vertices` is Vector<Vector<Number>>. Dimension decided by the first vertex's length.

    * `Spline`

        n-dimensional spline. `vertices` is Vector<Vector<Vector<Number>>>. Each member of `vertices` is a segment, each member of a segment is a vertex. Segment degree decided by its length. Dimension decided by the first segment's first vertex's length.

* blend : String

    Blend mode of the primitive. Defaults to `normal`.

    * `normal`
    * `alpha`
    * `add`
    * `darken`
    * `difference`
    * `erase`
    * `hardlight`
    * `invert`
    * `lighten`
    * `multiply`
    * `overlay`
    * `screen`
    * `subtract`

* vertices : Vector<*>

* fill : Brush

* stroke : Brush

* transform : Transform

    Extra transformation performed on the primitive. Can be nulled indicating no transformation.

Casting
=======

Casting rules are as follows:

To Any
------

No cast is needed from any type.

To Signal
---------

Cast is prohibited from any other type.

To Drawable
-----------

Cast is possible from Vector provided that it passes sanity check.

To Brush
--------

Cast is prohibited from any other type.

To Boolean
----------

* From `false` or `null` or `undefined`

    False.

* Otherwise

    True.

To Hash
-------

* From Brush

    No casting needed.

* From Boolean, String, Number, Color, Vector, Drawable, Matrix, Signal or Any

    Casting prohibited.

To Color
--------

* From Number

    Treats the number as a 32-bit hardware color.

* From Vector

    No cast needed if the Vecntor is a sane Color representation.

* Others

    Casting prohibited.

To Number
---------

* From String

    * String is a representation of a number

        Number corresponding to the string.

    * Otherwise

        Length of the string.

* From Vector, Drawable or Hash

    Count of members of the Vector or Hash.

* From Color

    Hardware color value (0xAARRGGBB) of the Color.

* From Boolean, Matrix, Signal, Brush or Any

    0.

To String
---------

* From Number

    Decimal representation of the number.

* From Boolean

    `true` or `false`.

* From Color

    Values of each component printed as human readable.

* From Vector, Drawable or Matrix

    Members cast to String, separated by `, ` and encapsulated by a pair of `[]`.

* From Hash or Brush

    Members cast to String, keys and values separated by ` : `, pairs separated by `, ` and encapsulated by a pair of `{}`.

* From Signal or Any

    Type String.

To Vector
---------

* From Number

    Vector with only one member being the number.

* From String

    Vector containing char codes from the string.

* From Hash

    Vector of key / value pairs from the Hash.

* From Matrix or Drawable

    No cast needed.

* From Color

    Vector from the second element through the last.

* From Boolean, Brush, Signal or Any.

    Vector with only one member being the object.

