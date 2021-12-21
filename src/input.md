# Command-line input format specification

**overreact** is both a library and a command-line application. In this
subsection, we briefly describe the minimal input specification for the
command-line application for doing first-principles microkinetic simulations.
Don't worry, the input is very simple, yet flexible.

<!-- TODO: cite this docs in the paper: "Further guidance and advanced usage information is available in the online documentation (\hrefdoc)". -->

Basically, **overreact** parses complex reaction schemes with the help of a
[domain-specific language (DSL)](https://en.wikipedia.org/wiki/Domain-specific_language)
designed to be as flexible and intuitive as possible to any chemist. For
instance, as a purely illustrative example, the following
[Curtin-Hammett system](https://en.wikipedia.org/wiki/Curtin%E2%80%93Hammett_principle)

<!-- CITE 10.1021/jo00404a002 ? -->

\\[ \require{mhchem} \ce{ P\_{A}(w) <- [A(w)]^{\ddagger} <- A(w) <=> B(w) ->
[B(w)]^{\ddagger} -> P\_{B}(w) } \\]

could be modelled very easily as follows (saved, say, in a `curtin_hammett.k`
file):

```
// This is a comment and is ignored by overreact.

$scheme
 // Here we define our reactions.
 A(w) <=> B(w)
 A(w) -> A‡(w) -> P_A(w)
 B(w) -> B‡(w) -> P_B(w)
$end

$compounds
 // Here we specify the files for all species.
 A(w):   A@water.out
 B(w):   B@water.out
 A‡(w):  A_TS@water.out
 B‡(w):  B_TS@water.out
 P_A(w): P_A@water.out
 P_B(w): P_B@water.out
$end
```

## Some things to note

-   `//` indicates a **comment**. They are ignored until the end of the line.
-   **Blank lines** are also ignored.
-   Two **blocks** are required: the `$scheme` block and the `$compounds` block.
-   `$end` indicates the **end of a block**. It is optional: opening a new block
    closes the previous one.
-   **Compound labels** are case-sensitive. They must start with a letter but
    can contain any character except spaces. _Labels in the `$scheme` block
    should match the ones in `$compounds`_.
-   **Stoichiometric coefficients** are specified as multipliers in front of the
    compound labels, e.g. `2 * A(w)`, `3 * A(w)`, etc.. `A(w)` actually is
    equivalent to `1 * A(w)`.
-   `->` means a **forward reaction** (listing first reactants, then products).
-   `<-` means a **backward reaction** (listing first products, then reactants).
-   `<=>` means an **equilibrium**. They are useful when one does not want
    separately model both forward and backward reactions. _Equilibria are
    assumed to be much faster than any other reaction in the scheme_.
-   `‡` indicates a **transition state**. _It is considered part of the compound
    label_. You can also use the easier-to-type `#` instead. That is, `A#(w)` is
    means the same thing as `A‡(w)`.
-   `(w)` indicates a **solvated context**. _It is considered part of the
    compound label_. It is used to identify whether a concentration correction
    should be applied. The default is `(g)`, which is understood as gas phase.
    _The actual string is currently ignored_: we could have written `A(aq)`,
    `A(l)` or even `A(dcm)` instead, with the same effect. _We might use solvent
    information in the future_.
-   **Paths to files** are relative to the directory where the model file is
    located.
-   The **order** of the species in the `$compounds` block is not important. The
    same applies to the order of the reactions in the `$scheme` block.

## Multiple reactions in a single line

We can get even closer to the original chemical notation, as **overreact**
accepts multiple reactions in a single line. As such, the following is a
`$scheme` block equivalent to the one above:

```
$scheme
 P_A(w) <- A‡(w) <- A(w) <=> B(w) -> B‡(w) -> P_B(w)
$end
```

## Some ilustrative examples

1. A simple model for the
   [synthesis of ammonia](https://en.wikipedia.org/wiki/Haber_process):

```
$scheme
 // Synthesis of ammonia (notice how flexible the DSL is)
 3 * H2(g) + N2(g) -> TS#(g) -> 2 * NH3(g)

$compounds
 // Paths to the files for the species (notice $end is optional)
 H2(g):  h2.out
 N2(g):  n2.out
 TS#(g): ts.out
 NH3(g): nh3.out
```

2. A simple
   [Michaelis-Menten](https://en.wikipedia.org/wiki/Michaelis%E2%80%93Menten_kinetics)-like
   scheme (with
   [competitive inhibition](https://en.wikipedia.org/wiki/Competitive_inhibition)):

```
$scheme
 // A simple Michaelis-Menten-like scheme
 C(aq) + S(aq) <=> CS(aq) -> CS‡(aq) -> C(aq) + P(aq)  // C(aq) is the catalyst

 // The inactivation of the catalyst is modeled as competitive inhibition
 C(aq) + I(aq) <=> CI(aq)
$end

$compounds
 C(aq):   c.out
 S(aq):   s.out
 CS(aq):  cs.out
 CS‡(aq): cs_ts.out
 P(aq):   p.out

 // Inactivation
 I(aq):   i.out
 CI(aq):  ci.out
$end
```
