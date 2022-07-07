# General errors (apply to everything)
- **arithmetic error**:
    - error due to finite floating-point precision in the computer
- **hardware error**:
    - spontaneous failure / inconsistencies inside computer hardware
- **programmer error**:
    - Algorithms not correctly implemented

# Single-point DFT calculation
- **model error**:
    - Physicist's modelling choices
    - finite size effect, problem reduction from physics one is actually interested in
    - Smearing (seen as a physical temperature)
    - difference of exact n-body electronic schrödinger equation to Kohn-Sham model (but at the continuous level)
    - pseudopotential error, XC functional choice, 
- **discretisation error**: Error obtained by projecting the continuous PDE into a finite-dimensional non-linear problem (so this is both basis discretisation and k-point discretisation, quadrature error, )
    - Smearing (seen as a computational technique for BZ sampling)
- **algorithm error**:
    - finite convergence threshold
    - forces are not the derivatives of the energy to machine precision
    - randomised linear algebra?
    - Choice of initial guess
    - Settings of the optimisation routine

# Potential generation errors
- **Errors in reference data**:
    - Inconsistency and biases in the reference data (i.e. the DFT data or similar provided)
        - data or setup (same k-point sampling / Ecut across big data set, which are differently well converged)
        - Heterogeneous data sources
    - Errors due to XC model etc (see above)
- **Sampling error on training set**:
    - Error in selection of the training set, not representatitve to actual problem
- **Model error**:
    - Error in predictions between best fit of model to the reference data
    - Statistical model to predict the qoi
    - Finite locality of the descriptor
    - Truncation of (radial) basis
    - Regularisation techniques
    - Incompleteness of descriptors (3-body)
    - defined with respect to infinite training set
    - Weight assignment (if weights assigned a priori)
- **Fitting error**: (a bit like algorithm error for DFT)
    - "Error induced from the fitting process", e.g. stochastic optimisation processes
    - Weight assignment (if weights determined by fit)

# Properties from atomistic simulations
- **Potential error**:
    - all the above
- **sampling error**:
    - finite MD trajectory size
    - finite points for E-V curve
- **analogy error**:
    - sampling the wrong ensemble compared to what would be needed for physical property
    - property deduced from the simulation is not the measured physical property
    - Neglect of nuclear quantum effects
    - thermostat error / barostat error

## Equilibrium properties
- sampling

## Dynamical properties
- sampling
- model for observable
