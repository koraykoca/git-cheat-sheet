# GIT - a Version Control System

Git is a Version Control System (VCS) which is widely used in practice. It makes easier to work on a project as a team. You can track changes on the code and communicate with your team mates through the code remotely.

In the Git version control system, every state is called a commit, which describes the changes from the previous version. Every file in the project, together with the history, is stored in a repository (a directory). You can manage Git repositories either from your IDE, or from the command line.

You can create your own repository or you can fork a repository which is already created by someone else.

## Basic Git Commands

To ensure proper attribution of your contributions, it is essential to configure your identity in Git prior to committing changes. To do this, execute the following commands in your terminal to set your Git username and email:

```bash
git config --global user.name <your_name>
git config --global user.email <your_email>
```

To start a repository in the current directory, use _**git init**_. Then add the url of the remote repository:
```bash
git init
git remote add origin <repo_url>
git fetch
```

Or clone the repository on your local machine. To be able to clone with SSH, add SSH Key to GitHub/GitLab profile. Process:
```bash
ssh-keygen  # This will create id_rsa.pub. Copy the value of the public SSH key (id_rsa.pub) and add it to your GitHub/GitLab account in settings. 
git clone <SSH-URL-for-the-repository>
# if permission denied error occurs, do the following
ssh-add <path-to-id_rsa>
```
If we work on someone else's project, we need to fork the project first. Then we will use _**git clone**_ command as following:
```bash
git clone <repository_url>
```
With the command without flags, you will clone whole project with all branches. After cloning the repository, we can see them locally. 

If we want to clone a branch:
```bash
git clone --single-branch --branch <branchname> <repository_url>
```

If we want to clone a specific branch from already cloned repo:
```bash
git fetch <repo_url or remote_name> <remote_branch_name>:<give_a_name_for_local_branch>
# Example: git fetch https://github.com/qgis/QGIS.git release-3_24:release-3_24
```

> git fetch command only downloads the data to your local repository — it doesn’t automatically merge changes with any of your work or modify what you’re currently working on. You have to merge/incorporate changes manually into your work when you’re ready.

Now we can make changes on them on our machine. After editing, we can send our local changes to the online repository so that our teammates will be able to see our changes. For this, we use _**git add**_ command. If we want to add all files we made changes on, then we can use _** git add -u**_. If we want to add everything including new files, we can use _**git add --all**_ or _**git add .**_ command. When we want to add only a specific file, we use _**git add <name_of_the_file>**_:

```bash
git add --all  # or git add .
# or we can specify the file
git add <file1_name>
# or we can specify many files
git add <file1_name> <file2_name> <file3_name>
# or we can exclude new files and just update all tracked files
git add -u  
# or we can decide which changes to include in the current commit
git add -p
# or we can add all, but exclude some files
git add .
git reset -- <excluded_file>
# remove back an added file
git rm --cached <file_name>
```

When we want to discard changes and undo the add command, we can use _**git reset <file_name>**_ command. We check always the status of our GIT using _**git status**_ command. This command shows us what branch we're on, what files are in the working or staging directory, and any other important information. We will save our changes to the local repository with _**git commit**_ command. We can inform our teammates about the changes with a short message. For this, we will use the following to commit the file and set the commit message:

```bash
git commit <name_of_the_file> -m <"commit_message">
```

If you issue a git commit without specifying a commit message, the default Git editor (Vim) will pop up. Here, you can write your commit message. However, we can make e.g. Notepad++ as Git’s editor by executing the command:
```bash
git config --global core.editor <path_to_notepad++.exe> -multiInst -notabbar -nosession -noPlugin
```

Git can ask about our identity after executing this command. In this case we will set our name and e-mail address as:

```bash
git config user.name <user_name>
git config user.email <email_address>
```

Now we are ready to send our changes to the online repository, so that they can be shared with the rest of the world. However, when somebody else on our team made some changes in the repository which we don't have them on our local repository, we need to _**pull**_ these remote changes because there can be some kind of conflicts between what we have locally and what is living online. In this case _**git pull**_ command takes recent changes that are living on the remote repository and get them to the local repository.
After that we can send our changes without problem with _**git push**_ command. This command uploads all local branch commits to the remote. We can check where our remote target is with _**git remote -v**_ command.

```bash
git push
```

## Git Branching

Branching means that we diverge from the main line of the development and continue to work without messing with that main line. We prefer to work on the copy of the master branch and work on the project independently from our teammates. After that we will merge our changes/branch with the main branch. To create a new branch, we use _**git branch**_ command. To switch to an existing branch, we use _**git checkout**_ command. This command switches to the specified branch and updates the working directory. 

```bash
git branch <branch_name>
git checkout <branch_name>
git checkout -  # checkout to the previous branch you were working with (it's similar to `cd -` for directories)
```

It's typical to create a new branch and switch to that new branch at the same time. This can be done in one operation with

```bash
git checkout -b <branch_name>
```

You can change the name of the current branch with this command:
```bash
git branch -m <new_name>
```

