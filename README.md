## Using Git

[Basics](#basics)  
[Adding and Changing Things](#adding-and-changing-things)    
[Undo Changes and Recover Files](#undo-changes-and-recover-files)   
[Viewing Commits](#viewing-commits)  
[Branch and Merge](#branch-and-merge)  
[Commands for Remotes](remote-commands.md)  
[Favorites](#favorites)  
[Resources](#resources)

#### Note on Paths

In this file, directory paths are written with a forward slash as on MacOS, Linux, and the Windows-Bash shell: `/dir1/dir2/somefile`.    


## Basics

1. When using Git locally, what are these?  Define each one in a sentence
   * Staging area - ```The files containing source code prepared to be committed.```
   * Working copy - ```A copy of the file you're working on.```
   * master - ```A main branch of all working branches.```
   * HEAD - ```A label of our commits, which usually refers to the latest commit.```

2. When you install git on a new machine (or in a new user account) you should perform these 2 git commands to tell git your name and email.  These values are used in commits that you make:
   ```
   git config --global user.name "Napasakorn Boonkerd"
   git config --global user.email napasakorn.save@gmail.com
   ```

3. There are 2 ways to create a local Git repository.  What are they?
   - ```Create new repository by using "git init"```
   - ```Clone exiting ropository by using "git clone <url>"```

4. When you create a git repository by entering `git init`, Git will create a "hidden" directory for the local repository.  Where is the directory for this local repository (relative to the directory where you typed "git init")?
   ```
   The directory of this repository is the existing directory where you typed "git init"
   ```


## Adding and Changing Things

Suppose your working copy of a repository contains these files and directories:
```
README.md
out/
    a.exe
src/a.py
    b.py
    c.py
test/
    test_a.py
    ...
```     

1. Add README.md and *everything* in the `src` directory to the git staging area.
   ```
   git add README.md
   git add src/
   ```

2. Add `test/test_a.py` to the staging area (but not any other files).
   ```
   git add test/test_a.py
   ```

3. List the files in the staging area.
   ```
   git diff --name-only --cached
   ```


4. Remove `README.md` from the staging area. (Useful if you accidentally add something you don't want to commit.)
   ```
   git rm --cached README.md
   ```

5. Commit everything in the staging area to the repository.
   ```
   git commit -m "add new files"
   ```


6. Describe 2 steps to configure the repository so git will ignore all files in the `out/` directory:
   - ```
      Creat a file name ".gitignore" in the repository.
      ```
   - ```
      Type "out/" in file ".gitignore".
      ```

7. Command to move all the .py files from `src` to the top-level directory of this repository, so they are also moved in the Git repo.
   ```
   git mv src/a.py a.py
   git mv src/b.py b.py
   git mv src/c.py c.py
   ```

8. Commit this change with the message "moved src directory":
   ```
   git commit -m "moved src directory"
   ```


9. Command to add **all changed files** (but not untracked files) to the staging area using a single command.
   ```
   git add .
   ```

10. **Delete** the file `c.py` from your working copy **and** the repository:
      ```
      git rm -f c.py
      ```


## Undo Changes and Recover Files


1.  Display the differences between your *working copy* of `a.py` and the `a.py` in the *local repository* (HEAD revision):
      ```
      git diff HEAD a.py
      ```
2. Display the differences between your *working copy* of `a.py` and the version in the *staging area*. (But, if a.py is not in the staging area this will compare working copy to HEAD revision):
   ```
   git diff a.py
   ```
3. **View changes to be committed:** Display the differences between files in the staging area and the versions in the repository. (You can also specify a file name to compare just one file.) 
   ```
   git diff --staged <filename>
   ```

4. **Undo "git add":** If `main.py` has been added to the staging area (`git add main.py`), remove it from the staging area:
   ```
   git restore --staged main.py
   ```

5. **Recover a file:** Command to replace your working copy of `a.py` with the most recent (HEAD) version in the repository.  This also works if you have deleted your working copy of this file.
   ```
   git checkout a.py
   ```

6. **Undo a commit:** Suppose you want to discard some commit(s) and move both HEAD and "master" to an earlier revision (an earlier commit)  Suppose the git commit graph looks like this (`aaaa`, etc, are the commit ids)
   ```
   aaaa ---> bbbb ---> cccc ---> dddd [HEAD -> master]
   ``` 
   The command to reset HEAD and master to the commit id `bbbb`:
   ```
   git reset --hard bbbb
   ```

7. **Checkout old code:** Using the above example, the command to replace your working copy with the files from commit with id `aaaa`:
   ```
   git reset --soft aaaa
   ```
    Note:
    - Git won't let you do this if you have uncommitted changes to any "tracked" files.
    - Untracked files are ignored, so after doing this command they will still be in your working copy.
 

## Viewing Commits

1. Show the history of commits, using one line per commit:
   ```
   git log --oneline
   ```
   Some versions of git have an *alias* "log1" for this (`git log1`).

2. Show the history (as above) including *all* branches in the repository and include a graph connecting the commits:
   ```
   git log --graph
   ```

3. List all the files in the current branch of the repository:
   ```
   git ls-files
   ```
   example output:
   ```
   .gitignore
   README.md
   a.py
   b.py
   test/test_a.py
   test/test_b.py
   ```


## Branch and Merge

1. Create a new branch named `dev-foo`:
   ```
   git checkout -b dev-foo
   ```
2. Display the name of your current branch:
   ```
   git branch --show-current
   ```
3. List the names of **all** branches, including remote branches:
   ```
   git branch -a
   ```
4. Switch your working copy to the branch named `dev-foo`:
   ```
   git checkout dev-foo
   ```

5. **Merge:** To merge the work from `dev-foo` into the master branch, perform these steps:
   1. step one
      ```
      # check out the branch 'master' which is the branch wished to merge into.
      git checkout master
      ```
   2. step two
      ```
      # run git merge command with the branch name that you want to merge.
      git merge dev-foo
      ```


6. Describe under what conditions a merge may fail.
   ```
   A merge may fail if the same part of the same file in two branches has something that differs.
   ```



## Favorites

- ```To remove a file from the staging area, use the command "git rm --cached <filename>."```
- ```To list all the files in current working, use the command "git ls-files"```
- ```To list all the files in staging area, use the command "git diff --name-only --cached"```

---
## Resources

My favorit Git resources: [Bitbucket](https://www.atlassian.com/git/tutorials/learn-git-with-bitbucket-cloud) for basics of Git commands.  
[Pro Git Online Book][ProGit] Chapters 2 & 3 contain the essentials. Downloadable PDF is also available.     
[Visual Git Reference](https://marklodato.github.io/visual-git-guide) one page with illustrations of git commands.

Try Git:

[Learn Git Interactive Tutorial][LearnGitInteractive] excellent visual tutorial.   
[Git Visualizer][VisualizeGit] execute Git commands in a web browser and see the results as a graph.    

[ProGit]: https://www.git-scm.com/book/en/v2 "Pro Git online book on Git-scm.com"
[ProGitPdf]: https://progit2.s3.amazonaws.com/en/2016-03-22-f3531/progit-en.1084.pdf "Pro Git v.2 PDF on AWS. Longer, book format."
[LearnGitInteractive]: https://learngitbranching.js.org "Interactive graphical git tutorial"
[VisualizeGit]: http://git-school.github.io/visualizing-git/ "Online tools draws a graph of commits in a repo as you type"
[markdown-cheatsheet]: https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet
[github-markdown]: https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax
[vscode-markdown-preview-enhanced]: https://marketplace.visualstudio.com/items?itemName=shd101wyy.markdown-preview-enhanced
