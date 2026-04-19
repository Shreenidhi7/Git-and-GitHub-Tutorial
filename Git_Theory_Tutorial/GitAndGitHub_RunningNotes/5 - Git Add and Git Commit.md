
Ways to create a file with data in it.
1. In VS Code
	1. Click on "New File" option
	2. Provide the name and extension for the file
		1. data_ingestion.txt
			1. Hey, i am ingesting the data in this file.
2. Through Terminal
	1. echo "This is another data ingestion file" > data_ingest.txt

These files are currently untracked "U"
If we get the git staus
```
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        data_ingest.txt
        data_ingestion.txt

nothing added to commit but untracked files present (use "git add" to track)
```

How git knows that these 2 are new files?
1. We have .git and it keeps an eye, but it doesn't actually track it. 
2. When we do git status
	1. Its giving us some hints on the newly created files
	2. Also tells us what to do if we need to commit the changes

---
If we just want to add data_ingestion file and don't want to do anything with data_ingest file

```
PS D:\Git and GitHub\Git_Practical_Tutorial> git add data_ingest.txt
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   data_ingest.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        data_ingestion.txt

PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

Creating a commit
- We need to write a message [Its a good practice]
	- Each commit message should tell us something why the commit was made.
- Recommendation - It is always recommended write the message in the simple Present Tense
	- It should be like you are commanding a git to do something

```
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        data_ingest.txt
        data_ingestion.txt

nothing added to commit but untracked files present (use "git add" to track)
PS D:\Git and GitHub\Git_Practical_Tutorial> git add data_ingest.txt
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   data_ingest.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        data_ingestion.txt

PS D:\Git and GitHub\Git_Practical_Tutorial> git commit -m "Ingest Data"
[master b10dd53] Ingest Data
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 data_ingest.txt
PS D:\Git and GitHub\Git_Practical_Tutorial>
```

Once this is ingested, we would be left with the file "data_ingest" which was not tracked yet
```
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        data_ingest.txt
        data_ingestion.txt

nothing added to commit but untracked files present (use "git add" to track)
PS D:\Git and GitHub\Git_Practical_Tutorial> git add data_ingest.txt
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   data_ingest.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        data_ingestion.txt

PS D:\Git and GitHub\Git_Practical_Tutorial> git commit -m "Ingest Data"
[master b10dd53] Ingest Data
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 data_ingest.txt
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        data_ingestion.txt

nothing added to commit but untracked files present (use "git add" to track)
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

**Git Graph Representation**

![[Pasted image 20260413180551.png]]

---

Ingesting another data with new file iot_data_ingestion.txt => I am ingesting real-time data
Now, if we do git status, we can see 2 untracked file
1. data_ingest.txt
2. iot_data_ingestion.txt

```
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        data_ingestion.txt
        iot_data_ingestion.txt

nothing added to commit but untracked files present (use "git add" to track)
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

Now, if i want to create a snapshot for both the files
- git add data_ingestion.txt iot_data_ingestion.txt

Tip -> Whenever we are working will so many files, it difficult to write each file name one by one.
We can make use of command -> git add .
- This command will automatically add all the files and simple bundle those files and take a snapshot of all the files

```
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        data_ingestion.txt
        iot_data_ingestion.txt

nothing added to commit but untracked files present (use "git add" to track)
PS D:\Git and GitHub\Git_Practical_Tutorial> git add .
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   data_ingestion.txt
        new file:   iot_data_ingestion.txt

PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

Now, we can observe that the state is changed to "A"
- This means the files are added into the staging area

Sometimes, if we are hurry and we forgot to provide a message in the commit
If we just type **git commit and press Enter**
**There would be a hint: Waiting for your editor to close the file...** 
- It opens up the file called "COMMIT_EDITMSG" and asks us to write a message there

Its like the git is saying that we know you are busy, but its my duty to take your commit message.
Yes, you forgot to add message in the terminal, its fine, you can add message here as well
So whatever we write in the "COMMIT_EDITMSG", that would be taken as the commit message
Save the file and close the file
The moment we close the file, the commit would be done automatically

```
PS D:\Git and GitHub\Git_Practical_Tutorial> git add .
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   data_ingestion.txt
        new file:   iot_data_ingestion.txt

PS D:\Git and GitHub\Git_Practical_Tutorial> git commit
[master 28669ec] Data Ingest and IOT Data Ingestion
 2 files changed, 2 insertions(+)
 create mode 100644 data_ingestion.txt
 create mode 100644 iot_data_ingestion.txt
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

From this commit, our master branch moved up by one more commit.
This time we don't see 2 commits, we see only one commit.
Because we bundled the files and created only one commit for both the files.

**Graph Representation**

![[Pasted image 20260413183007.png]]


----

**EDIT A FILE**

We make some changes to the file which is already committed.
Example - 
iot_data_ingestion.txt

```
I am ingesting real-time data
New Data Ingested - New Line Added
```

We will see a mark called "M". This is called Modified.
This time, this is not say its UNTRACKED, it say its MODIFIED
Because, the changes are made on top of the exiting file, here just the file is modified with some new data

```
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   iot_data_ingestion.txt

no changes added to commit (use "git add" and/or "git commit -a")
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

Again Adding and Committing the Changes

```
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   iot_data_ingestion.txt

no changes added to commit (use "git add" and/or "git commit -a")
PS D:\Git and GitHub\Git_Practical_Tutorial> git add .
PS D:\Git and GitHub\Git_Practical_Tutorial> git status  
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   iot_data_ingestion.txt

PS D:\Git and GitHub\Git_Practical_Tutorial> git commit -m "new iot data ingested"
[master 1dd6575] new iot data ingested
 1 file changed, 2 insertions(+), 1 deletion(-)
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

---

**Graph Representation**

![[Pasted image 20260413184155.png]]


---

- We can observe that our graph is growing with each commit
- Also we observe that all other changes are done on the master branch
- Ideally we do not create changes in the master branch
	- That is the reason we have the concept of branches

Before we talk of branches, we shall discuss about the "HEAD".
If we click on the graph and click on the graph checkpoint.
It tells
- This commit is included in "HEAD"
- Branches "master"
If i go to .git and click on the file named "HEAD"
- This is what is written in it
	- ref: refs/heads/master
---

What is this HEAD?
- Basically in short, "HEAD" refers to the "latest commit" thar we make in the branch
- Currently we have just one branch, that is master.
	- Here the HEAD is at the latest commit "new iot data ingested"

Why is it important?
- Whenever we create a branch, we always create a branch from the HEAD of the current branch.
	- Currently we are working on master/main/parent branch
- Assume, if we want to work with other team mates
	- Myself and other teammate is working on the same particular project
	- Obviously, now from the current branch or latest commit/HEAD we want to create another branch 