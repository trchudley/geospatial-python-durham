# Quick start with Python for geospatial analysis

This is an informal document is designed to get you up and running with using Python for geospatial tasks. It is not designed to be a comprehensive tutorial - it will instead, link to authoritative sources for information on installs/downloads etc. However, as open source software, there are often multiple and conflicting options to pick from. Here, I am to give you - to the best of my knowledge - the up-to-date 'best' options for installing and using Python for geospatial analysis in the current ecosystem.

NB - when stuck, generative AI is actually pretty good for coding purposes (although I like to minimise using it for the most part to ensure I have my own understanding, and for environmental reasons). It's good primarily because it is _immediately falsifiable_: if it starts hallucinating, then the code/solution it proposes simply won't work. You can go back and query it, and potentially it might fix things. No guarantee though.

## Installing Python

There are three components to understand when setting up Python:

1. Actually installing Python (e.g. having, say, Python 3.12 on your system, and when you run the `python` command in your terminal, it will open it up).
2. Installing the many *packages* that make Python useful (e.g. `numpy` or `xarray` or `matplotlib`).
3. Managing *environments* so you can have multiple versions of Python with different combinations of versions and packages.

As a result, we can think of a fresh Python install like a new smartphone: your phone will come with pre-installed apps such as phone, calendar, clock, notes, etc., but to make proper use of your phone the vast majority of users will want to go to an app store and install specific apps that are tailored and useful to you. In Python terms, our pre-installed apps are the [Standard Library](https://docs.python.org/3/library/index.html), which may include basic capabilities like `os`, `datetime`, `random`, and `math`. Our 'app stores' are known as *package managers*, and include options such as `pip` or `conda`.

To make things more confusing, we often talk about having multiple Python *environments*. This is because Python packages often have numerous and conflicting dependencies. For one task, you might need the latest bleeding-edge version of `numpy` to take advantage of a recently added function. For another, you might be dependent on a old piece of software that requires a Python version <3.10. Single large, bloated installs often stop working for reasons you might not understand, but are to do with conflicting *dependencies* (e.g. what versions of software are required in the background) from different packages. As a result, you generally want to work want small installs (known as *environments*) with the minimal packages necessary for a project. In phone terms, imagine for some contrived reason that Instagram and Outlook cannot be installed on the same phone: as a result, you might want a 'social media' version of your phone for doomscrolling and a 'work' version of your phone for checking your emails. These are Python environments. 

<!-- To make things even more complex, sometimes the packages (apps) we install are interdependent and mutually exclusive: a package we want for one task (e.g. satellite analysis) may, in the background critically [depend on](https://xkcd.com/2347/) a specific version of a numerical analysis package (e.g. `v.2.41`, as a useful function was introduced at that version). However, a package for another task (e.g. time-series analysis) may depend on another version. Our package managers are designed to *manage dependencies* and make sure that all the background required packages play nicely with all the packages you want. -->

### Miniconda

There are numerous ways to install Python and [things can get confusing](https://xkcd.com/1987/). To avoid confusion, I will recommend only one way, which is called 'Miniforge' and [can be installed by following the instructions at the following link](https://github.com/conda-forge/miniforge).

Miniforge is chosen for the following reasons:
 - Miniforge runs _on the command line only_ (this is what the 'Mini' means). It is lightweight, and installable across Windows/MacOS/UNIX, your laptop, a University desktop, or an HPC.
 - Miniforge provides `conda` and `mamba` as package managers. Using these as your primary package manager is preferable to `pip` for many scientific applications, as it accounts for software dependencies beyond pure Python packages (e.g. [GDAL software](https://gdal.org/en/stable/) for geospatial purposes.)
 - Miniforge defaults to the `conda-forge` "channel" (think: app store). This is where most scientific packages are uploaded and maintained, rather than the default `conda` "channel", which is designed for commercial users.

### The command line

One note here is that this means you will have to understand the command line a _little_. This may also involve installing WSL if you are on a Windows machine. A good introduction/crash course is [here](https://developer.mozilla.org/en-US/docs/Learn_web_development/Getting_started/Environment_setup/Command_line). You really don't need to understand a lot - really just practicing using/understanding the basic commands such as `cd`, `mkdir`, `rm`, and `ln` will get you most of the way. It is also useful to know, in broad terms, that `.sh` bash scripts can be used to chain together commands ([introduction here](https://www.freecodecamp.org/news/bash-scripting-tutorial-linux-shell-script-and-command-line-for-beginners/)). Finally, it is worth understanding that you have a configuration file (e.g. `.bashrc`, `zshrc`, etc depending on your terminal) that is run silently on terminal startup - editing this means that you can do useful things such as define 'aliases' (shortcuts) to help you operate efficiently in the background.

### Conda / Mamba environments

After installing Miniconda, you will have `conda` and `mamba` available on your machine. Both are interchangeable: `mamba` was designed as a drop-in replacement for `conda` that works a lot faster and with better error messages. As a result, I will refer to `mamba` here, but both are the same - just replace `conda` with `mamba` in commands. An authoritative tutorial [is located here](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html).

After installing, you can create a new environment, here called `geospatial`, as follows:

```bash
$ mamba create --name geospatial
```

After creating it, you can then activate the environment:

```bash
$ mamba activate geospatial
```

There will probably be some indication in your terminal that this environment is active - e.g. `(geospatial)` at the beginning of the command line. 

Once the environment is active, you can install the required packages. You can chain together as many as you like. 

```bash
(geospatial) $ mamba install python geopandas rioxarray matplotlib
```

Here,  I have included python and three others - all other packages recommended here are should be dependencies of these three. If you find they aren't, you can always go back and install them them (e.g. `mamba install xarray`). If you need a specific version of anything, this is also possible (e.g. `mamba install python=3.9` or `python<=3.10` or `python>3.11`)


## How to interact with Python

### Command line

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

### Visual Studio Code

A common way of interacting with programmatic text files is [Visual Studio Code](https://code.visualstudio.com/). It is effectively a fancy text editor, so there isn't too much to say by way of a basic tutorial, but there is one [here](https://code.visualstudio.com/docs/python/python-tutorial) if you like (note that it's telling you to install Python, environments, and packages in ways other than `conda`/`mamba` - ignore these tips!). By installing a few add-ons (these will tend to be automatically recommended - e.g. a Python add-on when you open a `.py` file) there will be useful functionality: such as colour-coding your code in a useful way, or identifying errors - like a 'spell-check' for programming. You can open a terminal within the window in order to quickly run your scripts to test them. There are also advanced options, such as automatic code formatting (e.g. `black`), or `ssh` capability for interacting with HPCs.

### Jupyter Notebooks

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

## Using Python

To do - create some simple Notebooks to show examples.

### Basic Python

https://github.com/trchudley/GEOG2462/blob/main/Week_1_Search_and_Download/0_Using_Jupyter_Notebooks.ipynb

 - Variables and data types
 - Loops and conditional statements
 - Functions and classes

## Python for Data Analysis

 - Data analysis: `numpy` and `Pandas`
 - Working with files: `glob` for getting files, data extraction, etc

### Geospatial Python

 - Vector analysis: `geopandas`
 - Multidimensional analysis at netCDF files: `xarray`
 - Raster analysis: `rioxarray`