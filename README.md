# Cyclic Causal Inference (CCI)

CCI is a constraint-based algorithm for causal discovery with cycles, latent variables and/or selection bias. CCI feels like FCI, but CCI can handle cycles.

CCI discovers the maximal almost ancestral graph (MAAG) of some directed graph G, provided that the global Markov property and d-separation faithfulness holds according to G. Such properties are reasonable when G is the directed graph of an SEM-IE and linearity holds for example. 

Details: https://arxiv.org/abs/1805.02087

# Installation

The package depends on the MASS and pcalg packages on CRAN, so please install these first. Then:

> library(MASS)

> library(pcalg)

> library(devtools)

> install_github("ericstrobl/CCI")

> library(CCI)

# How to Use After the Install

The algorithm essentially runs like pc() in the pcalg package:

> DCG = generate_DCG_LE(15,2) #instantiate a directed cyclic graph with 15 vertices and on average 2 edges per node. Automatically includes 0-3 selection and 0-3 latent variables.

> sample_DCG = sample_DCG_LE(nsamps=1000, DCG) #generate Gaussian samples from the DCG

> suffStat=list() #all parameters needed by Fisher's z test

> suffStat$C = cor(sample_DCG);

> suffStat$n = 1000;

> G=cci(suffStat,gaussCItest,alpha=0.01,p=ncol(sample_DCG)) # run CCI

> cci$maag #print the recovered MAAG

