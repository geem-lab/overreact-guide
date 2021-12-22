# Installing **overreact**

The recommended way of installing the package is from the command line using
[pip](https://pip.pypa.io/en/stable/):

```console
$ pip install overreact
```

> **✏️** You may need to call `pip3` instead of `pip`.

The above command will install a minimal set of features. **If you plan to use
the command-line interface, you have to specify the `cli` extra feature**:

```console
$ pip install overreact[cli]
```

> **💡** If you would like to use automatic differentiation (through Google's
> [JAX library](https://github.com/google/jax)) instead of the default numerical
> differentiation, you have to specify the `fast` extra feature as well:
>
> ```console
> $ pip install overreact[cli,fast]
> ```

## Dependencies

**overreact** depends on:

-   [`cclib`](https://github.com/cclib/cclib/) (parser for computational
    chemistry logfiles).
-   [SciPy](https://github.com/scipy/scipy/) (numerical integration,
    optimization, unit conversion and others).

> **✏️** Don't worry, these dependencies are automatically installed when you
> install **overreact** using `pip` as indicated above.

As stated above, extra functionality is provided such as a command-line
interface. If you would like to install the full set of supported features, you
can specify the following extra flags:

```console
$ pip install overreact[cli,fast]
```

The line above installs [Rich](https://github.com/willmcgugan/rich) (used in the
command-line interface) and [JAX](https://github.com/google/jax) (speeds up
calculations) as well.

> **⚠️** An extra `solvents` flag is available that adds some solvent properties
> by means of the [thermo](https://github.com/CalebBell/thermo) library. **It is
> not fully integrated into the package yet**: it is meant to provide, in the
> future, dynamic viscosities for solvents in the context of the Collins-Kimball
> theory for diffusion-limited reactions
> ([_Journal of Colloid Science_, **1949**, 4, 425–437](<https://doi.org/10.1016/0095-8522(49)90023-9>);
> [_Industrial & Engineering Chemistry_, **1949**, 41, 2551–2553](https://doi.org/10.1021/ie50479a040)).
> **Stay tuned and, if you are interested,
> [let's discuss it](https://github.com/geem-lab/overreact/discussions)!**

## Troubleshooting

### Can't install overreact: `pip: command not found` or similar

You may need to install [pip](https://pip.pypa.io/en/stable/) on your system.

> **💡** The pip developers have provided an excellent
> [installation guide](https://pip.pypa.io/en/stable/installation/) for you.

### Can't run overreact: `overreact: command not found` or similar

If you get this error, two things could be happening:

#### 1️⃣ You haven't properly installed the package.

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

#### 2️⃣ You are missing the `overreact` command in your `PATH`.

To fix this, you have to add the pip executable directory (i.e. the place where
pip puts executables during installation) to your `PATH`. For example, if you
installed overreact using `pip install overreact` as indicated above, the
overreact executable will be inside `~/.local/bin`.

This can be solved by adding the following line to your `~/.bashrc` file (or
`~/.zshrc` if you use zsh):

```shell
export PATH="$HOME/.local/bin:$PATH"
```

> **💡** Read more about
> [`PATH` on the Unix & Linux Stack Exchange](https://unix.stackexchange.com/a/26059/211802).
