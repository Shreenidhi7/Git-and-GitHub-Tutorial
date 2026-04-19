
What is that thing that will actually make us an outlier when we are developing projects?
What is that particular thing that will actually tell us that we are not just learning/understanding git commands

This area will actually tell us that we are actually understanding the GIT
- The area/topic is called gitignore

Scenario -
1. We have this folder "Git_Practical_Tutorial" and we want to track it
	1. We can say git init and track it.
2. Lets assume we have multiple folders
	1. We want to create a different tracking, so we would be initializing git in the individual folder so that our git repo is independently tracked in those folders
3. But lets assume we initialized the git repo in the particular folder called "Git_Practical_Tutorial" and now within this parent root folder which is also called as repo we do not want to track a few files. How do we do that?
	1. It is possible, we will just understand this with a real time example

Git_Practical_Tutorial -> This is our folder/project
1. Assume we have something called API secrets
	1. Lets create a file called api_secrets.txt
		1. api_shr = "000000000000000000000"
		2. api_dash = "999999999999999999999"
			1. Its untracked for now.
	2. I will create another file called .env
		1. We create .env file to create environment variables for our api keys
			1. api_key = "XXXXXXXXXXXXXXXXXXXXXXXXXX"
2. Now the above 2 files [api_secrets.txt & .env] are sensitive.
	1. These files shouldn't be published in the public git repo

We cannot go ahead with git add . => this will even publish the sensitive data
If we do git status, these 2 sensitive data files shows are untracked.

```
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .env
        api_secrets.txt

nothing added to commit but untracked files present (use "git add" to track)
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

---

Even though by mistake if we add these secret files to public repository, its very risky.
So what do we do to negate this. Do we have any workaround to this?

Yes, there is a file that we want to create in the parent repository/root repository, where we have .git as well.
- File name -> .gitignore

What is .gitignore file?
- This file is a savior, it asks for all those files which we want to ignore, when provided it will ignore those files
```
.env
api_secrets.txt
```

Now, if we check with git status, those 2 files will be gone.
We will not see .env and api_secrets.txt files. These files are now ignored.
```
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .gitignore

nothing added to commit but untracked files present (use "git add" to track)
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

Going further .gitignore file has to tracked, but .gitignore has only the name of the files [.env & api_secrets]
It doesn't have the values displayed.
```
PS D:\Git and GitHub\Git_Practical_Tutorial> git add .      
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   .gitignore

PS D:\Git and GitHub\Git_Practical_Tutorial> git commit -m "gitignore file"
[master f0e0866] gitignore file
 1 file changed, 2 insertions(+)
 create mode 100644 .gitignore
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

---
Now, if we check the git log, gitignore commit would also be listed.
```
PS D:\Git and GitHub\Git_Practical_Tutorial> git log --oneline
f0e0866 (HEAD -> master) gitignore file
1dd6575 new iot data ingested
28669ec Data Ingest and IOT Data Ingestion
b10dd53 Ingest Data
08a8756 initial commit
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

The HEAD is pointing at the latest commit i.e at the gitignore commit

---

**Graph Representation**

![[Pasted image 20260413205535.png]]

---

Question?
- If we want to ignore the entire folder, can we do that?
Answer
- Yes

One very important to note here.
Scenario
- Assume we create a folder named "bronze" - Its an empty folder.
- Now our assumption is that when we do git status, it should the folder name as untracked. Right?
Answer/Solution
- The thing is GIT do not track empty folders
	- If we have a file inside the folder, then the folder is tracked.
- GIT do not actually care about empty folders

```
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        bronze/

nothing added to commit but untracked files present (use "git add" to track)
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

---

Now we shall add the bronze folder in the .gitignore as well

Before adding bronze folder in .gitignore
```
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        bronze/

nothing added to commit but untracked files present (use "git add" to track)
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

.gitignore file
```
.env
api_secrets.txt
bronze/
```


After adding bronze folder in .gitignore
```
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   .gitignore

no changes added to commit (use "git add" and/or "git commit -a")
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

----
---

Now, we have some empty folders, and we still want to track it. Can it be done?
In the previous example we understood that the empty folders cannot be tracked.
Lets understand this with an example

Lets create a folder - silver - its an empty folder
Why do we need to track it?
- We might need to track it because we need to keep the structure.
- Maybe we don't have files for now, but in future we might have files or we just want to keep empty folder [so that any person/any time uses this repository will be having the structure]

There is a thing we have within the GIT, We need to simply create another file within this.
Its called **.gitkeep**
This file [.gitkeep] has to added inside the empty folder we want to keep as reference for future
silver -> .gitkeep
Its like we are saying GIT, i know this folder is empty, but keep this folder.
```
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        silver/

nothing added to commit but untracked files present (use "git add" to track)
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

![[Pasted image 20260413211811.png]]


---

Adding and Committing Silver Folder

```
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        silver/

nothing added to commit but untracked files present (use "git add" to track)
PS D:\Git and GitHub\Git_Practical_Tutorial> git add .
PS D:\Git and GitHub\Git_Practical_Tutorial> git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   silver/.gitkeep

PS D:\Git and GitHub\Git_Practical_Tutorial> git commit -m "added silver folder"
[master 5976fd0] added silver folder
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 silver/.gitkeep
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

----

**Graph Representation**

![[Pasted image 20260413212038.png]]

"HEAD" is pointing to the latest commit.

---

