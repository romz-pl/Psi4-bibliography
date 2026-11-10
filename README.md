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

J. F. Gonthier and C.D. Sherrill, J. Chem. Phys. 145, 134106 (2016).


R. M. Parrish, J. F. Gonthier, C. Corminboeuf, and C.D. Sherrill, J. Chem. Phys. 143, 051103 (2015).


R. M. Parrish and C.D. Sherrill, J. Am. Chem. Soc. 136, 17386 (2014).


R. M. Parrish, T. M. Parker, and C.D. Sherrill, J. Chem. Theory Comput. 10, 4417 (2014).


R. M. Parrish and C.D. Sherrill, J. Chem. Phys. 141, 044115 (2014).


B. Jeziorski, R. Moszynski, and K. Szalewicz, Chem. Rev. 94, 1887 (1994).


T. M. Parker, L. A. Burns, R. M. Parrish, A. G. Ryno, and C. D. Sherrill, J. Chem. Phys. 140, 094106 (2014).


E. G. Hohenstein and C. D. Sherrill, WIREs Comput. Mol. Sci. 2, 304-326 (2012).


E. G. Hohenstein and C. D. Sherrill, J. Chem. Phys. 132, 184111 (2010).


E. G. Hohenstein, R. M. Parrish, C. D. Sherrill, J. M. Turney, and H. F. Schaefer III, J. Chem. Phys. 135, 174107 (2011).


E. G. Hohenstein, H. M. Jaeger, E. J. Carrell, G. S. Tschumper, and C. D. Sherrill, J. Chem. Theory Comput. 7, 2842-2851 (2011).


R. M. Parrish and C. D. Sherrill, J. Chem. Phys. 139, 174102 (2013).


E. G. Hohenstein and C. D. Sherrill, J. Chem. Phys. 133, 014101 (2010).


E. G. Hohenstein and C. D. Sherrill, J. Chem. Phys. 133, 104107 (2010).


A. J. Stone and A. J. Misquitta, Chem. Phys. Lett. 473, 201 (2009).


E. Papajak and D. G. Truhlar, J. Chem. Theory Comput. 7, 10-18 (2011).


E. Bolton, Y. Wang, P. A. Thiessen, S. H. Bryant. PubChem: Integrated Platform of Small Molecules and Biological Activities, Chapter 12 in Annual Reports in Computational Chemistry, Volume 4 (American Chemical Society: Washington, DC, 2008). See https://pubchem.ncbi.nlm.nih.gov/.


C. D. Sherrill and H. F. Schaefer III, Advances in Quantum Chemistry, Vol. 34, edited by P.-O. Löwdin (Academic Press, New York, 1999), pages 143-269.


S. Hirata and R. J. Bartlett, Chem. Phys. Lett. 321, 216 (2000).


J. Olsen, J. Chem. Phys. 113, 7140 (2000).


Peng, Ayala, Schlegel, and Frisch, J. Comput. Chem. 17, 49 (1996).


Bakken and Helgaker, J. Chem. Phys. 117, 9160 (2002).


Schlegel, Theor. Chim. Acta 66, 333 (1984).


Fischer and Almlof, J. Phys. Chem. 96, 9770 (1992).


Schlegel, Ab Initio Methods in Quantum Chemistry, (1987).


Bofill, J. Comp. Chem. 15, 1-11 (1994).


P. Piecuch, S. A. Kicharski, and R. J. Bartlett, J. Chem. Phys. 110, 6103 (1999).


N. C. Handy, Chem. Phys. Lett. 74, 280 (1980).


J. Olsen, B. O. Roos, P. Jørgensen, and H. J. Aa. Jensen, J. Chem. Phys. 89 2185 (1988).


J. Schirmer, Phys. Rev. A 26, 2395 (1982).


A. B. Trofimov, I. L, Krivdina, J. Weller, and J. Schirmer, Chem. Phys. 329, 1 (2006).


C. Häaettig and K. Hald, Phys. Chem. Chem. Phys. 4, 2111 (2002).


F. A. Evangelista, A. C. Simmonett, H. F. Schaefer III, D. Mukherjee, and W. D. Allen, Phys. Chem. Chem. Phys. 11, 4728 (2009).


F. A. Evangelista, W. D. Allen, and H. F. Schaefer III, J. Chem. Phys. 125, 154113 (2006).


F. A. Evangelista, A. C. Simmonett, W. D. Allen, H. F. Schaefer III, and J. Gauss, J. Chem. Phys. 128, 124104 (2008).


