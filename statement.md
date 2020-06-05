# Welcome!

This Python template lets you get started quickly with a simple one-page playground.

```python runnable
from PIL import Image, ImageDraw

MAX_ITER = 80

EPSILON = 0.001
   
def cubicbrot(c):
    z = c
    n = 0
    while (abs(z) <= 2 or abs(z-1) <= 2 or abs(z+1) <= 2) and n < MAX_ITER:
        f = (z*z*z)-z
        p = 3*z*z-1
        if abs(p) <= EPSILON:
            return MAX_ITER
        z = z - (f/p)
        if abs(z) <= EPSILON:
            return n
        if abs(z-1) <= EPSILON:
            return n
        if abs(z+1) <= EPSILON:
            return n
        n += 1
    return n

# Image size (pixels)
WIDTH = 600
HEIGHT = 400

# Plot window
RE_START = -2
RE_END = 1
IM_START = -1
IM_END = 1

palette = []

im = Image.new('RGB', (WIDTH, HEIGHT), (0, 0, 0))
draw = ImageDraw.Draw(im)

for x in range(0, WIDTH):
    for y in range(0, HEIGHT):
        # Convert pixel coordinate to complex number
        c = complex(RE_START + (x / WIDTH) * (RE_END - RE_START),
                    IM_START + (y / HEIGHT) * (IM_END - IM_START))
        # Compute the number of iterations
        m = cubicbrot(c)
        # The color depends on the number of iterations
        color = 255 - int(m * 255 / MAX_ITER)
        # Plot the point
        draw.point([x, y], (color, color, color))

im.save('output.png', 'PNG')

```

# Advanced usage

If you want a more complex example (external libraries, viewers...), use the [Advanced Python template](https://tech.io/select-repo/429)
