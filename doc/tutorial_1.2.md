# Tutorial 1.2: Building Transition Metal Complexes from Fragments

In this exercise we familiarise with the use of molecular fragments, attachment points, and connection rules. The goal is to build a small space of building blocks, also known as a "fragment space", from scratch.

> **NOTE** This exercise is best performed while having access to the Internet. In fact, DENOPTIM will call for an online service that converts SMILES to 3D-structures. When off-line, it will offer the user with the choice to use a local functionality from [CDK](https://cdk.github.io/), which is OK but slower and less accurate.


## Create a Space of Building Blocks (Fragment Space)

1. Open the Graphical User Interface (GUI) by running `denoptim` from within the `dnp_workshop` environment.
2. Chose `Make Fragments` from the list of shortcuts, or `File` -> `New` -> `New Molecular Fragments`.
3. Using the button under *Import a structure from `File`*, load the structure of each of the Pt complex files stored in this folder.
4. Click on atoms to select them (see the note below for a hint on how to select atoms) and then `Remove Atoms` to remove them and isolate the molecular fragment you are interested in, or `Atom to AP` to replace a single-connected atom with an attachment point.
5. Repeat steps 3 and 4 as much as needed to generate the following fragments:
	- Iodine (X-ligand) with one attachment point (AP) with APClass `Xlig:1`
	- NO<sub>2</sub> (X-ligand) with APClass `Xlig:1`
	- P(Ph)<sub>3</sub> (L-ligand) with one APClass `MPhosphine:1`
	- Pyridine (L-ligand) with APClass `MPy:1`
	- the five-atom ring of imidazolylidene (a N-heterocyclic carbene, or NHC, fragment) with one AP with class `MImidazolylidene:1` and two APs with class `ImidazolylideneSubN:0` each replacing one of the substituents on the N atoms.
6. We now create some organic fragments to populate the N-substituents on the NHC fragment. Since NHCs can often be synthesised starting from amines (see [*Chem. Rev.* **2011**, 111, 4, 2705–2733](https://doi.org/10.1021/cr100328e), you can generate the structure of an amine by clicking on *Import structure from `SMILES`* and type a [SMILES string](https://www.daylight.com/dayhtml/doc/theory/theory.smiles.html). For example, generate these amines and converted them to fragments by replacing the N atom with an attachment point of class `ImidazolylideneSubN:1`:
	- `CN`
	- `c1(C)ccccc1N`
	- `C1CCCCC1N`
7. Save this small library of fragments to an SDF file, call it `my_library_of_fragments.sdf` under the `exercise_1.2` folder.
8. We now create the compatibility rules for assembling Pt complexes by combining molecular building blocks. In DENOPTIM, click `File`->`New`->`New Compatibility Matrix`
9. `Import APClasses` by loading first the `Pt-CO_fragment.sdf` file and then the ´my_library_of_fragments.sdf´. In both cases, choose ´Scaffolds and Fragments´ when asked about the type of building block.
10. Then `Add Compatibility Rule` between `Llig:0` and all the APClasses that represent the capability to coordinate a metal as a L-ligand, namely `MPy:1`, `MPhosphine:1`, and `MImidazolylidene:1`. Hold the `command`/`CTRL` key to select multiple entries. Note that the two lists refers to different role of the attachment point: *growing graph*, and *incoming fragment*.
11. Add the compatibility rule between `Xlig:0` and `Xlig:1`
12. Add the compatibility rule between `ImidazolylideneSubN:0` and `ImidazolylideneSubN:1`
13. We now define the rules to saturate open valences. Import the APClasses from `H_and_Me.sdf`, move to the `Capping Rules` tab, and `Add Capping Rule` to `ImidazolylideneSubN:0` with `hyd:1`
14. Last, we define what attachment points cannot stay unused, but have no capping group. Move to the `Forbidden Ends` tab and `Add Forbidden End Rule` to `Llig:0`  and `Xlig:0`.
15. Save the compatibility matrix as `my_compatibility_matrix.par` under the `exercise_1.2` folder.

> **NOTE** Right-click on the molecular viewer to get the vast functionality offered by [Jmol](http://jmol.sourceforge.net/), including, for instance, see the `Select` -> `Invert Selection`. In particular, in the right-click menu you can chose `Console` to open Jmol's command line interface and use the `select` command. Here are some common examples of use:
> - `select _N`: selects all nitrogen atoms.
> - `select atomno >= 10 and atomno <= 43`: selects atoms from number 10 to 43 in the list of atom. Note the use of a the logical operator `and`.
> - `select search("<SMARTS>")` where `<SMARTS>` is a [SMARTS substructure search query](https://www.daylight.com/dayhtml/doc/theory/theory.smarts.html). For example,
>	- `select search("[#7]-[#6]")`: selects all nitrogen and carbon atoms of any kind that are connected by a single bond.
	- `select search("[r5]")`: selects all atoms that are part of a five-member ring.
> - `select selected OR connected(selected)`: propagates selection to all atoms connected to currently selected atoms.
> - `select none`: clears the list of selected atoms.
> Refer to [Jmol's documentation](https://chemapps.stolaf.edu/jmol/docs/) for further details on the functionality provided by Jmol.

## Explore the fragment space
Here we will briefly use the fragment space to generate all the Pt complexes that are encoded in the space we have just generated.
1. Click on `File`->`New`->`New Virtual Screening`.
2. In the windows for the configuration of the run, under the `Space of Building Blocks` tab browse to specify:
- `Pt-CO_fragment.sdf` for the *Scaffold fragments library *
- `my_library_of_fragments.sdf` for the *Fragments library*
- `H_and_Me.sdf` for the *Capping groups library*
- `my_compatibility_matrix.par` for the *Compatibility matrix file*
- since we have heavy atoms, we need to specify 1000 for the maximum molecular weight.
3. For having a way to sort the generated Pt complexes we make DENOPTIM calculate the molecular weight. Switch to the `Fitness Provider` tab and type `MW` in the text box defining the equation of the fitness.
4. Click on `Run Now...` and confirm you want to run the experiment. A dialog will tell you where the results will be places: remember that name.
5. For a short moment the bar on the top-right part of the DENOPTIM window, which was originally blue, will turns grey to indicate that all the submitted tasks are still running. Then it will turn blue to indicate that the run is completed.
6. `File`->`Open Recent` to select the results and open them.

## Discussion
- How to define a fragment space that for Pt complexes where the properties of the metal center can vary with the largest range?
- Conversely, how to design a fragment space that allows to achieve the finest resolution when mapping the properties of the Pt complex?
- Reflect over strategies to design fragment spaces for exploring properties of a central transition metal (e.g., the effective electron density on the metal) vs exploring inter-molecular interaction properties (e.g., interaction of the transition metal complex with the surrounding environment, like with solvent and surfaces).

## Go Beyond Classical Chemistry
DENOPTIM can handle any arrangement of atoms and pseudo-atoms. Have  look in the `exercise_1.2/examples_with_Du` for examples where dummy atoms are used to represent multi-hapto metal-ligand bonding.

Although you can open these file via the GUI, we use this opportunity to use the command line interface for opening files with DENOPTIM. Try:
```
denoptim examples_with_Du/MOL000006.sdf
```
