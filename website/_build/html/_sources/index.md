# Geospatial programming with Python at Durham University

> Tom Chudley  
> thomas.r.chudley@durham.ac.uk  
> Department of Geography, Durham University

## Target Audience

This informal set of documents is designed for colleagues in the Department of Geography at Durham University to get beginners up and running with using Python for geospatial programming tasks. However, in practice, it is generally applicable apart from some of the specifics of the HPC interface.

## Purpose

As open source software, there are often multiple and conflicting options and advice to pick from when setting up Python. Figuring out the setup that works for you can be a large time drain and put people off from taking advantage of everything that Python has to offer. Here, I aim to give you - to the best of my knowledge - the up-to-date 'best' options for installing and using Python for geospatial analysis in the current ecosystem, as well as a broad-level introduction to the tools you have access too. It aims to be specific on particular quirks of the Durham system. It is not designed to be a comprehensive tutorial - it instead aims to give you the 'best' way of doing something, leaving you to fill in the gaps with your own research (e.g. googling and LLMs). However, there will also be links to useful sources for information on installs/downloads as we go.

This material can be as an [online Jupyter Book](https://trchudley.github.io/geospatial-python-durham/). The backend repository can be found at the [GitHub repository](https://github.com/trchudley/geospatial-python-durham) - this could be useful as many of the webpages are in fact Jupyter Notebooks, which you can download and use. At the Github repo, individual Markdown and Jupyter Notebook files can be found within the `website` directory in the root folder, then organised into directories and named according to the web address of individual pages.

## Tips

Section 1 (Installing Python) is not the most enthralling start - setting up a rigorous Python environment can be challenging, and was one of the main motivations for beginning to create this documentation! If you'd like to just get a feel for what Python can do for you, I would recommend browsing section 2 (Using Python) instead. If you would like to play with Python and Jupyter Notebooks without having to install it on your machine, you could always run an instance of [Google Colab](https://colab.research.google.com/).

NB - when stuck, generative AI is actually pretty good for coding purposes (although I like to minimise using it to ensure I have my own understanding of how my code works, as well as for environmental reasons). It's a good use of AI primarily because, unlike using it for writing prose, it is _immediately falsifiable_: if it starts hallucinating, then the code/solution it proposes simply won't work. You can go back and provide the error message, and it may even be able to fix its mistakes.
