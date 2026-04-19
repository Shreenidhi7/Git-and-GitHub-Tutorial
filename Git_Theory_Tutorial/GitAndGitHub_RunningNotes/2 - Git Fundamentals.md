
What is GIT?
- Git is a version control system.

Think of it like a time machine for your code.
Why time machine?
- Assume, we have played a game [GTA Vice City], once we complete a mission, we would save the progress, so that the next time we play, we would continue from where we have stopped, rather than starting from the 1st mission.
- Similarly, we have written some code and have halted the progress in mid way, and then assume we have shifted our focus to some other thing.
	- Now, we need to save the progress -> this is where we create a checkpoint for our code
		- Its like i have done till x, and whenever i want to continue, i will continue from x
			- The point x would be referenced as checkpoint
				- The checkpoint in Git terminologies is called as "commit"
	- Example - Hey, today i wrote down this code and i want to commit this progress. So that from tomorrow i will continue from this checkpoint/commit and i can create a new commit at the end of tomorrow to track tomorrow's progress
- Assume on the 1st day you have done some changes in the code
- On the 2nd day, you have made few more changes
- But on the 3rd day, you think the changes you made on 2nd day is not valid
- In this case, we can go back to the commit/changes of the 1st day, the 2nd day commits would be nullified, so this could be done if we have commits on the progress of the code completion.
	- This is the reason, we can refer git and commit to time machine.
-
Git was a revolution during 2005's since it was open source and Git actually solved a lot of problems
Git is a software used to time travel with the code development.
There are so many managed services that's been built on GIT, but under the hood, it is still GIT
Once we understand GIT, we can easily understand GitHub, Azure DevOps and all other managed services. but the root is git, we need to understand GIT 


----

**GIT**
GIT is the software/version control system/ a framework
With GIT
- We can track changes made to our code
- We can go back in time to see older versions
- We can work in team without messing up each other's work.
	- Team members will be working in an isolated environment

**GITHUB**
GITHUB is a managed platform to host your git repositories online
- Its a platform which host our git folders online
	- Lets say we have a project and we want to host it somewhere[cloud] where other could also contribute to it.
		- We can make the repo public/private depending on our use case, but for example if its public[open to all], other developers also could contribute to the project.
			- If its public - anyone/everyone can access it.
			- If its private - only authorized people can access it.
	- That's how people/teams collaborate in the organization

---

Git is the tool, we use on our local computer
GitHub is where we store and share the git projects on the cloud
We can collaborate with others, review code, track issues, etc.
Git and GitHub go hand in hand, if we understand the concepts with git, then GitHub is easy to follow

----

**Repository**
- People usually call it as "Repo"
- A Repository(repo) is just a project folder tracked by Git.
	- We can call it as a Root folder/Parent folder - In which we will be storing all out artifacts/code/pdf files/text files/markdown files etc.
- What does the Repository contain?
	- It contains our code, documents and history of all our changes
- Where can it be stored?
	- It can be stored locally [on our machine] or remotely [on GitHub] 


---

