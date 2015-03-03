API Layer
=========

The API layer defines a set of API that should be implemented by Implementation Layer. It consists of following interfaces.

IPresentationNode
-----------------

Type name "Presentation". `IPresentationNode` provide various information about the presentation environment.

* Input Fields

    * aspectRatio : Number

        The aspect ratio used to calculate optimal resolution.

    * maxHeight : Number

        Indicated max resolution that can be used combined with aspect ratio.

    * nominalHeight : Number

        This is used to calculate the global scale parameter visible to nodes internally. Nodes should use the global scale only when dealing with Signals.

* Output Fields

    * time : Number

        The current time on master timeline, in milliseconds.

    * width : Number

        The current optimal width, in pixels.

    * height : Number

        The current optimal height, in pixels.

    * stageWidth : Number

        The current stage width, in pixels.

    * stageHeight : Number

        The current stage height, in pixels.

IOutputNode
-----------

Type name "Output". When evaluated, outputs the signal passed in. Only `IOutputNode`s and `IDebugOutputNode`s can be used as entry points.

* Input Fields

    * signal : Signal

IDebugOutputNode
----------------

Type name "DebugOutput". When evaluated, beside the signal passed in, prints the value of `message` along with other implementation specific debug data to any debug output avaliable.

* Input Fields

    * signal : Signal
    * message : String

IValueNode
----------

Type name "Value". When evaluated, copies value of input `value` to output, optionally as a specific type.

* Input Fields

    * value : Any
    * as : String
    * cached : Boolean

        When `cached` is true, the Node will fetch input only when it is evaluated the first time.

* Output Fields

    * value : Any

IConcatNode
-----------

Type name "Concat". If `value` is a Vector, concats the two Vectors. Otherwise push `value` to the end of `base`.

* Input Fields

    * base : Vector
    * value : Any

* Output Fields

    * value : Vector

IHashNode
---------

Type name "Hash". When evaluated, converts input fields to a Hash.

* Input Fields

    * keys : Vector
    * values : Vector

* Output Fields

    * value : Hash

IRendererNode
------------

Type name "Renderer". When evaluated, renders a Drawable to a Signal.

* Input Fields

    * width : Number
    * height : Number
    * content : Drawable
    * world : Matrix
    * projection : Matrix
    * cached : Boolean

        When `cached` is true, the Node will re-render only when it is evaluated the first time, or when the dimensions changed.

* Output Fields

    * output : Signal

ISolidNode
----------

Type name "Solid". When evaluated, outputs a solid Signal with set color and size.

* Input Fields

    * width : Number
    * height : Number
    * color : Color

* Output Fields

    * output : Signal

ICheckerNode
------------

Type name "Checker". When evaluated, outputs a checkerboard Primitive to an optional Drawable with set color, frequency and size.

* Input Fields

    * width : Number
    * height : Number
    * color1 : Color
    * color2 : Color
    * frequencyX : Number
    * frequencyY : Number
    * base : Drawable

* Output Fields

    * output : Drawable

IPrimitiveNode
--------------

Type name "Primitive". When evaluated, outputs an user defined Primitive to an optional Drawable.

* Input Fields

    * base : Drawable
    * type : String
    * blend : String
    * vertices : Vector
    * fill : Brush
    * stroke : Brush
    * transform : Transform

* Output Fields

    * output : Drawable

IBrushNode
----------

Type name "Brush". When evaluated, outputs an user defined Brush.

* Input Fields

    * width : Number
    * caps : String
    * joint : String
    * miterLimit : Number
    * type : String
    * texture : Signal
    * colors : Vector
    * ratios : Vector
    * spreadMethod : String
    * matrix : Matrix
    * polar : Boolean
    * focalPointRatio : Number

* Output Fields

    * output : Brush

ITransformNode
--------------

Type name "Transform". When evaluated, outputs an user defined Transform.

* Input Fields

    * anchor : Vector
    * rotation : Vector
    * scale : Vector
    * position : Vector

* Output Fields

    * output : Transform

IKeyframesNode
--------------

Type name "Keyframes". Interpolation is possible between Numbers, Colors, Brushes, Vector<Number>s (`as` `Vector`), Transforms, Splines (`as` `Spline`) and Primitives (`type` `Polyline` or `Spline`). The type should be specified through the parameter `as`. A 2-dimensional Spline is used to control both spacial and temporal aspects.

* Input Fields

    * keyframes : Spline
    * as : String
    * time : Number
    * cacheSpline : Boolean

        When `true`, fetches the keyframes Spline only once.

* Output Fields

    * value : Any

IChannelSplitNode
-----------------

Type name "ChannelSplit".

* Input Fields

    * signal : Signal

* Output Fields

    * alpha : Signal
    * red : Signal
    * green : Signal
    * blue : Signal

IChannelMergeNode
-----------------

Type name "ChannelMerge".

* Input Fields

    * base : Signal
    * alpha : Signal
    * red : Signal
    * green : Signal
    * blue : Signal

* Output Fields

    * output : Signal

IMergeNode
----------

Type name "Merge". Blends two Signals with a certain blend mode. The sizes must match.

* Input Fields

    * signalA : Signal
    * signalB : Signal
    * blend : String
    * alpha : Number

        Controls the alpha of `signalB`.

* Output Fields

    * output : Signal

IThresholdNode
--------------

Type name "Threshold". Performs thresholding on a Signal.

* Input Fields

    * signal : Signal
    * threshold : Color
    * inverse : Boolean

        When `true`, a low pass threshold filter.

    * separate : Boolean

        When `true`, channels are tested separately. Otherwise a pixel is preserved only if it satisfied the threshold in all channels.

* Output Fields

    * output : Signal

IBoxBlurNode
------------

Type name "BoxBlur". Performs a box blur of a certain iteration on given signal. When `iterations` equals `3`, the filter approximates a Gaussian blur.

* Input Fields

    * signal : Signal
    * radiusX : Number
    * radiusY : Number
    * iterations : Number

* Output Fields

    * output : Signal