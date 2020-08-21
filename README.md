# mpl_sankey

This is a simple package to produce sankey plots with matplotlib.
It is an alternative to the `matplotlib.sankey`
[module](https://matplotlib.org/api/sankey_api.html), which sacrifices some
flexibility in exchange for a much simpler interface.

Specifically, this package only produces standard horizontal sankey plots, but
it does so automatically from data, rather than requiring the user to figure
out the spatial distribution of nodes/flows.

## How it works

There is a single method, `sankey()`, which accepts one argument `data` and
several optional keyword arguments.

`data` must be a 2-dimensional tabular object with at least 3 columns: best
results are obtained with `pandas.DataFrame`s, but `numpy.array`s and simple
lists of lists are also accepted.

- each row corresponds to a "flow"
- the first column stores the weights (that is, the tickness of each flow
  drawn), and must be an `int` or `float`
- each other column denotes a node (by its label, which can have any type)
  where the flow passes, at each stage
- if `data` is a `pandas.DataFrame`, then the column names are represented on
  top of each stage


## Example

```python
from mpl_sankey import sankey
from matplotlib import pyplot as plt
import pandas as pd

data = pd.DataFrame([[1, 'a', 1, 'I', 1, 'success'],
                     [2, 'b', 2, 'III', 2, 'discard'],
                     [1, 'b', 1, 'II', 2, 'success'],
                     [1, 'c', 1, 'II', 2, 'discard'],
                     [2.5, 'a', 2, 'IV', 1, 'discard'],
                     [2, 'a', 1, 'I', 1, 'success']],
                    columns=['Weight', 'First', 'Then', 'After', 'Finally', 'Outcome'])
                    
plt.figure(figsize=(12, 3))
sankey(data, cmap=plt.get_cmap('viridis'))
plt.savefig('featured.png', bbox_inches='tight')

```

<img src="https://raw.githubusercontent.com/toobaz/mpl_sankey/master/notebooks/featured.png">

Find more in the [Examples notebook](https://github.com/toobaz/mpl_sankey/blob/master/notebooks/Examples.ipynb).


## Installation and dependencies

You can install this package through PyPi with `pip install mpl_sankey`, or
just clone the repo from github.

The package requires `pandas` (and, obviously, `matplotlib`) to work.

