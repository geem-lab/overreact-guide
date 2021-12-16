[![DOI](https://zenodo.org/badge/214332027.svg)](https://zenodo.org/badge/latestdoi/214332027)

[![CI](https://github.com/geem-lab/overreact/actions/workflows/python-package.yml/badge.svg)](https://github.com/geem-lab/overreact/actions/workflows/python-package.yml)
[![coverage](https://codecov.io/gh/geem-lab/overreact/branch/main/graph/badge.svg?token=4WAVXCRXY8)](https://codecov.io/gh/geem-lab/overreact)
[![PyPI](https://img.shields.io/pypi/v/overreact)](https://pypi.org/project/overreact/)
[![total downloads](https://pepy.tech/badge/overreact)](https://pepy.tech/project/overreact)
[![downloads/month](https://pepy.tech/badge/overreact/month)](https://pepy.tech/project/overreact)
[![Python Versions](https://img.shields.io/pypi/pyversions/overreact)](https://pypi.org/project/overreact/)
[![GitHub license](https://img.shields.io/github/license/geem-lab/overreact)](https://github.com/geem-lab/overreact/blob/main/LICENSE)

[![API documentation](https://img.shields.io/badge/docs-available-blue)](https://geem-lab.github.io/overreact/overreact.html)
[![GitHub Discussions](https://img.shields.io/github/discussions/geem-lab/overreact)](https://github.com/geem-lab/overreact/discussions)
[![GitHub issues](https://img.shields.io/github/issues-raw/geem-lab/overreact)](https://github.com/geem-lab/overreact/issues)
[![Made in Brazil 🇧🇷](https://img.shields.io/badge/made%20in-Brazil-009c3b)](https://github.com/geem-lab/overreact-guide#funding)

# Welcome to **overreact**!

<div align="center">
    <img alt="overreact" src="https://raw.githubusercontent.com/geem-lab/overreact-guide/master/logo.png" />
</div>

**overreact** is a **library** and a **command-line tool** for building and
analyzing homogeneous microkinetic models[^microkinetic] from first-principles
calculations[^ethane]:

```python
In [1]: from overreact import api

In [2]: api.get_k("S -> E‡ -> S",
   ...:           {"S": "data/ethane/B97-3c/staggered.out",
   ...:            "E‡": "data/ethane/B97-3c/eclipsed.out"})
Out[2]: array([8.16880917e+10])
```

It uses **precise thermochemical partition funtions**, **tunneling corrections**
and data is **parsed directly** from computational chemistry output files thanks
to [`cclib`](https://cclib.github.io/) (see the
[list of its supported programs](https://cclib.github.io/#summary)).

## Installation

**overreact** is a Python package, so you can easily install it with
[`pip`](https://pypi.org/project/pip/):

```console
$ pip install "overreact[cli,fast]"
```

See the
[installation guide](https://geem-lab.github.io/overreact-guide/install.html)
for more details.

> **🚀** **Where to go from here?** Take a look at the
> [short introduction](https://geem-lab.github.io/overreact-guide/quickstart.html).
> Or see
> [below](https://geem-lab.github.io/overreact-guide/intro.html#how-to-read-this-documentation)
> for more guidance.

## Citing **overreact**

If you use **overreact** in your research, please cite:

> F. S. S. Schneider and G. F. Caramori. _**geem-lab/overreact**: a tool for
> creating and analyzing microkinetic models built from computational chemistry
> data, v1.0.1_. **2021**.
> [DOI:10.5281/ZENODO.5643960](https://zenodo.org/badge/latestdoi/214332027).
> Freely available at: <<https://github.com/geem-lab/overreact>>.

Here's the reference in [BibTeX](http://www.bibtex.org/) format:

```bibtex
@misc{overreact2021,
  howpublished = {\url{https://github.com/geem-lab/overreact}}
  year = {2021},
  author = {Schneider, F. S. S. and Caramori, G. F.},
  title = {
    \textbf{geem-lab/overreact}: a tool for creating and analyzing
    microkinetic models built from computational chemistry data, v1.0.1
  },
  doi = {10.5281/ZENODO.5643960},
  url = {https://zenodo.org/record/5643960},
  publisher = {Zenodo},
  copyright = {Open Access}
}
```

> **✏️** A paper describing **overreact** is currently being prepared. When it
> is published, the above BibTeX entry will be updated.

## License

**overreact** is open-source, released under the permissive **MIT license**. See
[the LICENSE agreement](https://github.com/geem-lab/overreact/blob/main/LICENSE).

## Funding

This project was developed at the [GEEM lab](https://geem-ufsc.org/)
([Federal University of Santa Catarina](https://en.ufsc.br/), Brazil), and was
partially funded by the
[Brazilian National Council for Scientific and Technological Development (CNPq)](https://cnpq.br/),
grant number 140485/2017-1.

[^microkinetic]:

Microkinetic modeling is a technique used to predict the outcome of complex
chemical reactions. It can be used to investigate the catalytic transformations
of molecules. **overreact** makes it easy to create and analyze microkinetic
models built from computational chemistry data.

[^ethane]:

The three-line example code calculates the rate of methyl rotation in ethane (at
[B97-3c](https://doi.org/10.1063/1.5012601)). Surprisingly, the error found is
less than 2%
[when compared to available experimental results](http://dx.doi.org/10.1126/science.1132178).
