[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)


# carriercapture

![](https://github.com/WMD-group/carriercapture/blob/master/schematics/Logo.png)

A set of codes to compute carrier capture and recombination rates in semiconducting compounds. 
This topic has a rich history starting from the work by [Huang and Rhys](http://rspa.royalsocietypublishing.org/content/204/1078/406.short) in 1950. 
Our implementation was inspired by the approach (and FORTRAN code) employed by [Alkauskas and coworkers](https://journals.aps.org/prb/abstract/10.1103/PhysRevB.90.075202), but has been adapted
to also describe anharmonic potential energy surfaces. 

## Installation

The codes are written in [Julia](https://julialang.org), while the [Jupyter Notebooks](http://jupyter.org) also contain [Python](https://www.python.org), which are all assumed to be installed.

The [Brooglie](https://github.com/RedPointyJackson/Brooglie) package is used to solve the time-independent Schrödinger equation and can be installed by:

`Pkg.clone("https://github.com/RedPointyJackson/Brooglie")`  
`Pkg.add("Plots")`  
`Pkg.add("Arpack")`  
`Pkg.add("Polynomials")`  
`Pkg.add("CSV")`
`Pkg.add("DataFrames")`
`Pkg.add("LaTeXStrings")`
`Pkg.add("ArgParse")`
`Pkg.add("YAML")`
`Pkg.add("LsqFit")`

## Development

Development is in progress and hosted on [Github](https://github.com/WMD-group/carriercapture). 
Please use the [issue tracker](https://github.com/WMD-group/carriercapture/issues/) for feature requests, bug reports and more general questions. If you would like to contribute, please do so via a pull request.

## Usage

A typical usage will consist of about four steps, implemented in a series of short programs which may be run from the command line. Input for the calculations is provided in `input.yaml`.

1. Prepare a sequence of structures with displacements which interpolate between two defect states. Run single-point energy calculations on these structures, and extract the total energies. Scripts for preprocessing may be found in XXX

2. Generate configuration coordinate diagrams with polynomial fits to the data (`GetPotential.jl`). Solve these potential energy surfaces for the phonon wavefunctions for each defect.

<center>
<img src="example_GaAs/cc_example_labelled_potentials.png" width="400" />
</center>

3.  Calculate the overlap between phonons in the donor and acceptor potentials to give the capture coefficient for a given temperature range (`GetRate.jl`)

4. Calculate the lifetimes and rates for a given defect 

## Theory

The capture of electrons or holes by point defects in a crystalline materials requires the consideration of a number of factors, which include:

## Limitations

The expected use case for this code is to ... 

## Examples

The following examples are provided to illustrate some of the applications of these codes:

* GaAs defect (./example_GaAs) 


### Electronic matrix elements

> The electronic matrix element frequently causes feelings of discomfort (Stoneham, 1981)

The capture coefficient between an initial and final state for this computational set up is given by (eq. 22 in [Alkauskas and coworkers](https://journals.aps.org/prb/abstract/10.1103/PhysRevB.90.075202))

<a href="https://www.codecogs.com/eqnedit.php?latex=C_p&space;=&space;V&space;\frac{2\pi}{\hbar}&space;g&space;W_{if}^2&space;\sum_m&space;w_m&space;\sum_n&space;|\langle&space;\xi_{im}|&space;Q&space;-&space;Q_0&space;|&space;\xi_{fn}\rangle|^2&space;\delta(\Delta&space;E&space;&plus;&space;m\hbar\Omega_i&space;-n\hbar\Omega_f)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?C_p&space;=&space;V&space;\frac{2\pi}{\hbar}&space;g&space;W_{if}^2&space;\sum_m&space;w_m&space;\sum_n&space;|\langle&space;\xi_{im}|&space;Q&space;-&space;Q_0&space;|&space;\xi_{fn}\rangle|^2&space;\delta(\Delta&space;E&space;&plus;&space;m\hbar\Omega_i&space;-n\hbar\Omega_f)" title="C_p = V \frac{2\pi}{\hbar} g W_{if}^2 \sum_m w_m \sum_n |\langle \xi_{im}| Q - Q_0 | \xi_{fn}\rangle|^2 \delta(\Delta E + m\hbar\Omega_i -n\hbar\Omega_f)" /></a>

Here, *V* is the volume of the supercell, *W<sub>if</sub>* is the electron-phonon overlap and *ξ<sub>im</sub>* and *ξ<sub>fn</sub>* describe the wavefunctions of the *m<sup>th</sup>* and *n<sup>th</sup>* phonons in the initial *I* and final *f* states. The delta function term serves to conserve energy and in practice is replaced by a smearing Gaussian of finite width *σ*.

## Extended Reading List

* [Heny and Lang, Nonradiative capture and recombination by multiphonon emission in GaAs and GaP (1977)](https://journals.aps.org/prb/pdf/10.1103/PhysRevB.15.989) **Seminal contribution that introduces many concepts**

* [Huang, Adiabatic approximation theory and static coupling theory of nonradiative transition (1981)](http://engine.scichina.com/doi/10.1360/ya1981-24-1-27) **Useful context for the static approximation**

* [Stoneham, Non-radiative transitions in semiconductors (1981)](http://iopscience.iop.org/article/10.1088/0034-4885/44/12/001/meta) **Review on models and theory**

* [Markvart, Determination of potential surfaces from multiphonon transition rates (1981)](http://iopscience.iop.org/article/10.1088/0022-3719/14/15/002) **Treatment of anharmonicity**

* [Markvart, Semiclassical theory of non-radiative transitions (1981)](http://iopscience.iop.org/article/10.1088/0022-3719/14/29/006/meta) **Semiclassical treatment of matrix elements following Landau and Holstein**

## TODO

Using [DifferentialEquations.jl](https://github.com/JuliaDiffEq/DifferentialEquations.jl) rather than Brooglie

