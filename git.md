
# Renaming the Local master branch to main
$ git branch -m master main





# Changing the Last Commit Pushed or not Pushed
https://linuxize.com/post/change-git-commit-message/

### Changing the Most Recent Commit
*Before changing the commit message, you can also add other changes*
$ git add .
$ git commit --amend -m "New commit message."
*If it is pushed, force push to update the history of the remote repository*
$ git push --force <remoteName> <branchName>

### Changing an Older or Multiple Commits
*N is the number of commits to perform a rebase on*  
$ git rebase -i HEAD~5  
*this displays the latest X commits in your default editor*  
*Move to the lines of the commit message you want to change and replace pick with reword*  
*Save the changes and close the editor*  
*For each chosen commit, a new text editor window will open. Change the commit message, save the file, and close the editor.*  
Force push the changes to the remote repository  
$ git push --force <remoteName> <branchName>






# Get remote branch to local repo, 2 ways:

### create mybranch and track origin/abranch
$ git checkout -b mybranch origin/abranch
*(new local branch has different name with tracked remote branch)*

### only create 'abranch', with the same name in remote repo
$ git checkout --track origin/abranch
*(new local branch has the same name with tracked remote branch)*





# Escape from vim
$ git commit 
*if you write the commit command without -m, a vim editor is opened.*

**For escape from vim without saving:** tap i (input mode) and then ESC
**For escape from vim with saving:** write this three char -> :wq 

<esc> :w <enter>
to write to the file and

<esc> :q <enter>
to quit. Note: things in <> denote key presses.





# How to check the differences between local and github before the pull
https://stackoverflow.com/questions/6000919/how-to-check-the-differences-between-local-and-github-before-the-pull
$ git fetch origin

### to see code differences
$ git diff main origin/main

### to see commits that differ from each other
$ git cherry main origin/main
$ git cherry origin/main main





# 5 steps to change GitHub default branch from master to main
https://stevenmortimer.com/5-steps-to-change-github-default-branch-from-master-to-main/

## Step 1 
### create main branch locally, taking the history from master
$ git branch -m master main

## Step 2 
### push the new local main branch to the remote repo (GitHub) 
$ git push -u origin main

## Step 3
### switch the current HEAD to the main branch
$ git symbolic-ref refs/remotes/origin/HEAD refs/remotes/origin/main

## Step 4
### change the default branch on GitHub to main
### https://docs.github.com/en/github/administering-a-repository/setting-the-default-branch

## Step 5
### delete the master branch on the remote
$ git push origin --delete master





# How to Gitignore (untrack) files already pushed to GitHub repository.
https://dev.to/ademola_isr/how-to-gitignore-untrack-files-already-pushed-to-github-repository-1h96

## Step 1 
### Clean the tree
$ git add .
$ git commit -m "message"

## Step 2 
### Remove all the files in the repository.
$ git rm -r --cached
*adding -cached allow us to remove the files from the index. Our files are still present*

## Step 3
### Add everything and push
$ git add .
$ git commit -m "gitignore fix"
$ git push