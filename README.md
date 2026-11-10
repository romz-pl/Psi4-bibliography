# Psi4 Quantum Chemistry Package

## What Psi4 Is

**[Psi4](https://psicode.org/)** is a free, open-source suite of ab initio electronic structure programs. "Ab initio" means the calculations start from the fundamental equations of quantum mechanics rather than from empirical parameters. Psi4 is designed for the efficient, high-accuracy simulation of molecular energies, geometries, and properties. It is distributed under the GNU Lesser General Public License v3 (LGPL-3.0) and is developed on [Psi4 GitHub](https://github.com/psi4/psi4).

Its defining characteristic is its architecture: a computational core written in C++ that is driven by a native Python layer. This hybrid design lets users write short, readable input files for routine work while also scripting complex, multi-step workflows in Python, and it lets developers add new methods without rewriting the whole program.

Psi4 is the successor to the original PSI program family, which was developed by the research group of [Henry F. Schaefer III](https://en.wikipedia.org/wiki/Henry_F._Schaefer_III). Primary development of Psi4 is currently carried out by research groups led by David Sherrill (Georgia Tech) and T. Daniel Crawford (Virginia Tech), together with a broad community of contributors.

## Scientific Scope

Psi4 covers a wide range of electronic structure methods:

Wavefunction methods include Hartree-Fock (HF) self-consistent field theory, configuration interaction (CI), and coupled-cluster theory, including CCSD and CCSD(T), along with equation-of-motion (EOM) variants for excited states. Many-body perturbation theory, notably Møller-Plesset perturbation theory (MP2 and higher orders), is available, as are multiconfigurational methods such as CASSCF. Density cumulant theory and symmetry-adapted perturbation theory (SAPT) for intermolecular interactions are also implemented.

Density functional theory (DFT) is a major component. Psi4 supports a large library of exchange-correlation functionals, including hybrid and range-separated functionals, through its integration with the Libxc library, along with dispersion corrections and time-dependent DFT for excited-state calculations.

Properties and analyses include molecular gradients and geometry optimization, harmonic vibrational frequencies, population analyses, electric and magnetic properties, and spectroscopic quantities. Relativistic corrections are supported through the exact two-component (X2C) approach.

Solvation and environment effects can be modeled through implicit solvent approaches, including the PCMSolver library for the polarizable continuum model and the DDX library, which has been integrated for linear response and time-dependent SCF calculations.

## Key Technical Features

### Basis Sets and Integrals

Psi4 ships with an extensive library of Gaussian basis sets, including the Pople, Dunning correlation-consistent (cc-pVXZ and aug-cc-pVXZ), and Karlsruhe def2 families, plus many specialized sets. Integral evaluation relies on the [Libint library](https://github.com/evaleev/libint), which is a standard in the field. Psi4 has also introduced the density-fitting approximation across many parts of the code, which substantially reduces computational cost and input/output demands.

### Numerical Acceleration

Beyond density fitting, Psi4 incorporates Cholesky decomposition of the electron repulsion integrals and Laplace-transformed energy denominators, both of which lower the cost of correlated calculations. Its design also emphasizes memory and disk management so that large calculations can run on typical research clusters.

### Automation

A major theme of recent development is automation of multi-step protocols. The program can perform geometry optimizations using complete-basis-set (CBS) extrapolation, and it supports focal-point analysis, a technique for approaching high-accuracy reference energies by combining results from different levels of theory and basis sets. These workflows, which used to require hand-written scripts, can now be expressed in a few lines of input.

### Python Integration

Because the top-level driver is a Python module, Psi4 can be imported and used alongside libraries such as NumPy, SciPy, and the wider scientific Python ecosystem. This makes it practical to build custom analyses, feed results into machine-learning pipelines, or interface with other simulation tools. The Psi4NumPy project provides educational and reference implementations of quantum chemistry methods in pure Python, which are useful for both teaching and prototyping.

### Distributed Computing

A rewrite of the top-level computation driver, combined with adoption of the MolSSI QCArchive infrastructure, makes Psi4 well suited to distributed computing. Large numbers of independent calculations, such as screening thousands of molecules, can be dispatched across clusters and their results collected in a central database.

## Input Format

Psi4 accepts a concise, Python-like input language. A typical input file defines a molecule, sets options, and calls an energy, gradient, or property function:

```
molecule {
  O
  H 1 0.96
  H 1 0.96 2 104.5
}

set basis def2-svp
energy('pbe0')
```

The same calculation can be written as a full Python script that imports the psi4 module, which is preferable when results need to be post-processed or combined with other code.

Psi4 also builds on the molecular-geometry conventions common to chemistry software, supports Z-matrix and Cartesian coordinates, and handles symmetry detection automatically.

## Installation and Platforms

Psi4 is available through several channels: conda binary packages from conda-forge (the most common route for end users), Docker images, and source builds using CMake. The project supports Linux and macOS, and Windows users typically run it through WSL or a container. Build dependencies include libint, libxc, and the BLAS and LAPACK libraries, and the project documentation provides a build assistant to help with dependency management.

Version history matters when choosing a release. Version 1.1 marked a major overhaul that converted the top-level code to a Python module, rewrote the build system, and added automated CBS and focal-point workflows. Later releases added features such as implicit solvation support in linear response via DDX and C++20 compliance of the API. The most recent release I could confirm is version 1.9.1 (February 2024), so check the GitHub releases page for anything newer before relying on specific version details.

## Relationship to Other Software

Psi4 is often compared with several other open-source and commercial codes. Compared with PySCF, another Python-based package, Psi4 offers a more "black-box" interface with input-file workflows and a broad set of ready-made high-level methods, whereas PySCF is more of a toolkit oriented toward tensor-level control, including periodic and solid-state calculations. Compared with ORCA, a widely used commercial-friendly program, Psi4 provides a native Python API and open-source transparency, while ORCA offers highly optimized local correlation methods such as DLPNO-CCSD(T), which Psi4 does not match in that specific area (Psi4 does offer DLPNO-MP2).

Psi4 is also the preferred quantum chemistry backend for the OpenFermion project, which connects quantum chemistry calculations to quantum computing. This has made it a common choice in research on quantum algorithms for chemistry, where classical reference data and molecular Hamiltonians are needed.

## Strengths and Limitations

Among its strengths, Psi4 is free and open source, has a well-documented and actively maintained codebase, offers a broad method set in one package, and integrates cleanly with modern Python workflows. Its focus on automation and distributed computing suits high-throughput research.

Its limitations include a smaller user community than some commercial packages, less specialized performance for certain very large systems compared with codes tuned for massively parallel supercomputers, and a more limited suite of solid-state and periodic-boundary methods than dedicated periodic codes provide.

## Summary

Psi4 combines a high-performance C++ core with a flexible Python interface, covering Hartree-Fock, density functional, perturbation, coupled-cluster, and multiconfigurational methods, together with properties, solvation models, and automated composite workflows. Its open-source license, Python integration, and support for distributed computing make it a strong choice for academic research, method development, and high-throughput chemistry, as well as a practical backend for quantum computing research.

Before using Psi4 in a project, consult the official manual at psicode.org and the GitHub repository for the current version, supported features, and installation instructions.


## Bibliography

## 2023

+ Jha, A., Nottoli, M., Mikhalev, A., Quan, C., Stamm, B. **Linear scaling computation of forces for the domain-decomposition linear Poisson–Boltzmann method**, [J. Chem. Phys. 158, 104105 (2023)]( https://doi.org/10.1063/5.0141025).

+ Luu, D. and Patkowski, K. **Overcoming Artificial Multipoles in Intramolecular Symmetry-Adapted Perturbation Theory**, [J. Phys. Chem. A 127, 356-377 (2023)](https://doi.org/10.1021/acs.jpca.2c06465).

+ Müller, M., Hansen, A., and Grimme, S. **ωB97X-3c: A composite range-separated hybrid DFT method with a molecule-optimized polarized valence double-ζ basis set**, [J. Chem. Phys. 158, 014103 (2023)](https://doi.org/10.1063/5.0133026).


## 2022

+ Xie, Y., Smith, D. G. A., and Sherrill, C. D. **Implementation of symmetry-adapted perturbation theory based on density functional theory and using hybrid exchange–correlation kernels for dispersion terms**, [J. Chem. Phys., 157, 024801 (2022)]( https://doi.org/10.1063/5.0090688).

+ Behnle, S. and Fink, R. F. **UREMP, RO-REMP, and OO-REMP: Hybrid perturbation theories for open-shell electronic structure calculations**, [J. Chem. Phys. 156, 124103 (2022)](https://doi.org/10.1063/5.0081285)

## 2021

+ Schriber, J. B., Sirianni, D. A., Smith, D. G. A., Burns, L. A., Sitkoff, D., Cheney, D. L., Sherrill, C. D. **Optimized damping parameters for empirical dispersion corrections to symmetry-adapted perturbation theory**, [J. Chem. Phys. 154, 234107 (2021)](https://doi.org/10.1063/5.0049745).

+ Waldrop, J. M. and Patkowski, K. **Nonapproximated third-order exchange induction energy in symmetry-adapted perturbation theory*, [J. Chem. Phys. 154, 024103 (2021)](https://doi.org/10.1063/1.4994190).

+ Behnle, S. and Fink, R. F. **OO-REMP: Approaching Chemical Accuracy with Second-Order Perturbation Theory**, [J. Chem. Theory Comput. 17, 3259 (2021)](https://doi.org/10.1021/acs.jctc.1c00280).

+ Grimme, S., Hansen, A., Ehlert, S., and Mewes, J.-M. **r^2SCAN-3c: A “Swiss army knife” composite electronic-structure method**, [J. Chem. Phys. 154, 064103 (2021)](https://doi.org/10.1063/5.0040021)


## 2020

Lehtola, S. Phys. Rev. A. 101, 012516 (2020). https://doi.org/10.1103/PhysRevA.101.012516

Lehtola, S. Phys. Rev. A. 101, 032504 (2020). https://doi.org/10.1103/PhysRevA.101.032504

Lehtola, S. J. Chem. Phys. 152, 134108 (2020). https://doi.org/10.1063/1.5144964

Lehtola, S., Visscher, L., and Engel, E. J. Chem. Phys. 152, 144105 (2020). https://doi.org/10.1063/5.0004046

Herbst, M. F., Scheurer, M., Fransson, T., Rehn, D. R., and Dreuw, A. WIREs Comput. Mol. Sci., (2020) DOI: 10.1002/wcms.1462, Preprint https://adc-connect.org/q/publications

Smith, D. G. A., Burns, L. A., Simmonett, A. C., Parrish, R. M., Schieber, M. C., Galvelis, R., Kraus, P., Kruse, H., Di Remigio, R., Alenaizan, A., James, A. M., Lehtola, S., Misiewicz, J. P., Scheurer, M., Shaw, R. A., Schriber, J. B., Xie, Y., Glick, Z. L., Sirianni, D. A., O'Brien, J. S., Waldrop, J. M., Kumar, A., Hohenstein, E. G., Pritchard, B. P., Brooks, B. R., Schaefer, H. F., Sokolov, A. Yu., Patkowski, K., DePrince, A. E., Bozkaya, U., King, R., Evangelista, F. A., Turney, J. M., Crawford, T. D., and Sherrill, C. D. "PSI4 1.4: Open-source software for high-throughput quantum chemistry." J. Chem. Phys. 152, 184108 (2020). https://doi.org/10.1063/5.0006002

Bozkaya, U. J. Chem. Phys. 153, 244115 (2020). https://doi.org/10.1063/5.0035811

## 2019

Nottoli, M., Stamm, B., Scalmani, G., Lipparini, F. J. Chem. Theory Comput. 15, 6061 (2019).

Lehtola, S. J. Chem. Theory Comput. 15, 1593 (2019). https://doi.org/10.1021/acs.jctc.8b01089

Lehtola, S. J. Chem. Phys. 151, 241102 (2019). https://doi.org/10.1063/1.5139948

Lehtola, S. Int. J. Quantum Chem. 119, e25945 (2019). https://doi.org/10.1002/qua.25945

Houck, S. E. and Mayhall, N. J. J. Chem. Theory Comput. 15, 2278-2290 (2019).

Caldeweyher, E., Ehlert, S., Hansen, A., Neugebauer, H., Spicher, S., Bannwarth, C., and Grimme, S. "A generally applicable atomic-charge dependent London dispersion correction." J. Chem. Phys. 150, 154122 (2019). https://doi.org/10.1063/1.5090222

Behnle, S. and Fink, R. F. "REMP: A hybrid perturbation theory providing improved electronic wavefunctions and properties." J. Chem. Phys. 150, 1241077 (2019). https://doi.org/10.1063/1.5086168

## 2018

Patkowski, K., Zuchowski, P. S., and Smith, D. G. A. J. Chem. Phys. 148, 164110 (2018).

Laqua, H., Kussmann, J., and Ochsenfeld, C. J. Chem. Phys. 149, 204111 (2018).

Norman, P., Ruud, K., and Saue, T. "Principles and Practices of Molecular Properties: Theory, Modeling, and Simulations." John Wiley & Sons, 2018.

Smith, D. G. A., Burns, L. A., Sirianni, D. A., et al. "PSI4NUMPY: An Interactive Quantum Chemistry Programming Environment for Reference Implementations and Rapid Development." J. Chem. Theory Comput. 14, 3504-3511 (2018).

Bozkaya, U. J. Comput. Chem. 39, 351-360 (2018). https://doi.org/10.1002/jcc.25122

Brandenburg, J. G., Bannwarth, C., Hansen, A., and Grimme, S. J. Chem. Phys. 148, 064104 (2018). https://doi.org/10.1063/1.5012601

## 2017

McGibbon, R. T., Taube, A. G., Donchev, A. G., Siva, K., Hernández, F., Hargus, C., Law, K. H., Klepeis, J. L., Shaw, D. E. J. Chem. Phys. 147, 161725 (2017).

Thompson, T. H. and Ochsenfeld, C. J. Chem. Phys. 147, 144101 (2017). https://doi.org/10.1063/1.4994190

Bozkaya, U. and Sherrill, C. D. J. Chem. Phys. 147, 044104 (2017). https://doi.org/10.1063/1.4994918

## 2016

Gonthier, J. F. and Sherrill, C. D. J. Chem. Phys. 145, 134106 (2016).

Smith, D. G. A., Burns, L. A., Patkowski, K., and Sherrill, D. J. Phys. Chem. Lett. 7, 2197-2203 (2016).

Stamm, B., Cancès, E., Lipparini, F., Maday, Y. J. Chem. Phys. 144, 054101 (2016).

Wang, L.-P. and Song, C. J. Chem. Phys. 144, 214108 (2016).

Bozkaya, U. and Sherrill, C. D. J. Chem. Theory Comput. 12, 1179-1188 (2016). https://doi.org/10.1021/acs.jctc.5b01128

Bozkaya, U. Phys. Chem. Chem. Phys. 18, 11362-11373 (2016). https://doi.org/10.1039/c6cp00164e

Bozkaya, U. J. Chem. Phys. 144, 144108 (2016). https://doi.org/10.1063/1.4945706

Bozkaya, U. and Sherrill, C. D. J. Chem. Phys. 144, 174103 (2016). https://doi.org/10.1063/1.4948318

Verstraelen, T. et al. "Minimal Basis Iterative Stockholder: Atoms in Molecules for Force-Field Development." J. Chem. Theory Comput. (2016) 12 (8): 3894–3912 https://doi.org/10.1021/acs.jctc.6b00456.

## 2015

Parrish, R. M., Gonthier, J. F., Corminboeuf, C., and Sherrill, C. D. J. Chem. Phys. 143, 051103 (2015).

Verma, P., Derricotte, W. D., Evangelista, F. A. J. Chem. Theory Comput. (2015). https://doi.org/10.1021/acs.jctc.5b00817

Grimme, S., Brandenburg, J., Bannwarth, C., and Hansen, A. J. Chem. Phys. 143, 054107 (2015).

Martínez-Araya, J. I. J. Math. Chem. 53, 451 (2015).

Lestrange, P. J., Egidi, F., Li, X. J. Chem. Phys. 143, 234103 (2015). https://doi.org/10.1063/1.4937410

Pinski, P., Riplinger, C., Valeev, E., and Neese, F. J. Chem. Phys. 143, 034108 (2015).

Liakos, D., Sparta, M., Kesharwani, M., Martin, J., and Neese, F. J. Chem. Theory Comput. 11, 1525 (2015).

## 2014

Parrish, R. M. and Sherrill, C. D. J. Am. Chem. Soc. 136, 17386 (2014).

Parrish, R. M., Parker, T. M., and Sherrill, C. D. J. Chem. Theory Comput. 10, 4417 (2014).

Parrish, R. M. and Sherrill, C. D. J. Chem. Phys. 141, 044115 (2014).

Parker, T. M., Burns, L. A., Parrish, R. M., Ryno, A. G., and Sherrill, C. D. J. Chem. Phys. 140, 094106 (2014).

Martin, J. M. L. Mol. Phys. 112, 785 (2014).

Lipparini, F., Scalmani, G., Lagardère, L., Stamm, B., Cancès, E., Maday, Y., Piquemal, J.-P., Frisch, M., Mennucci, B. J. Chem. Phys. 141, 184108 (2014).

Dreuw, A. and Wormit, M. WIREs Comput. Mol. Sci. 5, 82-95 (2014).

Hesselmann, A. and Korona, T. J. Chem. Phys. 141, 094107 (2014).

Bozkaya, U. J. Chem. Theory Comput. 10, 4389-4399 (2014). https://doi.org/10.1021/ct500634s

## 2013

Parrish, R. M. and Sherrill, C. D. J. Chem. Phys. 139, 174102 (2013).

DePrince, A. E. and Sherrill, C. D. J. Chem. Theory Comput. 9, 293-299 (2013).

DePrince, A. E. and Sherrill, C. D. J. Chem. Theory Comput. 9, 2687-2696 (2013).

Bozkaya, U. and Sherrill, C. D. J. Chem. Phys. 138, 184103 (2013).

Soydas, E. and Bozkaya, U. J. Chem. Theory Comput. 9, 1452 (2013).

Bozkaya, U. and Sherrill, C. D. J. Chem. Phys. 139, 054104 (2013).

Bozkaya, U. J. Chem. Phys. 139, 104116 (2013).

Sure, R. and Grimme, S. J. Comput. Chem. 15, 1672 (2013).

Cancès, E., Maday, Y., Stamm, B. J. Chem. Phys. 139, 054111 (2013).

Schäffer, R. and Jansen, G. Mol. Phys. 111, 2570 (2013). https://doi.org/10.1080/00268976.2013.827253

## 2012

Hohenstein, E. G. and Sherrill, C. D. WIREs Comput. Mol. Sci. 2, 304-326 (2012).

Bozkaya, U. and Schaefer, H. F. J. Chem. Phys. 136, 204114 (2012).

Schäffer, R. and Jansen, G. Theor. Chem. Acc. 131, 1235 (2012).

## 2011

Hohenstein, E. G., Parrish, R. M., Sherrill, C. D., Turney, J. M., and Schaefer, H. F. III. J. Chem. Phys. 135, 174107 (2011).

Hohenstein, E. G., Jaeger, H. M., Carrell, E. J., Tschumper, G. S., and Sherrill, C. D. J. Chem. Theory Comput. 7, 2842-2851 (2011).

Papajak, E. and Truhlar, D. G. J. Chem. Theory Comput. 7, 10-18 (2011).

Cheng, L. and Gauss, J. J. Chem. Phys. 135, 084114 (2011).

Bozkaya, U., Turney, J. M., Yamaguchi, Y., Schaefer, H. F. III, and Sherrill, C. D. J. Chem. Phys. 135, 104103 (2011).

Bozkaya, U. J. Chem. Phys. 135, 224103 (2011).

Grimme, S., Ehrlich, S., and Goerigk, L. J. Comput. Chem. 32, 1456 (2011).

Hujo, W. and Grimme, S. J. Chem. Theory Comput. 7, 3866 (2011).

Izsák, R. and Neese, F. J. Chem. Phys. 135, 144105 (2011).

Rizzo, A., Coriani, S., Ruud, K. "Response Function Theory Computational Approaches to Linear and Nonlinear Optical Spectroscopy." In Computational Strategies for Spectroscopy. (2011) https://doi.org/10.1002/9781118008720.ch2.

## 2010

Hohenstein, E. G. and Sherrill, C. D. J. Chem. Phys. 132, 184111 (2010).

Hohenstein, E. G. and Sherrill, C. D. J. Chem. Phys. 133, 014101 (2010).

Hohenstein, E. G. and Sherrill, C. D. J. Chem. Phys. 133, 104107 (2010).

Evangelista, F. A., Prochnow, E., Gauss, J., and Schaefer, H. F. III. J. Chem. Phys. 132, 074107 (2010).

Grimme, S., Antony, J., Ehrlich, S., and Krieg, H. J. Chem. Phys. 132, 154104 (2010).

Podeszwa, R., Pernal, K., Patkowski, K., Szalewicz, K. J. Phys. Chem. Lett. 1, 550 (2010).

Olsen, J. M., Aidas, K., and Kongsted, J. J. Chem. Theory Comput. 6, 3721-3734 (2010).

## 2009

Stone, A. J. and Misquitta, A. J. Chem. Phys. Lett. 473, 201 (2009).

Evangelista, F. A., Simmonett, A. C., Schaefer, H. F. III, Mukherjee, D., and Allen, W. D. Phys. Chem. Chem. Phys. 11, 4728 (2009).

Kurlancheek, W. and Head-Gordon, M. Mol. Phys. 107, 1223 (2009).

Cammi, R. J. Chem. Phys. 131, 164104 (2009).

Pernal, K., Podeszwa, R., Patkowski, K., Szalewicz, K. Phys. Rev. Lett. 103, 263201 (2009).

Neese, F., Wennmohs, F., and Hansen, A. Chem. Phys. 356, 98-109 (2009).

## 2008

Bolton, E., Wang, Y., Thiessen, P. A., Bryant, S. H. PubChem: Integrated Platform of Small Molecules and Biological Activities, Chapter 12 in Annual Reports in Computational Chemistry, Volume 4 (American Chemical Society: Washington, DC, 2008). See https://pubchem.ncbi.nlm.nih.gov/.

Evangelista, F. A., Simmonett, A. C., Allen, W. D., Schaefer, H. F. III, and Gauss, J. J. Chem. Phys. 128, 124104 (2008).

Wennmohs, F. and Neese, F. Chem. Phys. 343, 217-230 (2008).

Kallay, M. and Gauss, J. J. Chem. Phys. 129, 144101 (2008).

Lu, B. Z., Zhou, Y. C., Holst, M. J., McCammon, J. A. Commun. Comput. Phys. 3, 973 (2008).

Chai, J.-D. and Head-Gordon, M. Phys. Chem. Chem. Phys. 10, 6615 (2008).

## 2006

Trofimov, A. B., Krivdina, I. L., Weller, J., and Schirmer, J. Chem. Phys. 329, 1 (2006).

Evangelista, F. A., Allen, W. D., and Schaefer, H. F. III. J. Chem. Phys. 125, 154113 (2006).

Grimme, S. J. Comput. Chem. 27, 1787-1799 (2006).

Podeszwa, R., Bukowski, R., and Szalewicz, K. J. Chem. Theory Comput. 2, 400 (2006).

Fink, R. F. Chem. Phys. Lett., 428, 461 (2006). https://doi.org/10.1016/j.cplett.2006.07.081

## 2005

Tomasi, J., Mennucci, B., and Cammi, R. Chem. Rev. 105, 2999 (2005).

Morell, C., Grand, A., and Toro-Labbé, A. J. Phys. Chem. A 109, 205 (2005).

Dreuw, A. and Head-Gordon, M. Chem. Rev. 105, 4009 (2005). https://doi.org/10.1021/cr0505627.

## 2004

Grimme, S. J. Comput. Chem. 25, 1463-1473 (2004).

## 2002

Häaettig, C. and Hald, K. Phys. Chem. Chem. Phys. 4, 2111 (2002).

Bakken, V. and Helgaker, T. J. Chem. Phys. 117, 9160 (2002).

Wu, Q. and Yang, W. J. Chem. Phys. 116, 515 (2002).

Weigend, F. Phys. Chem. Chem. Phys. 4, 4285-4291 (2002). https://doi.org/10.1039/B204199P

## 2001

Krylov, A. I. Chem. Phys. Lett. 350, 522-530 (2001).

## 2000

Hirata, S. and Bartlett, R. J. Chem. Phys. Lett. 321, 216 (2000).

Olsen, J. J. Chem. Phys. 113, 7140 (2000).

Krylov, A. I., Sherrill, C. D., and Head-Gordon, M. J. Chem. Phys. 113, 6509 (2000).

## 1999

Sherrill, C. D. and Schaefer, H. F. III. Advances in Quantum Chemistry, Vol. 34, edited by P.-O. Löwdin (Academic Press, New York, 1999), pages 143-269.

Piecuch, P., Kicharski, S. A., and Bartlett, R. J. J. Chem. Phys. 110, 6103 (1999).

Pedersen, T. B., Koch, H., and Hättig, C. J. Chem. Phys. 110, 8318 (1999).

## 1998

Sherrill, C. D., Krylov, A. I., Byrd, E. F. C., and Head-Gordon, M. J. Chem. Phys. 109, 4171 (1998).


Stratmann, R. E., Scuseria, G. E., and Frisch, M. J. J. Chem. Phys. 109, 8218 (1998). https://doi.org/10.1063/1.477483.

Ochsenfeld, C., White, C. A., and Head-Gordon, M. J. Chem. Phys. 109, 1663 (1998). https://doi.org/10.1063/1.476741

Cancès, E. and Mennucci, B. J. Math. Chem. 23, 309 (1998).

## 1997

Chaban, G., Schmidt, M. W., and Gordon, M. S. Theor. Chem. Acc. 97, 88-95 (1997).

Crawford, T. D., Stanton, J. F., Allen, W. D., and Schaefer, H. F. III. J. Chem. Phys., 107, 10626 (1997).

## 1996

Peng, C., Ayala, P. Y., Schlegel, H. B., and Frisch, M. J. J. Comput. Chem. 17, 49 (1996).

## 1995

Nooijen, M. and Bartlett, R. J. J. Chem. Phys. 102, 3629 (1995).

Pedersen, T. B. and Hansen, A. E. Chem. Phys. Lett. 246, 1 (1995). https://doi.org/10.1016/0009-2614(95)01036-9.

## 1994

Jeziorski, B., Moszynski, R., and Szalewicz, K. Chem. Rev. 94, 1887 (1994).

Bofill, J. M. J. Comp. Chem. 15, 1-11 (1994).

## 1993

Klamt, A. and Schüürmann, G. J. Chem. Soc., Perkin Trans. 2 5, 799 (1993).

## 1992

Fischer, T. H. and Almlöf, J. J. Phys. Chem. 96, 9770 (1992).

Rappe, A. K., Casewit, C. J., Colwell, K. S., Goddard, W. A. III, Skiff, W. M. J. Am. Chem. Soc., 25, 114 (1992).

## 1991

Curtiss, L. A., Raghavachari, K., Trucks, G. W., and Pople, J. A. J. Chem. Phys. 94, 7221-7230 (1991).

## 1990

Malmqvist, P.-A., Rendell, A., and Roos, B. O. J. Phys. Chem. 94, 5477-5482 (1990).

## 1989

Raghavachari, K., Trucks, G. W., Pople, J. A., and Head-Gordon, M. Chem. Phys. Lett. 157, 479-483 (1989).

Sosa, C., Geertsen, J., Trucks, G. W., Bartlett, R. J., and Franz, J. A. Chem. Phys. Lett. 159, 148-154 (1989).

Parr, R. G. and Yang, W. Density Functional Theory of Atoms and Molecules, Oxford University Press, USA, 1989. ISBN: 0195357736, 9780195357738

Haser, M. and Ahlrichs, R. J. Comp. Chem. 10(1), 104 (1989). https://doi.org/10.1002/jcc.540100111

## 1988

Olsen, J., Roos, B. O., Jørgensen, P., and Jensen, H. J. Aa. J. Chem. Phys. 89, 2185 (1988).

## 1987

Pople, J. A., Head-Gordon, M., and Raghavachari, K. Chem. Phys. 87, 5968 (1987).

Schlegel, H. B. Ab Initio Methods in Quantum Chemistry (1987).

## 1986

Pulay, P. and Saebø, S. Theor. Chim. Acta 69, 357 (1986).

## 1984

Schlegel, H. B. Theor. Chim. Acta 66, 333 (1984).

Kutzelnigg, W. Int. J. Quantum Chem. 25, 107-129 (1984).

## 1982

Purvis, G. D. and Bartlett, R. J. J. Chem. Phys. 76, 1910-1918 (1982).

Schirmer, J. Phys. Rev. A 26, 2395 (1982).

Szabo, A. and Ostlund, N. S. Modern Quantum Chemistry: Introduction to Advanced Electronic Structure Theory (1982). ISBN: 0486691861

## 1981

Jeziorski, B. and Monkhorst, H. J. Phys. Rev. A 24, 1668 (1981).

## 1980

Handy, N. C. Chem. Phys. Lett. 74, 280 (1980).

Roos, B. O. Chem. Phys. 48, 157-173 (1980).

Pulay, P. Chem. Phys. Lett. 73, 393-398 (1980).

## 1978

Ammeter, J. H., Bürgi, H.-B., Thibeault, J. C., and Hoffmann, R. J. Am. Chem. Soc. 100, 3686 (1978). https://doi.org/10.1021/ja00480a005

## 1965

Kohn, W. and Sham, L. J. Phys. Rev. 140, A1133-A1138 (1965).

## 1964

Hohenberg, P. and Kohn, W. Phys. Rev. 136, B864-B871 (1964).

Bondi, A. J. Phys. Chem. 68, 441 (1964).

## 1950

Foldy, L. L. and Wouthuysen, S. A. Phys. Rev. 78, 29-36 (1950).

## 1930

Hylleraas, E. Z. Phys. 65, 209 (1930).