L. Cheng and J. Gauss, J. Chem. Phys. 135, 084114 (2011).


P. Verma, W. D. Derricotte, F. A. Evangelista, J. Chem. Theory Comput. (2015). https://doi.org/10.1021/acs.jctc.5b00817


B. Jeziorski and H. J. Monkhorst, Phys. Rev. A 24, 1668 (1981).


K. Raghavachari, G. W. Trucks, J. A. Pople, and M. Head-Gordon, Chem. Phys. Lett. 157, 479-483 (1989).


G. D. Purvis and R. J. Bartlett, J. Chem. Phys. 76, 1910-1918 (1982).


C. Sosa, J. Geersten, G. W. Trucks, R. J. Barlett, and J. A. Franz, Chem. Phys. Lett. 159, 148–154 (1989).


B. O. Roos, Chem. Phys. 48, 157-173 (1980).


G. Chaban, M. W. Schmidt, and M. S. Gordon, Theor. Chem. Acc. 97, 88-95 (1997).


P. Pulay, Chem. Phys. Lett. 73, 393-398 (1980).


P.-A. Malmqvist, A. Rendell, and B. O. Roos, J. Phys. Chem. 94, 5477-5482 (1990).


F. A. Evangelista, E. Prochnow, J. Gauss, and H. F. Schaefer III, J. Chem. Phys. 132, 074107 (2010).


F. Wennmohs and F. Neese, Chem. Phys. 343, 217-230 (2008).


A. E. DePrince III and C. D. Sherrill, J. Chem. Theory Comput. 9, 293-299 (2013).


A. E. DePrince III and C. D. Sherrill, J. Chem. Theory Comput. 9, 2687-2696 (2013).


L. A. Curtiss, K. Raghavachari, G. W. Trucks, and J. A. Pople, J. Chem. Phys. 94, 7221-7230 (1991).


J. A. Pople, M. Head-Gordon, and K. J. Raghavachari, Chem. Phys. 87, 5968 (1987).


T. D. Crawford, J. F. Stanton, W. D. Allen, and H. F. Schaefer III, J. Chem. Phys., 107, 10626 (1997).


C. D. Sherrill, A. I. Krylov, E. F. C. Byrd, and M. Head-Gordon, J. Chem. Phys. 109, 4171 (1998).


A. I. Krylov, C. D. Sherrill, and M. Head-Gordon, J. Chem. Phys. 113, 6509 (2000).


W. Kurlancheek and M. Head-Gordon, Mol. Phys. 107, 1223 (2009).


T. B. Pedersen, H. Koch, and C. Hattig, J. Chem. Phys. 110, 8318 (1999).


U. Bozkaya, J. M. Turney, Y. Yamaguchi, H. F. Schaefer III, and C. D. Sherrill J. Chem. Phys. 135, 104103 (2011).


U. Bozkaya and C. D. Sherrill J. Chem. Phys. 138, 184103 (2013).


U. Bozkaya, J. Chem. Phys. 135, 224103 (2011).


E. Soydas and U. Bozkaya, J. Chem. Theory Comput. 9, 1452 (2013).


U. Bozkaya and H. F. Schaefer III, J. Chem. Phys. 136, 204114 (2012).


U. Bozkaya and C. D. Sherrill, J. Chem. Phys. 139, 054104 (2013).


U. Bozkaya, J. Chem. Phys. 139, 104116 (2013).


Grimme, J. Comp. Chem. 25 1463-1473 (2004).

Grimme, J. Comp. Chem. 27, 1787-1799 (2006).


S. Grimme, J. Antony, S. Ehrlich, and H. Krieg, J. Chem. Phys. 132, 154104 (2010).


S. Grimme, S. Ehrlich, and L. Goerigk, J. Comput. Chem. 32, 1456 (2011).


Q. Wu and W. Yang, J. Chem. Phys. 116, 515 (2002).


P. Hohenberg and W. Kohn, Phys. Rev. 136, B864-B871 (1964).


W. Kohn and L.J. Sham, Phys. Rev. 140, A1133-A1138 (1965).


R.G. Parr and W. Yang, Density Functional Theory of Atoms and Molecules Oxford University Press, USA, 1989 ISBN:0195357736, 9780195357738


L. L. Foldy and S. A. Wouthuysen, Phys. Rev. 78, 29-36 (1950)


W. Kutzelnigg, Int. J. Quantum Chem. 25, 107-129 (1984)


D. Smith, L. Burns, K. Patkowski, and D. Sherrill, J. Phys. Chem. Lett. 7, 2197-2203 (2016).


