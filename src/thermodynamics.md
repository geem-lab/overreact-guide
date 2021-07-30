# How it works

**overreact** takes computational chemistry outputs as **data sources** and uses them to calculate thermodynamic and kinetic properties as shown in the following diagram.

<!-- Currently, overreact only supports quantum chemistry outputs.
In the future we might get data from actual experiments, databases or using machine learning. -->

```mermaid
graph TD;
    A[Data sources] --> B[Free energy data for all species];
    X[Reaction hypotheses] --> Y[Reaction network]
    Y --> D[Reaction rate equations];
    B --> C[Free energy data for reactions];
    Y --> C;
    Z[Initial concentrations] --> E;
    D --> E{ODE solver};
    C --> J[Reaction rates];
    I[Conditions] --> J;
    J --> E;
    E --> F[Concentrations for all species as a function of time];
    F --> G[Kinetic predictions];
```

<!-- G -> X; -->

**Conditions** include temperature.

<!-- , pressure, and any other conditions that might be used in a simulation -->

Free energy data for reactions allow us to calculate reaction rates as `k(T, p)`.

Reaction rate equation laws are calculated using the **reaction rate equations** and are of the form `dy/dt(y)`.

Initial concentrations are given by the user as `y0[i]`.

**Concentrations for all species** are calculated using the **ODE solver** and are of the form `y[i, t]`.

The dictionary is then used to generate a plot.

The goal is to provide a tool for calculating thermodynamic properties of chemical systems.

By comparing calculated properties and kinetic predictions with actual experimental data, we refine our **hypotheses**.

## Notes about thermodynamics

overreact employs standard statistical thermodynamical partition functions (the
Rigid Rotor Harmonic Oscillator), but also two Quasi-Rigid Rotor Harmonic
Oscillator approximations, one for entropy and one for enthalpy, for when
vibrational frequencies are too small.

A Head-Gordon damping is used for the treatment of QRRHO, which ensures the
standard procedure is used for frequencies well above
:math:`100 \text{cm}^{-1}`.

See the treatments for entropy and enthalpy in the Jupyter Notebook about
QRRHO (TODO(schneiderfelipe): add link).%
