Kivy_Matplotlib
===============

Simple widget to display a Matplotlib Figure in kivy. Also a basic toolbar widget to pan and zoom the plot.
**Android/IOS not supported (until matplotlib can be ported to those systems)**

Usage
======
**Basic example**
```python
import matplotlib as mpl
from kivy_matplotlib import MatplotFigure
from kivy.base import runTouchApp

# Make plot
fig = mpl.figure.Figure(figsize=(2, 2))
fig.gca().plot([1, 2, 3])

# MatplotFigure (Kivy widget)
fig_kivy = MatplotFigure(fig)

runTouchApp(fig_kivy)
```

**Example with Toolbar**

```python
import matplotlib as mpl
from kivy.app import App
import numpy as np
from kivy.lang import Builder
from kivy_matplotlib import MatplotFigure, MatplotNavToolbar
kv = """
BoxLayout:
orientation: 'vertical'

MatplotFigure:
    id: figure_wgt
    size_hint: 1, 0.7
MatplotNavToolbar:
    id: navbar_wgt
    size_hint: 1, 0.3
    figure_widget: figure_wgt
"""

class testApp(App):
    title = "Test Matplotlib"

    def build(self):

        # Matplotlib stuff, figure and plot
        fig = mpl.figure.Figure(figsize=(2, 2))
        t = np.arange(0.0, 100.0, 0.01)
        s = np.sin(0.08 * np.pi * t)
        axes = fig.gca()
        axes.plot(t, s)
        axes.set_xlim(0, 50)
        axes.grid(True)

        # Kivy stuff
        root = Builder.load_string(kv)
        figure_wgt = root.ids['figure_wgt']  # MatplotFigure
        figure_wgt.figure = fig

        return root

testApp().run()
```

Requirements
============

- Kivy (>1.8)
- Matplotlib (>1.4)

Credits
=======
Jeyson Molina (jeyson.mco at gmail.com)
