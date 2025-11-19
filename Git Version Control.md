
# Git Commands

### `init`
Initialize a new Git repository
```
git init
```
### clone
```
git clone <repository_url>
```
### status
tell  about
- modified files (files that are changed but not staged).
- untracked files (files that Git is not tracking).
- staged files (files that are staged and ready to be committed).
```
git status 
```

### add
add changes to the staging area
the repository should update these changes once the user runs the commit .
```
git add .
```

**Unstage** a single file or files after running `git add`
```
git reset HEAD index.html
git reset HEAD index.html
`git rm --cached <file>`
```

### commit
Save the changes you have made (or staged) to the local repository.
This allows you to roll back to a previous commit .
Git creates a snapshot of your repository.
```
git commit -m "commit message"
```

```
git remote add origin file:///c/git-server/myproject.git
```
```
git branch -M main
```
```
git push -u origin main
```

### remote add
creates a connection between  local Git repository and the remote Git repository
enabling to push and pull changes between them
"origin" by default is a nickname for the remote repository
```
git remote add origin file:///c/git-server/myproject.git
git remote add origin https://github.com/alireza0/trojan-english.git
```

### push

the remote repository will reflect all the changes you committed locally
`<remote_repo>`: alias to the remote repository (“origin” by default)
--all: pushes all your local branches to the remote repository
--force: overwrites the `main` branch on the remote repository

```
git push <remote_repo> <branch>
git push ---all origin
git push --force origin main
```

### pull
fetches and merges the changes in the remote repository with those in the local repository
combines two commands: `git fetch` and `git merge`
```
git pull origin feature-branch
```

### branch

List of all branches in the repository
```
git branch
```

Create a new branch
```
git branch <branch_name>
```

Delete the branch
```
git branch -d <branch_name>
```

### checkout

Go back to a previous commit
```
git checkout <commit-hash>
```

Go back 2 commits
```
git checkout HEAD~2
```

The following command creates a new branch named `“feature_branch”` and **switches** to it
```
git checkout -b feature_branch
```

Discard the changes you’ve made to a file and **restore** it to its previous version
```
git checkout -- <file-name>
git checkout <branch-name> -- <file-name>
```

### log

Displays the entire commit history of your current branch
```
git log
```

```
git log --oneline
```

### show
inspect the changes and message of a specific commit
```
git show <commit-hash>
```


### Other Git Commands
https://www.datacamp.com/blog/git-commands


### Git Online Course

address: https://campus.datacamp.com/courses/introduction-to-git

email: `xasihel148@gusronk.com`

pass: `xasihel148@gusronk.com--P@ssword`

### Ultimate Git Commands
```
git add README.md
git commit -m "first commit"
git branch -M main

git remote add origin https://github.com/Yashar-Nasiri/automate-pentest.git
git remote add origin file:///D:/git-server/automate-pentest.git
git push -u origin main
```