When we want to push something that is in our new branch to the main/master branch, we need to first switch to the main branch. Then, we use _**git merge**_ command to merge our new branch into the main branch. After merging, we will be done with the new branch which we created and can delete it with _**git branch -d branch_name**_. If we don't want to delete and keep the branch also on the remote repository, we use 
```bash
git push --set-upstream origin <branch_name>
```
But generally, the whole process will be like as the following:
```bash
git checkout -b <branch_name>  # branch creating and switching to it
# After doing some changes on the files
git add <file_name>            # changes are staged in order to be committed
git commit -m <"some_message"> # telling what you changed/did
git checkout main              # switching to the main branch
git merge <branch_name>        # get changes back to the main branch
git push                       # changes pushed to the main branch
git branch -d <branch_name>    # deleting the new branch
```

Some operations with branches:
```bash
git branch -a                             # to see branches
git remote set-head origin -a             # to make current checkouted branch origin
git branch -m <oldname> <newname>         # to change the name of a branch
git branch -u origin/<BRANCH> <BRANCH>    # to set up a branch to track a remote branch
git branch -d <branch_name>               # to delete branch locally
git push origin --delete <branch_name>    # to delete branch remotely
git fetch origin                          # to retrieve all branches and updates
git fetch origin --prune                  # to connect to a shared remote repository remote and fetch all remote branch refs. It will then delete remote refs that are no longer in use on the remote repository
```

## Operations with commits
- Add a new code change to previous commit
```bash
git add <modified_file>
git commit --amend  # if you want to change the commit message
git commit --amend --no-edit  # if you don't want to change the commit message
git push  # if you didn't push the commit to remote
git push -f origin <branch_name>  # if you pushed the commit to remote before 
```
- Change last commit message
```bash
git commit --amend -m "new commit message"
```
- Change or delete previous commit messages
```bash
git rebase -i <a-commit-hash>  # find commit hash with git log command
# write "edit" in front of the commit that you want to change 
# change the message with git commit --amend
git rebase --continue

# Or
git rebase -i HEAD~n  # start an interactive rebase for the last n commits
# To remove a commit, delete the corresponding line. To edit a commit, replace the word pick with edit next to the commit you want to amend.
```

- Undo the last commit but keep changes
  
After running the following command, the changes will be not-staged changes in the working directory
 ```bash
  git reset --soft HEAD~1  # it will return to the "1" before the current revision
```
- Undo the last commit and reset changes
```bash
git reset HEAD@{1}  # it will remove the changes in your staged files
git reset --hard HEAD~1  # it will remove all changes in your unstaged and staged files
git push -f origin <branch_name>
```

- `git cherry-pick`: This command is used to apply changes from a specific commit, or to apply a commit from a branch: 
```bash
# merge a commit from another branch to master
git checkout master
git cherry-pick <commit SHA>  # to apply changes from a specific commit
git cherry-pick <first_commit_SHA>^..<second_commit_SHA>  # to include a range of commits from one specific commit up to another
```

- You can put a push rule for commit messages in Gitlab:
 `Menu > Projects > Settings > Repository > Push Rules`

## Git Rebase
Git rebase rewrites commits from one branch onto another branch. It is a useful alternative to merging and it gives us a cleaner linear history. Rebase means we are making the last commit of the target branch (e.g. main branch) base commit of our branch, and then we will add/move our commits onto this base commit. 

```bash
# in feature branch
git rebase main
```

Cleaner history helps us troubleshoot bugs faster. Therefore, before making a pull request from our branch into main/master branch, it can be better to use git rebase instead of git merge and then create a pull request. However, if you have commits which other team members pulled them down and worked on them, then rewriting those commits and pushing them again will be not a good idea, because other team members will have to re-merge their work and things will get messy when you try to pull their work back into yours. 

Git rebase is also useful when you solve conflicts in a PR. After solving the conflicts, you can force push and update your PR. 

## Pull Request (PR)
A PR is created to ask owner of the project to pull your changes. You are asking the main/master repository's owner to pull files from your repository. This process is like following:

- there is an accessible repository,
- you can fork it,
- you can clone the forked repository and make changes in your own fork,
- you can push your changes to your own fork,
- you can make a pull request from your own fork and the owner of the upstream repository, which you cannot push directly to, will decide whether or not to merge your pull request.

To test the pull request, we can do as following:
```bash
git fetch origin pull/<Pull ID>/head:<BRANCHNAME>  # BRANCHNAME: give a name for branch will be being created.
git checkout <BRANCHNAME>  # test the code in this branch
```
After testing, you can checkout to the main/master branch.

## Git stash
_**git stash**_ command is great when we are not ready to commit the changes, but we want to switch branches or we want to rewert back temporarily to where you started. We can do a stash on these changes and git will save them in a temporary space. 
```bash
git stash save <a_message>  # create a stash
git stash push -m <a_message> <file_path>  # to save a specific path to the stash
git stash list              # see the stashes 
git stash apply <stash_id>  # apply the changes in the stash
git stash pop               # take the first stash in the list, apply those changes and delete/drop the stash 
git stash drop <stash_id>   # delete the stash
git stash clear             # delete all stashes
```

We need to commit our changes then pull the remote repo then we push our changes. A good workaround for this is following:
```bash
git stash       # put aside all the uncommitted changes you have 
git pull        # do whatever you want, for example pull
git stash pop   # get the latest item you put aside
```

