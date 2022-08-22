# Tutorials with DENOPTIM

This repository collects data sets for hands-on exercises to get started with DENOPTIM.
To just do the tutorials go to [https://denoptim-project.github.io/tutorials](https://denoptim-project.github.io/tutorials).


## Local Builds
Local builds are useful to develop new pages. If you are just interested in doing the tutorials, please ignore this page and go to [https://denoptim-project.github.io/tutorials](https://denoptim-project.github.io/tutorials).

### Environment
The compiled version of the tutorials is build with sphinx. To run sphinx you need also to load an environment with all the dependencies. You can use Conda to create such environment with this command:
```
conda env create -f doc/local_build.yaml
```
This is done only once on a machine. Then, every time you need to build locally, you can do just:
```
conda activate devel_dnp_tutorials

```

> The same dependencies are loaded also by the automated workflow that published the compiled documentation (see [.github/workflows/documentation.yaml](.github/workflows/documentation.yaml). Any change in either environment must be synched.

### Building with sphinx
From the distribution folder, which is where this very README.md file sits, run this command to build the webpages locally:
```
sphinx-build doc _build
```
Once the building is completed successfully, you can navigate the pages using the browser or your choice. From the CLI, you can do it like this on Mac:
```
open _build/index.html
```
on Linux:
```
xdg-open _build/index.html
```

## Contributing
Feel free to suggest changes and improvements. Fork this repo and make a pull request once you have created your suggested changes on your fork.

<b>Warning!</b> These tutorials use a dataset that might need to be updated upon introduction of changes. Any change that requires a change in the dataset will have to involve making a release of this repository to create a .zip/.tar.gz archive that can be linked in the [instructions about downloading the dataset](doc/getting_started.md).
