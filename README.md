# Matrix of Orthogonalised Atomic Orbital Coefficients Representation for Radicals and Ions
<p align="center">
<img src="https://github.com/hits-ccc/MAOC/blob/main/Images/git_0.png" width="500" height="300">
</p>
This repository offers some insight into the code behind the Matrix of Orthogonalized Atomic Orbital Coeffients, a novel molecular representation that can be used to distinguish compounds with various charge and spin multiplicities. 
Furthermore, the article this github supports introduces two new chemical datasets, N-HPC-1, REDOX, and a variation of the QM7b dataset known as QM7b(X), which are also explained in this repository.

## MAOC: A charge-variant molecular representation
The Matrix of Orthogonalized Atomic Orbital Coefficients (MAOC) is a charge-variant, symmetry-invariant molecular and atomic representation that can be used for quantum machine learning in predicting the QM properties (not limited to them) of molecular systems regardless of the ML model or system size. 
Users who are interested in generating MAOC can do so by installing the pypi package that supports the article that proposes MAOC:

`pip install maoc-support-functions`

The GitHub tutorial demonstrates how to use this package to build the MAOC representation.

Before installing MAOC, one should be aware of the dependencies that this package relies on:

| Dependencies | Version | PATH |
| :---: | :---: | :---: |
| `pandas` | 1.0.5  | https://pandas.pydata.org/ | 
| `numpy`  | 1.20.0 | https://numpy.org/ |
| `scikit-learn` | 1.2.1 | https://scikit-learn.org/stable/ | 
| `pyscf` | 2.1 | https://pyscf.org/index.html | 
| `qml` | 0.4.0.27 | https://www.qmlcode.org/index.html | 
| `natsort` | 8.3.1 | https://natsort.readthedocs.io/en/stable/index.html |
| `openbabel` | 3.1.1.1 | https://openbabel.org/docs/dev/UseTheLibrary/PythonInstall.html |

Please see the collapsed section below for more information on how to use the codes from the maoc-support-functions package, or refer to the package's pypi documentation ([MAOC](https://pypi.org/project/maoc-support-functions/))

<details>
<summary>How to use Full_MAOC </summary>
  
   
####   output=Full_MAOC(path=None, basis_set='pcseg-0',charge=0,spin=0)
   
   INPUT:
   
   * --path       -> (Str) The full path to your xyz files. Keep in mind that the *.xyz extension is required ;
   
   * --basis_set   -> (Str) The basis set that the user wishes to use to generate orthogonalized atomic orbitals. The reference basis set is kept unchanged (ANO), but users can simply modify the code to change it (defailt: 'pcseg-0') ;
   
   * --charge -> (Int) The molecular system's charge (default:0) ;
   
   * --spin -> (Int) The molecular system's spin multiplicity (default:0).
   
   OUTPUT:
   
   * output -> The MAOC ndarray sorted and flattened to ensure that it meets all of the symetry requirements for being a rotationally, permutationally, and translationally invariant representation.
  
</details>
<details>
<summary>How to use PCX-MAOC </summary>
  
   
####   output=PCX_MAOC(path=None, basis_set='pcseg-0',charge=0,spin=0,nr_pca=1)
   
   INPUT:
   
   * --path       -> (Str) The full path to your xyz files. Keep in mind that the *.xyz extension is required ;
   
   * --basis_set   -> (Str) The basis set that the user wishes to use to generate orthogonalized atomic orbitals. The reference basis set is kept unchanged (ANO), but users can simply modify the code to change it (default: 'pcseg-0') ;
   
   * --charge -> (Int) The molecular system's charge (default:0);
   
   * --spin -> (Int) The molecular system's spin multiplicity (default:0) ;
   
   * --nr_pca -> (Int) The number of principal components used in the representations generated by using the PCA dimensionality reduction technique to reduce the sorted matrix of atomic orbital coefficients (default:1) .
   
   OUTPUT:
   
   * output -> The PCX MAOC ndarray sorted and flattened to ensure that it meets all of the symetry requirements for being a rotationally, permutationally, and translationally invariant representation.
</details>

### MAOC: A representation of all molecular systems

MAOC's universal application is one of its most distinguishing features.
This means that MAOC can be used to represent any type of molecule, from monatoms to single molecules and molecules with periodic boundary conditions (PBC).

<p align="center">
<img src="https://github.com/hits-ccc/MAOC/blob/main/Images/git_1.png" width="700" height="300">
</p>

This repository only contains code that operates with xyz coordinates. The code for periodic systems is easily modifiable by PySCF users with experience. Experienced QM users who have worked with periodic compounds and input files such as cif but have not had the opportunity to use PySCF should contact us for assistance.
The package's defined basis sets cover the majority of the atoms in the periodic table. If one needs to use a different basis set than those defined in the PySCF package or wishes to use atoms whose basis sets are not defined, please consult [Ref A](https://github.com/pyscf/pyscf/blob/master/examples/gto/04-input_basis.py) and [Ref B](https://www.basissetexchange.org).

