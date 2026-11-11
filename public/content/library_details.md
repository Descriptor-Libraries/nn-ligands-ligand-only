# Library Details

## Molecule Identification
The initial library consisted of approximately 300 bidentate N-donor ligands covering seven ligand subclasses: bipyridine, phenanthroline, bisimidazole, bisoxazoline, bioxazoline, pyridine-oxazoline and pyridine-imidazole ligands. These ligands were primarily ligands utilized in reactions previously performed by the Doyle, Reisman and Sigman groups. A brief search of other relevant reactions was conducted as well to expand the library. To expand the library beyond this initial space, a search for all commercially available ligands was performed.16 Some additional ligands which were combinations of existing ligands were also surveyed. The combinatorial ligand space as well as the commercial space was filtered to remove ligands that were not likely applicable to catalysis or were not strictly bidentate N-donor ligands. Specifically, ligands were removed if:
-	Molecular weight > 500.000 g/mol
-	Tridentate ligand binding site present 
-	Bidentate binding site matching one of the 7 included substructures was not present
-	Multiple bidentate bindings sites were present 
-	Molecule contained a boronic acid, free alcohol, free amine, iodide, phosphate, acid chloride, alkyne, allene, imine, free sulfur, crown ether, sulfone, unstable bonds, radicals, selenium
-	Ligands were duplicates when considering isotopes
-	Ligands were duplicates when not-considering stereochemistry
-	Ligands contained any metals

In addition, only a single stereoisomer was included for each ligand. With respect only to the stereocenters immediately adjacent to the N binding atoms, each ligand was calculated as the S or S,S  stereochemistry. There are a few exceptions where the opposite stereochemistry (R or R,R) was included if this was due to priority but matched the orientation of the rest of the library. This was done to allow for meaningful nuance to be described from steric descriptors rather simply classifying ligands as R or S. 

## Conformational Searching & Conformer Selection

RDKit and Open Babel were used to obtain an initial guess for the geometry of the free ligand from a SMILES string using a Python script. The free ligand was used due to issues generating the proper 3D structure from the SMILES strings for the metal ligand complex. A script developed from the Schrodinger python API was then used to constrain the free ligand geometry through addition of copper, formation of bonds between the nitrogen donor atoms and the metal center and addition of two standard ligands to generate four-coordinate [LCu(F)2] complexes. Copper was chosen due to force field compatibility. Molecular Mechanics conformations searches were performed using MacroModel for these complexes using the OPLS4 force field without solvation and within a 5 kcal/mol window. Bonds to the metal center were restrained to the input geometry during the conformer search. If the conformer search yielded less than 20 structures, all conformers were taken forward for DFT computation. If more than 20 conformers were located, the Kelley-penalty method was used to select representative conformers for the ensemble. This truncated ensemble was used in place of the full conformer ensemble in these instances. Using these conformers, a script was used to generate either the square planar or tetrahedral geometry using Ni without altering the geometry of the bidentate N-donor ligand. The square planar complex generated was [LNi(H)2] while the tetrahedral complex used was [LNi(F)2]. 

## DFT Computations

These amended complexes were carried forward for DFT calculations. All DFT calculations were performed using Gaussian (version 16 C.01).8 Geometry optimizations and frequency calculations of these complexes were performed at the B3LYP23-D3BJ12,24/LANL2TZ13(Ni), 6-31G(d)25 (other atoms) level of theory with an ultrafine integration grid. An effective core potential (ECP) was applied to Nickel. These optimized geometries were used for subsequent single points at the M0626-D3/Def2-TZVP14 level of theory. NBO analysis was performed using the NBO program (version 7.0). The levels of theory were chosen according to benchmarking analysis and feasibility for this number of computations. If the calculations did not terminate normally after 3 attempts are resolving termination errors, the ligand or conformer was removed from the library. Ligands with excluded conformers for this reason are noted in the attached documentation.  A python script was then used to extract the optimized geometry x,y,z coordinates from the DFT output file and remove the metal and additional ligands from the complex to yield the free N,N-ligand structure. The three single point calculations were repeated for these free ligand structures at the M06-D3/Def2-TZVP level of theory.

From the DFT calculations, global, atomic, and bond-level properties were collected for each conformer using an amended version of [Get Properties](https://github.com/SigmanGroup/BNNY/property_collection). 

The dynamic range of properties across the conformational ensemble of a single aryl bromide was summarized by using five condensed measures for each of the properties.

| Descriptor              | Definition                                                                                      |
| ----------------------- | ------------------------------------------------------------------------------------------------|
| Boltz                   | Boltzmann-weighted average of a property from all the conformers in an ensemble (T = 298.15 K)  |
| max                     | highest value of a property given by any conformer in an ensemble                               |
| min                     | lowest value of a property given by any conformer in an ensemble                                |
| low_E                   | value of a property from the lowest energy conformer in the ensemble                            |
| range                   | absolute value of the max - min property value within an ensemble                               |

An extended explanation of the computational workflow used to build the ligand library, as well as details on the collected and predicted descriptors can be found in the original publication supporting information.

## Citation
