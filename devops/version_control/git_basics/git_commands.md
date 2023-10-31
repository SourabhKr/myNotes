## Git Commands

### Working, Staging, Committed

#### Working:
> To clean the working directory and delete the new files added in the working directory not staged or committed:<br>
**git clean** : Used to clean the working directory, by recursively removing the files that are not under version control, starting from the current directory. If any <path> is given only those paths are affected. <br><br>
**-d**  normally git clean will  not delete the untracked directory, recursively. Add this flag to track and delete those. <br> **-f**  to forcefully delete if git configuration variable clean.requireForce is not set to false. <br> **-n** to not delete but only show the files that will be impacted(dry run). <br>
Ex: `git clean -nfd` (to show which all files in the working directory will be delete)<br>
    `git clean -fd` -- to actually delete the files. <br>    
Show the list of files that will be added with the next commit <br>
`git ls-files --others --exclude-standard` <br><br>
For restoring all the files from the staging, the current working directory will be overwritten with the existing commit.<br> 
    `git resotre .` <br>
    `git restore <path>` -- for a specific file. 

<br>

#### Staging

> To see the difference in the changes done in staging and not yet committed. <br> `git diff`: The git diff command displays the changes between the working directory and the staging area. It is used in combination with git status and git log commands for analyzing the state of a git repository. The `--cached` option displays the changes between the staging area and the HEAD. It shows what has been added to the staging area and staged for a commit. <br> <br>
`git diff` HEAD command shows all the changes made between the working directory and HEAD, including changes in the staging area. It displays all the changes since the last commit, whether staged for commit or not. <br>
`git diff --cached` <br>
`git diff --name-only --cached`  -- for a specific file <br>
`git diff --cached --name-only --diff-filter=A`	  <br><br>
**Un-stage the files in Git** <br>
`git reset HEAD -- path/to/file` <br>
`git reset HEAD -- .`

