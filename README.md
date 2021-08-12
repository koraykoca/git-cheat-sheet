# GIT (a Version Control System)

GIT is a Version Control System (VCS) which is widely used in practice. It makes easier to work on a project as a team. You can track changes on the code and communicate with your team mates through the code remotely.

You can create your own repository or you can fork a repository which is already created by someone else. I will explain some important GIT commands in this blog.

## Basic GIT Commands

Firstly you need to clone the repository on your local machine. If we work on someone else's project, we need to fork the project first. Then we will use _**git clone**_ command as following:

```ruby
git clone url_of_the_repository
```

With this code, you will clone whole project with all branches. When you clone a repository for the first time, GIT can ask about your identity. In this case we will set our e-mail address and initialize the git as:

```ruby
git config user.email "email_address"
git init
```

After cloning the repository, we can see them locally. Now we can make changes on them on our machine. After editing, we can send our local changes to the online repository so that our teammates will be able to see our changes. For this, we use _**git add**_ command. If we want to add all files we made changes on, then we can use _**git add --all**_ command. When we want to add only a specific file, we use _**git add name_of_the_file**_:

```ruby
git add --all
# or we can specify the file
git add name_of_the_file
# or we can specify many files
git add name_of_the_file1 name_of_the_file2 name_of_the_file3 
```

We check always the status of our GIT using _**git status**_ command. It will tell us what has been changed. We will save our changes to the local repository with _**git commit**_ command. We can inform our teammates about the changes with a short message. For this, we will use the following to commit the file and set the commit message:

```ruby
git commit name_of_the_file -m "message_or_explanation"
```

Now we are ready to send our changes to the online repository, so that they can be shared with the rest of the world. However, when somebody else on our team made some changes in the repository which we don't have them on our local repository, we need to _**pull**_ these remote changes because there is some kind of conflicts between what we have locally and what is living online. In this case _**git pull**_ command takes recent changes that are living on the remote repository and get them to the local repository.
After that we can send our changes without problem with _**git push**_ command.

```ruby
git push
```

## GIT Branching

Branching means that we diverge from the main line of the development and continue to work without messing with that main line. We prefer to work on the copy of the master branch and work on the project independently from our teammates. After that we will merge our changes/branch with the main branch. To create a new branch, we use _**git branch**_ command. To switch to an existing branch, we use _**git checkout**_ command.

```ruby
git branch branch_name
git checkout branch_name
```

It's typical to create a new branch and switch to that new branch at the same time. This can be done in one operation with

```ruby
git checkout -b branch_name
```

When we want to push something that is in our new branch, we need to first switch to the main branch. Then, we use _**git merge**_ command to merge our new branch into the main branch. After merging, we will be done with the new branch which we created and can delete it with _**git branch -d branch_name**_. If we don't want to delete and keep the branch also on the remote repository, we use _**git push origin branch_name**_. But generally, the whole process will be like as the following:

```ruby
git checkout -b branch_name    # branch creating and switching to it
# Some changes on the files
git add file_name              # changes are staged in order to be committed
git commit -m "some_message"   # telling what you changed/did
git checkout main              # switching to the main branch
git merge branch_name          # get changes back to the main branch
git push                       # changes pushed to the main branch
git branch -d branch_name      # deleting the new branch
```