A. Szabo and N. S. Ostlund, Modern Quantum Chemistry: Introduction to Advanced Electronic Structure Theory 1982 ISBN:0486691861


S. Grimme, J. Brandenburg, C. Bannwarth, and A. Hansen, J. Chem. Phys. 143, 054107 (2015).


R. Sure and S. Grimme, J. Comput. Chem. 15, 1672 (2013).


M. Kallay and J. Gauss, J. Chem. Phys. 129, 144101 (2008).


J. M. L. Martin, Mol. Phys. 112, 785 (2014).


R. Cammi, J. Chem. Phys. 131, 164104 (2009).


A. Klamt, and G. Schüürmann J. Chem. Soc., Perkin Trans. 2 5, 799 (1993).


J. Tomasi, B. Mennucci, and R. Cammi Chem. Rev. 105, 2999 (2005).


E. Cancès, B. Mennucci J. Math. Chem. 23, 309 (1998).


E. Cancès, Y. Maday, B. Stamm J. Chem. Phys. 139, 054111 (2013).


B. Stamm, E. Cancès, F. Lipparini, Y. Maday J. Chem. Phys. 144, 054101 (2016).


F. Lipparini, G. Scalmani, L. Lagardère, B. Stamm, E. Cancès, Y. Maday, J.-P. Piquemal, M. Frisch, B. Mennucci J. Chem. Phys. 141, 184108 (2014).


M. Nottoli, B. Stamm, G. Scalmani, F. Lipparini J. Chem. Theory Comput. 15, 6061 (2019).


B. Z. Lu, Y. C. Zhou, M. J. Holst, J. A. McCammon Commun. Comput. Phys. 3, 973 (2008).


A. Jha, M. Nottoli, A. Mikhalev, C. Quan, B. Stamm J. Chem. Phys. 158, 104105 (2023).


A. Bondi J. Phys. Chem. 68, 441 (1964).


A. K. Rappe, C. J. Casewit, K. S. Colwell, W. A. Goddard III, W. M. Skiff J. Am. Chem. Soc., 25, 114 (1992).


R. T. McGibbon, A. G. Taube, A. G. Donchev, K. Siva, F. Hernáandez, C. Hargus, K. H. Law, J. L. Klepeis, D. E. Shaw J. Chem. Phys. 147, 161725 (2017).


Konrad Patkowski, Piotr S. .Zuchowski, Daniel G. A. Smith J. Chem. Phys. 148, 164110 (2018).


Christophe Morell, André Grand, and Alejandro Toro-Labbé J. Phys. Chem. A 109, 205 (2005).


Jorge Ignacio Martínez-Araya J. Math. Chem. 53, 451 (2015).


W. Hujo and S. Grimme J. Chem. Theory Comput. 7 3866 (2011).


J. Chai and M. Head-Gordon Phys. Chem. Chem. Phys. 10 6615 (2008).


K. Pernal, R. Podeszwa, K. Patkowski, K. Szalewicz Phys. Rev. Lett. 103 263201 (2009).


R. Podeszwa, K. Pernal, K. Patkowski, K. Szalewicz J. Phys. Chem. Lett. 1 550 (2010).


R. Schäffer and G. Jansen Theor. Chem. Acc. 131, 1235 (2012).


R. Schäffer and G. Jansen Mol. Phys. 111, 2570 (2013), https://doi.org/10.1080/00268976.2013.827253 .


H. Laqua, J. Kussmann and C. Ochsenfeld J. Chem. Phys. 149, 204111 (2018)


S. Lehtola J. Chem. Theory Comput. 15, 1593 (2019), https://doi.org/10.1021/acs.jctc.8b01089.


J. H. Ammeter, H.-B. Bürgi, J. C. Thibeault, and R. Hoffmann J. Am. Chem. Soc. 100, 3686 (1978), https://doi.org/10.1021/ja00480a005


S. Lehtola J. Chem. Phys. 151, 241102 (2019), https://doi.org/10.1063/1.5139948.


S. Lehtola Int. J. Quantum Chem. 119, e25945 (2019), https://doi.org/10.1002/qua.25945.


S. Lehtola Phys. Rev. A. 101, 012516 (2020), https://doi.org/10.1103/PhysRevA.101.012516.


S. Lehtola Phys. Rev. A. 101, 032504 (2020), https://doi.org/10.1103/PhysRevA.101.032504.


S. Lehtola J. Chem. Phys. 152, 134108 (2020), https://doi.org/10.1063/1.5144964.


