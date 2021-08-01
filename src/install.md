# Installation

You can install the package from the command line using
[pip](https://pip.pypa.io/en/stable/):

```bash
$ pip install overreact
```

(You may require calling `pip3` instead of `pip`.)

## Dependencies

**overreact** depends on:

-   [`cclib`](https://github.com/cclib/cclib/) (parser for computational
    chemistry logfiles).
-   [SciPy](https://github.com/scipy/scipy/) (numerical integration,
    optimization, unit conversion and others).

(Don't worry, these dependencies are automatically installed when you install
**overreact** using `pip` as indicated above.)

Optionally, extra functionality is provided such as a command-line interface
and solvent properties:

```bash
$ pip install 'overreact[cli,fast,solvents]'
```

This line installs [Rich](https://github.com/willmcgugan/rich),
[JAX](https://jax.readthedocs.io/en/latest/index.html) and
[thermo](https://github.com/CalebBell/thermo) as well.

<!-- Rich is used in the command-line interface, JAX helps speedup calculations,
and thermo is used to calculate the dynamic viscosity of solvents in the
context of the :doc:`tutorials/collins-kimball` for diffusion-limited
reactions. -->
