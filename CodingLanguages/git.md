# Git and Github

### Git Commands

- clone - Brings a repository that is hosted somewhere like github into a folder on your local machine
  - Ex. git clone (https link)
- status - shows all files that were updated or created or deleted but haven't been saved
  -  Ex. git status
- add - Track your files and changes in Git
  - Ex. git add README.md
  - Can also do **git add .** to do all files
- commit - Save your files in Git
  - Ex. git commit -m "Commit message" -m "Description box message"
  - Can also do **git commit -am "Commit message"** if the files you're adding are just modified and not newly added
- push - Upload Git commits to a remote repo, like Github
  - Ex. git push origin master
  - Can do **git push -u origin master** so you can just do **git push** for every push after
- pull - Download changes from remote repo to your local machine, the opposite of push
  - Ex. git pull
- init - Initializes a new git repository if created locally
  -  Ex. git init
  -  Then to connect it to repository, do **git remote add origin (https link)**
- reset - Allows you to unstage changes
  - Ex. **git reset** or **git reset filename**
  - Can also do **git reset HEAD~(number of commits you want to go back)**
    -  Ex. git reset HEAD~1
- log - Used to see all commits
  - Ex. git log
 
### Branching

- branch - allows you to see your current branches
  -  Ex. git branch
  -  Can rename a branch with **git branch -m newBranchName**
- checkout - allows you to create a new branch
  - Ex. **git checkout -b branchName** (the -b is for creating a new branch)
  - **git checkout branchName** for switching to different branch
- diff - Allows you to see the difference in changes between branches
  - Ex. **git diff branchName**
- merge - Merges two branches
  - Should be in current branch you want to merge into then **git merge branchName**
- Can delete using **git branch -d branchName**   
