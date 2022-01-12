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

The `--plot` flag can be used to produce kinetic profiles (e.g., plots of
concentrations as a function of time during the microkinetic simulation).

You can either plot all the species (`--plot=all`) or only the active ones
(i.e., the ones that actually change concentration during the simulation, up to
a reasonable threshold, `--plot=active`) or a single compound of interest
(`--plot="NH3(w)"`).

<!-- ...

\textcolor{red}{EXAMPLE NOT COOL! MAYBE THIS SHOULD BE GIVEN IN THE SUPPORTING
INFORMATION OR SIMPLIFIED. IN ANY CASE, CLEARLY PUT THE NAME AND EXTENSION OF
THE INPUT FILE. MENTION HOW TO ENTER EACH AVAILABLE OPTION: SOLVATION,
TUNNELING, TEMPERATURE, ETC...}

Naturally, all outputs should already be optimized in solution.

The paths to logfiles are relative to the path of the input file. As such, it is
very simple to run **overreact** when in the same directory as
\texttt{curtin_hammett.k}~(\cref{lst:run-example}). % \begin{lstlisting}[
caption={Example of running the command-line application of **overreact**.},
label={lst:run-example}, language={bash}, ]

# only thermodynamics and kinetic data:

$ overreact curtin_hammett.k

# data above plus microkinetics simulation:

$ overreact curtin_hammett.k "A(w):0.1" "B(w):0.05" --plot=active
\end{lstlisting}

The second line in~\cref{lst:run-example} performs all calculations and also
propagates a microkinetic simulation with the specified initial concentrations
given ($[\ce{A(w)}]$ = 0.1~M, $[\ce{B(w)}]$ = 0.05~M and zero for all other
species).

% Excerpts from the output for the example given above are available (NOT
REALLY!) in the supporting information. As such, the user specifies a set of
elementary reactions that are believed to be relevant for the overall chemical
phenomena. **overreact** offers a hopefully complete but simple environment for
hypothesis testing in first-principles chemical kinetics. The example above was
only illustrative. The next section shows example usage and comparisons.

\textcolor{red}{I recognise that this methodology section mixes both parts of
the theory and how to use it. It is written as if it is a bit theory and a bit
tutorial. I believe that by having a manual or a HOW-TO list in the SI that
shows all the options and how to use them in the code, this section should focus
on the theory and how it was implemented. I believe part of that is already
covered here, but not everything! I believe that this tutorial information could
be in another file (Manual or SI) Also, the results discussion section should go
beyond the "we tested so-and-so's reaction and our results were very close to
the experimental ones" . We should show the details, and the fact that if
certain corrections (like tunnelling) are omitted, the result can be worse or
better, that is, show the real capacity of the code, highlighting its potential,
and this can only be done with a detailed discussion of the cases studied.}

-->
