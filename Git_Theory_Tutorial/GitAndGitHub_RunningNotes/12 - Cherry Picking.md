
This is the topic, which is very much hidden.
Specifically in the data domain/real world/corporate world we might work with this particular area a lot. Its called Cherry Pick

What is Cherry Picking?
- Lets say we have a master branch and we have some commits.
- We have a HEAD [which is the latest commit]
- From the HEAD/latest commit, we created a new branch
	- In the new branch, assume we have created 2 commits
		- bug fix commit
		- development commit
- Now, we see that, the bug fix commit is really important and needs to the merged into the master.
- If we consider the previous example of rebase and merging the lastest -> this will take both "bug fix commit" & "development commit" as well. [This is not our requirement for now.]
	- We just need the "bug fix commit" to be merged to master
- Here is where Cherry Picking comes into existence.
	- We can actually pick the commit which we want to merge

Cherry Picking means we are just picking the specific commit which we want to add/apply on top of master branch 
Important Note - Whenever we are commiting this bug fix - we will get some commit id [qwerty]
So this commit id will be used to pick the commit, but when this commit id will be added to master branch a new commit id [asdfgh] will assigned [New commit id which would be assigned on the particular commit]

**Flow Diagram**

![[Pasted image 20260418210827.png]]

---

**Practical**

1. Create a new branch from master
	1. git switch -c "cherry_pick"
2. Lets make some changes in the file
	1. Readme.md file
		1. This is the best Readme file and I guess so :)
			1. git add .
			2. git commit -m "bug fix"
3. Lets make some more change in another file
	1. data_ingest.txt
		1. I am a serious developer
			1. git add .
			2. git commit -m "development"
4. If we see the gitgraph now, we can see there 2 commits ahead of the master branch

```
PS D:\Git and GitHub\Git_Practical_Tutorial> git switch -c "cherry_pick"
Switched to a new branch 'cherry_pick'
PS D:\Git and GitHub\Git_Practical_Tutorial> git branch
  bugfix
  bugfix2
* cherry_pick
  feature_nidh_1
  feature_shrn_1
  master
  rebase_feat
  rebase_feat_2
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch cherry_pick
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   readme.md

no changes added to commit (use "git add" and/or "git commit -a")
PS D:\Git and GitHub\Git_Practical_Tutorial> git add .
PS D:\Git and GitHub\Git_Practical_Tutorial> git commit -m "bug fix"
[cherry_pick 66b2670] bug fix
 1 file changed, 1 insertion(+)
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch cherry_pick
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   data_ingest.txt

no changes added to commit (use "git add" and/or "git commit -a")
PS D:\Git and GitHub\Git_Practical_Tutorial> git add .
PS D:\Git and GitHub\Git_Practical_Tutorial> git commit -m "development"
[cherry_pick e0920a6] development
 1 file changed, 0 insertions(+), 0 deletions(-)
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

Git Graph Representation

![[Pasted image 20260418212413.png]]

5. Now, we want to use the "bug fix" commit id, because i want to merge/cherry pick.
	1. In order to do so, we need 2 things
		1. We need to be in master branch [so we need to switch to master]
		2. We need the commit id of the commit which we need to merge.
			1. This is called cherry picking

```
PS D:\Git and GitHub\Git_Practical_Tutorial> git log --oneline
e0920a6 (HEAD -> cherry_pick) development
66b2670 bug fix
c8ac8fc (rebase_feat_2, master) data_ingest.txt - changes2
b8f9b65 (rebase_feat) ingest big data
458e740 ingest batch data
5093620 finally conflict resolved
bd99acb bug is fixed
789d902 (bugfix2) fixed bug 2
2ea1a4f conflits merged
8bd56f1 bug is fixed
cec4dbf (bugfix) fix bug
fdca9c8 merging feature_shrn_1
983c106 Merge branch 'feature_nidh_1'
624a26d master commit
3d7a6da (feature_nidh_1) ingested real time data
a5a7ee6 (feature_shrn_1) added more data
5ca01f9 added more data
5976fd0 added silver folder
b705359 ignored bronze folder
PS D:\Git and GitHub\Git_Practical_Tutorial> git switch master
Switched to branch 'master'
PS D:\Git and GitHub\Git_Practical_Tutorial> git branch
  bugfix
  bugfix2
  cherry_pick
  feature_nidh_1
  feature_shrn_1
* master
  rebase_feat
  rebase_feat_2
PS D:\Git and GitHub\Git_Practical_Tutorial> git cherry-pick 66b2670
[master 081e09e] bug fix
 Date: Sat Apr 18 21:16:39 2026 +0530
 1 file changed, 1 insertion(+)
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

Git Graph Representation
![[Pasted image 20260418213402.png]]

If we have multiple commits to cherry pick, that also could be done.
- git cherry-pick 66b2670 66b2671 66b2672
Important Note - 
- We need to make sure of the order we follow the order of commit
- It means if 66b2670 [this commit] is committed first, this should be picked up first for cherry picking and it should be followed by 66b2671 & 66b2672
Now, in our example, we don't have issues because both the changes and commits are of 2 different files.
If we have multiple commits in the same file, then while cherry picking, the commit order has to be followed strictly.

Best Use Case
- If we are working in dev environment and we have something called hotfix in our environment.
- So we don't actually have to promote the hot fix in QA first and other environments
- We can simply pick that particular commit and make that hotfix available directly in production using that commit id.

----
