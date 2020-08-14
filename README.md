# Integrative structure of the Nef-CD4(CD)-AP2(Δμ2-CTD) complex

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.3836213.svg)](https://doi.org/10.5281/zenodo.3836213)

These scripts demonstrate the use of [IMP](https://integrativemodeling.org), [MODELLER](https://salilab.org/modeller), and [PMI](https://github.com/salilab/pmi) in the modeling of the solution structure of the Nef-CD4-AP2 complex using 90 DSSO chemical cross-links and the X-ray structure of the crystal structure, a comparative model of the β2 subunit 24-89 region built based on the AP2 structure.

First, [MODELLER](https://salilab.org/modeller) is used to generate comparative model of the β2 subunit 24-89 region. Then, IMP
is used to model these components using crystal structure and the DSSO crosslinks to obtain the solution structure of the  Nef-CD4(CD)-AP2(Δμ2-CTD) complex.

The modeling protocol will work with a default build of IMP, but for most effective sampling, IMP should be built with [MPI](https://integrativemodeling.org/2.7.0/doc/ref/namespaceIMP_1_1mpi.html) so that replica exchange can be used.

## List of files and directories:

- `data`		                         contains all relevant data, input structures that were generated by MODELLER or deposited in PDB, etc.
  - `mod_extended_AP2beta2.py`  MODELLER script to add the β2 subunit 24-89 region built based on the AP2 structure using MODELLER

- `scripts`
  - `mod_Nef_AP2_newhelix.py`  the main IMP/PMI script modeling with 3 crystal interfaces



- `scripts/analysis`    The best 500 models from the modeling are accumulated in this directory, and updated as the calculation proceeds.
- `scripts/figures`    The structures of the lowest temperature replica will be written here as [RMF files](https://integrativemodeling.org/rmf/).


- `outputs` For reference, the models described in the Nup84 publication are
  deposited in this directory. For each of the two clusters discovered in
  the study, the cluster representative (the best scoring individual model in
  the cluster) is available in RMF format, together with the top five best
  scoring models in PDB format. An accompanying stat file contains useful
  statistics on the simulation, such as whether each of the crosslinks was
  satisfied. The localization densities, as shown in Figure 6 on the publication
  are also available, as Chimera session files.

## Running the MODELLER scripts:
- `cd data/`
- `(python mod_extended_AP2beta2.py > mod_extended_AP2beta2.log)` 

## Running the IMP/PMI scripts for the  Nef-CD4(CD)-AP2(Δμ2-CTD) complex:
- `cd scripts`
- `python mod_Nef_AP2_newhelix.py &> mod_Nef_AP2_newhelix.out` (on a single processor; prepend `mpirun -np 4` or similar if you built IMP with MPI support)
- You can add the `--test` option to the command line to quickly test the
  script; this simply runs the sampling for fewer steps (should complete
  in an hour or two).

Next, analyze resulting models (this script can also be used to
combine results from multiple independent runs):
- `cd scripts/analysis`
- `python run_analysis.py ../`
- (If you used the `--test` option above, use it here too.)

## Information

_Author(s)_: Ignacia Echeverria

_Date_: May 5th, 2020

_License_: [LGPL](http://www.gnu.org/licenses/old-licenses/lgpl-2.1.html).
This library is free software; you can redistribute it and/or
modify it under the terms of the GNU Lesser General Public
License as published by the Free Software Foundation; either
version 2 of the License, or (at your option) any later version.

_Last known good IMP version_: [![build info](https://integrativemodeling.org/systems/34/badge.svg?branch=master)](https://integrativemodeling.org/systems/) [![build info](https://integrativemodeling.org/systems/34/badge.svg?branch=develop)](https://integrativemodeling.org/systems/)

_Testable_: Yes.

_Parallelizeable_: Yes

_Publications_:
 - Kwon, Y., Kaake, R.M., Echeverria, I. et al. Structural basis of CD4 downregulation by HIV-1 Nef. Nat Struct Mol Biol (2020). (https://doi.org/10.1038/s41594-020-0463-z).

