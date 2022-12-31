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

### One Line

```
dw.Line(sx, sy, dx, ey, **kwargs)
```
```python
line = dw.Line(30,30,90,90,stroke='black')
d.append(line)
```

### Multiple Lines

This is SVG's `polyline`. 
(But draw2Svg renders as path with multiple L.)

```
dw.Lines(sx, sy, *points, close=False, **kwargs)
```

```python
lines = dw.Lines(15,10,55,10,45,20,5,20,fill='none',stroke='black')
```

```python
x = [30+x*10 for x in range(20)]
y = [80,20]*10
xy = [item for sublist in zip(x,y) for item in sublist]
d.append(dw.Lines(*xy,stroke='black',stroke_width=5,fill='none'))
```

### Polygon

SVG `Polygon` is `Lines` with `close=True`.

```python
polygon = dw.Lines(15,10,55,10,45,20,5,20,fill='red',stroke='black',close='true')
star = dw.Lines(48,16, 16,96, 96,48, 0,48, 88,96,
         stroke='black',fill='none',close='true')
```


### Rectangle

```
dw.Rectangle(x, y, width, height, **kwargs)
```
```python
# black interior, no outline
d.append(dw.Rectangle(10,10,90,150))
# no interior, black outline
d.append(dw.Rectangle(120,10,60,120,fill='none',stroke='black'))
# blue interior, thick semi-transparent red outline
d.append(dw.Rectangle(210,10,75,90,fill='#0000ff',stroke='red',
                      stroke_width=7,stroke_opacity=0.5))
# semi-transparent yellow interior, dashed green outline
d.append(dw.Rectangle(300,10,105,60,fill='yellow',fill_opacity=0.5,
                      stroke='green',stroke_width=2,stroke_dasharray='5,2'))
```

Rounded corners:

```python
# define both rx and ry
d.append(dw.Rectangle(10,10,80,180,rx='10',ry='10',stroke='black',fill='none'))
# if only one is given, it applies to both
d.append(dw.Rectangle(110,10,80,180,ry='20',stroke='black',fill='none'))
d.append(dw.Rectangle(210,10,80,180,rx='40',stroke='black',fill='none'))
# rx and ry unequal
d.append(dw.Rectangle(310,10,80,180,rx='30',ry='10',stroke='black',fill='none'))
d.append(dw.Rectangle(410,10,80,180,rx='10',ry='30',stroke='black',fill='none'))
```


### Circle
```
dw.Circle(cx, cy, r, **kwargs)
```
cx and cy point to circle's center, r refer to its radius

```python
d.append(dw.Circle(50,50,40))
d.append(dw.Circle(150,50,40,stroke='black',fill='none'))
d.append(dw.Circle(250,50,40,stroke='black',fill='none',stroke_width=15))
```


### Ellipse
```
dw.Ellipse(cx, cy, rx, ry, **kwarg)
```
(cx,cy) points to the center and (rx,ry) tells its radius

```python
d.append(dw.Ellipse(350,50,50,30))
d.append(dw.Ellipse(460,50,50,30,stroke='black',fill='none'))
d.append(dw.Ellipse(550,50,30,45,stroke='black',fill='none'))
```


### Pie

```
dw.Pie(cx, cy, r, startDeg, endDeg, **kwargs)
```

```python
pie = draw.Pie(cx=200, cy=150, r=100, startDeg=0, endDeg=90, fill= "None", stroke="pink")
```


## Color and Paining Properties

