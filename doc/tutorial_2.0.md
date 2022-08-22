# Tutorial 2.0: Evolutionary Design of *trans*-Pt(X)(X')(L)(CO)

## Introduction
In this exercise we play with the genetic algorithm while designing Pt compounds. To allow a chemical interpretation of the results, we define a chemical design goal: identify a set of ligands [X, X', L], where each X is a covalent ligand and L is a neutral donor (dative) ligand, that weaken the C&equiv;O bond of the carbonyl ligand in the square planar complex *trans*-Pt(X)(X')(L)(CO).

The variable strength of the CO bond results from the electronic properties of the metal fragment *trans*-Pt(X)(X')(L). The bonding between the metal and CO involves electron donation from the carbonyl carbon atom to the metal, and back-donation from an occupied *d*-orbital of the metal center to the CO &pi;-antibonding orbital. The accompanying weakening of the CO bond is reflected in bond elongation and red-shift of the corresponding stretching frequency. This effect is the basis for the [Tolman electronic parameter](https://en.wikipedia.org/wiki/Tolman_electronic_parameter), which is often used to classify ligands according to their electronic properties.

### Fitness
The fitness associated to each set [X, X', L] is defined by the length of the C&equiv;O bond of the carbonyl ligand in the square planar complex *trans*-Pt(X)(X')(L)(CO) as provided by the following molecular modelling protocol:
1. assembling of 3D building blocks to generate an initial molecular model.
2. light-weight conformational search performed by [Tinker](https://tinkertools.org/) in the torsional space (bond lengths and angles are not changed).
3. geometry optimization by semi-empirical method PM6 as implemented in [Spartan](https://www.wavefun.com/spartan).

Since we want to run several experiments in little time, this exercise is designed to avoid the time-consuming molecular modelling part needed to obtain the value of the fitness. In fact, the fitness value for all the candidates that can be generated by the building block space has been preliminary computed.

Therefore, the fitness provider (i.e., the Python script named `fitness_provider_fromDB.py`) is only searching for the fitness value for a given Pt complex in the list of pre-computed fitness values.

## Instructions
> **Note**: You can save the plots by right-clicking on them and choosing `Save As...`. Similarly, you can save pictures of molecular models by right-clicking on them and choosing `File`->`Save`->`Save As PNG`.

1. Start DENOPTIM from within the `exercise_2.0` folder. This is done from the Terminal (macOS/Linux) or the Anaconda prompt (Windows):
```
cd your_path_to_exercise_2.0
denoptim input_parameters
```
2. Inspect the parameters:
	- In the `Genetic Algorithm` tab, weights of mutation and crossover to 0: the algorithm will do neither crossover nor mutation. Instead, the weight of construction from scratch is 1: all new candidates will be built randomly from scratch (we will refer to this as "construction-only" experiment). Also, the experiment will use an initial population, which you can look at by opening the `initPopulation.sdf` file. Note that these are complexes with short CO bond (i.e., low fitness).
	- The `Fitness Provider` tab configures the call to the external python script that "calculates" the fitness.
	- In the `Space of Building Blocks` tab, you find the names of the files collecting the building blocks and the APClass compatibility rules.
	- Do `File`->`Open` to inspect the scaffold fragment at `lib_scaffolds.sdf` file.
		> **Question 1:** Which one is the attachment point representing the coordination site for the dative (L-type) ligand? What is the *attachment point class* (APClass)?

	- Click on `File`->`Open` and inspect the `compatibility_matrix.par` file.
		> **Question 2:** Which APClasses can be used on the attachment point for the L-type ligand? And for the X-type ligand?

	- Click on `File`->`Open` and inspect the `lib_fragments.sdf` file. Look for the fragments that offer attachment points belonging to the APClasses you have identified in the previous step.
		> **Question 3:** Use your chemical experience and intuition to guess what set of ligands [X, X', L] can produce a high fitness. Discuss the likeliness of randomly picking such a set.

3. Go back to the input parameters by clicking on `Active Tabs` -> `Prepare GA experiment` and start the evolutionary design by clicking on `Run now...` and follow the dialog: Once the experiment is submitted, you will be notified on where the output is being written.
	> **Note**: As seen in exercise 1.0, the bar in the top-right part of DENOPTIM's window turns grey to indicate the experiment is running. When it turns blue again, the experiment is complete.

4. When the experiment has been completed, open the output from `File`->`Open Recent...` and select the appropriate path. This opens a "GARun inspector" tab where you find:

 	- The evolution plot (top-right panel): each point is a a candidate, click on it to display the structure and properties of the candidate. By default, the plot show two blue lines: the *minimum* and the *maximum* value of the fitness in the population. The button `Show/Hide Population Stats` allows to add also the mean and median.

  	- The monitor plot (bottom-right panel): collects numerical indicators of the algorithm behaviour, such as the number of attempts to create candidates, which is the series shown by default. The button `Show/Hide Population Stats` allows to add/remove series to the plot.

	> **Question 4**: With the exclusion of generation 0 (i.e., the initial population given as input), how does are the candidate's fitness values distributed over the fitness axis during the course of the experiment? Explain this distribution. (Hint: remember what we noted when inspecting the input parameters in point 2)

5. Run two more independent experiments starting from the same input parameters. By default, each experiment uses an independent sequence of pseudo-random events. Therefore, to get independent repeats you can switch back to the input parameters by clicking on `Active Tabs` -> `Prepare GA experiment`, and submit again with `Run now...`. You can submit more than one experiment in parallel.

6. Now we produce another set of GA experiments where we change the way the software is allowed to generate new candidates. Via `Active Tabs` -> `Prepare GA experiment` go back to the input parameters and do the following in the `Genetic Algorithm` tab:
	- set *Crossover weight* = 1
	- set *Construction weight* = 0

7. Submit three such "crossover-only" experiments via the `Run now...` button.

8. Inspect the results of these "crossover-only" experiments.

	> **Question 5**: Explain what you observe in the evolution and monitor plots? (Hint: plot the *Duplicate Pre-Fitness* series)

9. Now, we produce "mutation-only" experiments. Again, via `Active Tabs` -> `Prepare GA experiment` go back to the input parameters and set the following in the `Genetic Algorithm` tab:
	- *Crossover weight* = 0
	- *Mutation weight* = 1
	- *Construction weight* = 0

	As before, run three such experiments.

10. Inspect the results of these "mutation-only" experiments.

 	> **Question 6**: Compare mutation and crossover in terms of capability to introduce new structural features in the population.

11. Finally, we combine crossover, mutation and random construction (we'll call these the "complete GA" experiments). Again, via `Active Tabs` -> `Prepare GA experiment` go back to the input parameters and set the following in the `Genetic Algorithm` tab:
	- *Crossover weight* = 1
	- *Mutation weight* = 1
	- *Construction weight* = 1

12. Inspect the results of these runs as well. In particular, chose an experiment that produced a population with a high mean fitness and, from the GARun Inspector, click on `Open Population Graphs` to visualize the molecules in the population at a late stage of the experiment (high generation number).

## Discussion
- Briefly discuss how crossover and mutation operations are suitable to i) identify unknown structural features that lead to high fitness, ii) generate candidates by inheriting such features, and iii) combine features into new offspring. Try to refer to the observations from the "crossover-only" and "mutation-only" experiments.
- Report the sample size: the number of candidates (i.e., #offspring * #generations) that were visited before collecting at least 3 candidate with fitness higher then 1.151 Å. Compare this number with the size of the reachable search space, i.e., 10332. What is the sample size for "construction-only" experiments? What for "complete GA"?