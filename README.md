# Epigenomics Data Analysis: From Bulk to Single Cell

## Contributers

### Environment

To be able to contribute to this repository and render files locally, you will 
need to have `Quarto>=1.9.37` installed. This has not been tested on earlier 
versions of Quarto, so it may still work on older versions.

Once quarto is installed, add the following extensions via the terminal:

```bash
quarto add --no-prompt quarto-ext/fontawesome
quarto add --no-prompt royfrancis/quarto-revealjs-header
quarto add --no-prompt royfrancis/quarto-revealjs-pointer
quarto add --no-prompt mcanouil/quarto-collapse-output@1.4.0
quarto add --no-prompt royfrancis/quarto-accordion
quarto add --no-prompt royfrancis/quarto-leaflet
quarto add --no-prompt royfrancis/quarto-team
```

We will be using `R-4.6.0` coupled with Bioconductor release `3.23` for this
workshop. PLease make sure you are using the right `R` version when adding new
material. If you have multiple `R` versions installed on your machine, you can
use [rig](https://github.com/r-lib/rig) to open `RStudio` with the desired 
version as follows:

```bash
 rig rstudio 4.6 
```

### Setting up a local version of the repo and adding new material

Start by cloning the repository as such:
```bash
git clone https://github.com/NBISweden/workshop-epigenomics.git
cd workshop-epigenomics
```

We will be using `renv` to keep track of the `R` packages we are using. The 
`renv.lock` file contains all the `R` packages, under bioc `3.23` which are used
in all `qmd` files. The same lock file is use by github actions to build and
deploy the workshop's website.

To add new material, create your own branch and try to use concise and 
informative names. For example:
```bash
# create a new branch locally
git checkout -b addMotifMaterial

# push to remote repo
git push -u origin addMotifMaterial
```

Alternatively, you can create the new branch on GitHub, pull the updates to 
your local repo, and switch to that branch to work.

> [!TIP]
> You can use `RStudio` to modify your `.qmd` files and make changes. To
> do so you will need to create a project. Go to File > New Project > Existing >
> Directory and add the path to your installed repository called 
> `workshop-epigenomics` and click 'Create Project'. 

Next, we will install the `R` packages listed in the `renv.lock` file. You will
need to do runt he following commands the first time you are setting up. Make
sure that you are using the correct `R` version and that you are in the root
directory of the repo.
```r
# check status
renv:status()

# make sure the library paths are correct (should be pointing to the local renv folder)
.libPaths()

# download the R packages specified in the lock file
renv::restore()
```

Now you are set up to start making changes and add new material. If there are 
`R` packages you are missing, you can either: 
1. reach out to Dania, who can add them to the lock file (easiest solution)
2. add them to the lock file yourself as follows: 

```r
# check status of packages
# ... this should also report missing packages if they are present in .qmd files 
# ... but not present in the lock file
renv:status()

# install the missing packages
renv::hydrate()

# or: directly install a specific package
# ... always make sure that the .libPaths() are set correctly and that you 
# ... are in the root of the repo
renv::install("myPackage")

# update the lock file
renv::snapshot()
```

You will notice that the `R` packages were installed locally under the 
`renv/library` folder, which is ignored by `git` (see `renv/.gitignore`).

New material can be added by topic as follows:
- slides: `presentations/yourTopic`
- tutorials: `tutorials/yourTopic`

PDF slides may be added as presentation. However, if you are comfortable with 
quarto, we recommend creating quarto presentation to keep the repository at a
good size.

Finally, to visualize how the website may look with your added material, you
can run the following from the root:
```bash
quarto render
```

The resulting `html` files will be outputted under the `_site` folder. Once
you have finalized your changes on your branch, you can create a pull request
to the main branch and assign reviewers if you wish.

## Students

ToDo: add instruction for students on how they can clone the repo and use the
`renv` lock file to run the tutorials, and how they can access material from
previous years.
