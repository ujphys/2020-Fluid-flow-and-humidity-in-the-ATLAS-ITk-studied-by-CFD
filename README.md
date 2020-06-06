# 2020-Fluid-flow-and-humidity-in-the-ATLAS-ITk-studied-by-CFD

## Getting started

Make you are using a Github account that has access to this repo, that the computer you are using has an SSH key that is uploaded to Github and that you SSH is configure to use that key to connect to github.com.

Use an existing key, or generate a new key like this:

    cd ~/.ssh/
    ssh-keygen -t rsa -b 4096 -C "si@mykonos.org.za"

call it something, e.g. github_rsa

    cat github_rsa.pub

Go to github.com, click settings, add SSH key, paste the contents from above.

Edit `~/.ssh/config`:

    Host github.com
	    User git
	    IdentityFile ~/.ssh/github_rsa

Then clone:

    git clone github.com:ujphys/repo_name.git


## Workflow
#### 1. Pull the latest master code
    git checkout master  
    git pull

#### 2. Checkout a new local branch to work on  
    git checkout -b mybranch
(replace "mybranch" with a descriptive name)

#### 3. Make changes as necessary
Try to split changes into multiple commits, each of which makes a clear, logically connected set of changes, that can easily be described in a sentence or two.

#### 4. Push changes to github
- option 1: (safe option) Create a github pull request.  
  Push the branch you are currently working on to github:

      git push origin mybranch

  Then create a github pull request. See for example https://help.github.com/articles/about-pull-requests/. We can then all see the changes, check them, and merge them when we are happy.

OR (only do this if you are sure about the commit and don’t need someone to look it over)

- option 2: (less safe option) Merge directly to master.

      git checkout master  

  Check if there are more recent changes to master in the meantime

      git pull

  if no changes present

      git merge --no-ff mybranch  
      git push origin master

  if changes were present, the neatest option is to rebase onto them:

      git checkout mybranch
      git rebase master
      git checkout master
      git merge --no-ff mybranch
      git push origin master

  **Notes**:  
  ** if there have been more recent changes, you can merge them in. However, it makes the history neater if you rather rebase your branch onto the latest master before continuing.

  The --no-ff flag prevents a fast-forward merge. This makes the history more explanatory — you can see that some changes were grouped together. Read up on fast forward merges for more details

## Installation
Platform specific installation notes are available for some systems:
  * Mac: README_mac_install.md
  * Ubuntu: README_ubuntu_install.txt
  
If you install on antoher system, like CentOS, please add a similar readme

#### Requirements 
- cmake (A recent version, probably >= 3)
- SFML >= 2
- ROOT
- galib (see notes about installing galib below)
- boost
- libssh
- vtk
- geant4
- json.hpp

#### galib

**Note:** Not confirmed if instruction below are still current. 

galib 2.4.7 is somewhat broken with recent compilers. It needs some code changes before it will compile. Once you have extracted it:

    cd galib247
    sed -i 's/initializer(GA/this->initializer(GA/g' ga/GA?DArrayGenome.C
    sed -i 's/crossover(GA/this->crossover(GA/g' ga/GA?DArrayGenome.C
    sed -i 's/comparator(GA/this->comparator(GA/g' ga/GA?DArrayGenome.C
    sed -i 's/mutator(GA/this->mutator(GA/g' ga/GA?DArrayGenome.C

#### json

The json library is in some package managers. 

If that does not work, you can download json.hpp from https://github.com/nlohmann/json/releases. Then move it somewhere in your path, for example:

    mkdir /usr/local/include/nlohmann
    sudo mv json.hpp /usr/local/include/nlohmann/

## Python Environment
(**Note:** if you update this instructions, please also update the instructions in the main README_mac_install.md file.)

The code under the `imaging/` folder requires a Python installation. At the time of writing, the various packages did not like to play nicely together, so this is a bit finicky. The quickest way to get a working environment is to import Martin's conda environment. 

First, install conda, the smallest version of which is Miniconda. Anaconda includes more packages and is a bigger download. Go to the setup folder (which should have a file called `py3imaging.txt`), and run:

    conda create --name py3imaging --file py3imaging.txt -c conda-forge -c menpo -c astra-toolbox -c anaconda -c nlesc

To activate the environment:

    source activate py3imaging 

