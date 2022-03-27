# How it works

**overreact** takes computational chemistry outputs as **data sources** and uses
them to calculate thermodynamic and kinetic properties as shown in the following
diagram.


```mermaid
graph TD
    class A,B,C,D,E,F,G,H,data,cond,hypo,init,pred normal

    data[/Data sources/] -.-> A[Free energy data <br> for all species];
    cond[/Conditions/] -.-> E;
    hypo[/Reaction hypotheses/] -.->|parser| G[Reaction network];
    init[/Initial concentrations/] -.-> D;
    cond -.-> A;

    subgraph inputs
        data
        cond
        hypo
        init
    end

    G --> F[Reaction rate laws] --> C[Reaction rate equations];
    A --> B[Free energy data for reactions];
    B --> E[Reaction rate constants] --> C --> D((ODE solver));
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

    D -.->|scipy| pred;
    pred -->|outputs| H[Kinetic predictions];


    pred[\Concentrations for all species as a function of time\]
```

**WARNING**: This above diagram greatly simplifies things. It is not a complete
description of the system and in no way substitutes the full read of the
upcoming paper.
