# Git Notes

### Mottos

- The changes that are committed are those that have been added to the index (staged changes)
- Frequently rebase your feature branch to make process of resolving conflict easier in the future. (diverged commits between the main and the feature branches)

### Renaming the Local master branch to main

> git branch -m master main

### Creating empty commit

> git commit --allow-empty -m "Upgrading to heroku-22"

### See the commit history

> git log --pretty=oneline
> git log --oneline

### to see remote repo address

> git remote -v
> git remote -v origin

### to add remote address to git for the directory

> git remote add origin git-url-address.git

### to set new remote address for the directory

> git remote set-url origin git-url-address.git

## Get remote branch to local repo, 2 ways:

### create newbranch and track origin/xbranch

> git checkout -b newbranch origin/xbranch

_(new local branch has different name with tracked remote branch)_

### create a branch with the same name in remote repo

> git checkout --track origin/xbranch

_(new local branch has the same name with tracked remote branch)_

### Push a branch to remote

> git checkout <branch>
> git push -u origin <branch>

or

> git checkout <branch>
> git push -u origin HEAD

## Switch to a specific commit then go back to the present

### Go to a specific commit state

_you can use a commit hash_

> git checkout a1b2c3

_you can use a tag name_

> git checkout v2.0.0

_you can use a tag name either with /tags prefix_

> git checkout tags/v2.0.0

_now we are in a state known as "detached HEAD", don't make any new commit here_

### Go back to main or master

> git checkout main

### Add an alias with command parameters in global

> git config --global alias.amend 'commit --amend --no-edit'

Then, use like below:

> git amend

### git reset SOFT, MIXED, HARD

Let's assume there are A, B, C, and D commits.  
_A - B - C - D <- HEAD --- A - B - C - D <- INDEX_

**Soft: If you would want to B, C, and D are in one commit**

> git reset --soft Ref-A  
> git reset --soft HEAD~3 (in this example)
> _A <- HEAD --- A - (B - C - D) <- INDEX_  
> Soft reset pretends to the changes are staged (index matches D) and you haven't did commit, so you can:  
> git commit -m "new commit message"
> _A - E <- HEAD --- A - E <- INDEX_

**Mixed: If you would want to B, C, and D are in two or more commits**

> git reset --mixed Ref-A it is default, and same with (> git reset Ref-A)  
> git reset --mixed HEAD~3 (in this example)
> git reset --mixed HEAD~1 (last commit)
> _A <- HEAD --- A <- INDEX_ but changes in B, C and D are still as it is  
> Mixed reset pretends to the changes are even not staged (index matches HEAD) and you haven't did commit, so you can:  
> `git add` and `git commit` in a different grouping, either one, two or more

**Hard: If you would want to B, C, and D are removed completely with all changes**

> git reset --hard Ref-A  
> git reset --hard HEAD~3 (in this example)  
> git reset --hard HEAD~1 (last commit)
> _A <- HEAD --- A <- INDEX_ all changes in B, C, D are completely removed  
> Hard reset pretends to you did not any changes after A.

**Hard: If you would want to B, C, and D are in different branch stemming from A**

> git branch <newbranch>  
> then now, you can do hard reset  
> git reset --hard Ref-A
> _A <- HEAD --- A <- INDEX_ all changes in B, C, D are completely removed but the commits A,B,C,D are in the <newbranch>
> You should always run `git status` before doing a hard reset to make sure your working directory is clean or that you're okay with losing your uncommitted changes. Anyway, you can recover any committed changes with the reflog; uncommitted changes that are removed with reset --hard are gone forever.

**As a Summary**
--soft : HEAD moves to the Ref, changes are left staged (in index).  
--mixed : HEAD moves to the Ref, unstage changes (extracted from index), changes are left in working tree.  
--hard : HEAD moves to the Ref, unstage changes (extracted from index), delete the changes as well as any uncommitted changes

## Changing the Last Commit Pushed or not Pushed

