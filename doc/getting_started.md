# Getting Started
To get started with the DENOPTIM tutorials follow this procedure:
* get just a little bit of knowledge of the command line ([Step 1](header-cli))),
* install **conda** on your system ([Step 2](header-conda)),
* create an environment for running **DENOPTIM** ([Step 3](header-dnp_env) - this is where you install DENOPTIM),
* download data sets needed for the exercises ([Step 4](header-dataset)).

---
(header-cli)=
## Step 1: Get a Command line
Some very simple commands are used in these tutorials. Here is a good introduction to [learn the basics](https://swcarpentry.github.io/shell-novice/) (Chapters 1-3 are well more than enough).
For the tutorial, you can use any command line interface of your choice:
* On **macOS/Linux** you can use the default Terminal and skip this section.
* On **Windows** you can use [Git for Windows installer](https://gitforwindows.org/) following the steps in the
  [Carpentries video tutorial](https://www.youtube-nocookie.com/embed/339AEqk9c-8?modestbranding=1&playsinline=1&iv_load_policy=3&rel=0).

---
(header-conda)=
## Step 2: Install Conda
Since **conda** is extremely popular in data sciences, chances are you already have it installed and know how to use it. In this case, you can jump directly to the [section Create DENOPTIM Environment](header-dnp_env), below.

The instructions are inspired by and derived from work by [Software Carpentry](http://software-carpentry.org) and [CodeRefinery](https://coderefinery.org/) which is licensed under the terms of the [Creative Commons Attribution license 4.0](https://creativecommons.org/licenses/by-sa/4.0/).

Miniconda (and Anaconda, too) comes with a complete Python distribution that lets
you create isolated **environments** that don't affect anything else.
**conda** is the tool that manages these environments.

### Do I Have Conda?
On **macOS/Linux**, open a Terminal and run the following command. On **Windows**, open the Anaconda prompt from the Windows search bar (if Anaconda Prompt is not found, then install Miniconda as shown below):

```
conda list
```

If you have conda installed, a list of packages will be printed and you can skip the installation and go to the upgrade section.

### Installation: If you don't have Miniconda or Anaconda at all

- From the [Miniconda installer page](https://docs.conda.io/en/latest/miniconda.html),
  download Miniconda3 installer with the latest Python version.
- Follow [regular installation instructions](https://conda.io/projects/conda/en/latest/user-guide/install/index.html#regular-installation)
  of your operating system.
- Make sure selecting:
    - installing just for you
    - "Add miniconda3 to my PATH environment variable"
    - "Register Miniconda3 as my default Python 3.9"


### Upgrade: If you have Miniconda or Anaconda but you have not used it for a long time

- If you have only old Anaconda, but not Miniconda, then install Miniconda3
  following the instruction above.
- If you have old Miniconda (no matter if you have Anaconda or not), follow the
  instruction below and upgrade Conda. Please replace `anaconda` with `conda`
  in the instruction for Windows and macOS:
    - [Windows](https://docs.conda.io/projects/continuumio-conda/en/latest/user-guide/install/windows.html#updating-conda)
    - [macOS](https://docs.conda.io/projects/continuumio-conda/en/latest/user-guide/install/macos.html#updating-anaconda-or-miniconda)
    - [Linux](https://docs.conda.io/projects/continuumio-conda/en/latest/user-guide/install/linux.html#updating-anaconda-or-miniconda)


### Setting path to Conda from your terminal shell

This step is usually not needed, but if after the installation you still get an error message like `conda command not found` whey you type `conda --version` in your shell terminal.

#### Windows
  1. Go to the Miniconda3 (or if you have a relatively new Anaconda, then
     Anaconda3) folder. You can find it by serching from File Explorer search
     bar.
  2. Navigate to `etc` folder, and then to `profile.d` folder. You will find
     the `conda.sh` file.
  3. In the folder, right click and choose "Git Bash Here". You should be able
     to see the path to this folder in the Git Bash (something like
     ~/Miniconda3/etc/profile.d).
  4. Run the following command (type the following and enter):
     ```shell
     $ echo ". '${PWD}'/conda.sh" >> ~/.bashrc
     ```
  5. Close Git Bash and reopen it.
  6. Verify that now Git Bash can "see" conda by running `conda --version`
  After step 5 you may see this warning but this is nothing to worry about and will
  not show up the next time you open Git Bash:
  ```
  WARNING: Found ~/.bashrc but no ~/.bash_profile, ~/.bash_login or ~/.profile.
  This looks like an incorrect setup.
  A ~/.bash_profile that loads ~/.bashrc will be created for you.
  ```
  *Reference: ["Setting Up Conda in Git Bash", Sep 2020, at Codecademy
  Forums](https://discuss.codecademy.com/t/setting-up-conda-in-git-bash/534473)*

#### macOS
  1. Open a terminal window.
  2. Find the `.zshrc` file (or `.bash_profile` if your shell is Bash)
     which should be located in your home directory
     (/User/your-user-name)
  3. Navigate to the directory where `.zshrc` is located (or `.bash_profile` if your shell is Bash).
  4. Add the following in `.zshrc` file (or `.bash_profile`):
  ```shell
  export PATH="$HOME/miniconda3/bin:$PATH"
  ```

#### Linux
  1. Open a terminal window.
  2. Run this command which will append to your `.bashrc` file (adapt the path if Miniconda has been installed
     to a different place):
  ```shell
  $ echo 'source $HOME/miniconda3/bin/activate' >> ~/.bashrc
  ```
  If you prefer not to edit your `.bashrc`, you can also run this command after opening your terminal (each time you open one)
  and it will bring all `conda` commands "into view":
  ```shell
  $ source $HOME/miniconda3/bin/activate
  ```


### How to uninstall/remove Conda

If you wish to remove Conda again after the workshop, here is how:

- [Windows](https://docs.conda.io/projects/continuumio-conda/en/latest/user-guide/install/windows.html#uninstalling-conda)
- [macOS](https://docs.conda.io/projects/continuumio-conda/en/latest/user-guide/install/macos.html#uninstalling-anaconda-or-miniconda)
- [Linux](https://docs.conda.io/projects/continuumio-conda/en/latest/user-guide/install/linux.html#uninstalling-anaconda-or-miniconda)

---
(header-dnp_env)=
## Step 3: Create DENOPTIM Environment

We now ask **conda** to create a dedicated environment for the workshop. The environment required **DENOPTIM** do **conda** will install is and make it available within such environment.
1. Open a new terminal (macOS/Linux) or a new GitBash (Windows) after having completed the installation of **conda**.
2. If you have not done so during the installation of Miniconda (see above), activate `conda` in Miniconda first using `conda activate` or `source ~/miniconda3/bin/activate`. If neither works, please go back to the installation section. You probably need to restart your shell terminal. Then try `conda activate` or `source ~/miniconda3/bin/activate` again.
3. Run the following command:
```
conda env create -f  https://raw.githubusercontent.com/denoptim-project/workshop-May2022/main/environment.yml
```
4. Make sure that you see "dnp_workshop" in the output when you ask for a list of all available environments:
```
conda env list
```

### Activating the `dnp_workshop` environment

In the workshop, we will ask you to activate this environment. This operation must be done every time you have a new session on the terminal. For example, when you open a new terminal.

Then run the following:
```
conda activate dnp_workshop
```

If this does not work, the `dnp_workshop` part should be replaced with the whole path, for example:
```
source activate ~/Miniconda3/envs/dnp_workshop
```


### How to verify the environment

Once activated, try the following command:
```
denoptim -v
```

You should see an output like this and not see errors (exact version numbers are not too important):
```
V3.1.0
```


### Deactivating the `dnp_workshop` environment
Deactivating will remove the `denoptim` command, so it is an operation meant for when you are done working with the software. After deactivating, you can always re-activate the environment again.
```
conda deactivate
```

---
(header-dataset)=
## Step 4: Download Datasets
Download all the data [from this link](https://github.com/denoptim-project/workshop-May2022/archive/refs/tags/v1.2.0.zip).
