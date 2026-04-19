
Lets discuss about the very much important topic - Its called stashing.
Stashing is a kind of temporary storage location that git provides to us.

Why do we need the temporary storage location?
- Lets create a scenario for us.

1. We create a new branch for us.
	1. git switch -c dev1_stash
2. In this branch we are supposed to do our development
	1. We shall create a new file
		1. development.txt
3. Assume we are developing something in the file development.txt
4. All of sudden in the midway, our manager asks us to work on something else which is quite urgent. But we were literally doing some development, we have to stop our development activity and switch to the work our manager asks us to do.
	1. What do we do in this situation?
5. Assume we have added the file [development.txt] and committed it in dev1_stash branch

```
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch master
nothing to commit, working tree clean
PS D:\Git and GitHub\Git_Practical_Tutorial> git switch -c "dev1_stash"
Switched to a new branch 'dev1_stash'
PS D:\Git and GitHub\Git_Practical_Tutorial> git branch
  bugfix
  bugfix2
  cherry_pick
* dev1_stash
  feature_nidh_1
  feature_shrn_1
  master
  rebase_feat
  rebase_feat_2
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch dev1_stash
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        development.txt

nothing added to commit but untracked files present (use "git add" to track)
PS D:\Git and GitHub\Git_Practical_Tutorial> git add .
PS D:\Git and GitHub\Git_Practical_Tutorial> git commit -m "work started"
[dev1_stash 8b4032b] work started
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 development.txt
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

6. Also we have added few more changes to the file [development.txt] but have not added or committed it yet
	1. More development is in progress. DND.....
7. Now if we try to switch to the master branch from dev1_stash branch
	1. It gives us the error
		1. It says - Your local changes for the file would be overwritten by checkout
			1. development.txt
		2. Please commit your changes or stash them before you switch branches.

```
PS D:\Git and GitHub\Git_Practical_Tutorial> git switch master
error: Your local changes to the following files would be overwritten by checkout:
        development.txt
Please commit your changes or stash them before you switch branches.
Aborting
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

8. But we are not in the position to commit the changes, because the additional changes what was made is still in the initial phase and is not ready to be added & committed to staging environment.
9. if we do git status, it shows us that there is some modification the file

```
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch dev1_stash
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   development.txt

no changes added to commit (use "git add" and/or "git commit -a")
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

10. Now, we can literally switch to master branch by stashing the changes
	1. Assume we have a working directory
		1. Our code is here in WD which are not committed
	2. So, now we can save these uncommitted changes in the temporary location/storage - Its called Stash
	3. Once stashed, we can go ahead and switch the branch.
	4. Command -> git stash push -m "My Development Paused"
		1. Saved working directory and index state on dev1_stash: My Development Paused
	5. Our all changes will be gone, they have gone into the temporary storage location which is stash

```
PS D:\Git and GitHub\Git_Practical_Tutorial> git switch master
error: Your local changes to the following files would be overwritten by checkout:
        development.txt
Please commit your changes or stash them before you switch branches.
Aborting
PS D:\Git and GitHub\Git_Practical_Tutorial> git stash push -m "My Development Paused"
Saved working directory and index state On dev1_stash: My Development Paused
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

11. If i try to switch the branch now, it should be possible and we wont see the file [development.txt] file itself in the master branch
	1. Because it has been stashed from the dev1_stash branch
![[Pasted image 20260418230040.png]]


----

Assume, we will work on the other task which our manager wanted us to do.
We shall do it quickly

```
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   data_ingest.txt

no changes added to commit (use "git add" and/or "git commit -a")
PS D:\Git and GitHub\Git_Practical_Tutorial> git add .
PS D:\Git and GitHub\Git_Practical_Tutorial> git commit -m "bug fixed"
[master b02e775] bug fixed
 1 file changed, 0 insertions(+), 0 deletions(-)
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

---

Now if we see the Git Graph, we could see our stash commit and where our development work stopped 

![[Pasted image 20260418230948.png]]

----

Since we have done what our manager had asked us to do, so now if we want to get back to our development activity, we have to go back to our dev branch
- git switch dev1_stash
```
PS D:\Git and GitHub\Git_Practical_Tutorial> git switch dev1_stash
Switched to branch 'dev1_stash'
PS D:\Git and GitHub\Git_Practical_Tutorial> git branch
  bugfix
  bugfix2
  cherry_pick
* dev1_stash
  feature_nidh_1
  feature_shrn_1
  master
  rebase_feat
  rebase_feat_2
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```


Now, if we need our code back, we can list the number of stash we have done so far
- git stash list
```
PS D:\Git and GitHub\Git_Practical_Tutorial> git stash list
stash@{0}: On dev1_stash: My Development Paused
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

**stash@{0}: On dev1_stash: My Development Paused**
stash@{0} - Index
dev1_stash - branch name
comment - My Development Paused
This means these are things which we have saved in out temporary location/storage
Basically Stash is a kind of stacked memory
- It means the latest stash will be at the top
![[Pasted image 20260418231813.png]]

