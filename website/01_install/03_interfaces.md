# Interfacing with Python

## Command line

After activating your environment, you can activate the Python interpreter simply by entering `python`:

```sh
(base) tom ~ % conda activate geospatial
(geospatial) tom ~ % python
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

1. The first is to write `.py` files, which are simply text files of Python commands that will be run one-by-one. These can be run through the Python interpreter (e.g. `python myscript.py`). This is useful for writing e.g. longer processing scripts that will be run autonomously to achieve tasks.
2. The second is to use a 'Jupyter Notebook' (files with the suffix `.ipynb`, a vestigial reference to when these were known as iPython notebooks). These are mixed-media files run in your browser. You can combine text and code, and they are useful for when you are actively tinkering with the data (e.g. plotting, statistics, analysis, etc.).

## Text Editors and Integrated Development Environments (IDEs) 

Ultimately, a `.py` file simply a text file of Python commands. You could write an entire software programme using only a plain-text editor such as Notepad (Windows) or TextEdit (MacOS) if you wish, and some masochists do. 

However, as your scripts get longer and more complex, it is nice to be able to write code in an environment that can help you with the small details - such as colour-coding code blocks to help you visualise structure ("syntax highlighting"); identifying errors in your code that will break your script; or by providing built-in functionality for running and debugging code.

If you are very familiar with e.g. MATLAB or R (using RStudio), you will be familiar with an Integrated Development Environment (IDE). This editing environment provides you with a window for your code, but also other windows for other functions, such as keeping track of variables or viewing figure outputs.

If you are very familiar with an IDE style of programming coming from MATLAB or R, then there are IDEs available for you - take a look into [spyder](https://www.spyder-ide.org/) or [PyCharm](https://www.jetbrains.com/pycharm/). However, 
IDEs have never _quite_ taken off in the same way for Python development. It's partly because of the wide range of purposes Python is used for beyond data science (including e.g. web development), the range of non-Python elements Python programmers often use (such as CLI-based environment management, git, or metadata files), and because of the development of modern alternative ways of doing data science, such as Jupyter Notebooks (more on that below).

Instead, my own preferred method is to use a _code editor_. Out of the box, these are effectively just fancy-looking text editors. However, by using extensions, they rapidly become very powerful tools, and can become the mainstay of how you interact with data files. I use my code editor for Python, MATLAB, metadata management, `ssh`-ing into HPCs, and even to write the document you are reading now!

### The 'best' editor -- Visual Studio Code

Out of all code editors, the most common is [Visual Studio Code](https://code.visualstudio.com/). As discussed above, it is effectively a fancy text editor, so there isn't too much to say by way of a basic tutorial, but there is one [here](https://code.visualstudio.com/docs/python/python-tutorial) if you like (note that it's telling you to install Python, environments, and packages in ways other than `conda`/`mamba` - ignore these tips!).

As mentioned, it is the packages that make VS Code truly powerful, but I wouldn't worry about these. Most worth installing will be recommended to you as you open files. For instance, once you open the a `.py` file, the 'Python' add-on will be recommended. This will give you the recquisite tools for syntax highlighting, linting (automatically making sure your code is laid out appropriately), and environment management. Just take a look at the instructions for what you're installing so that you know how to use it effectively.

I have also installed additional packages such as `black` (my preferred linter), the 'Remote - SSH' tool for accessing HPCs, tools for better git management, tools for previewing and linting markdown, csv, and Makefiles, and even an add-on for using Jupyter Notebooks within VS Code. I didn't do this all on day one though! Just know that if there's something you want to do with code or programming, there's probably some way that VS code can help.

## Jupyter Notebooks

The modern 'data sciencey' way of interacting with Python is through something called _Jupyter Notebooks_. These are mixed-media documents of text and code that allow you to annotate and iterate code production. If you want an example of what one looks like, then look no further than the 'Using Python' document of this repository, which is itself a Jupyter Notebook!

Jupyter Lab, the interface for your Notebook, can be installed via `conda`. It is recommended to do this in either your '`base`' environment or a purpose built environment (e.g. `jupyter-env`). This is because you don't want other packages creating conflicts with Jupyter.

```bash
(geospatial) tom ~ % conda activate base
(base) tom ~ % conda install jupyterlab
```

We can still use our other installed `conda` environments within this Jupyter environment, but it isn't automatic - it takes [a bit of jigging](https://medium.com/@patty.escalera/install-jupyter-lab-and-setup-a-conda-environment-54052443790b) using something called `ipykernel`. This isn't hard and is pretty self-explanatory:

```bash
(base) tom ~ % conda activate geospatial
(geospatial) tom ~ % conda install ipykernel
(geospatial) tom ~ % python -m ipykernel install --user --name geospatial-kernel --display
-name "Python (geospatial environment)"
```

Now, you can open Jupyter lab back in the other environment:

```bash
(geospatial) tom ~ %conda activate base
(base) tom ~ % jupyter lab
```

This will open an instance of Jupyter Lab as a tab of your web browser. Note that, by default, the Lab environments defaults to opening within the directory you are currently in. You may wish to `cd` to a different directory (e.g. the directory of the project you are working on) to make things convenient.

There will be an option on the home screen to create a new Notebook within the **“Python (geospatial env)”** environment. Alternatively, create a new Notebook and select the correct environment from the kernel dropdown menu in the top-right-hand corner of the notebook. Now, you will be able to access all of your `geospatial` environment packages from within Jupyter!

When you have finished with Jupyter, make sure to save your files and close it - either within the file menu in-browser, or by returning to your terminal and ending the operaturation using `ctrl+c` (or `cmd+c` on Mac).

I will let other tutorials take you in detail (e.g. [1](https://jupyter.org/try-jupyter/notebooks/?path=notebooks/Intro.ipynb), [2](https://realpython.com/jupyter-notebook-introduction/)) now that you're up and running - but now that we've set up Python and found ways to interact it, we can begin using it!
