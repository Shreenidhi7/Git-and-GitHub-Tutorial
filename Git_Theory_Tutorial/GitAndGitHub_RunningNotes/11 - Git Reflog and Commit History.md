
Now, we shall discuss about time travelling in GIT.
We shall discuss about how we UNDO our work.
- Assume, we have made some changes, but we don't want to apply this commit could be any reason and we want to go back to previous commit. 

Git Reflog - One of the most important thing we would learn in git.
Sometimes, we need to time travel back in time to do so we need to learn to the reflog and commit history topics in GIT

1. Lets switch to master branch
	1. git switch master
2. Lets delete a file by right clicking on the file and selecting delete option.
	1. data_ingest.txt
3. Lets do git status
	1. The status tells us that a file has been deleted
4. Lets add and commit the changes with the deleted file
	1. git add .
	2. git commit -m "delete data_ingest.txt"
5. Lets check the log aswell after the deletion
	1. git log --oneline
6. Now, there is a command which is a brother of git log command
	1. git reflog
		1. Its an advanced version of git log --oneline
			1. We get a little bit more detail as compared to git log --oneline
			2. In order to do time travelling, its better to use git reflog.
				1. Because, we get commit id in the shorter version
				2. We get the details of HEAD
					1. The latest commit is considered as HEAD{0}
					2. If i have to go back to the previous HEAD, then previous head would be called as HEAD{1} and so on.
7. So, now if we want to bring back the deleted file by going back to the previous file.

**Steps 1 -5**