S. Lehtola, L. Visscher, and E. Engel J. Chem. Phys. 152, 144105 (2020), https://doi.org/10.1063/5.0004046.


J. M. Olsen, K. Aidas, and J. Kongsted. J. Chem. Theory Comput. 6, 3721-3734 (2010).


A. Dreuw and M. Wormit. WIREs Comput. Mol. Sci. 5, 82-95 (2014).


M. F. Herbst, M. Scheurer, T. Fransson, D. R. Rehn, and A. Dreuw. WIREs Comput. Mol. Sci., (2020) DOI: 10.1002/wcms.1462, Preprint https://adc-connect.org/q/publications


S. E. Houck and N. J. Mayhall, J. Chem. Theory Comput. 15, 2278-2290 (2019).


A. I. Krylov, Chem. Phys. Lett. 350, 522-530 (2001).


M. Nooijen and R. J. Bartlett, J. Chem. Phys. 102, 3629 (1995).


L.-P. Wang and C. Song, J. Chem. Phys. 144, 214108 (2016).


R. Eric Stratmann, G. E. Scuseria, and M. J. Frisch J. Chem. Phys. 109, 8218 (1998), https://doi.org/10.1063/1.477483.


T. B. Pedersen, A. E. Hansen Chem. Phys. Lett. 246, 1 (1995), https://doi.org/10.1016/0009-2614(95)01036-9.


P. J. Lestrange, F. Egidi, X. Li J. Chem. Phys. 143, 234103 (2015), https://doi.org/10.1063/1.4937410.


Rizzo, S. Coriani, K. Ruud, “Response Function Theory Computational Approaches to Linear and Nonlinear Optical Spectroscopy”. In Computational Strategies for Spectroscopy, https://doi.org/10.1002/9781118008720.ch2.


A. Dreuw, M. Head-Gordon Chem. Rev. 105, 4009 (2005), https://doi.org/10.1021/cr0505627.


Norman, K. Ruud, T. Saue, “Principles and Practices of Molecular Properties: Theory, Modeling, and Simulations”. John Wiley & Sons, 2018


Verstraelen et al. “Minimal Basis Iterative Stockholder: Atoms in Molecules for Force-Field Development”. J. Chem. Theory and Comput. https://doi.org/10.1021/acs.jctc.6b00456.


A. Hesselmann and T. Korona, J. Chem. Phys. 141, 094107 (2014).


R. Podeszwa, R. Bukowski, and K. Szalewicz, J. Chem. Theory Comput. 2, 400 (2006).


Y. Xie, D. G. A. Smith, and C. D. Sherrill, J. Chem. Phys., 157, 024801 (2022)


E. Hylleraas Z. Phys. 65, 209 (1930).


P. Pulay and S. Saebø, Theor. Chim. Acta 69, 357 (1986).


P. Pinski, C. Riplinger, E. Valeev, and F. Neese, J. Chem. Phys. 143, 034108 (2015).


D. Liakos, M. Sparta, M. Kesharwani, J. Martin, and F. Neese, J. Chem. Theory Comput. 11, 1525 (2015).


F. Neese, F. Wennmohs, and A. Hansen Chem. Phys. 356, 98-109 (2009)


R. Izsák and F. Neese J. Chem. Phys. 135, 144105 (2011)


“PSI4NUMPY: An Interactive Quantum Chemistry Programming Environment for Reference Implementations and Rapid Development”, D. G. A. Smith, L. A. Burns, D. A. Sirianni, D. R. Nascimento, A. Kumar, A. M. James, J. B. Schriber, T. Zhang, B. Zhang, A. S. Abbott, E. J. Berquist, M. H. Lechner, L. A. Cunha, A. G. Heide, J. M. Waldrop, T. Y. Takeshita, A. Alenaizan, D. Neuhauser, R. A. King, A. C. Simmonett, J. M. Turney, H. F. Schaefer III, F. A. Evangelista, A. E. DePrince, T. D. Crawford, K. Patkowski, and C. D. Sherrill J. Chem. Theory Comput. 14, 3504-3511 (2018).


J. B. Schriber, D. A. Sirianni, D. G. A. Smith, L. A. Burns, D. Sitkoff, D. L. Cheney, C. D. Sherrill J. Chem. Phys. 154, 234107 (2021).


“A generally applicable atomic-charge dependent London dispersion correction”, E. Caldeweyher, S. Ehlert, A. Hansen, H. Neugebauer, S. Spicher, C. Bannwarth, and S. Grimme, J. Chem. Phys. 150, 154122 (2019). https://doi.org/10.1063/1.5090222


