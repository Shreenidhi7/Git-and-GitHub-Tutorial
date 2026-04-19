
In real life, we do see merge conflicts
Lets try creating a conflict and then try resolving them

Why do we get merge conflicts and What could be the common reason?
1. If 2 developer working on the same file [assume its data_ingest.txt]
	1. One developer commits the changes
	2. When Second developer tries to commit the changes on the same file
2. Here is where the conflict arises.
	1. Because both developers are changing/modifying the same file [data_ingest.txt]
		1. The 2nd merge will create a conflict.
3. There would be 3 versions when the final/2nd merge commit was made
	1. First one -  Before 2 developer branch out from master to make changes in file [data_ingest.txt] [Version 0]
	2. Second one - 1st developer working on the same file [data_ingest.txt] mergers his code to the master [Version 1]
	3. Third one - 2nd developer working on the same file [data_ingest.txt] tries to merge his code to the master. [Version 1]
4. We need to keep only one file, there cannot be multiple Version 1's
	1. There can be Version 0 [Before Code Fix] and Version 1 [After Code Fix]
	2. When the 2nd developer changes are submitted, GIT suggests to clear the conflict at the developer end and GIT will just make the Version 1 as per developer's mutual understanding 
5. Why the 2nd developer code merge is not considered as Version 2, but as Version 1 itself?
	1. Because this branch has the ancestor commit 
	2. Though both code changes are done at isolated branches
	3. The files changed are the same, the version history should be clean
		1. Due to this, the changes made by 2nd Developer on same is also considered as Version 1
![[Pasted image 20260414170550.png]]

6. What would be the solution for this now?
	1. Lets create a conflict and once we have the conflict, we can solve it 

----

1. Lets create a branch
	1. git switch -c bugfix
2. We shall create a bug in the file
	1. data_ingest.txt

```
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch master
nothing to commit, working tree clean
PS D:\Git and GitHub\Git_Practical_Tutorial> git switch master
Already on 'master'
PS D:\Git and GitHub\Git_Practical_Tutorial> git branch
  feature_nidh_1
  feature_shrn_1
* master
PS D:\Git and GitHub\Git_Practical_Tutorial> git switch -c bugfix
Switched to a new branch 'bugfix'
PS D:\Git and GitHub\Git_Practical_Tutorial> git branch
* bugfix
  feature_nidh_1
  feature_shrn_1
  master
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

```
Previous
This is another data ingestion file.
Shree here, I am actively working on this file.
I love ingesting data.
I am ingesting more data.

Bug Fix
This is another data ingestion file.
Shree here, I am actively working on this file.
I like ingesting data.
I am ingesting more data.

Changed/Fixed the word :: love -> like
```

Adding the changes and committing the code to the branch - bugfix

```
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch bugfix
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   data_ingest.txt

no changes added to commit (use "git add" and/or "git commit -a")
PS D:\Git and GitHub\Git_Practical_Tutorial> git add .
PS D:\Git and GitHub\Git_Practical_Tutorial> git commit -m "fix bug"
[bugfix cec4dbf] fix bug
 1 file changed, 0 insertions(+), 0 deletions(-)
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

---

In mean time, before the branch bugfix branch is merged to master.
Assume, according to the tech lead, the bug was not with love & like
The word itself shouldn't be there.
Instead of "I love ingesting data." or "I like ingesting data." => It should be like "I am ingesting data"
Tech lead makes the changes in the master branch itself.

```
PS D:\Git and GitHub\Git_Practical_Tutorial> git switch master
Switched to branch 'master'
PS D:\Git and GitHub\Git_Practical_Tutorial> git branch
  bugfix
  feature_nidh_1
  feature_shrn_1
* master
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   data_ingest.txt

no changes added to commit (use "git add" and/or "git commit -a")
PS D:\Git and GitHub\Git_Practical_Tutorial> git add .
PS D:\Git and GitHub\Git_Practical_Tutorial> git commit -m "bug is fixed"
[master 8bd56f1] bug is fixed
 1 file changed, 0 insertions(+), 0 deletions(-)
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

---

We have the code that is fixed in the branch "bugfix", but in meantime the changes has been already made by the lead in the "master" branch.
The developer says his code is ready to be merged.
So the lead will try to merge the branch "bugfix" to "master".
There arises the merge conflict.
```
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch master
nothing to commit, working tree clean
PS D:\Git and GitHub\Git_Practical_Tutorial> git switch master
Already on 'master'
PS D:\Git and GitHub\Git_Practical_Tutorial> git branch
  bugfix
  feature_nidh_1
  feature_shrn_1
* master
PS D:\Git and GitHub\Git_Practical_Tutorial> git merge bugfix -m "simple merge"
warning: Cannot merge binary files: data_ingest.txt (HEAD vs. bugfix)
Auto-merging data_ingest.txt
CONFLICT (content): Merge conflict in data_ingest.txt
Automatic merge failed; fix conflicts and then commit the result.
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

**Resolution**
1. We can even abort this conflict
	1. git merge --abort