```
PS D:\Git and GitHub\Git_Practical_Tutorial> git switch master
Already on 'master'
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
nothing to commit, working tree clean
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        deleted:    data_ingest.txt

no changes added to commit (use "git add" and/or "git commit -a")
PS D:\Git and GitHub\Git_Practical_Tutorial> git add .
PS D:\Git and GitHub\Git_Practical_Tutorial> git commit -m "delete data_ingest.txt"
[master 95fd945] delete data_ingest.txt
 1 file changed, 0 insertions(+), 0 deletions(-)
 delete mode 100644 data_ingest.txt
PS D:\Git and GitHub\Git_Practical_Tutorial> git log --oneline
95fd945 (HEAD -> master) delete data_ingest.txt
c8ac8fc (rebase_feat_2) data_ingest.txt - changes2
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
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

---

Step - 6

```
PS D:\Git and GitHub\Git_Practical_Tutorial> git reflog
95fd945 (HEAD -> master) HEAD@{0}: commit: delete data_ingest.txt
c8ac8fc (rebase_feat_2) HEAD@{1}: checkout: moving from master to master
c8ac8fc (rebase_feat_2) HEAD@{2}: checkout: moving from rebase_feat_2 to master
c8ac8fc (rebase_feat_2) HEAD@{3}: rebase (finish): returning to refs/heads/rebase_feat_2
c8ac8fc (rebase_feat_2) HEAD@{4}: rebase (start): checkout master
5e1a87d HEAD@{5}: checkout: moving from master to rebase_feat_2
c8ac8fc (rebase_feat_2) HEAD@{6}: commit: data_ingest.txt - changes2
b8f9b65 (rebase_feat) HEAD@{7}: checkout: moving from rebase_feat_2 to master
5e1a87d HEAD@{8}: commit: data_ingest.txt - changes1
b8f9b65 (rebase_feat) HEAD@{9}: checkout: moving from master to rebase_feat_2
b8f9b65 (rebase_feat) HEAD@{10}: merge rebase_feat: Fast-forward
458e740 HEAD@{11}: checkout: moving from rebase_feat to master
:...skipping...
95fd945 (HEAD -> master) HEAD@{0}: commit: delete data_ingest.txt
c8ac8fc (rebase_feat_2) HEAD@{1}: checkout: moving from master to master
c8ac8fc (rebase_feat_2) HEAD@{2}: checkout: moving from rebase_feat_2 to master
c8ac8fc (rebase_feat_2) HEAD@{3}: rebase (finish): returning to refs/heads/rebase_feat_2
c8ac8fc (rebase_feat_2) HEAD@{4}: rebase (start): checkout master
5e1a87d HEAD@{5}: checkout: moving from master to rebase_feat_2
c8ac8fc (rebase_feat_2) HEAD@{6}: commit: data_ingest.txt - changes2
b8f9b65 (rebase_feat) HEAD@{7}: checkout: moving from rebase_feat_2 to master
5e1a87d HEAD@{8}: commit: data_ingest.txt - changes1
b8f9b65 (rebase_feat) HEAD@{9}: checkout: moving from master to rebase_feat_2
b8f9b65 (rebase_feat) HEAD@{10}: merge rebase_feat: Fast-forward
458e740 HEAD@{11}: checkout: moving from rebase_feat to master
b8f9b65 (rebase_feat) HEAD@{12}: rebase (finish): returning to refs/heads/rebase_feat
:...skipping...
95fd945 (HEAD -> master) HEAD@{0}: commit: delete data_ingest.txt
c8ac8fc (rebase_feat_2) HEAD@{1}: checkout: moving from master to master
c8ac8fc (rebase_feat_2) HEAD@{2}: checkout: moving from rebase_feat_2 to master
c8ac8fc (rebase_feat_2) HEAD@{3}: rebase (finish): returning to refs/heads/rebase_feat_2
c8ac8fc (rebase_feat_2) HEAD@{4}: rebase (start): checkout master
5e1a87d HEAD@{5}: checkout: moving from master to rebase_feat_2
c8ac8fc (rebase_feat_2) HEAD@{6}: commit: data_ingest.txt - changes2
b8f9b65 (rebase_feat) HEAD@{7}: checkout: moving from rebase_feat_2 to master
5e1a87d HEAD@{8}: commit: data_ingest.txt - changes1
b8f9b65 (rebase_feat) HEAD@{9}: checkout: moving from master to rebase_feat_2
b8f9b65 (rebase_feat) HEAD@{10}: merge rebase_feat: Fast-forward
458e740 HEAD@{11}: checkout: moving from rebase_feat to master
b8f9b65 (rebase_feat) HEAD@{12}: rebase (finish): returning to refs/heads/rebase_feat
b8f9b65 (rebase_feat) HEAD@{13}: rebase (pick): ingest big data
458e740 HEAD@{14}: rebase (start): checkout master
23e0a48 HEAD@{15}: checkout: moving from master to rebase_feat
:...skipping...
95fd945 (HEAD -> master) HEAD@{0}: commit: delete data_ingest.txt
c8ac8fc (rebase_feat_2) HEAD@{1}: checkout: moving from master to master
c8ac8fc (rebase_feat_2) HEAD@{2}: checkout: moving from rebase_feat_2 to master
c8ac8fc (rebase_feat_2) HEAD@{3}: rebase (finish): returning to refs/heads/rebase_feat_2
c8ac8fc (rebase_feat_2) HEAD@{4}: rebase (start): checkout master
5e1a87d HEAD@{5}: checkout: moving from master to rebase_feat_2
c8ac8fc (rebase_feat_2) HEAD@{6}: commit: data_ingest.txt - changes2
b8f9b65 (rebase_feat) HEAD@{7}: checkout: moving from rebase_feat_2 to master
5e1a87d HEAD@{8}: commit: data_ingest.txt - changes1
b8f9b65 (rebase_feat) HEAD@{9}: checkout: moving from master to rebase_feat_2
b8f9b65 (rebase_feat) HEAD@{10}: merge rebase_feat: Fast-forward
458e740 HEAD@{11}: checkout: moving from rebase_feat to master
b8f9b65 (rebase_feat) HEAD@{12}: rebase (finish): returning to refs/heads/rebase_feat
b8f9b65 (rebase_feat) HEAD@{13}: rebase (pick): ingest big data
458e740 HEAD@{14}: rebase (start): checkout master
23e0a48 HEAD@{15}: checkout: moving from master to rebase_feat
458e740 HEAD@{16}: checkout: moving from master to master
:...skipping...
95fd945 (HEAD -> master) HEAD@{0}: commit: delete data_ingest.txt
c8ac8fc (rebase_feat_2) HEAD@{1}: checkout: moving from master to master
c8ac8fc (rebase_feat_2) HEAD@{2}: checkout: moving from rebase_feat_2 to master
c8ac8fc (rebase_feat_2) HEAD@{3}: rebase (finish): returning to refs/heads/rebase_feat_2
c8ac8fc (rebase_feat_2) HEAD@{4}: rebase (start): checkout master
5e1a87d HEAD@{5}: checkout: moving from master to rebase_feat_2
c8ac8fc (rebase_feat_2) HEAD@{6}: commit: data_ingest.txt - changes2
b8f9b65 (rebase_feat) HEAD@{7}: checkout: moving from rebase_feat_2 to master
5e1a87d HEAD@{8}: commit: data_ingest.txt - changes1
b8f9b65 (rebase_feat) HEAD@{9}: checkout: moving from master to rebase_feat_2
b8f9b65 (rebase_feat) HEAD@{10}: merge rebase_feat: Fast-forward
458e740 HEAD@{11}: checkout: moving from rebase_feat to master
b8f9b65 (rebase_feat) HEAD@{12}: rebase (finish): returning to refs/heads/rebase_feat
b8f9b65 (rebase_feat) HEAD@{13}: rebase (pick): ingest big data
458e740 HEAD@{14}: rebase (start): checkout master
23e0a48 HEAD@{15}: checkout: moving from master to rebase_feat
458e740 HEAD@{16}: checkout: moving from master to master
458e740 HEAD@{17}: commit: ingest batch data
5093620 HEAD@{18}: checkout: moving from rebase_feat to master
:...skipping...
95fd945 (HEAD -> master) HEAD@{0}: commit: delete data_ingest.txt
c8ac8fc (rebase_feat_2) HEAD@{1}: checkout: moving from master to master
c8ac8fc (rebase_feat_2) HEAD@{2}: checkout: moving from rebase_feat_2 to master
c8ac8fc (rebase_feat_2) HEAD@{3}: rebase (finish): returning to refs/heads/rebase_feat_2
c8ac8fc (rebase_feat_2) HEAD@{4}: rebase (start): checkout master
5e1a87d HEAD@{5}: checkout: moving from master to rebase_feat_2
c8ac8fc (rebase_feat_2) HEAD@{6}: commit: data_ingest.txt - changes2
b8f9b65 (rebase_feat) HEAD@{7}: checkout: moving from rebase_feat_2 to master
5e1a87d HEAD@{8}: commit: data_ingest.txt - changes1
b8f9b65 (rebase_feat) HEAD@{9}: checkout: moving from master to rebase_feat_2
b8f9b65 (rebase_feat) HEAD@{10}: merge rebase_feat: Fast-forward
458e740 HEAD@{11}: checkout: moving from rebase_feat to master
b8f9b65 (rebase_feat) HEAD@{12}: rebase (finish): returning to refs/heads/rebase_feat
b8f9b65 (rebase_feat) HEAD@{13}: rebase (pick): ingest big data
458e740 HEAD@{14}: rebase (start): checkout master
23e0a48 HEAD@{15}: checkout: moving from master to rebase_feat
458e740 HEAD@{16}: checkout: moving from master to master
458e740 HEAD@{17}: commit: ingest batch data
5093620 HEAD@{18}: checkout: moving from rebase_feat to master
23e0a48 HEAD@{19}: commit: ingest big data
5093620 HEAD@{20}: checkout: moving from master to rebase_feat
5093620 HEAD@{21}: commit (merge): finally conflict resolved
bd99acb HEAD@{22}: checkout: moving from master to master
:
```


---

Step - 7
In order to perform time travelling, we just need to perform
- 2 Options
	- By getting the exact commit id [Recommended Way]
	- By moving to the previous HEAD -> ex: HEAD~1
		- HEAD~0 -> it is the current Head
		- HEAD~1 -> it the previous Head
- git reset --hard HEAD~1
	- Once done, we will get our deleted file back.
- Now, if we do git reflog, we can see in the history that we have moved to the previous HEAD

```
PS D:\Git and GitHub\Git_Practical_Tutorial> git reset --hard HEAD~1
HEAD is now at c8ac8fc data_ingest.txt - changes2
PS D:\Git and GitHub\Git_Practical_Tutorial> git reflog
c8ac8fc (HEAD -> master, rebase_feat_2) HEAD@{0}: reset: moving to HEAD~1
95fd945 HEAD@{1}: commit: delete data_ingest.txt
c8ac8fc (HEAD -> master, rebase_feat_2) HEAD@{2}: checkout: moving from master to master
c8ac8fc (HEAD -> master, rebase_feat_2) HEAD@{3}: checkout: moving from rebase_feat_2 to master
c8ac8fc (HEAD -> master, rebase_feat_2) HEAD@{4}: rebase (finish): returning to refs/heads/rebase_feat_2
c8ac8fc (HEAD -> master, rebase_feat_2) HEAD@{5}: rebase (start): checkout master
```

![[Pasted image 20260418163925.png]]

----

Okay, we have brought back the deleted file [data_ingest.txt].
But if we go back the previous commit [means the file deleted commit] - Is that possible?
- Yes, that's possible but this time we shall not use HEAD~1, instead we will use the commit id way [which is the recommended way]
	- Commit ID is the source of truth

```
PS D:\Git and GitHub\Git_Practical_Tutorial> git reset --hard 95fd945
HEAD is now at 95fd945 delete data_ingest.txt
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```


![[Pasted image 20260418164940.png]]

Now we are same commit where the file was deleted.
If observed, we just moved back and forth with the git reset --hard "" with the help of git reflog command.


-----------------

**We shall go through a popular command - git diff**
- As the name suggests, it tells us the difference b/w 2 things
	- It can be b/w 2 branches
	- It can be b/w 2 areas
	- It can be b/w 2 files

1. We are in master branch
	1. git switch master
	2. git branch
2. We shall make use of readme.md file
	1. This is the best readme file. Trust me :)
3. Perform git diff
	1. It compares the working directory and the staging area

```
PS D:\Git and GitHub\Git_Practical_Tutorial> git diff
diff --git a/readme.md b/readme.md
index e69de29..1bc98c4 100644
--- a/readme.md
+++ b/readme.md
@@ -0,0 +1 @@
+This is the best readme file. Trust me :)
\ No newline at end of file
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

4. Once this readme.md file is added to the staging area, using git add .
	1. The file will be moved from working directory to staging area
	2. Now, if we perform -> git diff --staged
		1. It should show the similar diff 

```
PS D:\Git and GitHub\Git_Practical_Tutorial> git add .
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   readme.md

PS D:\Git and GitHub\Git_Practical_Tutorial> git diff --staged
diff --git a/readme.md b/readme.md
index e69de29..1bc98c4 100644
--- a/readme.md
+++ b/readme.md
@@ -0,0 +1 @@
+This is the best readme file. Trust me :)
\ No newline at end of file
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

Now Question.
- If we want to revert the changes in the readme.md file
- Thing is that, if we want to go back to the previous state, we could have done it through 
	- git reset --hard "commitid"
- But here, we have just moved to the staging area, we haven't committed it yet.
	- In this case, how do we revert the changes back to orginal state?
		- git reset
	- Since we haven't committed the changes in staging area, it is simple git reset that helps to bring the changes back to original [ That means it is in modified state, not in the added state ]
```
PS D:\Git and GitHub\Git_Practical_Tutorial> git reset
Unstaged changes after reset:
M       readme.md
```

One thing to note - git reset will revert all the files, but if we specify the file which we need to reset, we could do that as well [git reset filename]