(For a full list, see [W3C specifications](https://www.w3.org/TR/SVG11/styling.html).


### fill and stroke_color

Possible color keyword names are: aqua , black , blue , fuchsia , gray , green ,
lime , maroon , navy , olive , purple , red , silver , teal , white, and yellow.

Or #rrggbb, or #rgb (hexadecimal) or rgb(R,G,B) with 0-255 or with 0-100% for each value.

```python
c = ['red', '#9f9', '#9999ff', 'rgb(255,128,64)', 'rgb(60%,20%,60%)']
for i in range(5):
    y = (i+1)*10
    d.append(dw.Line(10,y,80,y,stroke=c[i],stroke_width=5))
```

### fill_opacity and stroke_opacity 

0 = transparent, 1 = solid.

```python
for i in range(5):
    y = (i+1)*10
    d.append(dw.Line(10,y,80,y,stroke='black',stroke_width=5,stroke_opacity=i/5+0.2))
```


### stroke_dasharray

```python
# nine-pixel dash, five-pixel gap
d.append(dw.Line(10,40,100,40,stroke_dasharray='9,5',stroke='black',stroke_width=2))
# five-pixel dash, three-pixel gap, nine-pixel dash, two-pixel gap
d.append(dw.Line(10,30,100,30,stroke_dasharray='5,3,9,2',stroke='black',stroke_width=2))
# Odd number of entries is duplicated
d.append(dw.Line(10,20,100,20,stroke_dasharray='9,3,5',stroke='black',stroke_width=2))
```


### stroke_width

```python
for i in range(20):
    d.append(dw.Line((i+1)*15,10,(i+1)*15,90,stroke='black',stroke_width=abs(10-i)+1))
```

### stroke_linecap

`stroke_linecap` can be set to `butt , round`, or `square`. 
Note that the latter two extend beyond the coordinates.

```python
d.append(dw.Line(10,15,50,15,stroke='black',stroke_linecap='butt',stroke_width=15))
d.append(dw.Line(10,45,50,45,stroke='black',stroke_linecap='round',stroke_width=15))
d.append(dw.Line(10,75,50,75,stroke='black',stroke_linecap='square',stroke_width=15))
# guide lines
d.append(dw.Lines(10,0,10,100,stroke='#999'))
d.append(dw.Lines(50,0,50,100,stroke='#999'))
```


### stroke_linejoin

Define the way lines connect at a corner with `stroke-linejoin`: `miter` (pointed),
`round`, or `bevel` (flat).

```python
d.append(dw.Line(0,20,300,20,stroke='gray'))
g = dw.Group(stroke_width=20,stroke='black',fill='none')
g.append(dw.Lines(10,80,50,20,90,80,stroke_linejoin='miter'))
g.append(dw.Lines(110,80,150,20,190,80,stroke_linejoin='round'))
g.append(dw.Lines(210,80,250,20,290,80,stroke_linejoin='bevel'))
d.append(g)
```

### stroke_miterlimit

When two line segments meet at a sharp angle and miter joins have been specified 
for `stroke-linejoin`, it is possible for the miter to extend far beyond the 
thickness of the line stroking the path. The `stroke-miterlimit` imposes a 
limit on the ratio of the miter length to the `stroke-width`. 
When the limit is exceeded, the join is converted from a miter to a bevel.
(From [W3C doc](https://www.w3.org/TR/SVG11/painting.html#StrokeMiterlimitProperty))

```python
d.append(dw.Line(0,30,300,30,stroke='gray'))
g = dw.Group(stroke_width=20,stroke='black',fill='none',stroke_linejoin='miter')
g.append(dw.Lines(10,90,40,30,70,90))
g.append(dw.Lines(100,90,130,30,160,90,stroke_miterlimit=2.3)) #jumps between 2.2 and 2.3
g.append(dw.Lines(190,90,220,30,250,90,stroke_miterlimit=1))
d.append(g)
```


## Path
```
path = dw.Path(**kwargs)
```
The following Path specifiers are also availiable as lowercase characters. In
that case, their movements are relative to current location.

Note that in `draw2Svg` it is not possible to have more than one element in a
command. But it is possible to add the commands directly, for instance

```python
p = dw.Path()
p.M(100,100).L(200,100).L(200,200).Z
```

### M = moveto

```
path.M(x,y)
```
Move to `x,y` (and draw nothing).


### L = lineto

```
path.L(x,y)
```

Draw a straigt line to `x,y`.

```python
g = dw.Group(stroke='black',fill='none')

p = dw.Path()
p.M(10,10).L(100,10)
g.append(p)

p = dw.Path()
p.M(10,20).L(100,20).L(100,50)
g.append(p)

p = dw.Path()
p.M(40,60).L(10,60).L(40,42)
p.M(60,60).L(90,60).L(60,42)
g.append(p)
```

### H = horizontal line

```
path.H(x)
```

Draw a horizontal line to the new `x` location.


### V = vertical line

```
path.V(x)
```

Draw a vertical line to the new `y` location.

```python
g = dw.Group(stroke='black',fill='none')

p = dw.Path()
p.M(10,10).H(100)
g.append(p)

p = dw.Path()
p.M(10,20).H(100).V(50)
g.append(p)
```


### Q = quadratic Bézier curve (one control point)

```
path.Q(x_ctl,y_ctl,x_end,y_end)
```

Draw a quadratic Bézier curve from current location to `x_end,y_end` by means
of `x_ctl,y_ctl`.

```python
# curve only (left)
p = dw.Path(stroke='black',fill='none',stroke_width=3)
d.append(p.M(30,75).Q(240,30,300,120))
# with control point and construction lines
d.append(dw.Use(p,300,0))
g = dw.Group(stroke='gray',fill='gray')
g.append(dw.Circle(330,75,3))
g.append(dw.Circle(600,120,3))
g.append(dw.Circle(540,30,3))
g.append(dw.Line(330,75,540,30))
g.append(dw.Line(540,30,600,120))
g.append(dw.Line(330,75,600,120,stroke_dasharray='5,5'))
g.append(dw.Circle(435,52.5,3))
g.append(dw.Circle(570,75,3))
g.append(dw.Line(435,52.5,570,75))
g.append(dw.Circle(502.5,63.75,4,fill='none'))
d.append(g)
```


### T = smooth quadratic Bézier curve (generated control point)

```
path.T(x,y)
```

Draws a quadratic Bézier curve from the current point to (x,y). The control 
point is assumed to be the reflection of the control point on the previous 
command relative to the current point. (If there is no previous command or if 
the previous command was not a Q, q, T or t, assume the control point is 
coincident with the current point.) (From [W3C Doc](https://www.w3.org/TR/SVG11/paths.html#PathDataQuadraticBezierCommands))

```python
# sequence left
p = dw.Path(stroke='black',fill='none',stroke_width=3)
d.append(p.M(30,60).Q(80,-10,100,60).Q(130,25,200,40))
# with smooth continuation right
p = dw.Path(stroke='black',fill='none',stroke_width=3,transform='translate(200,0)')
d.append(p.M(30,60).Q(80,-10,100,60).T(200,40))
```


### C = cubic Bézier curve (two control points)

```
path.C(x_ctl_1,y_ctl_1,x_ctl_2,y_ctl_2,x_end,y_end)
```

Draw a cubic Bézier curve by means of two control points (one for start and
one for end).

```python
pnt_1 = (40,50)
pnt_2 = (110,50)
ctl_1_x = (10,60,110,110,60,110)
ctls_2 = ((140,10),(90,10),(40,10),(40,10),(90,90),(40,90))

for i in range(6):
    trans = 'translate(%d,0)' % i*100
    p = dw.Path(stroke='black',fill='none',stroke_width=3,transform=trans)
    ctl_1 = (ctl_1_x[i],10)
    ctl_2 = ctls_2[i]
    p.M(*pnt_1)
    p.C(*ctl_1,*ctl_2,*pnt_2)
    d.append(p)
    g = dw.Group(stroke='gray',fill='gray',stroke_width=1,transform=trans)
    g.append(dw.Circle(*ctl_1,2))
    g.append(dw.Circle(*ctl_2,2))
    g.append(dw.Line(*pnt_1,*ctl_1))
    g.append(dw.Line(*pnt_2,*ctl_2))
    d.append(g)
```


### S = smooth cubic Bézier (one control point)

Similar to `T` in quadratic Bézier curve. The first control point is calculated 
as reflection of the previous second control point.

```
path.S(x_ctl_2,y_ctl_2,x_end,y_end)
```

```python
pnt_1 = (30,100)
pnt_2 = (100,100)
pnt_3 = (200,80)
ctl_1 = (50,30)
ctl_2 = (70,50)
ctl_3 = (150,40)

p = dw.Path(stroke='black',fill='none',stroke_width=3)
p.M(*pnt_1)
p.C(*ctl_1,*ctl_2,*pnt_2)
p.S(*ctl_3,*pnt_3)
d.append(p)

for pnt,ctl in zip((pnt_1,pnt_2,pnt_3),(ctl_1,ctl_2,ctl_3)):
    d.append(dw.Circle(*pnt,4))
    d.append(dw.Circle(*ctl,2,stroke='gray',fill='gray'))
    d.append(dw.Line(*pnt,*ctl,stroke='gray'))
```

  
### A = elliptical Arc

```
path.A(rx,ry,rot,largeArc,sweep,ex,ey)
	rx,ry = radius 
	rot = x-axis rotation
	largeArc = 1 or 0
	sweep = 1 (positive) or 0 (negative) angle
	ex,ey = end point
```

```python
p = dw.Path(stroke='red')
d.append(p.M(125,75).A(100,50,rot=0,largeArc=0,sweep=0,ex=225,ey=125))
p = dw.Path(stroke='blue')
d.append(p.M(125,75).A(100,50,rot=0,largeArc=0,sweep=1,ex=225,ey=125))
p = dw.Path(stroke='rgb(0 80 255)',stroke_dasharray='5 3')
d.append(p.M(125,75).A(100,50,rot=0,largeArc=1,sweep=0,ex=225,ey=125))
p = dw.Path(stroke='rgb(255 80 0)',stroke_dasharray='5 3')
d.append(p.M(125,75).A(100,50,rot=0,largeArc=1,sweep=1,ex=225,ey=125))
```



### Z = closepath  

```
path = Z()
```

Close the path.

```python
p = dw.Path(stroke='black',fill='none')
d.append(p.M(10,10).h(30).v(50).h(-30).Z())
d.append(p.M(50,10).h(30).v(50).Z())
```



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


## Issues and Questions


## TODO
- Insert images for the example code  
- How to know the possible `**kwargs` for the methods and also `**svgArgs` for dw.Drawing()