2. With the abort, the conflict will gone. Basically it aborted/stopped the merging [It didn't resolve the conflict]
	1. But our aim to resolve the conflict and merge the branch to main
```
PS D:\Git and GitHub\Git_Practical_Tutorial> git merge --abort
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch master
nothing to commit, working tree clean
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

Here we need to eliminate the conflict. We shall follow the previous flow
```
PS D:\Git and GitHub\Git_Practical_Tutorial> git merge bugfix -m "this guy fixed as well"
warning: Cannot merge binary files: data_ingest.txt (HEAD vs. bugfix)
Auto-merging data_ingest.txt
CONFLICT (content): Merge conflict in data_ingest.txt
Automatic merge failed; fix conflicts and then commit the result.
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

Lets open the file which is creating conflict

**Incoming Branch**
- Incoming Data means incoming branch [bugfix branch]
I like ingesting data.

**Current Branch**
- Current Data means current branch [master branch]
I am ingesting data

**Result**
I **am** ingesting data

![[Pasted image 20260414212020.png]]


How do we actually resolve the conflict
- If we accept the incoming data,result would be like this
	- Current + Incoming
		- I am ingesting data.
		- I like ingesting data.
	- This way we can actually keep both the code as well
- Or if the tech lead says his code is correct, then if we remove Incoming data, it will keep only the current data
	- I am ingesting data.
- Or if the developer is correct in that case, we keep only the Incoming data and remove the current data
	- I like ingesting data.
- In ideal scenario, we will say remove incoming, because master branch should be given more priority.
	- Here as well we kept the current change and removed the incoming change
- Final Snapshot
![[Pasted image 20260414213016.png]]

Once done selecting the change, we click on "Complete Merge" button
```
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch master
All conflicts fixed but you are still merging.
  (use "git commit" to conclude merge)

PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

Conflicts are over but we need to use git commit to conclude the merges
Now, if we look at Git Graph, it should show conflicts merged commit and the merge conflict should be resolved
![[Pasted image 20260414213507.png]]

We have kept the changes from the master branch.
We had the option to keep the changes from the bug fix branch aswell
We had the option to keep both.
Its up to developer/requirements on what exactly we need to make the version as our Version 1.
This is how we resolve conflicts in GIT

---

Now, we shall look at the scenario where we work on the same file, but still Git will not give us any conflicts.

1. Create a new branch
```
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch master
nothing to commit, working tree clean
PS D:\Git and GitHub\Git_Practical_Tutorial> git switch -c bugfix2
Switched to a new branch 'bugfix2'
PS D:\Git and GitHub\Git_Practical_Tutorial> git branch
  bugfix
* bugfix2
  feature_nidh_1
  feature_shrn_1
  master
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

2. We shall use the file [data_ingestion.txt]
	1. Here we will not change the exisitng sentence/words
		1. Instead we will add new like
			1. 6th line we shall add some sentence
```
Hey, i am ingesting the data in this file.
Master here. Let me also contribute to the project.



I am fixing this bug.
```

- Adding and committing the changes
```
PS D:\Git and GitHub\Git_Practical_Tutorial> git add .
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch bugfix2
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   data_ingestion.txt

PS D:\Git and GitHub\Git_Practical_Tutorial> git commit -m "fixed bug 2"
[bugfix2 789d902] fixed bug 2
 1 file changed, 5 insertions(+), 1 deletion(-)
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

Now, we shall switch back to master branch
- Changes to be done in the same file on the existing data
```
Hey, i am not ingesting the data in this file (bug is fixed).
Master here. Let me also contribute to the project.
```

Adding and Committing the Changes

```
PS D:\Git and GitHub\Git_Practical_Tutorial> git switch master
Switched to branch 'master'
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch master
nothing to commit, working tree clean
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   data_ingestion.txt

no changes added to commit (use "git add" and/or "git commit -a")
PS D:\Git and GitHub\Git_Practical_Tutorial> git add .
PS D:\Git and GitHub\Git_Practical_Tutorial> git commit -m "bug is fixed"
[master bd99acb] bug is fixed
 1 file changed, 1 insertion(+), 1 deletion(-)
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

Merging the changes from the branches

```
PS D:\Git and GitHub\Git_Practical_Tutorial> git switch master
Already on 'master'
PS D:\Git and GitHub\Git_Practical_Tutorial> git branch
  bugfix
  bugfix2
  feature_nidh_1
  feature_shrn_1
* master
PS D:\Git and GitHub\Git_Practical_Tutorial> git merge bugfix2 -m "lets see" 
Auto-merging data_ingestion.txt
CONFLICT (content): Merge conflict in data_ingestion.txt
Automatic merge failed; fix conflicts and then commit the result.
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

Visualize the merge editor
![[Pasted image 20260414215724.png]]

What is the conflict here?
- <<<< HEAD (Current Change)
	- It refers to the changes in master branch
- >>>> bugfix2 (Incoming Change)
	- It refers to the changes in the bugfix2 branch
- Basic explanation is that - Even if we are not contributing to the same line, it can create a conflict.
- Now its the same thing, if we want to resolve the conflict
	- In this version we are keeping the changes of both the files.

```
Hey, i am not ingesting the data in this file (bug is fixed).
Master here. Let me also contribute to the project.

Hey, i am ingesting the data in this file.
Master here. Let me also contribute to the project.


Hehe I am learning Git - Added during resolving merge conflict
I am fixing this bug.


```

There is no hard and set rule to accept incoming/keep the current change
This is totally customized. We can literally keep anything.

```
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch master
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)
        both modified:   data_ingestion.txt

no changes added to commit (use "git add" and/or "git commit -a")
PS D:\Git and GitHub\Git_Practical_Tutorial> git add .
PS D:\Git and GitHub\Git_Practical_Tutorial> git commit -m "finally conflict resolved"
[master 5093620] finally conflict resolved
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

**This time, we manually fixed the conflicts instead of using the code merge editor.**

Git Graph Representation

![[Pasted image 20260414220937.png]]



---

**Simple Flow**
1. We have 1st merge the branch
2. If we have conflicts, we remove the conflicts
3. Then we have to use
	1. git add .
	2. git commit -m ""
		1. These[git add and git commit] are non-negotiable {we have to do it after resolving the conflict }

This was all about merge and conflicts.

---
