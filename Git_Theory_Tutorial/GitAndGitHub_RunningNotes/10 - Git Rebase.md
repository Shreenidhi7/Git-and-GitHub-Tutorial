
We shall discuss about something which is very important and that a lot of people scare of - Its called **REBASE **

We should always use Rebase with precautions and once we understand the concept, it actually not that scary

- Lets assume, we are on the master branch and we have the HEAD [Latest Commit]
	- From HEAD, we have created a new branch [feature branch]
		- We have made some commits here.
- Also, in master branch, we have made some commits
- Now, if we want to merge the feature branch to master branch, its possible and till now we have experimented this - Using the merge command.

- Instead of MERGE, we can use something called as REBASE
	- So What is REBASE?
		- Lets say we have the master branch, we have some master branch commit.
			- Also we have a feature branch and some commits there are well.
		- Now the feature branch will be moved to the latest commit of master branch and then the commits on the feature branch will be created 
		- This is the concept of REBASE.
		- Earlier the feature branch originated from the old HEAD of master, but we have shifted its base

**Pictorial Representation**
![[Pasted image 20260417231804.png]]

What is the advantage of the REBASE?
- This acts a Fast Forward Merge
	- If we apply merge command after rebasing, it will become Fast Forward Merge.
	- It means, we don't have any kind of new commits in the master branch, all the commits are coming from feature branch.
		- This becomes fast forward merge.
	- The FFM actually looks really clean whenever we want to watch the history
		- This is the reason people use the combination of rebase and fast forward merge

How to handle conflict?
- Same way, we need to resolve the conflicts in the merge.
	- Once its rebased, obviously it will say that there is a conflict - pick any one particular which we want to keep/ignore - exactly the same way.
- The part which was discussed on how to resolve the conflict, that remains the same for all kinds on conflict.

----

**Practical's**

1. Lets create a branch
	1. git switch -c "rebase_feat"
2. We shall edit the file
	1. data_ingestion.txt
		1. I am ingesting big data

```
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch master
nothing to commit, working tree clean
PS D:\Git and GitHub\Git_Practical_Tutorial> git switch -c "rebase_feat"
Switched to a new branch 'rebase_feat'
PS D:\Git and GitHub\Git_Practical_Tutorial> git branch
  bugfix
  bugfix2
  feature_nidh_1
  feature_shrn_1
  master
* rebase_feat
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch rebase_feat
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   data_ingestion.txt

no changes added to commit (use "git add" and/or "git commit -a")
PS D:\Git and GitHub\Git_Practical_Tutorial> git add .
PS D:\Git and GitHub\Git_Practical_Tutorial> git commit -m "ingest big data"
[rebase_feat 23e0a48] ingest big data
 1 file changed, 1 insertion(+)
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

The changes are done in the new feature branch and the commit has been posted to feature branch.
If we see the master branch, it behind one commit.
Now we will simply move our HEAD to master branch.
1. Lets switch back to master branch
	1. git switch master
2. We shall edit the file
	1. data_ingest.txt
		1. I am ingesting batch data
```
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch rebase_feat
nothing to commit, working tree clean
PS D:\Git and GitHub\Git_Practical_Tutorial> git branch
  bugfix
  bugfix2
  feature_nidh_1
  feature_shrn_1
  master
* rebase_feat
PS D:\Git and GitHub\Git_Practical_Tutorial> ^C
PS D:\Git and GitHub\Git_Practical_Tutorial> git switch master
Switched to branch 'master'
PS D:\Git and GitHub\Git_Practical_Tutorial> git branch
  bugfix
  bugfix2
  feature_nidh_1
  feature_shrn_1
* master
  rebase_feat
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   data_ingest.txt

no changes added to commit (use "git add" and/or "git commit -a")
PS D:\Git and GitHub\Git_Practical_Tutorial> git add .
PS D:\Git and GitHub\Git_Practical_Tutorial> git commit -m "ingest batch data"
[master 458e740] ingest batch data
 1 file changed, 0 insertions(+), 0 deletions(-)
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

Git Graph Representation
![[Pasted image 20260418105030.png]]

Master is having its own commit, and feature branch is having its own commit.
Both the branch don't have the same commit, its different commit all together.

Now i want to rebase the particular branch, because i want to shift the base.
There are certain steps to do it. We shall follow one by one.

1. We have to go/switch to the feature branch from where we need to rebase.
	1. git switch rebase_feat
2. Now, we are on the feature branch - rebase_feat
3. Now, if we want to rebase, we shall perform
	1. git rebase master
		1. It means we are pointing to the HEAD of the master branch
		2. Once done, it will show the message
			1. Successfully rebased and updated refs/head/rebase_feat
			2. We can see the Graph moving ahead to master branch
		3. Now this becomes our Fast Forward Merge

