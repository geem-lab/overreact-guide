# How it works

**overreact** takes computational chemistry outputs as **data sources** and uses
them to calculate thermodynamic and kinetic properties as shown in the following
diagram.

```mermaid
graph TD;
    classDef normal font-variant:small-caps;
    classDef valuable font-variant:small-caps,fill:#9AC4F8;
    class A,B,C,D,E,F,G,H,data,cond,hypo,init,pred normal;

    data[/Data sources/]:::normal -.-> A[Free energy data <br> for all species]:::normal;
    cond[/Conditions/]:::normal -.-> E;
    hypo[/Reaction hypotheses/]:::normal -.-> G[Reaction network]:::normal;
    init[/Initial concentrations/]:::normal -.-> D;
    cond -.-> A;

    subgraph inputs
        data
        cond
        hypo
        init
    end

    G --> F[Reaction rate laws]:::normal --> C[Reaction rate equations]:::normal;
    A --> B[Free energy data <br> for reactions]:::valuable;
    B --> E[Reaction rate constants]:::valuable --> C --> D((ODE solver)):::normal;
    G --> B;

    subgraph overreact
        A
        B
        C
        D
        E
        F
        G
    end

    D -.-> pred[\Concentrations for all species <br> as a function of time\]:::normal;
    pred ==> H[Kinetic predictions]:::normal;

    subgraph outputs
        pred
    end
```

**WARNING**: This above diagram greatly simplifies things. It is not a complete
description of the system and in no way substitutes the full read of the
upcoming paper.
