# Installing **overreact**

You can install the package from the command line using
[pip](https://pip.pypa.io/en/stable/):

```console
$ pip install overreact
```

(You may require calling `pip3` instead of `pip`.)

The above command will install a minimal set of features. If you plan to use the
command-line interface, you have to specify the `cli` extra feature:

```console
$ pip install overreact[cli]
```

If you would like to use automatic differentiation (through Google's
[JAX library](https://github.com/google/jax)) instead of the default numerical
differentiation, you have to specify the `fast` extra feature as well:

```console
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

Optionally, extra functionality is provided such as a command-line interface and
solvent properties (**warning**: solvent properties are not yet fully integrated
into the package). If you would like to install the full set of features, you
can specify all extra flags:

```console
$ pip install overreact[cli,fast]
```

The line above installs [Rich](https://github.com/willmcgugan/rich) and
[JAX](https://github.com/google/jax) as well.

<!-- Rich is used in the command-line interface, JAX helps speedup
calculations, and [thermo](https://github.com/CalebBell/thermo) is used to
calculate the dynamic viscosity of solvents in the context of the
:doc:`tutorials/collins-kimball` for diffusion-limited reactions. -->

## Troubleshooting

### Can't install overreact: `pip: command not found` or similar

You may need to install [pip](https://pip.pypa.io/en/stable/) on your system.
_The pip developers have provided an excellent
[installation guide](https://pip.pypa.io/en/stable/installation/) for you._

### Can't run overreact: `overreact: command not found` or similar

If you get this error, two things could be happening:

1. You haven't properly installed the package.

To fix this first problem, take a look at
[a previous section](http://127.0.0.1:3000/install.html#installing-overreact).
If you're running a Unix, you can check if the package is installed by running
`pip list | grep overreact`:

```console
$ pip list | grep overreact
overreact             1.0.2
```

Alternatively, you can try to import the package directly from Python:

```console
$ python
Python 3.9.7 (default, Sep 10 2021, 14:59:43)
[GCC 11.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import overreact
>>> overreact.__version__
'1.0.2'
```

2. You are missing the `overreact` command in your `PATH`.

To fix this, you have to add the pip executable directory (i.e. the place where
pip puts executables during installation) to your `PATH`. For example, if you
installed overreact using `pip install overreact` as indicated above, the
overreact executable will be inside `~/.local/bin`.

This can be solved by adding the following line to your `~/.bashrc` file (or
`~/.zshrc` if you use zsh):

```shell
export PATH="$HOME/.local/bin:$PATH"
```

[See this for more about `PATH`](https://unix.stackexchange.com/a/26059/211802).
