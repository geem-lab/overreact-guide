# Installing **overreact**

You can install the package from the command line using
[pip](https://pip.pypa.io/en/stable/):

```bash
$ pip install overreact
```

(You may require calling `pip3` instead of `pip`.)

The above command will install a minimal set of features.
If you plan to use the command-line interface, you have to specify
the `cli` extra feature:

```bash
$ pip install overreact[cli]
```

If you would like to use automatic differentiation (through Google's [JAX library](https://github.com/google/jax)) instead of
the default numerical differentiation, you have to specify the
`fast` extra feature as well:

```bash
$ pip install overreact[cli,fast]
```

## Dependencies

**overreact** depends on:

-   [`cclib`](https://github.com/cclib/cclib/) (parser for computational
    chemistry logfiles).
-   [SciPy](https://github.com/scipy/scipy/) (numerical integration,
    optimization, unit conversion and others).

(Don't worry, these dependencies are automatically installed when you install
**overreact** using `pip` as indicated above.)

Optionally, extra functionality is provided such as a command-line interface
and solvent properties (**warning**: solvent properties are not yet fully integrated into the package).
If you would like to install the full set of features, you can specify all extra flags:

```bash
$ pip install overreact[cli,fast,solvents]
```

This line installs [Rich](https://github.com/willmcgugan/rich),
[JAX](https://github.com/google/jax) and
[thermo](https://github.com/CalebBell/thermo) as well.

<!-- Rich is used in the command-line interface, JAX helps speedup calculations,
and thermo is used to calculate the dynamic viscosity of solvents in the
context of the :doc:`tutorials/collins-kimball` for diffusion-limited
reactions. -->
