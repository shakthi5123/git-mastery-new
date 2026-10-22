Git installation

Git configuration
git config --global user.name "name"
git config --global user.email "email@gmail.com"

<!-- to check congiured username & email -->
git config --global user.name 
git config --global user.email

Stages:
U - Untracted  
A - Added or Staged
C - Commited 


To see all the commit use - git log --oneline 

managing your own projects 
making a checkpoint/snapshot or saved point 
   adding them 
   stagging them (git know the file exits but dont actually track them)
   commiting them (git tracks it)

To see all the commit use - git log --oneline (along with the latest commit you have done)

going back to previous saved point 
HEAD -> main this shows the latest last commit you have done so if you want to go back and undo the commit along with the changes before commit 

git reset --hard HEAD~1 (goes 1 step back)


To know what files are in what stages in other works know the stages of the files 
git status (gives extra info)
git status -s (to the point very precise)
Imp thing to note git status only works when it not yet commited or commited but did some changes then git status works 

so still if you want to see the commit history even after the commit we use 
git log 


Branching 
suppose we are working in a company eg cognizant over here 21 developers are there the task is to build the abc.com website 
the main branch has the code the source of truth which is working perfectly now shakthi have to build the feature navbar what he do is so first he copies the code from the main branch the do build the navbar feature if everything is working he merge it with the main branch this is called branching now aakanksha has to work on a feat/footer what she will do is take the copy of the shakthi merged commit from the main then work on it 

Merge conflict 
usually happens when branched code file of the 2 developer did the change on the same line git shows the conflict now git shows 3 options one is use the first change or second change or use both the changes 

Merging technique - ff(fast forward) merge, three way merge, squash merger , recursive strategy merge, rebase and merge 
mainly learn the first 2 

delete branch - after the merge to the main and switch to main then do - git branch -d feat/navbar

Stashing 


git diff & git diff --staged
Notice the difference: git diff shows unstaged changes, while git diff --staged shows changes staged for the next commit.


git restore README.md
What you learned: git restore <file> discards unstaged changes to that file, restoring its contents from the index (staging area).

git restore --staged <file>
What you learned: git restore --staged <file> removes the file from the staging area but preserves the file in your working directory.

git revert : Undo your latest commit
git revert HEAD

git reset --soft HEAD~1 — Local commit correction if you commited the file but then you dont want to commit it then use this command to put back the commit to the stagging area 

git reset --soft HEAD~1 - Undo the latest commit; keep changes staged
git reset --mixed HEAD~1 - Undo the latest commit; keep changes unstaged
git reset --hard HEAD~1 - Undo the latest commit and discard associated tracked changes

git remote -v - to check if the repo is in github or not 

If Your GitHub repository now contains a commit that your local repository hasn’t downloaded. 
git fetch origin
git pull

Remember the difference
git fetch - Downloads remote information without merging it into your current branch
git pull - Fetches remote changes and integrates them into your current branch
git push - Uploads your local commits to a remote repository
git clone - Creates a local copy of an existing remote repository

To delete the branch after merged to the main branch use - git branch -d feature/profile

Merge conflict issues 

Git stash - Temporarily Save Changes
Developers sometimes need to switch branches before their current work is ready to commit.

git stash list - to list all the stash 
* git stash temporarily shelves changes.
* git stash list lists saved stashes.
* git stash apply restores a stash but keeps it in the stash list.
* git stash pop restores a stash and normally removes it from the stash list after a successful application.


cherry-pick - Copy a Commit with git cherry-pick
Sometimes you create a useful commit on one branch and need that specific commit on another branch.

Rebase — Rewrite Branch History
Rebase helps you move a feature branch’s commits onto a newer base commit.