```
PS D:\Git and GitHub\Git_Practical_Tutorial> git status 
On branch master
nothing to commit, working tree clean
PS D:\Git and GitHub\Git_Practical_Tutorial> git switch master
Already on 'master'
PS D:\Git and GitHub\Git_Practical_Tutorial> git branch
  bugfix
  bugfix2
  feature_nidh_1
  feature_shrn_1
* master
  rebase_feat
PS D:\Git and GitHub\Git_Practical_Tutorial> git switch rebase_feat
Switched to branch 'rebase_feat'
PS D:\Git and GitHub\Git_Practical_Tutorial> git branch
  bugfix
  bugfix2
  feature_nidh_1
  feature_shrn_1
  master
* rebase_feat
PS D:\Git and GitHub\Git_Practical_Tutorial> git rebase master
Successfully rebased and updated refs/heads/rebase_feat.
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

**Git Graph Representation**
![[Pasted image 20260418110146.png]]

Now, the feature branch is originated from the master branch, hence its called the Fast Forward Merge
Even now there would be merge conflicts if the changes are made in same file.
If the changes are not made in the same file, the merge would be simpler and easy.

If we have merge the rebase_feat branch to master branch
Obviously we have to switch back to master
- git switch master
Merge the feature branch
- git merge rebase_feat
This would be called a Fast Forward Merge
Because there were no additional commits available at the master branch, So there wont be any merge commit.
We receive merge commit, only when we have Non Fast Forward Merge/3 Way Merge
This is the advantage of rebase

```
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch rebase_feat
nothing to commit, working tree clean
PS D:\Git and GitHub\Git_Practical_Tutorial> git switch master
Switched to branch 'master'
PS D:\Git and GitHub\Git_Practical_Tutorial> git branch
  bugfix
  bugfix2
  feature_nidh_1
  feature_shrn_1
* master
  rebase_feat
PS D:\Git and GitHub\Git_Practical_Tutorial> git merge rebase_feat
Updating 458e740..b8f9b65
Fast-forward
 data_ingestion.txt | 1 +
 1 file changed, 1 insertion(+)
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```


----

Assignment - Lets create a scenario, where we will have conflict when we are trying to rebase something and resolve the conflict

1. Create a new branch [rebase_feat_2]
	1. git switch -c rebase_feat_2
2. We shall edit the file
	1. data_ingest.txt
		1. Non Fast-Forward Merge/3 Way Merge [Feature_Rebase_1]
3. We shall add and commit to feature branch
4. Switch to Master branch [master]
	1. git switch master
5. We shall edit the same file
	1. data_ingest.txt
		1. Non Fast-Forward Merge/3 Way Merge [Feature_Rebase_2]
6. We shall add and commit to master branch
7. Now, go/switch the feature branch
	1. Rebase to master branch from the feature branch
		1. git rebase master
	2. There should be warning message indicating there are conflicts, we need to resolve them to move ahead with rebase.
8. Since both the branches have the commits in the same branch.
	1. There would be merge conflicts.
	2. Resolve those merge conflicts depending on which code to keep and which to discard.
	3. Then perform Merge Commit
		1. It includes
			1. git add 
			2. git commit
9. Important - Once the conflict is resolved the latest changes are added and committed.
	1. There is one more important command to run to complete the git rebasing
		1. git rebase --continue
			1. Successfully rebased and updated refs/heads/rebase_feat_2.
		2. If this command is not executed, then it is understood that rebasing is not fully completed.

---
Step 1 - 3

```
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch master
nothing to commit, working tree clean
PS D:\Git and GitHub\Git_Practical_Tutorial> git switch -c "rebase_feat_2"
Switched to a new branch 'rebase_feat_2'
PS D:\Git and GitHub\Git_Practical_Tutorial> git branch
  bugfix
  bugfix2
  feature_nidh_1
  feature_shrn_1
  master
  rebase_feat
* rebase_feat_2
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch rebase_feat_2
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   data_ingest.txt

no changes added to commit (use "git add" and/or "git commit -a")
PS D:\Git and GitHub\Git_Practical_Tutorial> git add .
PS D:\Git and GitHub\Git_Practical_Tutorial> git commit -m "data_ingest.txt - changes1"
[rebase_feat_2 5e1a87d] data_ingest.txt - changes1
 1 file changed, 0 insertions(+), 0 deletions(-)
