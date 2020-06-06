#This repo is for LaTeX documents.
##Please don't commit auxiliary files, logs etc. Only the source documents, *.tex, *.bib, figures

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