So, now to get back our development as it was before stashing, we need to perform below action
- git switch dev1_stash
- git stash list
- git stash apply
	- If we just pass the above command, by default it will apply the latest stash on top of our branch automatically
	- But the good practice is we tell which stash we want
		- git stash apply stash@{0}
	- Right now, we have just one stash, but its good practice to tell it.
		- But its deprecated now, we shall use just git stash apply now

```
PS D:\Git and GitHub\Git_Practical_Tutorial> git switch dev1_stash
Switched to branch 'dev1_stash'
PS D:\Git and GitHub\Git_Practical_Tutorial> git branch
  bugfix
  bugfix2
  cherry_pick
* dev1_stash
  feature_nidh_1
  feature_shrn_1
  master
  rebase_feat
  rebase_feat_2
PS D:\Git and GitHub\Git_Practical_Tutorial> git stash list
stash@{0}: On dev1_stash: My Development Paused
PS D:\Git and GitHub\Git_Practical_Tutorial> git stash apply stash@{0}    
error: unknown switch `e'
usage: git stash apply [--index] [-q | --quiet] [<stash>]

    -q, --[no-]quiet      be quiet, only report errors
    --[no-]index          attempt to recreate the index

PS D:\Git and GitHub\Git_Practical_Tutorial> git stash apply
On branch dev1_stash
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   development.txt

no changes added to commit (use "git add" and/or "git commit -a")
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

Now, we have development changes back.
But if we list the git stash now - it will be still there, we have to remove it manually
Till the commit is not made, the item cannot be removed from the list.
In order to remove the stash list, we have to add & commit the changes to staging area, then only the stash list can be removed
```
PS D:\Git and GitHub\Git_Practical_Tutorial> git stash list
stash@{0}: On dev1_stash: My Development Paused
PS D:\Git and GitHub\Git_Practical_Tutorial> git stash pop
error: Your local changes to the following files would be overwritten by merge:
        development.txt
Please commit your changes or stash them before you merge.
Aborting
On branch dev1_stash
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   development.txt

no changes added to commit (use "git add" and/or "git commit -a")
The stash entry is kept in case you need it again.
PS D:\Git and GitHub\Git_Practical_Tutorial>
```

For now, we shall add & commit the changes to staging area and then try removing the stash list
- git stash list -> to list the stash
- git stash pop -> to remove the stash from the list

```
PS D:\Git and GitHub\Git_Practical_Tutorial> git add .
PS D:\Git and GitHub\Git_Practical_Tutorial> git commit -m "Finally Work Done"
[dev1_stash f006666] Finally Work Done
 1 file changed, 2 insertions(+)
PS D:\Git and GitHub\Git_Practical_Tutorial> git status    
On branch dev1_stash
nothing to commit, working tree clean
PS D:\Git and GitHub\Git_Practical_Tutorial> git stash list
stash@{0}: On dev1_stash: My Development Paused
PS D:\Git and GitHub\Git_Practical_Tutorial> git stash pop
On branch dev1_stash
nothing to commit, working tree clean
Dropped refs/stash@{0} (21cb59a37d89b056c8538a3c023c442b709a6b7b)
PS D:\Git and GitHub\Git_Practical_Tutorial> git stash list
PS D:\Git and GitHub\Git_Practical_Tutorial>
```


---------------

Once again try - Actually with the command - git stash apply "stash@{0}"
- we need to use double inverted commas for the stash index
Tip - Whenever we are using special character in the command, we have take care of those things in double quotes.

```
PS D:\Git and GitHub\Git_Practical_Tutorial> git stash push -m "My serious Dev"
Saved working directory and index state On dev1_stash: My serious Dev
PS D:\Git and GitHub\Git_Practical_Tutorial> git stash list
stash@{0}: On dev1_stash: My serious Dev
PS D:\Git and GitHub\Git_Practical_Tutorial> git switch master
Switched to branch 'master'
PS D:\Git and GitHub\Git_Practical_Tutorial> git switch dev1_stash
Switched to branch 'dev1_stash'
PS D:\Git and GitHub\Git_Practical_Tutorial> git stash list
stash@{0}: On dev1_stash: My serious Dev
PS D:\Git and GitHub\Git_Practical_Tutorial> git stash apply "stash@{0}"
On branch dev1_stash
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   development.txt

no changes added to commit (use "git add" and/or "git commit -a")
PS D:\Git and GitHub\Git_Practical_Tutorial>
```

```
PS D:\Git and GitHub\Git_Practical_Tutorial> git stash apply "stash@{0}"
On branch dev1_stash
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   development.txt

no changes added to commit (use "git add" and/or "git commit -a")
PS D:\Git and GitHub\Git_Practical_Tutorial> git add .
PS D:\Git and GitHub\Git_Practical_Tutorial> git commit -m "Done!"
[dev1_stash 6940bbc] Done!
 1 file changed, 2 insertions(+), 1 deletion(-)
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```


----

Next section we shall learn about some advanced things
We shall look at some remote repository
We shall work with GitHub
- How to clone
- How to push
- Etc.
Also we shall setup GitHub profile
- We shall initiate a new folder
- And all other operation related to git and GitHub

---
