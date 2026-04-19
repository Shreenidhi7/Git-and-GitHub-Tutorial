
**Git Branches**
1. This topic is the heart of GIT
2. In the real world we work in a team with so many teammates
	1. So, for that particular purpose, we need to create branches

Until now we used only one branch i.e master
Lets say there is only one developer in the team, then that person can make changes in the master branch - that is file.
Lets say 2 new members joined the team and now they will also be contributing to the project
Now where the branching comes into existence.

In order for 3 persons to contribute, we should create a branch.
The new branch will be by default created from the head of the master branch/current branch

Flow
1. We first go to the master branch
	1. Ask Git to create a branch from me.
		1. The feature branch will be created from the HEAD of the master branch
			1. xyz_feat1
		2. The changes in feature branch [xyz_feat1] is independent/isolated [ The master branch has 0(Zero) knowledge about the changes in the feature branch ]
2. Now i being a lead developer, made some changes in the master branch and moving ahead with the commits.
	1. Now we understood that our teammate has made some commits in his feature branch [xyz_feat1] and we want to include those into master branch
	2. For that to happen, we need to use the merge operation.
	3. This will create one more commit, and this commit is actually representing the feature branch. This commit is called "merge commit"
		1. It means this commit is only for all the commits that we have in the feature branch [xyz_feat1]

This is the fundamental concept of  branches
What is the advantage of this?
- 2 people working parallelly without waiting for anyone to complete the task
- Both develop the code in parallel and there is no need to wait for anyone task's completion.
	- Because both work in isolated environments.

**Pic Representation**

![[Pasted image 20260414093432.png]]


---

**More errors we see while working in branches, more proficient we will become in git.**
**If we are not facing any errors, we are not actually learning git.**
**Git is strongly aligned towards errors/failures/code based failures and that's how we learn git.**
**We have to break something if we have learn git.**
**In order to fix it, we learn a lot of things**
**Very common scenario called "Merge Conflict"**
**Merge Conflict is sometimes very easy to sort or very difficult to sort.**
**That depends on how many branches we have, how many commits we have**

----

First we will try to see all those things related to branches.
1. If we want to list all the branches
	1. Command - git branch
		1. master
	2. Currently we have only one branch, that is master branch
```
PS D:\Git and GitHub\Git_Practical_Tutorial> git branch
* master
```

2. Now, we want to create a feature branch and in this feature branch, we create a new file or modify the existing file
	1. In order to create feature branch on top of master branch, we have to go to the master branch
	2. Currently we have only one branch, that is master branch, but in future we might have many branches
		1. So its good practice to go/move the master branch
		2. How can we move to a specific branch
			1. Command -> git switch master
				1. Already on "master"
		3. If we are already in master branch, it says already on master, else it will switch to master
			1. This is just to confirm we are at the root/master branch
```
PS D:\Git and GitHub\Git_Practical_Tutorial> git switch master
Already on 'master'
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

git switch "branch_name" -> this is a new command that was introduced in 2019, but before this people were using git checkout "branch_name"

```
PS D:\Git and GitHub\Git_Practical_Tutorial> git checkout master
Already on 'master'
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

Both are not the same, but have some similar actions.

git checkout -> Its actually built to perform lots of tasks, not just to switch the branch
git checkout can perform new branch. Switch to new branch, modify the files -> Basically with git checkout we can do a lot of things
git checkout is kind of heavy duty command

During 2019, git developers actually felt we should focus on a command which is only feasible for switching and creating branches. That is why they created **git switch**

3. Now if we want to create a new branch [Pre-requsite : We need to land on master branch - Because by default it will create a feature branch from the HEAD of the current branch - This way we are double confirming the we create feature branch on top of master branch - everytime we **git switch master or git checkout master** to make sure we are on master branch ]
	1. Earlier we were writing
		1. **git checkout -b feature_shrn_1**
			1. This command will create a new branch with the name "feature_shrn_1"
			2. If there is already a branch with the same name - it will not do anything
			3. If there is no branch with the same name - it creates a new branch and switches to the newly created branch
	2. With git switch command
		1. **git check -c feature_shrn_1 [-c => create]**
			1. This command will create a new branch with the name "feature_shrn_1"
			2. If there is already a branch with the same name - it will not do anything
			3. If there is no branch with the same name - it creates a new branch and switches to the newly created branch

```
PS D:\Git and GitHub\Git_Practical_Tutorial> git branch
* master
PS D:\Git and GitHub\Git_Practical_Tutorial> git switch master
Already on 'master'
PS D:\Git and GitHub\Git_Practical_Tutorial> git switch -c feature_shrn_1
Switched to a new branch 'feature_shrn_1'
PS D:\Git and GitHub\Git_Practical_Tutorial> git branch
* feature_shrn_1
  master
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

**Here we will see 2 branches, one is the newly created branch and other one is the master branch**
**Good thing is that the we are currently on the feature branch not on the master branch  -> This means it also tell in which branch i am currently on.**

We shall see the Git Graph View

![[Pasted image 20260414112134.png]]

On the same "HEAD", we have feature_shrn_1 branch and master branch -> both are at the same point
Now, lets say this feature_shrn_1 actually start working on some data files
Example - We are on feature_shrn_1 branch, we will modify some files
- data_ingestion.txt
	- Shree here, I am actively working on this file.
	- I love ingesting data.
- Once done modifying, we shall add and commit the changes to feature_shrn_1 branch

```
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch feature_shrn_1
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   data_ingest.txt

