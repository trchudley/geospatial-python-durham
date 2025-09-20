# Installing Python

There are three components to understand when setting up Python:

1. Actually installing Python (e.g. having, say, Python 3.12 on your system, and when you run the `python` command in your terminal, it will open it the Python interpreter).
2. Installing the many **packages** that make Python useful for scientific programming (e.g. `numpy` or `xarray` or `matplotlib`).
3. Managing **environments** so you can have multiple versions of Python with different combinations of versions and packages.

To conceptualise this, we can think of a fresh Python install like a new smartphone. Your phone will come with pre-installed apps such as phone, calendar, clock, notes, etc. In Python terms, our apps are known as _packages_, and those that come pre-installed are known as the [Standard Library](https://docs.python.org/3/library/index.html). Examples include `os`, `datetime`, `random`, and `math`. They are generally designed provide basic functionality for interacting with the OS, opening files and data, and providing basic mathermatical functionality.

To make proper use of your phone, the vast majority of users will not be happy with the basic apps on a smartphone. We will want to customise it by installing specific apps that are tailored and useful to you (e.g. WhatsApp, Instagram, etc). On smartphones, we do this via an app store. In Python, our 'app stores' are known as *package managers*, and include options such as `pip` or `conda`. We use this to install custom packages that we can use for specialist purposes (e.g. for opening geospatial data, or using statistical techniques).

There comes a point where you may have two contradictory uses for a phone that means you need more than one - think of people who have a personal phone and a work phone, for legal or security reasons. To make the analogy slightly more contrived, imagine for some reason that Instagram and Outlook cannot be installed on the same phone. As a result, you might want a 'social media' version of your phone for doomscrolling and a 'work' version of your phone for checking your emails. These are analogous to Python *environments*. For example, for one task you might need the latest bleeding-edge version of `numpy` to take advantage of a recently added function. For another, you might be dependent on an old piece of code that requires a Python version <3.10. It won't be possible to do both! If you carry on adding more and more packages to one install, eventually it will break for reasons you don't quite understand, but generally result from these conflicting *dependencies* (e.g. what versions of packages and software are required in the background) from different packages. As a result, you generally want to work want small installs (known as *environments*) with the minimal packages necessary for a project. 

<!-- To make things even more complex, sometimes the packages (apps) we install are interdependent and mutually exclusive: a package we want for one task (e.g. satellite analysis) may, in the background critically [depend on](https://xkcd.com/2347/) a specific version of a numerical analysis package (e.g. `v.2.41`, as a useful function was introduced at that version). However, a package for another task (e.g. time-series analysis) may depend on another version. Our package managers are designed to *manage dependencies* and make sure that all the background required packages play nicely with all the packages you want. -->

## Installing Python

### The 'default' options and why they might not be the best idea

Python is an open-source project: although there is an ['official' Python website](https://www.python.org/) and associated committees etc., anyone can (and indeed, is actively encouraged!) to build and extend on Python. Many groups and communities will put out improvements and extensions: this is great, at allows new ideas and methods to rapidly emerge and iterate. Communities can build solutions that are suited to their needs and share them with others. Some of them are so succesful they become the de-facto 'standard' way of doing things, even if it won't appear on the official Python website! 

The downside of this is approach is that can lead to [several overlapping ways of doing things](https://xkcd.com/927/) that can be confusing to beginners. When googling a way of doing something, you might find several solutions on forums and blogs. Sometimes the most-commonly used solution isn't the most official solution (indeed, if you download install Python according to the instructions on the python.org website, you will quickly start having a bad time when you begin trying to manage packages and environment). Sometimes you might find a great user-friendly guides only to find the proposed solution is outdated and broken. Sometimes the most common solution is actually inappropriate for your specific needs (e.g. in our case, geospatial approaches). Sometimes you can't find any obvious solution at all, just endless StackExchange forums full of nerds arguing with each other over which of their pet solutions is best. 

The intention of this guide is to give you a clear guide as to the 'best' solution, so you can skip the confusing phase and get on with doing science. I won't spend too much time, if any, on _why_ any particular solution is best - although I have outlined why some of the alternatives aren't ideal below - I will just point you towards the right materials to get on with the job. However, the reasoning will tend to be that these solutions are the most commonly used, robust, and well-suited for geospatial applications.

<!-- There are many ways to skin a cat, but in this guide I aim to save you time by recommending a single 'best' way that is useful for the largest range of scenarios, and particular for geospatial programming. -->

#### The default installation

On some OSs (e.g. MacOS), you may have a built-in install of Python that will run when you enter the `python` command into the Terminal. It is generally best to __avoid messing with these default installs of Python__. They tend to be quite outdated, and more importantly your system may be dependent on this install for critical tasks - break it at your peril!

You could try and use the official Python installer on [python.org](python.org), or install from the command line using built-in OS software managers (`apt`, `brew`), but these options tend to make environment management challenging. There are also full-featured distributions of Python such as [Anaconda](anaconda.com) that come with a massive set of pre-installed packages, but these tend to be bloated and large, including a lot of things you don't need. There are a lot of options out there, and if you don't keep track of where things are coming from things can [quickly get confusing!](https://xkcd.com/1987/).

#### The default package manager

Python comes with a lightweight way to manage packages and environments called `pip`. This is the default Python package management system, which connects to an online repository of public packages (think: app store) called the Python Package Index ([PyPI](https://pypi.org/)). This is lightweight and built-in, but is limited to only distributing Python packages. As a result, installing more advanced compiled libraries that require non-Python software becomes an absolute pain. A particular problem for geospatial packages is that most modern geospatial software is built upon foundational programs such as [GDAL](https://gdal.org), the geospatial data abstraction library (most of e.g. QGIS is built on this!). This is ultimately a C++ library, so attempting to install most geospatial Python packages via `pip` will tend to fail without doing some very finicky fixes. It is desirable to find something better to let us not have to worry about this.

As is common in the open source world, there are always [trendy new package managers emerging](https://xkcd.com/927/) (`uv` appears to be the latest, and `poetry` also has proponents for managing environments), but I would recommend letting the computer scientists be the trendsetters here and stick with established and robust options.

#### The default environment manager

Similarly, there is a default tool for managing virtual environments called `venv`. This again has slightly old and rudimentary methods and can't keep track of non-Python dependencies.

### The 'best' way - Miniforge and `conda`

The best way to install Python and manage packages and environments is through the `conda` tool, installable via the "Miniforge" distribution. 

Miniforge is a lightweight, simple installation that works across Windows/MacOS/Linux. It is command-line-only (this is what the 'mini' in Miniforge means). As a result, there is no bloated GUI interface, and the installation process and interface will be the same wherever you use it - be it your laptop, a University desktop, or an HPC. 

Once installed, you will have access to `conda`, a command line tool for package management. It emerged from the [Anaconda](anaconda.org) data science company, but `conda` itself is free and open source. Unlike `pip`, it is adept at managing non-Python dependencies. This is great for less technical users that do not wish to spend hours trying to make sure their other tools and dependencies are playing nicely with Python. As a resulst, it has a large take-up in data science and applied sciences.

`conda` allows you to download from a number of different repositories (think: app stores), but the most important one is the [`conda-forge`](https://conda-forge.org/), a large community effort that is the de-facto location where scientists upload their tools and packages (think: apps) for you to use. By using the Miniforge install, you will be downloading from the `conda-forge` by default (this is what the 'forge' in Miniforge means), so you won't have to worry about this again until you start developing your own tools and packages!


#### Installation

[For full information, see the instructions at the following link](https://github.com/conda-forge/miniforge). In short, you can download the installer using either `curl` or `wget`, preferably whilst in your home directory (whether you use `curl` or `wget` will depend on your OS and shell). For example:

```sh
curl -L -O "https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-$(uname)-$(uname -m).sh"
```

or

```sh
wget "https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-$(uname)-$(uname -m).sh"
```

You can then run the install script:

```sh
bash Miniforge3-$(uname)-$(uname -m).sh
```

And follow the promps appropriately. You may be prompted to initialise conda via `conda init`, and/or you can restart your terminal (lines that set up `conda` will be automatically added to your shell `rc` file, which will be created if you don't already have one).


## Using `conda`

### Setting up an environment

After you have installed Miniforge, you might notice that your command line interface looks slightly different:

```sh
(base) tom ~ % 
```

Note the new appearance of `(base)`. This indicates you are now in an _environment_ - namely, one with the name "base". This now means that when you use any software installed in this environment (in our case, python and any associated software), it will now be directing all commands to run a specific, isolated set of those programs. You can tell where these programs are by running the `which` command. For example:

```sh
(base) tom ~ % which python
/Users/tom/miniforge3/bin/python
```

See - the `python` being used is in our base `miniforge` directory!

`conda` always sets up a `base` environment by default. This is where `conda` itself is installed. However, you shouldn't work in this environment - if you begin to install loads of packages here, you may find you break your `conda` installation entirely and have to reinstall everything from scratch!

As a result, we should always create a new environmen to begin doing work in. Let's create one called `geospatial`, as follows:

```sh
(base) tom ~ % conda create --name geospatial python
```

This means _"create a new environment that is called 'geospatial', and install python within it"_

After creating it, you can then activate the environment:

```sh
(base) tom ~ %  conda activate geospatial
```

Iif we now look at our terminal, we can now see that `(geospatial)` at the beginning of the command line:

```sh
(geospatial) tom ~ % 
```

By running `which`, we will also see that you point to a different Python install.

```sh
(geospatial) tom ~ % which python
/Users/tom/miniforge3/envs/geospatial/bin/python
```

We can run `conda info --envs` to see what environments are avaiable, which will also highlight which one is active.

```sh
(geospatial) tom ~ % conda info --envs

# conda environments:
#
base                   /Users/tom/miniforge3
geospatial           * /Users/tom/miniforge3/envs/geospatial
```

### Installing packages

Once the environment is active, you can begin to install packages. Make sure you are in the correct environment, and then you use `conda install` to chain together as many desired packages as you like. 

```sh
(base) tom ~ %  conda activate geospatial
(geospatial) tom ~ % conda install geopandas rioxarray matplotlib
```

Here,  I have included three packages: `geopandas`, `rioxarray`, and `matplotlib`. You can keep on adding names to install as many packages as you like. `conda` will do some thinking, and then you will be prompted to install all the packages with a `[y/n]` prompt.

You might be surprised to see that many many packages - tens or possibly even hundreds - are going to be installed. As a package manager, `conda` automatically figures out what other dependencies need to be installed (e.g. `geopandas` needs `pandas`, and `rioxarray` requires `xarray`). 

`conda` will also figure out how to manage _conflicts_. It will always try and install the most recent and up-to-date version of anything it installs, but sometimes some packages requires specific versions. For instance, the latest version of package Z may be v3.6. Package X requires at least Z 3.0 (a fancy new command was introduced in this version). Package Y recquires at least Z v2.8, but _can't_ yet use anything beyond v3.4 (a reliable old command was deprecated in this version, and the package Y maintainers haven't yet managed to fix things in the background). As a result, if you try and install packages X and Y in the same environment, `conda` will ensure that pacakge Y v3.4 will be installed. Every time you install a new package, `conda` is figuring out how to do this on a scale of hundreds of packages, making them all work together seamlessly without you noticing. 

Eventually, there will be a point where even `conda` can't make magic work (e.g. package A requires package C `>=6.2` and package B requires C `<5.0`), and it might refuse to install a specific package in this case. This is why we manage multiple environments, and try and keep them as lightweight and project-specific as possible.

You can also request specific version of software yourself, if so required. This is possible by specifying a version number (e.g. `conda install python=3.9` or `python<=3.10` or `python>3.11`). From now on, `conda` will continue to manage the packages whilst keeping your preferred version. At any point, you can unpin this flag. You can also manually request to upgrade packages to their latest versions, uninstall packages, and pin and unpin versions. An authoritative tutorial [is located here](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html).

### Reproducability: sharing environments

In the interests of reproducing your science, you may wish to share with others your exact environments you used to run software, ensuring that all versions match and everything can be installed with a simple one-line command. 

This can be done creating, sharing, and installing from an environment file (`environment.yml`). This is a text-based markup file that has an example structure as follows:

```yaml
name: geospatial
channels:
  - conda-forge
dependencies:
  - python
  - rioxarray
  - geopandas
  - matplotlib
```

You can also specify specific versions if necessary (e.g. `python=3.12`). If you have an `environment.yml` file to hand, you can install the environment by running the following command:

```sh
conda env create -f environment.yml
```

If you would like to create an `environment.yml` of your own to share with others, you can automatically create one at any point by ensuring you are in the correct environment you want to share, and running:

```sh
conda export -f environment.yml
```

This creates a new file called `environment.yml` in the current directory. One note though, is that it will be a very long, explicit list of packages, including all dependencies and with all version numbers explicitly stated. This is great for ensuring you share an exactly reproducable environment, but in a lot of cases you might prefer to offer flexibliity and allow updates. In this case, a smaller, manual `enviornment.yml` (like the one above, and which I have included within this repository) is probably preferable. 

### An additional note - `mamba`

(You can ignore this if you wish!)

As mentioned above, once your environments get large (with dependencies, numbers of installed packages can reach the hundreds), then what was quite a simple operation to solve dependencies ("find package Z where `<=3.9` to satisfy package X and `>3.4` to satisfy Y)" can become a monster task with exponentially growing possiblities and conflicts to resolve. For quite a while, `conda` had relatively rudimentary solutions to resolve dependencies (initially a graph-based solution). However, as software needs grew, this began to be slow and innefficiant at resolving large environments.

A project called `mamba` was created (continuing the snake theme), which 'forked' `conda` and replaced the default solver with a new, fast, C++-based solution called `libmamba`. Everything else was a drop-in replacement - e.g. `conda install numpy` simply became `mamba install numpy`. This was a massive difference - depency resolutions that took minutes or hours on `conda` suddenly took seconds. Naturally, in a classic open-source move, `mamba` was slowly becoming the default.

However, as of late 2023, `conda` adopted `libmamba` back into its own code. Now, `conda` is nearly as fast as `mamba`! You may still see in my code and notes that I continue to use `mamba`. I slightly prefer the log notes, error messages, and find it slightly faster for some scenarios. If you find you are struggling with `conda`, try the same command but with `mamba` instead (after installing Miniconda, both will be available to you). However, nowadays, it (hopefully) won't make much of a difference to all but powerusers.
