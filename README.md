# DEO Structure MCMC for sampling DAGs
 This repository contains a Jupyter notebook where functions for sampling DAGs (using a costumizable structure MCMC) are implemented. The sampler can use different types of parallel tempering schemes.

 ### Types of moves
The structure MCMC can use 3 different types of moves:
* MC3 move (adding, removing, reversing an edge)
* REV move (New Edge Reversal)
* MBR move (Markov Blanket Resampling)

### Different samplers
There are 4 different samplers in the notebook (3 involving different parallel tempering schemes and 1 simple structure MCMC without parallel tempering). The most efficient sampler is the DEO structure MCMC.  

### DEO structure MCMC function (example available in the notebook)
Tu run a structure MCMC using DEO (Deterministic Even Odd) parallel tempering scheme, call the function:
```
DEO_sampler= deo_structure_mcmc(...) 
```
The arguments of the function are:

```
n_variables_p: number of nodes of the network
max_parents_p: number of maximum parents per node
n_iter: number of iterations after the first tuning phase
cache: cache containing the local scores of the nodes for each parents set
training_iter: number of iterations for the first tuning phase (to find the optimal number of chains and optimal temperatures)
n_chains_p: starting number of chains (it has to be big enough otherwise an error is displayed)
prob_rev: probability of performing a REV move (recommended= 0.7)
prob_mbr: probability of performing a MBR move (recommended= 0.2)
seed: random seed
dynamic: if True the second tuning phase is not stopped (recommended= True)
geometric: if True the temperatures are not tuned and the number of chains remains equal to n_chains_p (recommended= False)
complete: set False to output only the DAGs, their scores, the final number of chains, the rejection ratio among chains and the temperatures
step_tune: the number of samples that are taken into account for the second tuning phase (to update only the temperatures)
n_tune: number of times the second tuning phase is performed (if dynamic== True then n_tune= inf)
uniform_p: if True the uniform prior is used, if False the sparse prior is used (uniform_p= False by default)
```

### Other samplers (less performing)
To run the SEO (Stochastic Even Odd scheme) structure MCMC call the function:
```
SEO_sampler= seo_structure_mcmc(...) 
```

To run a structure MCMC where, in the cummunication phase, only 1 random swap among chains is allowed:
```
single_swap_pt_sampler= rand_structure_mcmc(...) 
```

To run a simple structure MCMC without parallel tempering call the function:
```
no_pt_sampler= structure_mcmc(...) 
```

### Useful tips
The function
```
cache= cache_f(path,max_parents,n_nodes) 
```
uses a .jkl file as input (containing BDeu or BGe local scores). Those files can be easily generated, for discrete datasets, using [GOBNILP](https://jcussens.github.io/#Software). A list of datasets (some of them are artificially generated from reference networks) and their respective .jkl files can be found in the "data" folder.

Diagnostic functions are added at the end of the notebook (function to compute the score of a DAG, to compute the posterior probability of all the edges for a MCMC run, etc.). 
