# Welcome to **overreact**!

<div style="text-align:center;">

![overreact](https://raw.githubusercontent.com/geem-lab/overreact-docs/master/logo.png)

</div>

**overreact** is a _library_ and a _command-line tool_ for creating and
analyzing microkinetic models[^microkinetic].
Data is parsed directly from computational chemistry output files thanks to
[`cclib`](https://cclib.github.io/) (see the [list of supported programs](https://cclib.github.io/#summary)).

<!-- ## _Ab initio_ thermochemistry

-   Concentration corrections
-   Symmetry corrections

## Microkinetic modelling

-   Microkinetics simulations

## Degree of rate control

-   Degree of rate control
-   Degree of selectivity control -->

[^microkinetic]:

Microkinetic modeling is a techinque used to predict the
outcome of complex chemical reactions.
It can be used to investigate the catalytic transformations of
molecules.
**overreact** makes it easy to create and analyze microkinetic models built
from computational chemistry data.

## Installation

**overreact** is a Python package, so you can easily install it with `pip`.
See the [installation instructions](https://geem-lab.github.io/overreact-docs/install.html).

## Documentation

Full documentation is hosted on Read the Docs.

Take a look in the side bar for background information, step-by-step usage instructions and tutorials.

Add links above (no sidebar stuff, etc.).

On how to use **overreact** as a command-line tool.

Take a look at the [command-line tool documentation](https://geem-lab.github.io/overreact-docs/command-line.html).

Take a look at the [library documentation](https://geem-lab.github.io/overreact-docs/library.html).

Take a look at the [tutorials](https://geem-lab.github.io/overreact-docs/tutorials.html).

Learn about [how it works](https://geem-lab.github.io/overreact-docs/howitworks.html).

### Code examples as Jupyter notebooks

Guide the user to Jupyter notebooks.

On how to use **overreact** as a Python library.

Take a look at the [example notebooks](https://geem-lab.github.io/overreact-docs/notebooks.html).

## License

**overreact** is open-source, released under the permissive **MIT license**.
See [LICENSE](https://github.com/geem-lab/overreact-docs/blob/master/LICENSE).

## Citing **overreact**

If you use **overreact** in your research, please cite:

> F. S. S. Schneider and G. F. Caramori. **overreact**: a tool for creating and analyzing microkinetic models built from computational chemistry data. 2021.
> Available at: <https://github.com/geem-lab/overreact>.

Here's the reference in [BibTeX](http://www.bibtex.org/) format:

    <!-- @article{overreact,
      title = \textbf{overreact}: a tool for creating and analyzing microkinetic models built from computational chemistry data},
      author = {Schneider, F. S. S. and Caramori, G. F.},
      journal={J. Chem. Phys.},
      volume={155},
      number={1},
      pages={0},
      year = {2021},
      publisher={American Chemical Society (ACS)},
      doi={10.1063/1.5058983},
      url={https://doi.org/10.1063/1.5058983}
    } -->

    @misc{overreact2021,
      author = {Schneider, F. S. S. and Caramori, G. F.},
      title = \textbf{overreact}: a tool for creating and analyzing microkinetic models built from computational chemistry data, ver. 1.0},
      howpublished = {\url{https://github.com/geem-lab/overreact}},
      year = {2021},
    }

## Funding

This project was supported by CNPq ([Brazilian National Council for Scientific and Technological Development](https://www.gov.br/cnpq/pt-br)) grant number 140485/2017-1.
