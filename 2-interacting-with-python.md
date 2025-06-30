# How to interact with Python

## Command line

After activating your environment, you can activate the Python interpreter simply by entering `python`:

```bash
(base) $ mamba activate geospatial
(geospatial) $ python
Python 3.12.10 | packaged by conda-forge | (main, Apr 10 2025, 22:19:24) [Clang 18.1.8 ] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> import numpy as np
>>> np.sqrt(16)
np.float64(4.0)
>>> name = 'Tom'
>>> statement = f'My name is {name}'
>>> print(statement)
My name is Tom
```

This is fine for exploring what Python can do, and you should use it when explore basic data types etc. However, it's hard to write multi-line commands (e.g. functions), or save scripts for repeat use. As a result, we tend to gravitate towards two other options.

1. The first is to write text files, `.py` files, that can be run with a Python interpreter (e.g. `python myscript.py`). This is useful for writing e.g. longer processing scripts that will be run autonomously to achieve tasks.
2. The second is to use a 'Jupyter Notebook' (saved as `.ipynb`, a vestigial reference to when these were known as iPython notebooks). These are mixed-media files run in your browser. You can combine text and code, and they are useful for when you are actively tinkering with the data (e.g. plotting, statistics, analysis, etc.).

## Visual Studio Code

A common way of interacting with programmatic text files is [Visual Studio Code](https://code.visualstudio.com/). It is effectively a fancy text editor, so there isn't too much to say by way of a basic tutorial, but there is one [here](https://code.visualstudio.com/docs/python/python-tutorial) if you like (note that it's telling you to install Python, environments, and packages in ways other than `conda`/`mamba` - ignore these tips!). By installing a few add-ons (these will tend to be automatically recommended - e.g. a Python add-on when you open a `.py` file) there will be useful functionality: such as colour-coding your code in a useful way, or identifying errors - like a 'spell-check' for programming. You can open a terminal within the window in order to quickly run your scripts to test them. There are also advanced options, such as automatic code formatting (e.g. `black`), or `ssh` capability for interacting with HPCs.

## Jupyter Notebooks

Jupyter Lab, the interface for your Notebook, can be installed via `conda`/`mamba`. It is recommended to do this in either your '`base`' environment or a purpose built environment (e.g. `jupyter-env`). This is because you don't want other packages creating conflicts with Jupyter.

```bash
$ mamba activate base
(base) $ mamba install jupyterlab
```

You can still use your other `conda`/`mamba` environments within this Jupyter environment, but it takes [a bit of jigging](https://medium.com/@patty.escalera/install-jupyter-lab-and-setup-a-conda-environment-54052443790b) using something called `ipykernel`. This isn't hard and is pretty self-explanatory:

```bash
(base) $ mamba activate geospatial
(geospatial) $ mamba install ipykernel
(geospatial) $ python -m ipykernel install --user --name geospatial-kernel --display
-name "Python (geospatial environment)"
```

Now, you can open Jupyter lab back in the other environment:

```bash
(geospatial) $ mamba activate base
(base) $ jupyter lab
```

Note that this will open the notebook in the directory you are currently in. You may wish to `cd` to the desired directory you are working within.

There will be an option on the home screen to  “Python (geospatial env)” to create a new notebook, or from within an existing notebok you can select it from the kernel dropdown menu in the top-right-hand corner of the notebook. Now, you will be able to access all of your `geospatial` environment packages from within Jupyter!

When you have finished with Jupyter, make sure to save your files and close it - either within the file menu in-browser, or by returning to your terminal and ending the operaturation using `ctrl+c` (or `cmd+c` on Mac).
