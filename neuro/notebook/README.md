# Cognitive Atlas Getting Started

This is a quick getting started container (and notebook it produced and serves)
to using the Cognitive Atlas via it's [Python API](https://github.com/CognitiveAtlas/cogat-python).
You can best get the dependencies by interacting with the container, when you build
locally from this repository or use the provided Docker Container on Docker Hub.

## Dependencies
Today we are going to be interacting wit the following software:

 - [Python](https://www.python.org/) is recommended to be used via a [miniconda](https://conda.io/docs/user-guide/install/index.html) or similar environment, so it's easy to install things.
 - [Cognitive Atlas](https://github.com/CognitiveAtlas/cogat-python) is a Python wrapper to the API served by [cognitiveatlas.org](https://www.cognitiveatlas.org)
 - [Jupyter](http://jupyter.org/) Notebook is an interactive environment for several languages, including Python!

We can use this software locally, **or** a [Docker](https://www.docker.com/) container for advanced users.


## Jupyter Notebook Local

You will need to have Python installed, and then install cognitiveatlas
and jupyter notebook with pip:

```bash
pip install cognitiveatlas jupyter
```

Then run jupyter notebook from the directory with the `ipynb` file (it means
ipython notebook).

```bash
jupyter notebook
```

## Build Locally

```bash
docker build -t vanessa/dinolesson-cogat .
docker run --rm -p 8888:8888 vanessa/dinolesson-cogat
```

If you want to bind a folder to the present working directory, the "work" directory
in the container to your present working directory (`$PWD`)

```bash
docker run --rm -v $PWD:/home/joyvan/work -p 8888:8888 vanessa/dinolesson-cogat
```