### MAOC: A charge ans spin-dependent molecular representation

<img align="left" src="https://github.com/hits-ccc/MAOC/blob/main/Images/git_2.gif" width="400" height="300">
The matrix of orthogonalized atomic orbital coefficients directly generated for the PySCF package is a charge- and spin-invariant representation of the systems.
Our group's recent focus has been on the properties of open-shell compounds (PAH and redox-active), so we required a charge-dependent representation that could differentiate compounds based on their nuclear coordinates, nuclear type, and charge/spin multiplicity. We made the MAOC charge and spin variant with a few simple tricks, so that two compounds with identical geometry but different charge and spin are represented differently. To learn more how we are doing that, please refer to the paper's [SI] (https://chemrxiv.org/engage/api-gateway/chemrxiv/assets/orp/resource/item/64746116e64f843f41f2b431/original/supplementary-material.pdf).

The GIF depicts the charge-dependence of the MAOC representation of a methane molecule with various charges/spin multiplicities.
The cosine similarity of the specific matrix to the charge zero matrix is indicated in the GIF. 

## Machine Learning

The codes provided from this [LINK](https://www.qmlcode.org/tutorial.html) were directly implemented in all of the codes used in the article this github supports. 

## Datasets
This section provides brief information about the datasets proposed in the article that this github supports.

<details>
  
<summary>N-HPC-1 dataset </summary>
  
### The dataset of N-heteropolycyclic compounds 
 <p align="center">
<img src="https://github.com/hits-ccc/MAOC/blob/main/Images/git_4.png" width="550" height="300">
  </p>
  
The N-HPC-1 dataset was inspired by the fascinating magnetic, electric, and optical properties of the N-doped PAH.
Because one of the characteristics of N-heteropolycycles is their open-shell stability, we decided to investigate some small open and closed-shell N-HPC in a combinatorial approach. The algorithm we developed to generate N-doped PAH is available [HERE](https://github.com/hits-ccc/MAOC/tree/main/Codes/Generative_Algorithm_for_N-Doped_Novel_Aromatics). To generate respective open-shell compounds, one, two, or three
electrons were removed, or one electron was added to the neutral molecules to produce eight groups
within the dataset: neutral singlets, neutral triplets, anionic doublets, cationic doublets, dicationic
singlets, dicationic triplets, tricationic doublets, and tricationic quartets. All of the compounds in the dataset have their geometry optimised using PBE0-D3/def2-TZVP and ORCA 5.0 package. 
This dataset is available [HERE](https://github.com/hits-ccc/MAOC/tree/main/Datasets/NHPC1). 
</details>

<details>
<summary>REDOX dataset </summary>
  
### A collection of a some popular redox-active compounds. 
<p align="center">
<img src="https://github.com/hits-ccc/MAOC/blob/main/Images/git_3.png" width="550" height="300">
  
There are 4,146 neutral , 4018 anionic and 687 cationic open- and closed-shell redox-active molecules with 1-4 unpaired electrons in this dataset.
Organic radicals (nitroxyl, phenoxyl, and galvinoxyl), carbonyl compounds (quinones, carboxylates, and phenazine-derived radicals), and cyanides are among the compounds represented in the dataset. All of the compounds in the dataset have their geometry optimised using PBE0-D3/def2-TZVP and ORCA 5.0 package. This dataset is available [HERE](https://github.com/hits-ccc/MAOC/tree/main/Datasets/REDOX). 
</p>
</details>

<details>
<summary>QM7b<sup> X </sup> dataset </summary>

### A dataset of open and closed-shell compounds based on the QM7b compounds
<p align="center">
<img align="center" src="https://github.com/hits-ccc/MAOC/blob/main/Images/git_5.png" width="550" height="300">
</p>

To evaluate the performance of MAOC for radicals and ions, the geometries of the anionic, cationic, and dicationic forms of the compounds in the QM7b dataset were optimised, and their various vertical and adiabatic properties were computed and strongly spin-contaminated species were removed from the dataset.
As a result, 7,197 geometry-optimized anion radicals, 6,999 geometry-optimized cation radicals, 7,198 geometry-optimized dications, and 7,208 anion radicals and 7,208 cation radicals in the geometry of the parent neutral molecule were added to the original QM7b dataset of neutral molecules.
This expanded dataset is known as QM7b<sup> X </sup>. The anionic, cationic, and dicationic compounds' geometries were optimised using PBE0-D3/def2-TZVP, and the SPE for vertical anions and cations were computed using the same combination of level of theory/basis set. 
</details>

## References

[1] https://chemrxiv.org/engage/chemrxiv/article-details/64160d85aad2a62ca1f937f6
