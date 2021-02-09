
---
jupytext:
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.10.0
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---

# Chapter 1

```{tableofcontents}
```
## List of concepts
Here are the list of concepts that we are going to encounter in this chapter.


```{code-cell} ipython3
:tags: ["remove-input"]
import pandas as pd
import networkx
import matplotlib.pyplot as plt
import numpy as np
from bokeh.io import output_notebook, show, save
output_notebook()
from bokeh.io import output_notebook, show, save
from bokeh.models import Range1d, Circle, ColumnDataSource, MultiLine
from bokeh.plotting import figure
from bokeh.plotting import from_networkx
from io import StringIO
```

```{code-cell} ipython3
:tags: ["remove-input"]
data = 'Source,Target,Weight\nA,B,2\nA,C,3\nB,D,5\nC,D,1\nD,G,2\nG,A,4'

df = pd.read_csv(StringIO(data), sep=',')
G = networkx.from_pandas_edgelist(df, 'Source', 'Target', 'Weight')

#Choose a title!
title = 'Concepts'

#Establish which categories will appear when hovering over each node
HOVER_TOOLTIPS = [("Concept", "@index")]

#Create a plot — set dimensions, toolbar, and title
plot = figure(tooltips = HOVER_TOOLTIPS,
              #tools="pan,wheel_zoom,save,reset", 
              tools="pan,wheel_zoom,reset",
              active_scroll='wheel_zoom',
            x_range=Range1d(-10.1, 10.1), y_range=Range1d(-10.1, 10.1), 
            title=title)

#Create a network graph object with spring layout
# https://networkx.github.io/documentation/networkx-1.9/reference/generated/networkx.drawing.layout.spring_layout.html
network_graph = from_networkx(G, networkx.spring_layout, scale=10, center=(0, 0))

#Set node size and color
network_graph.node_renderer.glyph = Circle(size=15, fill_color='salmon')

#Set edge opacity and width
network_graph.edge_renderer.glyph = MultiLine(line_alpha=0.5, line_width=1)

#Add network graph to the plot
plot.renderers.append(network_graph)

show(plot)
#save(plot, filename=f"{title}.html")
```

## Introduction

In this chapter, we learn about {term}`algorithm`s and flowcharts.

## Conclusion

We learned about algorithms and flowcharts.