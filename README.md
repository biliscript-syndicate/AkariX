AkariX
======

*As of 2015/3/4, development of this library is on halt indefinitely.* The code was written during mid Oct. ~ Nov. 2013 in private, and then put aside for apparent performance and usability problems. It is made public solely for sake of history (and in case that someone, though very unlikely, might find it somehow useful). It's not polished and performant enough for use in works facing the public.

All that follows are out of date. Read [my blog post on this](https://blog.a-kar.in/legacy-mode8-projects) (in Chinese) for more information.

> akari / noun.
>
> 1. light; illumination; glow; gleam;
> 2. lamp; light

AkariX is a scripting MG framework intended to work with bilibili Flash Player. AkariX is derived from Akari.biliScript in an attempt at improving abstraction and versatility, allowing users more freedom from the inner quirks of the player, and eventually better flow of ideas.

As the 'X' implies, AkariX is designed to provide an interface that is implementation independent. With proper implementation, a same piece of user code can be shared between backends while yielding the same result. This enables the development of better design and debug tools, consequently eliminating the need of dwelling into the depths of bilibili Flash Player in person.

Status
------

*As of 2015/3/4, development of this library is on halt indefinitely.* All that follows are out of date.

* Specifications `\specs`

    Architectural choices specific to reference implementations.

    * Level 0

        Level 0 represents the very minimum level of features needed for compositing any non-trivial motion graphic.

        Level 0 covers basic signal manipulation: thresholding, channel separating, merging and blurring; rendering vector graphics; and interpolating between values of interest.

* Samples `\samples`

    Not planned yet.

* Implementations `\impls`

    * biliScript - Implemented API Level 0 except depth sorting. Designated use: Primary realtime presentation

    * C# / Direct2D & WIC - Planned. Designated use: Design tool backend, High quality offline rendering

License
-------

For all source code in this repo:

> This program is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.
> 
> This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU General Public License for more details.
> 
> As additional permission under GNU GPL version 3 section 7, you may distribute non-source (e.g., minimized or compacted) forms of that code without the copy of the GNU GPL normally required by section 4, provided you include this license notice and a URL through which recipients can access the Corresponding Source.
