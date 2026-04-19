
Getting Started GIT
1. Open the VS code editor
2. Question - Do we need any kind of special extension that are required for GIT
	1. Yes, there is one very useful extension which will help us to visualize the progress that we are making for our repository, for our commits and all other checkpoints.
	2. Extension Name - Git Graph
		1. Go to Settings -> Extensions - Search for Git Graph - Install

Now, we have a folder that is opened in VS code and we can observe, its totally empty
"Git_Practical_Tutorial"
We will be using this folder as our root directory/repository
Repository is a fancy name for our root folder/parent folder where we track all the things.

Now basically the folder "Git_Practical_Tutorial" is not actually a repo/repository for now.
Because the thing is we haven't actually initiated or converted this folder into a repository.
This is just a directory/folder for now.

---

So how do we confirm that this just a directory/folder but not a repository?
- We can confirm that in VS code. Just click on "Source Control" tab in the left side navigation bar. [Its the embedded version of source control in VS code]
	- We see a message saying -
		- The folder currently open doesn't have a Git repository
		- You can initialize a repository which will enable "Source Control" feature powered by Git
**Snapshot Reference -** 
![[Pasted image 20260413092725.png|317]]

- So the basic understanding is - The folder "Git_Practical_Tutorial" is not our repository yet. Its still a directory/folder. But we have make it/convert it into a repository.
- We have installed Git Bash for git specific operations, but VS code itself have a way to perform git operations through its PowerShell terminal
- In order to open "PowersShell", we can click on 3 dots and select option "Terminal" and click on "New Terminal" [There is shortcut that could be used as well (Ctrl + Shift + `)]
- Once the terminal is opened - this how the terminal looks like
	- PS D:\Git and GitHub\Git_Practical_Tutorial>]
- Its currently pointing to D drive, Git and GitHub, Git Practical Tutorial folder
- By default, VS code opens our terminal in PS[PowerShell]
	- We can change it anytime by clicking on the dropdown beside the terminal name and change accordingly. We shall to stick to Powershell
	- Commands like touch,ls are not compatible with command prompt.

----

Currently, we shall run one command **"git status"**
- "git status" is the common command that we have to run everytime, wheneve we are working on the existing repository or a new one.
	- Being a good developer, we should run this command as the first command
- **PS D:\Git and GitHub\Git_Practical_Tutorial> git status**
	- **fatal: not a git repository (or any of the parent directories): .git**
- This confirms that this folder/directory is not actually a git repository

---

What is the config file? Why do we need it?
- Config file consists the email id and user name that would be used with all our commits, so that other people know that the person using the email address has made a particular commit.
- Also this particular email id will be used when we will be pushing our code to remote repository

Question
- Do we need to do the same practice of all the future repositories?
Answer
- No, that's the reason we have to use the global keyword while configuring the user email.
	- So, this particular email id will be saved in the global git settings of our system and every time we are working on any new repository anywhere in any drive{be it C,DE} -:> it will be automatically picked up.

Before creating a Git Repository, we need to config the git with our user details.
- PS D:\Git and GitHub\Git_Practical_Tutorial> git config --global user.email "shreenidhisharma7@gmail.com"
- PS D:\Git and GitHub\Git_Practical_Tutorial> git config --global user.name "Shreenidhi7"

---

How we can create a Git Repository? How we can convert this folder into a Git Repository?
- To create/initialize a repository, we need to run the command **git init**
- PS D:\Git and GitHub\Git_Practical_Tutorial> git init
	- Initialized empty Git repository in D:/Git and GitHub/Git_Practical_Tutorial/.git/

We see 3 stuff once we successfully run the **git init** command
1. Response from the terminal
	1. Initialized empty Git repository
2. Left bottom corner
	1. master
3. .git folder added in the folder "Git_Practical_Tutorial"
	1. But it might not be visible yet, we shall come to point later

But ideally, this would be the pure indication that our GitHub repository is initialized
If we want to confirm it, we can make use of **git status** command
- PS D:\Git and GitHub\Git_Practical_Tutorial> git status
	- On branch master
	- No commits yet
	- nothing to commit (create/copy files and use "git add" to track)
- In short, earlier we used to get a different response
	- **fatal: not a git repository (or any of the parent directories): .git**
		- This was because the git was not initialized, now since the git is initialized, we see that in which branch we are and the status about our commits.


Now we shall discuss why we wont see the .git folder yet?
- Basically .git folder is the backbone of our github repository
- .git is a hidden folder

To see the .git folder
- We need to actually remove .git extension from the list of the excluded folders
- In order to do that follow below steps
	- Click on "Settings"
	- Select option "Command Palette"
	- Write "Preferences: Open Settings (UI)" and click on this
		- The settings page would be displayed
	- Scroll down until we find the section "Exclude"
		- Click on the remove button, we should be able to see the .git folder

If the .git folder is not seen/dispalyed in the folder. The reason would be that in the settings, it might be included under the "Exclude" settings.
![[Pasted image 20260413140532.png]]

Once the .git folder was removed from the Exclude settings, the .git folder will be visible/displayed under out directory "Git_Practical_Tutorial"
![[Pasted image 20260413140832.png]]

---

**Important Note - Its not recommended to touch the .git folder**
Because .git is the backbone of all the checkpoints that we will be creating in our code

---

If we want to check the progress on the git, then we need to use the git commands.

- Now since, we have initilized our git repository, we have the git folder visible, we shall check the status of or git now
	- PS D:\Git and GitHub\Git_Practical_Tutorial> git status
		- On branch master
		- No commits yet
		- nothing to commit (create/copy files and use "git add" to track)
- Git says that we are on the master branch.
	- There is a command in git which can list all the branches available in our repository.
	- The command is called **git branch**
		- If this command is responsible to tell about all the branches in our repository, then which branch it should return now?
		- The answer would be straight forword -> It should be master branch
	- Lets check that
		- PS D:\Git and GitHub\Git_Practical_Tutorial> git branch
		- PS D:\Git and GitHub\Git_Practical_Tutorial> 
		- We are seeing nothing in the response.

Why don't we see anything in the response? What could be the reason?
- The master is there, but it is not actually registered.
- We need to register the branch just for the initial commit.
- Git will not recognize our branch if it doesn't have any commit
- So, in order to register a branch, it should have at least 1 commit
	- This is the reason in most of the code base we see something called as initial commit
- Initial Commit -> Initial Commit is register the master branch/main branch

What can be a commit?
- Commit can be any progress, lets say we want to add/edit a file
- Create a new file in the explorer with text/txt as an extension.
	- Its a good practice to create a filename as **redme.md**
		- md is the extension for markdown
	- readme.md can have an introduction of this particular repository.
- Once we create a file **readme.md**
	- we can see U beside the readme.md file -> this refers as Untracked.
- This file is created using the master branch

**Making an initial commit**
1. Add the file
	1. PS D:\Git and GitHub\Git_Practical_Tutorial> git add .
2. Commit the changes
	1. PS D:\Git and GitHub\Git_Practical_Tutorial> git commit -m "initial commit"

```
PS D:\Git and GitHub\Git_Practical_Tutorial> git add .
PS D:\Git and GitHub\Git_Practical_Tutorial> git commit -m "initial commit"
[master (root-commit) 08a8756] initial commit
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 readme.md
```

Once the commit is done, that would be enough to register the branch.
We don't have to follow this **initial commit** steps for all the branches, because our parent is registered.
Now if we run git branch, we see the ouptut/response as **master**
- PS D:\Git and GitHub\Git_Practical_Tutorial> git branch
	* master

```
PS D:\Git and GitHub\Git_Practical_Tutorial> git add .
PS D:\Git and GitHub\Git_Practical_Tutorial> git commit -m "initial commit"
[master (root-commit) 08a8756] initial commit
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 readme.md
PS D:\Git and GitHub\Git_Practical_Tutorial> git branch
* master
```

Now, if we click on the Git Graph
Below if the visual representation
![[Pasted image 20260413145102.png]]

