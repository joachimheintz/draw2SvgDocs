# draw2Svg Manual

*This is fork to drawSvg, in which we try to readjust its coordinate system to follow SVG standard*

A Python 3 library for programmatically generating SVG images (vector drawings) and rendering them or displaying them in a Jupyter notebook.

Most common SVG tags are supported and others can easily be added by writing a small subclass of `DrawableBasicElement` or `DrawableParentElement`.

An interactive [Jupyter notebook](https://jupyter.org) widget, `drawSvg.widgets.DrawingWidget`, is included that can update drawings based on mouse events.


## Initialization

### Install and Call
*This isn't work yet, we're still not on PyPI*
Install with `pip install draw2Svg` on command line, after that import to your project with `import`.
Initiate a drawing instance with `draw.Drawing(WIDTH,HEIGHT)`


```python
import draw2Svg as draw

d = draw.Drawing(400, 300)
```

## Prerequisites

Cairo needs to be installed separately. When Cairo is installed, drawSvg can output PNG or other image formats in addition to SVG. See platform-specific [instructions for Linux, Windows, and macOS from Cairo](https://www.cairographics.org/download/). Below are some examples for installing Cairo on Linux distributions and macOS.

**Ubuntu**

```
$ sudo apt-get install libcairo2
```

**macOS**

Using [homebrew](https://brew.sh/):

```
$ brew install cairo
```
