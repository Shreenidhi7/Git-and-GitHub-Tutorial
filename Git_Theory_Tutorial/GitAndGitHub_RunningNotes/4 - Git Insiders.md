
Now, we shall discuss about the building blocks of git.
Lets discuss about .git
Lets discuss about add, commit, and everything that is related in detail.


.**git [Dot Git]**
1. .git is the brain/backbone/major part of out git repository.
2. It is also called as a Database
	1. Because it keeps a track of all the versions, all the history, all the commits, all the checkpoints, all the progress.
	2. So everything we are doing in a repository be it to achieve version control - so that we can just time travel b/w the versions
		1. We should be able to do it with .git
3. Without .git our code folder is just a directory, but with .git it becomes a repository
	1. We can actually perform version control
4. This [.git] is the 1st thing we get whenever we preform **git init** command in the terminal
 
**Entire Flow**

![[Pasted image 20260413150710.png]]

**What is a Working Directory?**
1. Working directory is a kind of folder/directory/area where we create/modify the files.
	1. Its basically a place where we do our development.
	2. In our example- the folder is "Git_Practical_Tutorial"

Actual Difference between Working Directory and Repository
1. Lets say we created 1st,2nd & 3rd file [Be it any extension]
2. We created these 3 new files in the working directory

Why it is called that we created these 3 new files in the working directory and not in the repository?
- Its because whatever the number of files we have created, Git is not aware of these 3 new files
	- Working Directory can be referred to as Local Workspace or it is independent/hidden/not exposed to Git Until and unless we tell the git to track these files

3. These 3 new files are not part of our repository because git doesn't know that these 3 new files exist [only we know it/only the person who created it knows it]
4. We need to bundle these 3 files [1st, 2nd & 3rd]
	1. We simply bundle these 3 files and we transfer these 3 files to the staging area.
		1. For what purpose?
			1. To create a snapshot of these 3 files
5. Then we say commit this snapshot, then it goes to the repository and creates a commit of this snapshot that it has taken at the moment when we had added these files in the snapshot in the staging area
6. Now, assume we modified all the 3 files and this modification again happened in the working directory, but git will not be aware of the changes made to all 3 files unless it is tracked.
	1. Now we say add these 3 files in the staging area again so that we can make another commit and this commit will again go to the repository
	2. **So, now we have made 2 commits and all these information is stored in the database called .git**
7. Whenever we make changes, and those changes are not staged that means those changes are in the working directory
	1. Only the person written it is aware of those changes
8. Then we add those changes in the staging area/snapshot area - where we say just take the snapshot of the state of my file and then just commit a particular snapshot

What is the purpose of the Snapshot here?
- To understand this, we can relate to a very popular analogy that is very popular in the industry
- Lets say we want to copy 3 files from any folder from our local system
	- I simply select all 3 files, i will perform CTRL+C & CTRL+V
- Selecting the files which we need to commit. [CTRL+C]
- Then we need to bundle these 3 files
- Then i need to commit these files to the repository [CTRL+V]

These 3 stages "Working Directory", "Staging Area(Snapshot)", "Repository" are called the basic building blocks of GIT

---

**File States**
1. There are basically 3 different kinds of file states
	1. Untracked
	2. Staged
	3. Committed

- Whenever we create new files, we see a mark of "U"
- "U" represents Untracked
- It means these files are just the part of working directory and not actually being tracked by GIT
- Then we say add these files in the staging area
- Then commit the changes/additions

- Whenever there is an existing file, we just want to modify it, we will see something called "Modified" ["M"]
- Once the file is modified, we need to move this file in the staging area so that those changes can be snapshot.
- Then this snapshot will be committed in the repository

* Every time we create a new file, it will be marked as "U" [Untracked]
* Every time we modify an existing file, it will be marked as "M" [Modified]

---
