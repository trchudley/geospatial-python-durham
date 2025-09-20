# Version control: `git` and GitHub

> **Page in Production**

## Why use `git` for your science

As your Python projects grow more complex, you may reach the point where it becomes useful for you to learn version control software: nearly universally, this means `git` and integration with the online website GitHub.

There are a number of reasons to do this:

 - To keep track of changes in your code in a more rigourous manner than e.g. OneDrive. You will be able to track versions of code, see what changed, and when you did it. You will be able to introduce automated testing to ensure that changes you make to your code hasn't broken anything or inadvertently changes your results.
 - This becomes key when you begin collaborating on code with others. Through the use of features such as branching and pull requests, `git` ensures that work being done by seperate people on seperate machines can come together in a consistent and functional manner.
 - Aid reproducability. Sharing your code online allows others to use, benefit from, and develop your work. A great example is [sharing code necessary to reproduce figures](https://github.com/hannahpicton/jakobshavn_isbrae) rather than just sharing the raw data. 
 - You can go further and develop entire packages to help people use your data and methods easier. See e.g. [pypromice](https://github.com/GEUS-Glaciology-and-Climate/pypromice) to help people download Promice data. Uploading these packages to github could be the last step, or it could be the first step in also getting them installable on e.g. `pip` and `conda`. 

### Difference between `git` and GitHub

`git` and GitHub can often be used interchangeably, but it is important to note they are not the same. `git` is a local, open-source version control system that can used to keep track of changes locally. GitHub is an online web platform (for-profit, owned by Microsoft) that allows you to host your repositories online. Online hosting is a real strength that massively enhances your ability to perform open and reproducable science. 

GitHub is, ultimately, the primary game in town, but it's important to note that it isn't wholly part of the same feel-good open-source community as the rest of the tools I've been recommending. There are open-source alternatives, the main one being GitLab, but this is less beginner-friendly and costs money. GitHub is free, but remember - if you aren't the customer, you're the product!

## Installing `git` and `gh`

- **Install `git`**:
  - Linux:  

    ```bash
    sudo apt install git   # Ubuntu/Debian
    sudo dnf install git   # Fedora
    ```

  - macOS:  

    ```bash
    brew install git
    ```

  - Windows:  
    Download from [git-scm.com](https://git-scm.com).

- **Install GitHub CLI (`gh`)**:  
  The GitHub CLI makes interacting with GitHub from your terminal easier.
  - Linux/macOS:  
    ```bash
    brew install gh
    ```
  - Windows: Available via `winget` or the GitHub installer.  

- **Check installation**:
  ```bash
  git --version
  gh --version

## Setting up a repository

Repositories (or *repos*) are folders whose history `git` tracks.

### On GitHub

1. Log into [GitHub](https://github.com).
2. Click **New repository**.
3. Choose a name, description, and set visibility (private for personal work, public to share).
4. Leave *“Initialize with README”* unchecked if you plan to connect an existing local folder.

### Locally

1. Navigate to your project folder:

   ```bash
   cd my-project
   ```
2. Initialize `git`:

   ```bash
   git init
   ```
3. Link it to GitHub (replace with your repo URL):

   ```bash
   git remote add origin https://github.com/username/my-project.git
   ```

### Recommended basic files

These files help organize and communicate your project.

#### `.gitignore`

Lists files/folders `git` should not track (e.g., large datasets, temporary files).

Example:

```
*.pyc
__pycache__/
data/raw/
.env
```

#### `README.md`

Explains your project: purpose, how to install dependencies, and how to run analyses.
This is the first thing others see.

#### `LICENSE`

Defines how others can use your code. Common choices for science:

* [MIT License](https://choosealicense.com/licenses/mit/) (permissive, simple)
* [GPL](https://choosealicense.com/licenses/gpl-3.0/) (ensures sharing and openness)

#### `environment.yml`

For reproducibility. Defines the Python environment (packages, versions) used in your project.

Example:

```yaml
name: climate-analysis
channels:
  - conda-forge
dependencies:
  - python=3.11
  - numpy
  - pandas
  - matplotlib
  - jupyter
```

## Using a personal repository

### Committing and pushing

Typical workflow:

1. Stage changes:

   ```bash
   git add myscript.py
   ```
2. Commit with a message:

   ```bash
   git commit -m "Add data cleaning function"
   ```
3. Push to GitHub:

   ```bash
   git push origin main
   ```

Think: *add → commit → push*.

### Branching

Branches let you experiment without breaking your main work.

* Create a new branch:

  ```bash
  git checkout -b new-analysis
  ```
* Switch back and merge when ready:

  ```bash
  git checkout main
  git merge new-analysis
  ```

## Working with others

**Tip:** Start small — just version-control your code, README, and environment files.
Collaboration and branching come naturally once you’re comfortable.

### Forking

If you want to contribute to someone else’s repository but don’t have write access:

* **Fork** it on GitHub (creates your copy).
* Clone your fork locally:

  ```bash
  git clone https://github.com/yourname/their-project.git
  ```

### Pull requests

When you’ve made changes in your fork and want the original repo to adopt them:

1. Push your branch to your fork.
2. On GitHub, open a **Pull Request (PR)** from your branch into the main project.
3. Project maintainers will review, discuss, and merge if appropriate.
