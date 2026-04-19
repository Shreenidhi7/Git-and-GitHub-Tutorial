
Now, we have created out GitHub account [username and email-id]
1. First thing which we need to do is to configure our GitHub username and email id
	1. PS D:\Git and GitHub\Git_Practical_Tutorial> git config --global user.email "shreenidhisharma7@gmail.com"
	2. PS D:\Git and GitHub\Git_Practical_Tutorial> git config --global user.name "Shreenidhi7"
2. While providing the username and email, if we provide the different username and email, it git config will simply override it.
3. Once we have configure, what would be the next thing we need to do?
	1. We want to host our local repository to the remote repository
		1. Local Repository - System's Working Directory
		2. Remote Repository - GitHub
4. We need to go to GitHub and create a new repository
	1. Repository Name  -  Git-and-GitHub-Tutorial
	2. We can make it Public Repository
	3. We can click on the checkbox and Add a README File
	4. By default "main" will be set as the default branch
		1. It just a new name for "master"
5. Now, our target is to push our local repository to the remote one which was just created in GitHub
6. We need go to code/click on code button and go to HTTPS
	1. Basically we have 2 very popular one [HTTPS,SSH]
	2. It good to use HTTPS method [Recommended]
7. Even before cloning the remote repository, we need have something called as **personal access token** in order to get started.
8. How do we get that token?
	1. Click on the Profile
	2. Click on Settings
	3. Click on Developer Settings
	4. Click on Personal Access Tokens [Its also called as PAT]
		1. Click on Token (Classic)
		2. Generate New Token
			1. Generate New Token (Classic)
	5. Once the token is generated, please copy and store it in a secure place [ It won't be visible again ]
9. Now, go back to the created repository and click on Code and select HTTPS and grab the URL
10. In order to push anything to the remote repository
	1. We use a command called git push
11. Even before using git push we should have something called as REMOTE ORIGIN
	1. How do we check if we have a remote origin or not?
		1. git remote -v
		2. If there is no response, then that means we don't have a remote origin
12. So we should be adding a remote url or a remote origin
	1. What is Origin?
		1. Origin is a kind of destination where we want to push our code
	2. To add the origin, we need to follow below command
		1. git remote add origin "https://github.com/Shreenidhi7/Git-and-GitHub-Tutorial.git"
	3. Once the origin is added, if we perform
		1. git remote -v
		2. This shows the origin.

```
PS D:\Git and GitHub> git init
Initialized empty Git repository in D:/Git and GitHub/.git/
PS D:\Git and GitHub\Git_Practical_Tutorial> git remote add origin "https://github.com/Shreenidhi7/Git-and-GitHub-Tutorial.git"          
PS D:\Git and GitHub\Git_Practical_Tutorial> git remote -v
origin  https://github.com/Shreenidhi7/Git-and-GitHub-Tutorial.git (fetch)
origin  https://github.com/Shreenidhi7/Git-and-GitHub-Tutorial.git (push)
PS D:\Git and GitHub\Git_Practical_Tutorial
```

13. Now, we can push this code
14. But obviously, when ever we want to push our local repository/working directory to remote repository/git and if the repo is new, we would push everything which we have added in local.
15. Gets go to the master branch and then try to push the code to remote repo
	1. In local we have the base branch name as "master"
	2. But in github, its called "main"
	3. One important thing -> the base branch should be same in local as well as remote
		1. Both should have "main" as with latest terminologies
	4. Since our local has the name "master"
		1. We need to rename our branch
		2. In order to do that, we have to switch to master
			1. git switch master
			2. git branch -m main
```
PS D:\Git and GitHub\Git_Practical_Tutorial> git switch master
Already on 'master'
PS D:\Git and GitHub\Git_Practical_Tutorial> git branch -m "main"
PS D:\Git and GitHub\Git_Practical_Tutorial> git branch
  bugfix
  bugfix2
  cherry_pick
  dev1_stash
  feature_nidh_1
  feature_shrn_1
* main
  rebase_feat
  rebase_feat_2
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

16. Now, if just provide the command to push my code like below, we shall get an error
	1. git push main
		1. fatal: 'main' does not appear to be a git repository
		2. fatal: Could not read from remote repository.
		3. Please make sure you have the correct access rights and the repository exists
	2. This is because, we have tell exactly where we need to push
17. If we google it, there it shows the command
	1. git push remote branch 
		1. git push origin main
	2. We already know what is our origin
		1. git remote -v
			1. origin  https://github.com/Shreenidhi7/Git-and-GitHub-Tutorial.git (fetch)
			2. origin  https://github.com/Shreenidhi7/Git-and-GitHub-Tutorial.git (push)
	3. Once we provide the command
		1. git push origin main
	4. GitHub will ask us to login to Github account
		1. What we think now is that we can grab the URL of any gitHub profile and simply push the code?
			1. Yes, it is doable and possible only if we have personal access token [PAT]
		2. The thing is we can read any repository easily, that's not a problem with public repository
			1. With the private repository, we need token for that as well
		3. Now we are pushing our code to the repository, if we are owner of the repository, then we have prove it, so we need to either sign it with browser or just provide the access token
	5. Personal Access Tokens are always good
![[Pasted image 20260419154131.png]]

18. Immediately after providing the PAT, we see there are some issues that have occurred.
	1. This is expected, because in the GitHub repository, we have some initial commit -> Readme.md file added through GitHub
	2. This initial commit isn't available in my local repo
```
PS D:\Git and GitHub\Git_Practical_Tutorial> git push origin main
To https://github.com/Shreenidhi7/Git-and-GitHub-Tutorial.git
 ! [rejected]        main -> main (fetch first)
error: failed to push some refs to 'https://github.com/Shreenidhi7/Git-and-GitHub-Tutorial.git'
hint: Updates were rejected because the remote contains work that you do not
hint: have locally. This is usually caused by another repository pushing to
hint: the same ref. If you want to integrate the remote changes, use
hint: 'git pull' before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

19. Best practice is that, we should always run fetch + merge command
	1. In modern days, we can just use git pull origin main
```
PS D:\Git and GitHub\Git_Practical_Tutorial> git pull origin main
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
Unpacking objects: 100% (3/3), 883 bytes | 147.00 KiB/s, done.
From https://github.com/Shreenidhi7/Git-and-GitHub-Tutorial
 * branch            main       -> FETCH_HEAD
 * [new branch]      main       -> origin/main
fatal: refusing to merge unrelated histories
PS D:\Git and GitHub\Git_Practical_Tutorial>
```

20. Now, if just try to run git branch.
	1. git branch
21. If we try to say git push origin main  - it will again fail, saying tip of current branch is behind
```
PS D:\Git and GitHub\Git_Practical_Tutorial> git branch 
  bugfix
  bugfix2
  cherry_pick
  dev1_stash
  feature_nidh_1
  feature_shrn_1
* main
  rebase_feat
  rebase_feat_2
PS D:\Git and GitHub\Git_Practical_Tutorial> git push origin main  
To https://github.com/Shreenidhi7/Git-and-GitHub-Tutorial.git
 ! [rejected]        main -> main (non-fast-forward)
error: failed to push some refs to 'https://github.com/Shreenidhi7/Git-and-GitHub-Tutorial.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. If you want to integrate the remote changes,
hint: use 'git pull' before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
PS D:\Git and GitHub\Git_Practical_Tutorial
```

22. if we do git pull origin main
	1. There is a fatal -> refusing to merge unrelated histories
	2. The problem here is we have created a local repo from scratch [Ideally we do not do that]
		1. We first create the remote repo and then clone it and do other stuffs/
	3. Now, we are just trying to pull
		1. What pull does it, it will simply merge the main branch to your main branch
	4. The issue here is that the github has a different git and our local has different git.
		1. The has a different commit [readme.md] and our local repo has a different commit [readme.md]
		2. In order to merge it, we need to give some commands
		3. git pull origin main --allow-unrelated-histories
			1. With this we need to give some message [the editor will automatically pop-up]
	5. Now, we do git push origin main
		1. It should be done, and if we go to the github, we should be able to see all our commits and changes

```
PS D:\Git and GitHub\Git_Practical_Tutorial> git push origin main  
To https://github.com/Shreenidhi7/Git-and-GitHub-Tutorial.git
 ! [rejected]        main -> main (non-fast-forward)
error: failed to push some refs to 'https://github.com/Shreenidhi7/Git-and-GitHub-Tutorial.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. If you want to integrate the remote changes,
hint: use 'git pull' before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
PS D:\Git and GitHub\Git_Practical_Tutorial> git pull origin main --allow-unrelated-histories
From https://github.com/Shreenidhi7/Git-and-GitHub-Tutorial
 * branch            main       -> FETCH_HEAD
Merge made by the 'ort' strategy.
 README.md | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 README.md
PS D:\Git and GitHub\Git_Practical_Tutorial> git pull origin main --allow-unrelated-histories
From https://github.com/Shreenidhi7/Git-and-GitHub-Tutorial
 * branch            main       -> FETCH_HEAD
Already up to date.
PS D:\Git and GitHub\Git_Practical_Tutorial> git push origin main                            
Enumerating objects: 72, done.
Counting objects: 100% (72/72), done.
Delta compression using up to 16 threads
Compressing objects: 100% (62/62), done.
Writing objects: 100% (71/71), 6.29 KiB | 378.00 KiB/s, done.
Total 71 (delta 34), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (34/34), done.
To https://github.com/Shreenidhi7/Git-and-GitHub-Tutorial.git
   ec85a7f..3460b2c  main -> main
PS D:\Git and GitHub\Git_Practical_Tutorial> 
```

23. We can see only main branch is there, why because we just pushed only the main branch.
This happens only when we try to push a local repo which doesn't even exist on the GitHub

Summary
1. We created our repo locally
2. We created a repo on the GitHub
3. We wanted to push our local repo to the remote repo
4. We actually set up the origin because we needed a destination
5. We provided PAT[Personal Access Token] (Proving we are the owner)
6. When we ran git push origin main command, we are saying this is our changes in local in main branch, push it to remote repo
	1. It was saying, remote repo has some changes{readme.md}, did we merge it in local branch?
		1. This can be resolved by git pull origin main
		2. It will ask for the message 
7. Then we shall push the code
8. Then our repo is hosted in GitHub

This is the tutorial for taking our GitHub repo from scratch.

---
