# R-based analysis of INCLUDE data on CAVATICA

# Pushing data from the INCLUDE Data Hub to CAVATICA
INSTRUCTIONS / link to slides

# Using CAVATICA/Data Studio
1. Start an *Analysis* instance
   a) New *Analysis*:
      Go to *Data Studio* tab > Create new analysis
      Set analysis name
      Select RStudio
      Select latest R version in Environment setup (eg R 4.3 - BioC 3.17)
      Select default Instance type, Attached Storage, Suspend Time
      Click on Start and wait for instance to initialize

   b) Existing *Analysis*:
      Go to *Data Studio* tab
      Click on Start and wait for instance to initialize

2. You should now be in an RStudio instance
   a) To create a new Project by cloning from Github
      Go to File > New Project... > Version Control > Git
      Enter Repository URL, Project directory name (if different)
      Click on Create Project
      May need to enter Github Username and PAT
      Once project opens in RStudio, in R console run `renv::init()` to initialize project

   b) Previously created *Analyses* should resume with R Project already open in RStudio.
      If not, go to File > Open Project... > Select .Rproj file.

3. Open analysis R script(s) and work as usual

4. Copy R Project to `/sbgenomics/output-files/` for later access/download (see notes below).
   Suggest using `rsync -u` in Terminal tab to only copy changes.

## Notes on working in CAVATICA/Data Studio:

Instance will be terminated after idle time (or manually) and newly installed R packages will not persist.
However, running `renv::restore()` will reinstall packages from local project cache based on `renv.lock` file.

Data Studio working dir is be:
`/sbgenomics/workspace`
R Project working directory should be:
`/sbgenomics/workspace/<R_PROJECT_NAME>`
>[!NOTE]
>Files in these dirs can be previewed but not accessed by clicking on the *Analysis Name* in the *Data Studio* tab.

CAVATICA Project *Files* (eg files transferred from INCLUDE Data Hub) are here:
`/sbgenomics/project-files`
(actually a symlink to /sbgenomics/projects/<USERNAME>/<USERNAME>/<CAVATICA_PROJECT>)
>[!NOTE]
>This directory is **read-only** from within Data Studio

Files will need to be copied to:
`/sbgenomics/output-files/`
in order to be accessible from the *Files* tab in your CAVATICA Project 
>[!NOTE]
>Any files or dirs copied to this location **will not be accessible until after the Data Studio instance is terminated**.
>(this ~~may~~ will take a few minutes)
