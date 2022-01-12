# Using **overreact** as a command-line tool

> **✏️** This an overview of the command-line tool. **If you're new to
> **overreact**, you probably want to [go over the tutorial](./tutorial.md)
> first.**

Most commonly, you'll use the command-line tool to manage, explore and analyze
your microkinetic simulations. The following is a brief overview of options
available in the command-line tool. **You can access the full help page by
running `overreact --help`**. Here's its output as of
[version 1.0.2](https://github.com/geem-lab/overreact/releases/tag/v1.0.2):

```console
$ overreact --help
usage: overreact [-h] [--version] [-v] [-c] [--plot PLOT] [-b BIAS]
                 [--tunneling {eckart,wigner,none}]
                 [--no-qrrho {both,enthalpy,entropy,none}] [-T TEMPERATURE]
                 [-p PRESSURE] [--method {Radau,BDF,LSODA}]
                 [--max-time MAX_TIME] [--rtol RTOL] [--atol ATOL]
                 path [concentrations ...]

📈 Create and analyze chemical microkinetic models built from computational
chemistry data. Read the user guide at https://geem-lab.github.io/overreact-
guide/ for more information and usage examples. Licensed under the terms of
the MIT License. If you publish work using this software, please cite
https://doi.org/10.5281/zenodo.5730603.

positional arguments:
  path                  path to a source (`.k`) or compiled (`.jk`) model input
                        file (if a source input file is given, but there is a
                        compiled file available, the compiled file will be
                        used; use --compile|-c to force recompilation of the
                        source input file instead)
  concentrations        (optional) initial compound concentrations (in moles
                        per liter) in the form 'name:quantity' (if present, a
                        microkinetic simulation will be performed; more than
                        one entry can be given) (default: None)

optional arguments:
  -h, --help            show this help message and exit
  --version             show program's version number and exit
  -v, --verbose         increase output verbosity (can be given many times,
                        each time the amount of logged data is increased)
                        (default: 0)
  -c, --compile         force recompile a source (`.k`) into a compiled (`.jk`)
                        model input file (default: False)
  --plot PLOT           plot the concentrations as a function of time from the
                        performed microkinetics simulation: can be either
                        'none', 'all', 'active' species only (i.e., the ones
                        that actually change concentration during the
                        simulation) or a single compound name (e.g. 'NH3(w)')
                        (default: none)
  -b BIAS, --bias BIAS  an energy value (in kilocalories per mole) to be added
                        to each individual compound in order to mitigate
                        eventual systematic errors (default: 0.0)
  --tunneling {eckart,wigner,none}
                        specify the tunneling method employed (use
                        --tunneling=none for no tunneling correction)
                        (default: eckart)
  --no-qrrho {both,enthalpy,entropy,none}
                        disable the quasi-rigid rotor harmonic oscillator
                        (QRRHO) approximations to both enthalpies and
                        entropies (see [doi:10.1021/jp509921r] and
                        [doi:10.1002/chem.201200497]) (default: both)
  -T TEMPERATURE, --temperature TEMPERATURE
                        set working temperature (in kelvins) to be used in
                        thermochemistry and microkinetics (default: 298.15)
  -p PRESSURE, --pressure PRESSURE
                        set working pressure (in pascals) to be used in
                        thermochemistry (default: 101325.0)
  --method {Radau,BDF,LSODA}
                        integrator used in solving the ODE system of the
                        microkinetic simulation (default: Radau)
  --max-time MAX_TIME   maximum microkinetic simulation time (in s) allowed
                        (default: 86400)
  --rtol RTOL           relative local error of the ODE system integrator
                        (default: 1e-05)
  --atol ATOL           absolute local error of the ODE system integrator
                        (default: 1e-11)
```

The following is a brief description of the most commonly used options:

## The path to the model input file

The command-line tool requires the path to either a model source file (`.k`) or
a compiled one (`.jk`), from which it will read the given logfiles and calculate
all the thermodynamic and kinetic quantities of interest.

> **💡** [Click here](./input.md) to learn all about the **syntax of the model
> source file format**.

> **⚠️** **overreact** compiles your model (i.e., generates `.jk` files from the
> `.k` ones you've written) and tries to use the compiled ones whenever they are
> available. **If you want to force recompilation of the source file (e.g., your
> `.k` has changed), you can use the `--compile` or `-c` option (see below).**

## Initial concentrations

All the remaining positional arguments are considered initial concentrations of
compounds in the model. They are given in the form `name:quantity`, where `name`
is the name of a compound (defined in the model source file) and `quantity` is
the number of moles of that compound per liter of the working fluid (i.e.,
**concentrations are given in moles per liter**).

If at least one initial concentration is given, a microkinetic simulation will
be performed, and the concentrations of the model species at the end of the
simulation will be printed to the standard output.

> **⚠️** Kinetic profiles (e.g., plots of concentrations as a function of time)
> won't be produced by default. **You should use the `--plot` option in order to
> produce kinetic profiles (see below).**

## Produce kinetic profiles 📈

The `--plot` flag can be used to produce kinetic profiles (e.g., plots of
concentrations as a function of time during the microkinetic simulation).

You can either plot **all the species** (`--plot=all`) or only the **active
ones** (i.e., the ones that actually change concentration during the simulation,
up to a reasonable threshold, `--plot=active`) or a **single compound** of
interest (`--plot="NH3(w)"`).

## Energetics, kinetics and bias correction

The flags `--temperature` (or `-T`) and `--pressure` can be used to set the
working **temperature and pressure**, respectively, to be used in all
thermodynamic and kinetic calculations. Units are in kelvins and pascals,
respectively, and the default values are 298.15 K and 101.325 kPa.

The `--qrrho` flag can be used to enable or disable the **quasi-rigid rotor
harmonic oscillator** (QRRHO) approximations for entropies
([_Theory. Chem. Eur. J._, **2012**, 18: 9955-9964](https://doi.org/10.1002/chem.201200497)))
and enthalpies
([_J. Phys. Chem. C_ **2015**, 119, 4, 1840–1850](http://dx.doi.org/10.1021/jp509921r))).
The default value is `both`, which means that both entropies and enthalpies will
be corrected, but you can also choose to only enable the correction for
entropies (`--qrrho=entropy`) or only for enthalpies (`--qrrho=enthalpy`), or to
disable the correction altogether (`--qrrho=none`).

**Quantum tunneling approximations** can be selected or disabled with the
`--tunneling` flag. The default value is `eckart` (for the Eckart model), and
other valid options are `--tunneling=wigner` (Wigner model) and
`--tunneling=none` (no tunneling correction).

A **bias energy** (in kilocalories per mole) can be added to the model to
mitigate eventual systematic errors by using `--bias` (or `-b`). This will add a
constant energy value to each individual compound in the model. This is zero by
default.

> **⚠️** You should probably have a good reason to add a bias energy correction
> to your model.

## Force recompilation of the source file

The `--compile` (or, equivalently, `-c`) option forces the recompilation of the
source file (`.k`) into a compiled (`.jk`) model input file. **This is useful if
you want to make sure you're using the latest version of the source file.**

<details>
    <summary style="cursor: pointer;">
        🤔 Why doesn't overreact recompile my model automatically?
    </summary>
    <p>
        This is a design decision. The reason is that overreact is designed
        to work with <strong>very large models</strong>,
        and they can be slow interpret
        (imagine a model with a lot of reactions and a lot of species;
        <strong>overreact</strong> would have to read every logfile every time you run it,
        which can be quite slow).
    </p>
</details>

## Tuning the integrator

Some options are available to tune the integrator used in solving the
microkinetic ODE system:

-   The `--method` flag can be used to specify the **integrator** to be used
    (possible values are `Radau`, `BDF` and `LSODA`). The default is `Radau`.
-   The `--rtol` and `--atol` flags can be used to override the default
    **relative and absolute local errors** of the ODE system integrator (the
    default values are \\(10^{-5}\\) and \\(10^{-11}\\), respectively, which can
    be given in scientific notation as `--rtol=1e-5` and `--atol=1e-11`).
-   The `--max-time` flag can be used to specify the **maximum microkinetic
    simulation time** (in seconds) allowed (the default is 86400 seconds, or one
    day)

Take a look at the
[documentation of the `scipy.integrate.solve_ivp` function](https://docs.scipy.org/doc/scipy/reference/generated/scipy.integrate.solve_ivp.html)
for low-level details on the integrator options.
