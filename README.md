## Git (and ROS Workspace) Cheat Sheat

## Cloning Repositories
- Option 1: git clone url --recursive
- Option 2:
  1.	git clone url
  2.	git submodule init
  3.	git submodule update

## Initializing ROS Workspace
1.	git clone "https://gitlab.com/name/repository_name_ws.git"
2.	cd  repository_name_ws/
3.	mkdir src/
4.	catkin_make 
5.	Copy .gitignore from another repository

## Adding Submodules
1.	cd src/
2.	git submodule add  https://gitlab.com/name/sub-repository.git

## Setting Up Submodules to Track Specific Branch
1.	git config -f .gitmodules submodule.<path>.branch <branch>

## Adding, Committing, and Pushing Changes

### Individual Submodule
1.	cd src/sub-repository/
2.	git  add [.][file1 fille2 ...]
3.	git commit –m “[message]”
4.	git push 

### All Submodules
1.	git submodule foreach 'git add [.][file1 fille2 ...] '
2.	git submodule foreach 'git commit -m "[message]"'
3.	git submodule foreach 'git push'

### Super Repository
1.	git add [.][file1 fille2 ...]
2.	git commit -m "[message]"
3.	git push 

### Super Repository and All Submodules
1.	git submodule foreach 'git add [.][file1 fille2 ...] ‘
2.	git submodule foreach 'git commit -m "[message]"'
3.	git add [.][file1 fille2 ...]
4.	git commit -m "[message]"
5.	git push --recurse-submodules=on-demand

## Pulling Changes

### Individual Submodule
1.	cd src/sub-repository/
2.	git pull

### All Submodules
1.	git submodule update --remote --merge

### Super Repository
1.	git pull 

## Switching Branches

### Individual Submodule
1.	cd src/sub-repository/
2.	git checkout [-b] branch_name

### All Submodules
1.	git submodule foreach ‘git checkout [-b] branch_name’

### Super Repository
1.	git checkout [-b] branch_name
2.	git submodule foreach -q --recursive 'git checkout $(git config -f $toplevel/.gitmodules submodule.$name.branch)' 

## Removing Submodules
1. Delete submodule section in .gitmodules
2. git add .gitmodules; git commit -m "removed submodule from .gitmodules"
3. Delete submodule section in .git/config
4. git rm --cached path_to_submodule
5. rm -rf .git/modules/path_to_submodule
6. git commit -m "removed submodule"
7. rm -rf path_to_submodule

## Creating Custom Git Commands
1.	Create a new file called git-{command-name}
2.	Add #!/bin/bash as the first line of git-{command-name}
3.	Add custom command to git-{command-name}
4.	sudo chmod +x git-{command-name}
5.	Move git-{command-name} to ~/bin
6.	Add PATH=$PATH:$HOME/bin to ~/.bashrc
7.	Now you can type git {command-name} to run this command

## Notes
- When changing branches in super repository, all submodules must be set up to track a specific branch for the second command to work. If submodules are not set up to track specific branches, submodules will end up in detached HEAD state (bad)
- The –b option creates a new branch
- Caching credentials (avoids re-entering credentials for each submodule): git config --global credential.helper cache
