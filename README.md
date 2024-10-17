# Vector-based-images
We created vectors to produce Drosophila embryo, larval, head and testes images
Steps:
import matplotlib.pyplot as plt
from matplotlib.patches import Ellipse, Circle, Polygon, PathPatch
import matplotlib.patches as patches
import numpy as np
from matplotlib.path import Path

# Set up the plot
fig, ax = plt.subplots()

# Example 1: Simple ellipse with dots
ellipse = Ellipse((0.2, 0.8), width=0.2, height=0.4, edgecolor='black', facecolor='none')
ax.add_patch(ellipse)

# Adding dots inside the ellipse
dot_positions = [(0.18, 0.75), (0.22, 0.85), (0.24, 0.78), (0.20, 0.70)]
for pos in dot_positions:
    ax.add_patch(Circle(pos, 0.02, color='black'))

# Example 2: Detailed ellipse with circles inside the edge
ellipse2 = Ellipse((0.4, 0.8), width=0.2, height=0.4, edgecolor='black', facecolor='none')
ax.add_patch(ellipse2)

# Adding a series of circles around the edge
num_circles = 15
angles = np.linspace(0, 2 * np.pi, num_circles)
for angle in angles:
    x = 0.4 + 0.1 * np.cos(angle)
    y = 0.8 + 0.2 * np.sin(angle)
    ax.add_patch(Circle((x, y), 0.02, edgecolor='black', facecolor='none'))

# Example 3: Segmented form for fly larva
path_data = [
    (Path.MOVETO, [0.6, 0.8]),
    (Path.LINETO, [0.65, 0.75]),
    (Path.LINETO, [0.7, 0.8]),
    (Path.CLOSEPOLY, [0.6, 0.8])
]
codes, verts = zip(*path_data)
path = Path(verts, codes)
patch = PathPatch(path, edgecolor='black', facecolor='none')
ax.add_patch(patch)

# Example 4: Worm-like structure
worm_x = [0.8, 0.82, 0.84, 0.86, 0.88]
worm_y = [0.7, 0.72, 0.74, 0.72, 0.7]
ax.plot(worm_x, worm_y, color='black', lw=2)

# Example 5: Fly head (rough example using circles)
head = Circle((1.0, 0.8), 0.05, color='gray')
eye1 = Circle((0.98, 0.82), 0.02, color='red')
eye2 = Circle((1.02, 0.82), 0.02, color='red')
ax.add_patch(head)
ax.add_patch(eye1)
ax.add_patch(eye2)

# Example 6: Fly wings (symmetrical pattern)
left_wing = Polygon([[1.1, 0.75], [1.15, 0.8], [1.1, 0.85]], closed=True, edgecolor='black', facecolor='gray')
right_wing = Polygon([[1.1, 0.75], [1.05, 0.8], [1.1, 0.85]], closed=True, edgecolor='black', facecolor='gray')
ax.add_patch(left_wing)
ax.add_patch(right_wing)

# Set the axis limits
ax.set_xlim(0, 1.2)
ax.set_ylim(0.6, 0.9)

# Hide the axes
ax.set_axis_off()

# Show plot
plt.show()
