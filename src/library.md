# Getting started with **overreact** as a library

🎯 **overreact also has a detailed API documentation**, which you can read
[here](https://geem-lab.github.io/overreact/overreact.html).

Here is an overview of **overreact**'s capabilities as a
[Python](https://www.python.org/) library. **overreact** allows you to build any
thinkable reaction model:

```python
>>> import overreact as rx
>>> from overreact import constants
>>> scheme = rx.parse_reactions("S -> E‡ -> S")
>>> scheme
Scheme(compounds=('S', 'E‡'),
       reactions=('S -> S',),
       is_half_equilibrium=(False,),
       ...)
```

The `‡` symbol is used to indicate transition states (but the `#` symbol is also
accepted). Many different reactions can be specified at the same time by
properly giving a list. Equilibria are recognized as having `<=>`. Reactions
preserve the order they appeared in the input.

Similarly, compound data is retrieved from logfiles using `parse_compounds`:

```python
>>> compounds = rx.parse_compounds({
...     "S": "data/ethane/B97-3c/staggered.out",
...     "E‡": "data/ethane/B97-3c/eclipsed.out"
... })
>>> compounds
{'S': {'logfile': 'data/ethane/B97-3c/staggered.out',
       'energy': -209483812.77142256,
       ...},
'E‡': {'logfile': 'data/ethane/B97-3c/eclipsed.out',
       'energy': -209472585.3539883,
       ...}}
```

After both two line above, we can start analyzing our complete model:

```python
>>> rx.get_k(scheme, compounds)
array([8.16e+10])
```

Even with a rather simple level of theory
([B97-3c](https://doi.org/10.1088/1361-648X/aabcfb)), this result compares well
with the
[experimentally determined value (\\( 8.3 \times 10^{10} \text{s}^{-1} \\))](https://doi.org/10.1126/science.1132178).

<!-- This small error of is due to the very accurate
thermochemical and tunneling corrections employed. -->

The line above works by calculating internal energies, enthalpies and entropies
for each compound, but you can do this in separate lines as well. In fact, in
any temperature:

```python
>>> rx.get_internal_energies(compounds) # 298.15 K by default
array([-2.09280338e+08, -2.09271131e+08])
>>> rx.get_internal_energies(compounds, temperature=400.0)
array([-2.09275396e+08, -2.09266995e+08])
```

Values are always in joules per mole and honor the original order of compounds,
as they were initially given. The same thing can be done for enthalpies and
entropies (in joules per mole per kelvin):

```python
>>> temperature = 300.0
>>> enthalpies = rx.get_enthalpies(compounds, temperature=temperature)
>>> enthalpies
array([-2.092778e+08, -2.092686e+08])
>>> entropies = rx.get_entropies(compounds, temperature=temperature)
>>> entropies
array([227.9, 221.9])
```

Now free energies are easy, we just use full power of NumPy arrays:

```python
>>> freeenergies = enthalpies - temperature \* entropies
>>> (freeenergies - freeenergies.min()) / constants.kcal
array([0. , 2.63129486])
```

In the above, we calculated free energies relative to the minimum.

More code examples of using **overreact** as a library are given in the
[`notebooks`](https://github.com/geem-lab/overreact-guide/tree/master/notebooks)
folder. A more detailed description of the available code examples is given
[next](notebooks.md).
