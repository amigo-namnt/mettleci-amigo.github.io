# Jenkins Pipeline produces error 'No such DSL method findFiles'

# Symptom

At the end of a Jenkins Pipeline deployment step (using the `mettleci datastage deploy` command) you receive an error message that looks like this...

```
Command failed.

No such DSL method 'findFiles' found among steps 
[acceptGitLabMR, addGitLabMRComment, archive, bat, build, ... ]
```

# Cause

Your Jenkins platform does not have the [findFiles](https://www.jenkins.io/doc/pipeline/steps/pipeline-utility-steps/#findfiles-find-files-in-the-workspace) command available as you don’t have the [Pipeline Utility Steps](https://plugins.jenkins.io/pipeline-utility-steps/) plugin installed.

# Solution

Install the [Pipeline Utility Steps](https://plugins.jenkins.io/pipeline-utility-steps/) plugin in your Jenkins platform.