PS D:\Git and GitHub\Git_Practical_Tutorial>
```

----
Steps 4 - 6

```
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch rebase_feat_2
nothing to commit, working tree clean
PS D:\Git and GitHub\Git_Practical_Tutorial> git switch master
Switched to branch 'master'
PS D:\Git and GitHub\Git_Practical_Tutorial> git branch
  bugfix
  bugfix2
  feature_nidh_1
  feature_shrn_1
* master
  rebase_feat
  rebase_feat_2
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   data_ingest.txt

no changes added to commit (use "git add" and/or "git commit -a")
PS D:\Git and GitHub\Git_Practical_Tutorial> git add .
PS D:\Git and GitHub\Git_Practical_Tutorial> git commit -m "data_ingest.txt - changes2"
[master c8ac8fc] data_ingest.txt - changes2
 1 file changed, 0 insertions(+), 0 deletions(-)
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

----
Step - 7

```
PS D:\Git and GitHub\Git_Practical_Tutorial> git status   
On branch master
nothing to commit, working tree clean
PS D:\Git and GitHub\Git_Practical_Tutorial> git switch rebase_feat_2
Switched to branch 'rebase_feat_2'
PS D:\Git and GitHub\Git_Practical_Tutorial> git branch
  bugfix
  bugfix2
  feature_nidh_1
  feature_shrn_1
  master
  rebase_feat
* rebase_feat_2
PS D:\Git and GitHub\Git_Practical_Tutorial> git rebase master
warning: Cannot merge binary files: data_ingest.txt (HEAD vs. 5e1a87d (data_ingest.txt - changes1))
Auto-merging data_ingest.txt
CONFLICT (content): Merge conflict in data_ingest.txt
error: could not apply 5e1a87d... data_ingest.txt - changes1
hint: Resolve all conflicts manually, mark them as resolved with
hint: "git add/rm <conflicted_files>", then run "git rebase --continue".
hint: You can instead skip this commit: run "git rebase --skip".
hint: To abort and get back to the state before "git rebase", run "git rebase --abort".
hint: Disable this message with "git config set advice.mergeConflict false"
Could not apply 5e1a87d... # data_ingest.txt - changes1
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

![[Pasted image 20260418140608.png]]


---
**Step - 8 & 9 [Important Steps]**

```
PS D:\Git and GitHub\Git_Practical_Tutorial> git status   
On branch master
nothing to commit, working tree clean
PS D:\Git and GitHub\Git_Practical_Tutorial> git switch rebase_feat_2
Switched to branch 'rebase_feat_2'
PS D:\Git and GitHub\Git_Practical_Tutorial> git branch
  bugfix
  bugfix2
  feature_nidh_1
  feature_shrn_1
  master
  rebase_feat
* rebase_feat_2
PS D:\Git and GitHub\Git_Practical_Tutorial> git rebase master
warning: Cannot merge binary files: data_ingest.txt (HEAD vs. 5e1a87d (data_ingest.txt - changes1))
Auto-merging data_ingest.txt
CONFLICT (content): Merge conflict in data_ingest.txt
error: could not apply 5e1a87d... data_ingest.txt - changes1
hint: Resolve all conflicts manually, mark them as resolved with
hint: "git add/rm <conflicted_files>", then run "git rebase --continue".
hint: You can instead skip this commit: run "git rebase --skip".
hint: To abort and get back to the state before "git rebase", run "git rebase --abort".
hint: Disable this message with "git config set advice.mergeConflict false"
Could not apply 5e1a87d... # data_ingest.txt - changes1
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
interactive rebase in progress; onto c8ac8fc
Last command done (1 command done):
   pick 5e1a87d # data_ingest.txt - changes1
No commands remaining.
You are currently rebasing branch 'rebase_feat_2' on 'c8ac8fc'.
  (all conflicts fixed: run "git rebase --continue")

nothing to commit, working tree clean
PS D:\Git and GitHub\Git_Practical_Tutorial> git add data_ingest.txt  
PS D:\Git and GitHub\Git_Practical_Tutorial> git commit -m "accepted the changes form master branch" 
interactive rebase in progress; onto c8ac8fc
Last command done (1 command done):
   pick 5e1a87d # data_ingest.txt - changes1
No commands remaining.
You are currently rebasing branch 'rebase_feat_2' on 'c8ac8fc'.
  (all conflicts fixed: run "git rebase --continue")

nothing to commit, working tree clean
PS D:\Git and GitHub\Git_Practical_Tutorial> git rebase --continue 
Successfully rebased and updated refs/heads/rebase_feat_2.
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch rebase_feat_2
nothing to commit, working tree clean
PS D:\Git and GitHub\Git_Practical_Tutorial>
```

**Git Graph Representation**

![[Pasted image 20260418141816.png]]


-------------