When you apply a stash (or popping out commits using the git stash pop command), merge conflicts may occur. You can solve them or abort the whole git stash process. To abort the process, you can run: 
```bash
git reset --merge
```

## Updating Forked Repository 

When there are changes or new branches in the main repository, we need to take them into our forked repository to be able to work on them. First of all, we need to go to the directory where we cloned the repository. We set the original repository as our upstream repository and we fetch the upstream from the original repository. After that, we will create and checkout to the branch which was newly added to the original repository (to create a branch in the same repo, _**git branch branch_name**_ or, more commonly _**git checkout -b branch_name**_, the latter creates the branch then checks it out so we can immediately start working on it) and pull the changes into our local repository then push to the forked repository. The process is as following:

```bash
git remote add upstream <original_repo_url>  # upstream points the original repo
git fetch upstream   # fetch tells git: "download the data to the local repository , but don't automatically merge it"
git checkout -b <original_repo_branch_to_transfer>
git pull upstream <original_repo_branch_to_transfer>  # pull tells git: "fetch it, and also merge it with my current branch."
git push --set-upstream origin <original_repo_branch_to_transfer>
```

## .gitignore file
Sometimes we want GIT to ignore some files in the Repo folder like log files. In this case we need to specify these files in .gitignore file. An example file can be found in this repository. 
```bash
touch .gitignore                          # create the file in the current local repo folder
git config core.excludesFile .gitignore   # configure it
echo cockpit.pro.user >> .gitignore       # write the file name which will be ignored by git into the .gitignore file
git add .gitignore                        
git commit -m "start ignoring cockpit.pro.user"
git push
```

To exclude some files from gitignore, put ! before it:
```bash
/*.txt  # ignore all txt files
!requirements.txt  # but, don't ignore requirements.txt file
```

## Removing of untracked files
```bash
git clean -n -d  # Print out the list of files and directories which will be removed (dry run)
git clean -f     # Delete the files from the repository
git clean -f -d  # Delete the directories from the repository
git clean -f -X  # Remove ignored files
git clean -f -x  # Remove ignored files and non-ignored files
```

## Git Tags
Tags help putting reference to different commits that are important to be noticed. For example, tagging a commit with the release version 3.0 means that the commit was the final commit before the launch of the 3.0 version of the software.

```bash
git tag   # to see the tags in the repo
git tag <tag_name> <branch_name>  # add tag to the last commit (the commit to which the HEAD points) on the branch
git tag -a <tag_name> -m "<Message_for_commit>" <commit_hash_code>  # add tag to a specific commit on the branch
git push --tags  # push the tags to the remote
git tag -f <tag_name_to_update>  # update a tag to the last commit
git tag -f <tag_name_to_update> <hash_code_new_commit>  # update a tag to a specific commit
git push --force origin <tag_name>  # push the updates to the remote repo
git tag -d <tag_name>  # delete a tag
git push origin :<tag_name>  # delete the tag in the remote repo
```

## Git Submodules
We can have another repository within one repository. This is useful when you have dependencies to another projects in your project. You can have full access to the repository of the dependency in your project. Submodules are just references to certain commits. It's like having a symlink to another repository. You can access to a specific version of the dependency with commit hash. To update the references:
```bash
git submodule update
```

To update a specific submodule:
```bash
git submodule update --init --remote <submodule_path>  # --remote flag ensures that the submodule is updated to the latest commit on the branch specified in the .gitmodules file
cd <submodule_path>
git checkout <branch-name>
```

To apply a git command to all initialized submodules, use git submodule foreach:
```bash
git submodule foreach git checkout master
git submodule foreach git status
git submodule foreach git diff
```

## Patches
When we want to fix an issue or make a refactoring, we can create a patch file and send it to the maintainer. The maintainer can examine and apply the changes in the patch file if it is beneficial. 
```bash
git diff > <file_name>.patch  # Create a git patch
git apply <file_name>.patch --stat  # List all files which will be changed
git apply <file_name>.patch   # Apply the git patch
git apply <file_name>.patch --whitespace=fix  # Fix trailing whitespaces while applying the patch
```

We can also exclude or include some files before applying the patch
```bash
git apply --exclude=<file_name.ext> <file_name>.patch
git apply --include=<file_name.ext> <file_name>.patch 
```

## Working with two hosting services like Github and Gitlab:
- push a project from GitHub to GitLab:
```bash
git remote add gitlab gitlab_repo_url     # Add the new gitlab remote to your existing repository
git push gitlab                           # then push
```
- push a project from GitLab to GitHub:
```bash
git remote add github <github_repo_url>
git push --mirror github
```
- to merge branches from two projects
```bash
git merge <branch_name> --allow-unrelated-histories
```
- push to both Github and Gitlab 
```bash
git remote set-url –-add origin <github_url>
```

- You can turn a folder within a Git repository into a brand new repository:
https://docs.github.com/en/get-started/using-git/splitting-a-subfolder-out-into-a-new-repository

#### Reference: [Git-Book](http://git-scm.com/book/en/v2)