https://linuxize.com/post/change-git-commit-message/

### Changing the Most Recent Commit

_Before changing the commit message, you can also add other changes_

> git add .
> git commit --amend -m "New commit message."
> _Amends a commit without changing its commit message_
> git commit --amend --no-edit
> _If it is pushed, force push to update the history of the remote repository_
> git push --force
> git push --force <remoteName> <branchName>

### Changing an Older or Multiple Commits

_N is the number of commits to perform a rebase on_

> git rebase -i HEAD~5  
> _this displays the latest X commits in your default editor_  
> _Move to the lines of the commit message you want to change and replace pick with reword_  
> _Save the changes and close the editor_  
> _For each chosen commit, a new text editor window will open. Change the commit message, save the file, and close the editor._  
> Force push the changes to the remote repository  
> git push --force <remoteName> <branchName>

## How to check the differences between local and github before the pull

https://stackoverflow.com/questions/6000919/how-to-check-the-differences-between-local-and-github-before-the-pull

> git fetch origin

### to see code differences

> git diff main origin/main

### to see commits that differ from each other

> git cherry main origin/main
> git cherry origin/main main

# Tags

**A tag is used to label and mark a specific commit in the history.**
https://git-scm.com/book/en/v2/Git-Basics-Tagging
https://stackoverflow.com/questions/35979642/what-is-git-tag-how-to-create-tags-how-to-checkout-git-remote-tags

### to list the tags in local

> git tag

### to add a tag annotated for the current HEAD in local

> git tag -a tag_name -m "message"

### to add a tag annotated for a previous commit in local

> git tag -a v1.0 -m "message" 9fceb02

### to add a tag lightweight in local

> git tag v12.0

### to push the local tags to remote

_By default, the git push command doesn’t transfer tags to remote servers, so needs --tags flag_

> git push origin v1.5 _// a specifig tag_  
> git push origin --tags _//all tags_

### to delete the tag in local

> git tag -d v1.0
> _Note that this does not remove the tag from any remote servers._

### to delete the tag in remote

> git push origin --delete v.1.0

### to get the tags from remote into local

> git fetch --all --tags

# 5 steps to change GitHub default branch from master to main

https://stevenmortimer.com/5-steps-to-change-github-default-branch-from-master-to-main/

## Step 1

### create main branch locally, taking the history from master

> git branch -m master main

## Step 2

### push the new local main branch to the remote repo (GitHub)

> git push -u origin main

## Step 3

### switch the current HEAD to the main branch

> git symbolic-ref refs/remotes/origin/HEAD refs/remotes/origin/main

## Step 4

### change the default branch on GitHub to main

### https://docs.github.com/en/github/administering-a-repository/setting-the-default-branch

## Step 5

### delete the master branch on the remote

> git push origin --delete master

# How to Gitignore (untrack) files already pushed to GitHub repository.

https://dev.to/ademola_isr/how-to-gitignore-untrack-files-already-pushed-to-github-repository-1h96

## Step 1

### Clean the tree

> git add .
> git commit -m "message"

## Step 2

### Remove all the files in the repository.

> git rm -r --cached <file> > _adding -cached allow us to remove the files from the index. Our files are still present_

## Step 3

### Add everything and push

> git add .
> git commit -m "gitignore fix"
> git push

### Go back to the selected commit on your local environment

> git checkout <commit-id> .
> Don’t forget the final ‘.’ — You aren’t required to add this, and it may look like it has worked but if you leave this off it will take you to a new “detached head state” where you can make changes and it will allow you to make commits, but nothing will be saved and any commits you make will be lost.

# Escape from vim

> git commit
> _if you write the commit command without -m, a vim editor is opened._

**For escape from vim without saving:** tap i (input mode) and then ESC
**For escape from vim with saving:** write this three char -> :wq

<esc> :w <enter>
to write to the file and

<esc> :q <enter>
to quit. Note: things in <> denote key presses.
