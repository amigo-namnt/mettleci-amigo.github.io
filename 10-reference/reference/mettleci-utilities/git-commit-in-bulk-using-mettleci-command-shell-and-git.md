# Git Commit in Bulk Using MettleCI Command Shell and Git

When you have a large DataStage project which you wish to get under Git version control it would be onerous to have to commit each individual artefact using the MettleCI Workbench individually. A much more efficient approach to use the MettleCI Command Line Interface. This procedure requires your computer to have both a Git client and the MettleCI Command Line Interface installed. The primary input to the process is a whole-of-Project 'archive' ISX files for each Project you wish to import into Git.

# Initial commit procedure

1.  Ensure you have already [installed the MettleCI Command Line](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/488898631/Installing+MettleCI+Command+Line+Interface). 
    
2.  Ensure that the DataStage project ISX file(s) you wish to commit are available on your machine.
    
3.  Use your Git client to `clone` the remote Git repository you will be checking into.  Ensure the current branch is `master.`
    
4.  Check whether the cloned Git repository has a `datastage` directory at the root. If this doesn't exist create it now. This folder is **mandatory** in order for MettleCI's automated deployment function to operate correctly.
    
5.  Check whether the cloned Git repository has a `filesystem` directory at the root. If this doesn't exist create it now. This folder is **mandatory** in order for MettleCI's automated deployment function to operate correctly.
    
6.  Navigate to the command shell folder and locate the `mettleci.cmd` file.
    
7.  Run the command shell by executing either the mettleci or `mettleci.cmd` from the command line. This will start an interactive session, the current working directory does not matter.
    
8.  Run the `isx cut` command to split the project ISX file(s) into a **temporary directory**, this step can be repeated multiple times if there is more than one ISX for a given project. Documentation of this command can be found [here](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/458817574/ISX+Cut+Command).
    
9.  The cut ISX files will be dumped into your temporary directory in the following directory structure `<ISX source engine name>/<ISX source project name>/<category name - recursive>/<Job Name>.isx`
    
10.  Copy all ISX files and directories from within the `<source ISX project name>` directory to the `datastage` directory of  your cloned Git repository.  The final Git repository directory structure should match `datastage/<category name - recursive>/<job name>.isx`
    
11.  Use Git to add, commit and push all changes.  [Atlassian's Git tutorial](https://www.atlassian.com/git/tutorials/learn-git-with-bitbucket-cloud#copy-and-add-files) provides a good summary of how to do this.
    
12.  Verify the commit is visible in your Git repository against the Master branch.
    

> [!INFO]
> This procedure will generate ISX files which, although fully functional in all other respects, will **not** support the preview of the DataStage Job canvas by the [MettleCI Job Visualisation Plugin for Atlassian Bitbucket](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/733675614/Installing+the+MettleCI+Job+Visualisation+Plugin+for+Atlassian+Bitbucket).  Depending on the number of projects you need to complete, this process can easily be scripted, if required.

Once all production assets have been checked in, we recommend that you Tag this particular revision in case you need to quickly refer to it later in your DevOps-for-DataStage or DataStage Upgrade initiative. You can tag your Git repository revision using the Git command line or, in most cases, your Git repository’s user interface.