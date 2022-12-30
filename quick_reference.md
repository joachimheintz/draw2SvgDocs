# draw2Svg Quick Reference

Repository: [https://github.com/aufarah/draw2Svg](https://github.com/aufarah/draw2Svg)

Documentation: [https://draw2svg.netlify.app/](https://draw2svg.netlify.app/)

```
import draw2Svg as dw
```

## Canvas and Document Structure
```
d = dw.Drawing(width, height, origin=(0,0), idPrefix='d',
                 displayInline=True, **svgArgs)
```

It is recommended to use a unique `idPrefix` for each svg on a webpage.

```python
d = dw.Drawing(400, 300, idPrefix='pic')
```


## Basic Shapes

### Line, Lines and Polygon

```
dw.Line(sx, sy, dx, ey, **kwargs)
```
```python
line = dw.Line(30,30,90,90,stroke='black')
d.append(line)
```

```
dw.Lines(sx, sy, *points, close=False, **kwargs)
```

```python
lines = dw.Lines(15,10,55,10,45,20,5,20,fill='none',stroke='black')
```

Polygon is `Lines` with `close=True`.

```python
polygon = dw.Lines(15,10,55,10,45,20,5,20,fill='red',stroke='black',close='true')
star = dw.Lines(48,16, 16,96, 96,48, 0,48, 88,96,
         stroke='black',fill='none',close='true')
```



### Rectangle
```
dw.Rectangle(x, y, width, height, **kwargs)
```


### Circle
```
dw.Circle(cx, cy, r, **kwargs)
```
cx and cy point to circle's center, r refer to its radius


### Ellipse
```
dw.Ellipse(cx, cy, rx, ry, **kwarg)
```
(cx,cy) points to the center and (rx,ry) tells its radius


### Pie
```
dw.Pie(cx, cy, r, startDeg, endDeg, **kwargs)
```
(cx,cy) point to arc's center, startDeg to its initial angle and endDeg to its final angle



## Stroke Keywords

### stroke_width

### stroke_color

### stroke_opacity

### stroke_dasharray


## Path
```
path = dw.Path(**kwargs)
```


### Path datas (actually commands)

>The `<path>` element is used to define a path.  
>  
The following commands are available for path data:  
>  
M = moveto  
L = lineto  
H = horizontal lineto  
V = vertical lineto  
C = curveto  
S = smooth curveto  
Q = quadratic Bézier curve  
T = smooth quadratic Bézier curveto  
A = elliptical Arc  
Z = closepath  
>
Lowercase commands mean that their movements are relative to current location



## Text
```
dw.Text(text, fontSize, x=None, y=None, *, center=False,
           valign=None, lineHeight=1, lineOffset=0, path=None,
           startOffset=None, pathArgs=None, tspanArgs=None,
           cairoFix=True, _skipCheck=False, **kwargs)
```

### TSpan


## Gradient, Clip, Mask

### Linear Gradient
```
gradient = dw.LinearGradient(x1, y1, x2, y2, gradientUnits='userSpaceOnUse', **kwargs)
gradient.addStop(offset, color, opacity=None)
```


### Radial Gradient
```
gradient = dw.RadialGradient(cx, cy, r, **kwargs)
gradient.addStop(offset, color, opacity=None)
```

### Clip

Clip is an element that hold other elements inside it (such as path, rect, etc). No argument:

```
clip_name = dw.ClipPath()
```

To add shape as Clip, use `.append()` method.
To apply Clip, fill `clip_path` argument with `clip_name`.


### Mask
```
mask_name = dw.Mask()
```

To add shape as Clip, use `.append()` method.
To apply Clip, fill `mask` argument with `mask_name`.





## Group, Use etc

### Group
```
dw.Group(**kwargs)
```


## Transformations


