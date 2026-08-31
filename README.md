# Quantitative Finance Lab

This is where I am keeping the smaller notebooks I write while I work through
probability and quantitative finance properly. It is still an early learning
repo. Right now it contains one Brownian-motion notebook, not a strategy
library, backtester, or finished research framework.

## What is here

- [`notebooks/brownian_motion.ipynb`](notebooks/brownian_motion.ipynb) works
  through one-, two-, and three-dimensional Brownian paths in Python.
- `pyproject.toml` and `poetry.lock` pin the Python environment used for the
  notebook.

The notebook starts from the definition of a Wiener process, turns the
increments into a discrete simulation, and checks the basic scaling rule
\(\operatorname{Var}(B_t)=t\). The plots are useful for building intuition,
but a plotted finite grid is still only an approximation to a continuous-time
process.

## Run it

This repo uses Python 3.12 and Poetry.

```bash
poetry install --no-root
poetry run jupyter lab notebooks/brownian_motion.ipynb
```

The notebook uses a fixed random seed so the examples can be rerun. Change the
seed if you want a different path.

## What this does not contain yet

There is no market-data pipeline, option pricer, trading strategy, or machine
learning model here yet. I would rather add those as I understand and test them
than list work that is not in the repository.

My next exercise is to move the simulation into a small tested Python module,
then build geometric Brownian motion while keeping the assumptions and sanity
checks visible.
