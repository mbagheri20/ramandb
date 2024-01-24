[![Licence](https://img.shields.io/github/license/mbagheri20/ramandb.svg)](LICENSE.txt)
[![SciData](https://img.shields.io/badge/Sci._Data-Bagheri_M.%26_Komsa_H.P._(2023)-red)](https://doi.org/10.1038/s41597-023-01988-5)

# Computational Raman Database

In this repository, all the versions of datasets contain Raman tensors and other vibrational information, such as phonon eigenmodes, Born charges (adopted from the Phonon database), and symmetry information, stored in a JSON document that can be queried with a simple python script.
You can browse the latest version of the database on [Computational Raman Database](https://ramandb.oulu.fi/) website. where you can find interactive Raman, IR spectra, and Phonon band structures with other related data on each structure page. The materials can be searched using formula, the number of atoms, Materials project id, dimensionality, and a lot of other keywords.

## Update logs

### version 1.0.1 (2024.0.1.24)

We updated Raman tensors of 33 materials after the first release of the database due to the calculation problems, mainly related to how errors were handled.

For 9 materials, VASP 5.4.4 gave two warnings "Warning from LATTYP: Got some problem with cell dimensions!" and "LRF_COMMUTATOR internal error: the vector ******* |phi(0)> is not orthogonal to |phi(0)>". Both warnings were ignored in our previous calculations by the error control center (Custodian). We recalculated all these materials using VASP 6, which did not show any such issues.

In addition, in some cases the dielectric function calculations were not fully converged. This was partly due to ignoring "internal ERROR: LINEAR_RESPONSE_DIIS matrix is zero, try to call with LRESET". Based on our initial benchmarking, we opted to ignore this warning. In addition, VASP sometimes incorrectly marked the calculations as converged when they were not. We checked for possible poorly converged materials in the whole database and recalculated them with VASP 6 if either the energy change ("dE" in VASP output) or the difference between input and output charge density ("rms(c)" in VASP output) of the last step is larger than 0.1. For 24 structures the results changed markedly, i.e., the convergence parameters became smaller, and the Raman spectra also changed. These are included in the updated dataset.
list of changed materials can be found [here](https://github.com/mbagheri20/ramandb/blob/main/list.txt)

## How to cite

If you have used ramandb, please cite the following article:

- "High-throughput computation of Raman spectra from first principles",

  Mohammad Bagheri and Hannu-Pekka Komsa, Sci. Data **2023** 10 (80)

  https://doi.org/10.1038/s41597-023-01988-5  (Open Access)

  ```
  @article{CRD,
     author = {Bagheri, Mohammad and Komsa, Hannu-Pekka},
     title = {High-throughput computation of Raman spectra from first principles}
     journal = {Scientific Data},
     volume = {10},
     number = {80},
     year = {2023},
     doi = {10.1038/s41597-023-01988-5},
     URL = {https://doi.org/10.1038/s41597-023-01988-5}
  }
  ```
  
## Acknowledgements

Phonon results are adapted from [phonondb](http://phonondb.mtl.kyoto-u.ac.jp/index.html) under CC BY 4.0.