M. Haser and R. Ahlrichs, J. Comp. Chem. 10(1), 104 (1989). https://doi.org/10.1002/jcc.540100111


T. H. Thompson and C. Ochsenfeld J. Chem. Phys. 147, 144101 (2017). https://doi.org/10.1063/1.4994190


“PSI4 1.4: Open-source software for high-throughput quantum chemistry”, D. G. A. Smith, L. A. Burns, A. C. Simmonett, R. M. Parrish, M. C. Schieber, R. Galvelis, P. Kraus, H. Kruse, R. Di Remigio, A. Alenaizan, A. M. James, S. Lehtola, J. P. Misiewicz, M. Scheurer, R. A. Shaw, J. B. Schriber, Y. Xie, Z. L. Glick, D. A. Sirianni, J. S. O’Brien, J. M. Waldrop, A. Kumar, E. G. Hohenstein, B. P. Pritchard, B. R. Brooks, H. F. Schaefer III, A. Yu. Sokolov, K. Patkowski, A. E. DePrince III, U. Bozkaya, R. King, F. A. Evangelista, J. M. Turney, T. D. Crawford, and C. D. Sherrill J. Chem. Phys. 152, 184108 (2020). https://doi.org/10.1063/5.0006002


“Nonapproximated third-order exchange induction energy in symmetry-adapted perturbation theory”, J. M. Waldrop and K. Patkowski J. Chem. Phys. 154, 024103 (2021). https://doi.org/10.1063/1.4994190


C. Ochsenfeld, C. A. White, M. Head-Gordon J. Chem. Phys. 109, 1663 (1998) https://doi.org/10.1063/1.476741


“REMP: A hybrid perturbation theory providing improved electronic wavefunctions and properties”, S. Behnle and R. F. Fink, J. Chem. Phys. 150, 1241077 (2019). https://doi.org/10.1063/1.5086168


“OO-REMP: Approaching Chemical Accuracy with Second-Order Perturbation Theory”, S. Behnle and R. F. Fink, J. Chem. Theory Comput. 17, 3259 (2021). https://doi.org/10.1021/acs.jctc.1c00280


“UREMP, RO-REMP, and OO-REMP: Hybrid perturbation theories for open-shell electronic structure calculations”, S. Behnle and R. F. Fink J. Chem. Phys. 156, 124103 (2022). https://doi.org/10.1063/5.0081285


“Two new unitary-invariant and size-consistent perturbation theoretical approaches to the electron correlation energy”, R. F. Fink Chem. Phys. Lett., 428, 461 (2006) https://doi.org/10.1016/j.cplett.2006.07.081


U. Bozkaya, J. Chem. Theory Comput. 10, 4389-4399 (2014). https://doi.org/10.1021/ct500634s


U. Bozkaya, J. Chem. Theory Comput. 12, 1179-1188 (2016). https://doi.org/10.1021/acs.jctc.5b01128


U. Bozkaya, Phys. Chem. Chem. Phys. 18, 11362-11373 (2016). https://doi.org/10.1039/c6cp00164e


U. Bozkaya, J. Chem. Phys. 144, 144108 (2016). https://doi.org/10.1063/1.4945706


U. Bozkaya and C. D. Sherrill, J. Chem. Phys. 144, 174103 (2016). https://doi.org/10.1063/1.4948318


U. Bozkaya and C. D. Sherrill, J. Chem. Phys. 147, 044104 (2017). https://doi.org/10.1063/1.4994918


U. Bozkaya, J. Comput. Chem. 39, 351-360 (2018). https://doi.org/10.1002/jcc.25122


U. Bozkaya, J. Chem. Phys. 153, 244115 (2020). https://doi.org/10.1063/5.0035811


D. Luu and K. Patkowski, J. Phys. Chem. A 127, 356-377 (2023). https://doi.org/10.1021/acs.jpca.2c06465


F. Weigend, Phys. Chem. Chem. Phys. 4, 4285-4291 (2002). https://doi.org/10.1039/B204199P


J. G. Brandenburg, C.Bannwarth, A. Hansen, S. Grimme, J. Chem. Phys. 148, 064104, (2018). https://doi.org/10.1063/1.5012601


M. Müller and A. Hansen and S. Grimme J. Chem. Phys. 158, 014103 (2023). https://doi.org/10.1063/5.0133026


S. Grimme and A. Hansen and S. Ehlert and J.-M. Mewes J. Chem. Phys. 154, 064103 (2021). https://doi.org/10.1063/5.0040021

