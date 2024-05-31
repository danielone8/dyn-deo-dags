# DEO Structure MCMC for sampling DAGs
 This repository contains a jupyter notebook that contains functions for sampling DAGs using a costumizable structure MCMC that can use different types of parallel tempering algorithms.

 ### Types of move
The structure MCMC can use 3 different types of moves:
* MC3 move (add, remove, reversal of an edge)
* REV move (New Edge Reversal)
* MBR move (Markov Blanket Resampling)

### Different samplers
There are 4 different samplers in the notebook: 

### DEO structure MCMC without parallel tempering
Tu run a structure MCMC using DEO parallel tempering scheme call the function:
```
DAGs_sampler=deo_structure_mcmc() 
```
The arguments of the function are:

```
n_variables_p: number of nodes of the Network
max_parents_p: number of maximum parents per node
n_iter: number of iterations after the first tuning phase
cache: cache containing the local scores of the nodes
training_iter: number of iterations for the first tuning phase (to find optimal number of chains and temperatures)
n_chains_p: starting number of chains (it has to be big enough otherwise an error is displayed)
prob_rev: probability of performing a REV move (recommended= 0.7)
prob_mbr: probability of performing a MBR move (recommended= 0.2)
seed: random seed
dynamic: if True the second tuning phase is not stopped (recommended= True)
geometric: if True the temperatures are not tuned and the number of chains remains n_chains_p (recommended= False)
complete: set False to output only the DAGs, their scores, the final number of chains, the rejection ratio among chains, the temperatures
step_tune: the number of samples that are taken into account for the second tuning phase (to update only the temperatures)
n_tune: number of times the sceond tuning phase is performed (if dynamic== True, n_tune= inf)
uniform_p: if True the uniform prior is used, if False the sparse prior is used (uniform_p= False by default)
```