no changes added to commit (use "git add" and/or "git commit -a")
PS D:\Git and GitHub\Git_Practical_Tutorial> git add .
PS D:\Git and GitHub\Git_Practical_Tutorial> git commit -m "added more data"
[feature_shrn_1 5ca01f9] added more data
 1 file changed, 0 insertions(+), 0 deletions(-)
PS D:\Git and GitHub\Git_Practical_Tutorial> git log --oneline
5ca01f9 (HEAD -> feature_shrn_1) added more data
5976fd0 (master) added silver folder
b705359 ignored bronze folder
f0e0866 gitignore file
1dd6575 new iot data ingested
28669ec Data Ingest and IOT Data Ingestion
b10dd53 Ingest Data
08a8756 initial commit
:
```

We shall see all the previous commits, because it will take care of all the previous commits as well.
The feature branch "feature_shrn_1" actually originated from the master commit [5976fd0 (master) added silver folder] [ This is called Ancestor Commit/Branch ]

Lets check the Graph Representation

![[Pasted image 20260414120930.png]]

Now, the feature_shrn_1 is ahead of master branch.
That means feature branch has one extra commit.
Now if we want to switch back to master branch - we could do it by typing
- git switch master
We can observe that the HEAD just moved backwards, because this is the HEAD of the master branch

![[Pasted image 20260414121420.png]]

---

Now, since we have moved our HEAD to master branch, the latest changes on the data_ingest.txt wont be visible, because both the branches are isolated.
data_ingest.txt was modified in the feature_shrn_1 branch
so, the data_ingest.txt will not be updated in the master branch unless we merge the changes from feature_shrn_1 to master

The moment we switch b/w the branches, we can see the changes.
data_ingest.txt  - master
- This is another data ingestion file
data_ingest.txt - feature_shrn_1
- This is another data ingestion file.
- Shree here, I am actively working on this file.
- I love ingesting data.

This branching feature helps us develop so many things parallelly.

Now, we added few more data
- data_ingest.txt
	- This is another data ingestion file.
	- Shree here, I am actively working on this file.
	- I love ingesting data.
	- I am ingesting more data.
```
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch feature_shrn_1
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   data_ingest.txt

no changes added to commit (use "git add" and/or "git commit -a")
PS D:\Git and GitHub\Git_Practical_Tutorial> git add .
PS D:\Git and GitHub\Git_Practical_Tutorial> git commit -m "added more data"
[feature_shrn_1 a5a7ee6] added more data
 1 file changed, 0 insertions(+), 0 deletions(-)
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

Now, if we see the Git Graph Representation
- The feature_shrn_1 is 2 more steps ahead of master branch

![[Pasted image 20260414122457.png]]

---

Now, lets say a new developer joined the team. This means we want to invite another developer.
That developer branch will obviously created from master branch [because its good practice]
In that case, we have to go to master branch
1. git switch master
	- Switched to branch 'master'
```
PS D:\Git and GitHub\Git_Practical_Tutorial> git switch master
Switched to branch 'master'
PS D:\Git and GitHub\Git_Practical_Tutorial> git branch
  feature_shrn_1
* master
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

Instead of Git Graph, we can even see where the HEAD points to
- ref: refs/heads/master
If we switch to feature_shrn_1 branch, the .git -> Head will also be updated
- ref: refs/heads/feature_shrn_1

2. We create one more branch from master
	1. git checkout -b feature_nidh_1
		1. Switched to a new branch "feature_nidh_1"
3. Lets say nidh is working on iot_data_ingestion file

```
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch feature_nidh_1
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   iot_data_ingestion.txt

no changes added to commit (use "git add" and/or "git commit -a")
PS D:\Git and GitHub\Git_Practical_Tutorial> git add .
PS D:\Git and GitHub\Git_Practical_Tutorial> git commit -m "ingested real time data"
[feature_nidh_1 3d7a6da] ingested real time data
 1 file changed, 2 insertions(+), 1 deletion(-)
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```


**Now, if we see the Git Graph, it will be very interesting**
![[Pasted image 20260414125316.png]]

---

Understanding the Graph Flow

![[Pasted image 20260414125617.png]]

1. Lets go the master branch.
2. Here we created a feature branch called feature_shrn_1
	1. We made 2 commits
		1. added more data
		2. added more data
3. Then we created another feature branch called feature_nidh_1
	1. We just made 1 commit
		1. ingested real time data

the commit on the branch feature_nidh_1 appears to be at the top, because it associated with the data and time stamps of each commit.

**One person is working on data_ingest.txt in feature_shrn_1 branch**
**Another person is working on iot_data_ingestion.txt in the feature_nidh_1 branch**
**And for master, both are unknown for now.**

If i also start to contribute to the project in the master branch with the data_ingestion.txt file
File - data_ingestion.txt
- Hey, i am ingesting the data in this file.
- Master here. Let me also contribute to the project.
```
PS D:\Git and GitHub\Git_Practical_Tutorial> git switch master
Switched to branch 'master'
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   data_ingestion.txt

