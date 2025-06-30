# Installing Python

There are three components to understand when setting up Python:

1. Actually installing Python (e.g. having, say, Python 3.12 on your system, and when you run the `python` command in your terminal, it will open it up).
2. Installing the many *packages* that make Python useful (e.g. `numpy` or `xarray` or `matplotlib`).
3. Managing *environments* so you can have multiple versions of Python with different combinations of versions and packages.

As a result, we can think of a fresh Python install like a new smartphone: your phone will come with pre-installed apps such as phone, calendar, clock, notes, etc., but to make proper use of your phone the vast majority of users will want to go to an app store and install specific apps that are tailored and useful to you. In Python terms, our pre-installed apps are the [Standard Library](https://docs.python.org/3/library/index.html), which may include basic capabilities like `os`, `datetime`, `random`, and `math`. Our 'app stores' are known as *package managers*, and include options such as `pip` or `conda`.

To make things more confusing, we often talk about having multiple Python *environments*. This is because Python packages often have numerous and conflicting dependencies. For one task, you might need the latest bleeding-edge version of `numpy` to take advantage of a recently added function. For another, you might be dependent on a old piece of software that requires a Python version <3.10. Single large, bloated installs often stop working for reasons you might not understand, but are to do with conflicting *dependencies* (e.g. what versions of software are required in the background) from different packages. As a result, you generally want to work want small installs (known as *environments*) with the minimal packages necessary for a project. In phone terms, imagine for some contrived reason that Instagram and Outlook cannot be installed on the same phone: as a result, you might want a 'social media' version of your phone for doomscrolling and a 'work' version of your phone for checking your emails. These are Python environments. 

<!-- To make things even more complex, sometimes the packages (apps) we install are interdependent and mutually exclusive: a package we want for one task (e.g. satellite analysis) may, in the background critically [depend on](https://xkcd.com/2347/) a specific version of a numerical analysis package (e.g. `v.2.41`, as a useful function was introduced at that version). However, a package for another task (e.g. time-series analysis) may depend on another version. Our package managers are designed to *manage dependencies* and make sure that all the background required packages play nicely with all the packages you want. -->

## Miniforge

There are numerous ways to install Python and [things can get confusing](https://xkcd.com/1987/). To avoid confusion, I will recommend only one way, which is called 'Miniforge' and [can be installed by following the instructions at the following link](https://github.com/conda-forge/miniforge).

Miniforge is chosen for the following reasons:
 - Miniforge runs _on the command line only_ (this is what the 'Mini' means). It is lightweight, and installable across Windows/MacOS/UNIX, your laptop, a University desktop, or an HPC.
 - Miniforge provides `conda` and `mamba` as package managers. Using these as your primary package manager is preferable to `pip` for many scientific applications, as it accounts for software dependencies beyond pure Python packages (e.g. [GDAL software](https://gdal.org/en/stable/) for geospatial purposes.)
 - Miniforge defaults to the `conda-forge` "channel" (think: app store). This is where most scientific packages are uploaded and maintained, rather than the default `conda` "channel", which is designed for commercial users.

## The command line

One note here is that this means you will have to understand the command line a _little_. This may also involve installing WSL if you are on a Windows machine. A good introduction/crash course is [here](https://developer.mozilla.org/en-US/docs/Learn_web_development/Getting_started/Environment_setup/Command_line). You really don't need to understand a lot - really just practicing using/understanding the basic commands such as `cd`, `mkdir`, `rm`, and `ln` will get you most of the way. It is also useful to know, in broad terms, that `.sh` bash scripts can be used to chain together commands ([introduction here](https://www.freecodecamp.org/news/bash-scripting-tutorial-linux-shell-script-and-command-line-for-beginners/)). Finally, it is worth understanding that you have a configuration file (e.g. `.bashrc`, `zshrc`, etc depending on your terminal) that is run silently on terminal startup - editing this means that you can do useful things such as define 'aliases' (shortcuts) to help you operate efficiently in the background.

## Conda / Mamba environments

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

