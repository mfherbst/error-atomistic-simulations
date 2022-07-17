# Overview of error sources in first-principle modelling

## General errors
Errors, which apply to all parts of a simulation.

1. **Arithmetic error**: Error due to finite precision of the floating-point / integer arithmetic
  - Usually rounding errors
2. **Hardware error**: Spontaneous failure / inconsistencies inside computer hardware
  - Examples: Random bit flips in main memory, bugs in CPU instructions
  - Cannot be neglected in exascale architectures (DOI 10.1177/1094342014522573)
3. **Programmer error**:
  - Algorithms not correctly implemented

It is hard to treat 2. and 3. systematically,
so it seems fair to generally neglect these error sources.

## Electronic structure simulation
<a name="dft" />

Discussed following the example of a density-functional theory (DFT) calculation.
See also the discussion in DOI 10.1039/d0fd00048e.

- **Model error**: Error due to the choices made with respect to the considered
  physical model, which treats some effects and neglects others (e.g. relativistic
  effects, vacuum fluctuations, ...). Examples:
  - Difference of a selected Kohn-Sham DFT model (LDA, PBE, SCAN) versus the exact
    $n$-body electronic Schrödinger equation *at the continuous level*.
  - Choice of XC functional
  - Choice of pseudopotential model / PAW setup
  - Problem reduction from the physics one is actually interested in:
    Finite size effects, selection of QM region (in QM/MM setups),
    replacement of functional groups, neglect of defects
  - Smearing (seen as a physical temperature)
- **Discretisation error**: Error obtained by projecting the continuous PDE into a
  finite-dimensional non-linear problem. Examples:
  - $k$-point sampling, Brillouin zone (BZ) quadrature (e.g. Tetrahedron method)
  - Smearing (seen as a computational technique for BZ sampling)
  - Basis selection and projection onto finite basis
- **Algorithm error**: Error due to the numerical technique used to solve
  the discretised problem. Examples:
  - Finite convergence thresholds in eigensolver, finite SCF convergence threshold
  - Settings of the optimisation routine (e.g. direct minimisation, geometry optimisation)
  - Hellman-Feynman mismatch (e.g. because of not yet having fully reached the stationary point in an SCF):
    E.g. forces are not the derivatives of the energy to machine precision
  - Choice of initial guess
  - Error induced by using randomised linear algebra

## Statistical learning and surrogatisation
<a name="potentials" />

For example the generation of interatomic potentials from DFT data.
In that case the targeted quantity of interest (QoI) are the DFT forces.
Typical surrogate models are based on a statistical fit
(e.g. linear regression, Gaussian process regression, neural networks)
on top of a featurisation technique like ACE, SOAP, ...

- **Model error**: Difference between the predictions made by a theoretical best fit
  of the chosen surrogate model for the targeted QoI and the QoI obtained at the level
  of the reference data. This error is defined with respect to taking an
  infinitely large training set composed of exact ground truth data (i.e. no
  discretisation error, exact solution to the electronic Schrödinger equation).
  Examples:
  - All details of the featurisation as well as the statistical surrogate model
  - Finite locality of the descriptor (e.g. cutoff radii for SOAP)
  - Incompleteness of descriptors (e.g. only 3-body terms used)
  - Truncation of (radial) basis
  - Weight assignment (if weights amongst the training data is assigned a priori)
  - Regularisation techniques (e.g. Gaussian random noise term, Tikhonov)
  - Maybe a better name could be **surrogatisation error** ?
- **Reference data error**: Combined error of the provided reference data
  (e.g. DFT or similar simulations, experimental data), including resulting
  inconsistencies or biases. Examples:
  - Biases from the computational setup used to generate the data,
    e.g. if the same $k$-point mesh / kinetic energy cutoff is used across a big data
    set for a plane-wave DFT simulation, not all data points are obtained to equal
    accuracy as different discretisation parameters might be required for each simulated
    system to obtain the same accuracy. Most importantly this can introduce subtle biases
    in the reference data itself.
  - Inconsistencies due to the chosen first-principle model deviating from the exact
    Schrödinger equation
  - Similar considerations apply to all aspects mentioned [in the section above](#user-content-dft).
  - Usage of heterogeneous data sources (with different accuracy, level of reliability)
- **Sampling error on training set**: Error in the selection of the training set. Examples:
  - Choosing a training set, which is not representative of the targeted problem
- **Fitting error**: Collection of all errors induced by the fitting process itself.
  Analogue of the "algorithm error" [in electronic stucture calculations](#user-content-dft). Examples:
  - Linear algebra / algorithm to solve least-squares problem
  - Stochastic optimisation routine for neural-network models
  - Weight assignment (if weights determined by fit)


## Property prediction from atomistic simulations
*TODO This section needs extension / polishing*

- **Potential error**: [See discussion above](#user-content-potentials)
- **Sampling error**:
    - finite MD trajectory size
    - finite points for E-V curve
- **Analogy error**:
    - Sampling a mismatching ensemble for the targeted physical conditions
      (e.g. sampling micro-canonical versus canonical ensemble)
    - Property deduced from the simulation is not the measured physical property
    - Neglect of nuclear quantum effects
    - Thermostat / barostat setup

### Equilibrium properties
- Sampling

### Dynamical properties
- Sampling
- Model for observable
