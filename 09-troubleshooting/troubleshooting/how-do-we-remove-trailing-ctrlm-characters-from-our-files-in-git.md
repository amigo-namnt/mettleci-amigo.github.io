# How do we remove trailing CTRL+M characters from our files in Git?

# Problem

When deploying non-DataStage assets (e.g. `.sh`, `.txt` and `.sql` files) using MettleCI you get CTRL-M characters (Carriage Return, ASCII 13, Hex 0x0D) added to the files while deploying from a Git repository to a DataStage Engine host.

# Cause

Windows/DOS uses two characters to represent the end of a line: Carriage Return (ASCII 13, Hex 0x0D) and Line Feed (ASCII 10, Hex 0x0A) which together are commonly referred to using the abbreviation `CRLF`.

Unix, on the other hand, uses only a single Line Feed (`LF`) character. The seemingly superfluous CTRL-M characters, therefore, appears in text files when you transfer them from Windows to Unix.

This issue is most likely to be caused by one or both of the following things:

*   Those files in your remote repository (i.e. GitHub, Bitbucket, etc.) have been created or edited on a Windows platform where the editor application is adding the CTRL-M character as part of the `CRLF` line ending expected by Windows.
    
*   **If** you are using a local working copy of that Git repository to manage versions of those files before pushing updated versions to the remote repository, that **local** Git repository might have an `autocrlf` setting that is automatically converting the line endings to `CRLF` when checking out files or committing them to the repository.
    

# Solution

Check some of the problematic text and SQL files by…

1.  Downloading them (i.e. via your browser, **not** obtaining them via local `git` commands) from your remote Git management system (e.g. Github, Bitbucket, etc) to a Windows machine
    
2.  Opening the downloaded files in a text editor (e.g. [Notepad++](https://notepad-plus-plus.org/)) then click on **View** → **Show Symbol** → **Show All Characters** (or click the `¶` menu on the toolbar) to display all the hidden characters, including CR and LF.
    

If you are using a local Git repository to interact with your remote Git repository management system, and you are comfortable working with the Git command line, Github [provides some instructions](https://docs.github.com/en/get-started/getting-started-with-git/configuring-git-to-handle-line-endings) to get things set up correctly and to remove unwanted CRLF instances in your existing repositories.