no changes added to commit (use "git add" and/or "git commit -a")
PS D:\Git and GitHub\Git_Practical_Tutorial> git add .
PS D:\Git and GitHub\Git_Practical_Tutorial> git commit -m "master commit"
[master 624a26d] master commit
 1 file changed, 2 insertions(+), 1 deletion(-)
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

I can see the changes form my branch "master" , because "master" branch is isolated from the other 2 branches

Now, if we see Git Graph Representation
![[Pasted image 20260414131006.png]]

Now, each branch is contributing to a different file, not on the same file.
In our case there are no conflicts, because we working on different files.
master => data_ingestion.txt
feature_ansh_1 => data_ingest.txt
feature_lamba_1 => iot_data_ingestion.txt

1. Since all the branches are working on different files, the merge would be simple.
2. There won't be any conflicts.
3. No 2 people are working on the same file.
4. Lets now try to merge one branch
5. To do that we need to go to master branch
	1. From master branch we want to merge the feature branch

```
PS D:\Git and GitHub\Git_Practical_Tutorial> git switch master
Already on 'master'
PS D:\Git and GitHub\Git_Practical_Tutorial> git branch
  feature_nidh_1
  feature_shrn_1
* master
PS D:\Git and GitHub\Git_Practical_Tutorial> git merge feature_nidh_1
Merge made by the 'ort' strategy.
 iot_data_ingestion.txt | 3 ++-
 1 file changed, 2 insertions(+), 1 deletion(-)
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch master
nothing to commit, working tree clean
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

We have provide the commit for the merge -> its called merge commit
now, just close the file, the commit message would be added.
![[Pasted image 20260414132138.png]]

Now, if i say git status
- PS D:\Git and GitHub\Git_Practical_Tutorial> git status
	- On branch master
	- nothing to commit, working tree clean

Its saying, we have merged one thing, but we need to obviously create a commit.
Its called MERGE COMMIT
Why did it ask me to write a message?
- Because there are basically 2 types of merges
	- Fast-forward merge
	- Non-Fast-forward merge

**Fast-Forward Merge**
- Assume, we have made 3 commits in the master branch and after that we created a branch
	- And in the branch we made 2 commits.
	- But we didn't make any commit/progress in the master branch
		- This is called Fast-forward merge
![[Pasted image 20260414133130.png]]


Non Fast-Forward Merge
- Assume, we have made 3 commits in the master branch and after that we created a branch
	- And in the branch we made 2 commits.
	- But in real-time example we will move forward in the master branch as well
		- Assume we have made some commits in the master branch as well
	- Now, when we try to merge the changes from feature branch to master
		- This is called Non Fast-forward merge
	- If we want to merge it, it will go above the commit which was made on master, it will create a new commit - This is our MERGE COMMIT
		- If we using the MERGE COMMIT, then we have define the mesasge
			- If we don't define it, it will pop-up the screen and we should write the message there
			- It can be handled by the command
				- git merge feature -m ""

![[Pasted image 20260414133633.png]]

Now, we can see that the feature_nidh_1 is merged to master branch.
All the commits in the feature_nidh_1 branch has been merged to master in the form of merge conflict.

----

Now we shall merge feature_shrn_1 as well to master

```
PS D:\Git and GitHub\Git_Practical_Tutorial> git switch master
Already on 'master'
PS D:\Git and GitHub\Git_Practical_Tutorial> git branch
  feature_nidh_1
  feature_shrn_1
* master
PS D:\Git and GitHub\Git_Practical_Tutorial> git merge feature_shrn_1 -m "merging feature_shrn_1"
Merge made by the 'ort' strategy.
 data_ingest.txt | Bin 76 -> 274 bytes
 1 file changed, 0 insertions(+), 0 deletions(-)
PS D:\Git and GitHub\Git_Practical_Tutorial> 

```

Git Graph Representation

![[Pasted image 20260414134321.png]]

Due to timestamp, the commit at feature branch feature_shrn_1 shows in the middle, not at the top.
Both feature branches have independent commits
All the code changes from both the branches are now present in the master branch.
That is how we merge all the code to master.

If we check the log now. It shows all the commits that has been made so far.
```
PS D:\Git and GitHub\Git_Practical_Tutorial> git log --oneline
fdca9c8 (HEAD -> master) merging feature_shrn_1
983c106 Merge branch 'feature_nidh_1'
624a26d master commit
3d7a6da (feature_nidh_1) ingested real time data
a5a7ee6 (feature_shrn_1) added more data
5ca01f9 added more data
5976fd0 added silver folder
b705359 ignored bronze folder
f0e0866 gitignore file
1dd6575 new iot data ingested
28669ec Data Ingest and IOT Data Ingestion
b10dd53 Ingest Data
08a8756 initial commit
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

