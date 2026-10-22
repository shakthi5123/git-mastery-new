Git & GitHub — Complete Cheat Sheet

A beginner-friendly, practical guide to Git and GitHub, from the basics to advanced workflows.

Goal: Understand what each command does, when to use it, and how to practice it.

⸻

Table of Contents

1. Git & GitHub Basics
2. Initial Setup
3. Create a Repository
4. Track Changes and Commit
5. Git Status and Diff
6. Git Log and History
7. Branches
8. Merge Branches
9. Resolve Merge Conflicts
10. GitHub Remote Operations
11. Clone and Fork
12. Pull Requests
13. Undo Changes
14. Git Reset vs Revert
15. Git Stash
16. Git Cherry-Pick
17. Git Rebase
18. Amend and Interactive Rebase
19. Git Reflog and Recovery
20. Git Tags and Releases
21. .gitignore
22. GitHub Issues and Actions
23. Daily Developer Workflow
24. Common Errors and Solutions
25. Essential Commands Reference
26. Practice Projects

⸻

1. Git & GitHub Basics

What is Git?

Git is a version control system that tracks changes in your code.

It allows you to:

* Save snapshots of your project.
* Track who changed what.
* Create branches for new features.
* Undo mistakes.
* Compare different versions of your code.

Example: You modify your React application and accidentally break it. Git helps you inspect the changes and recover an earlier version.

What is GitHub?

GitHub is an online platform for hosting Git repositories.

It allows you to:

* Store code online.
* Collaborate with developers.
* Review code using pull requests.
* Report bugs using issues.
* Automate tasks using GitHub Actions.

Remember:

* Git = version control on your computer and elsewhere.
* GitHub = online platform for hosting and collaborating on Git repositories.

Important Git terminology

Term	Meaning
Repository	A project tracked by Git
Working directory	Where you edit files
Staging area	Where you prepare changes for a commit
Commit	A saved snapshot in Git history
Branch	An independent line of development
Merge	Combines changes from branches
Remote	A reference to another repository
Clone	Copies a remote repository locally
Push	Uploads commits to a remote
Pull	Fetches and integrates remote changes
Fetch	Downloads remote information without integrating it into your current branch
Pull request	A request to review and merge changes on GitHub
HEAD	Usually identifies the commit currently checked out

How Git works

Git has three main areas:

1. Working directory
2. Staging area
3. Repository history

The basic workflow is:

Create or edit files
        |
        v
   git add
        |
        v
  Staging area
        |
        v
  git commit
        |
        v
 Repository history
        |
        v
   git push
        |
        v
 GitHub repository

⸻

2. Initial Setup

Install Git if necessary.

Check whether Git is installed:

git --version

On macOS, you can install Apple’s command-line developer tools by running:

xcode-select --install

If Git is already installed, you don’t need to reinstall it.

Configure your username

git config --global user.name "Your Name"

Configure your email

git config --global user.email "you@example.com"

Use the email associated with your GitHub account if you want your commits linked to that account.

You can also use a GitHub-provided private email address.

Check your configuration

git config --global user.name
git config --global user.email

View all global settings:

git config --global --list

View repository-specific settings:

git config --local --list

Remember: --global applies to your user account. --local applies to the current repository.

⸻

3. Create a Repository

A Git repository tracks the history of a project.

Method 1: Create a new local repository

mkdir git-practice
cd git-practice
git init

What happens?

* mkdir creates a folder.
* cd enters the folder.
* git init initializes Git in that folder.

Check the status:

git status

Create your first file

echo "Learning Git" > README.md

Check the status:

git status

Git will report that README.md is untracked.

Method 2: Clone an existing repository

git clone https://github.com/USERNAME/REPOSITORY.git

Enter the cloned directory:

cd REPOSITORY

Cloning downloads a repository and its available history into a local directory and normally configures its original remote as origin.

Use git init for a new local project. Use git clone for an existing repository.

⸻

4. Track Changes and Commit

A commit saves staged changes into Git history.

Step 1: Create a file

echo "My first project" > README.md

Step 2: Stage the file

git add README.md

Step 3: Commit the file

git commit -m "Add README"

Stage all changes

git add .

This stages additions, modifications, and deletions under the current directory, subject to Git’s ignore rules.

For a clearer view of everything Git considers changed, use:

git status

Commit staged changes

git commit -m "Describe the changes"

Good commit messages

git commit -m "Add login page"
git commit -m "Fix navbar alignment"
git commit -m "Update user authentication"
git commit -m "Remove unused components"

Write commit messages that explain what changed.

Important: git add . stages changes; it does not commit them.

⸻

5. Git Status and Diff

Check the status

git status

Shows:

* Untracked files.
* Modified files.
* Staged changes.
* The current branch.
* Whether the working tree is clean.

View unstaged changes

git diff

Shows changes in tracked files that have not been staged.

View staged changes

git diff --staged

Shows changes staged for the next commit.

The equivalent command is:

git diff --cached

Compare two branches

git diff main feature/login

Shows differences between the two branch tips.

Compare two commits

git diff COMMIT1 COMMIT2

Replace the placeholders with actual commit hashes.

Practical example

Modify a file:

echo "New line" >> README.md

Inspect the change:

git diff

Stage it:

git add README.md

Inspect the staged change:

git diff --staged

Commit it:

git commit -m "Update README"

⸻

6. Git Log and History

Git stores commits in a history.

View commit history

git log

Compact history

git log --oneline

Example:

a81f302 Add login page
b42d118 Update README
c93e721 Initial commit

View history as a graph

git log --oneline --graph --all

This is especially useful when working with branches and merges.

Show the latest commit

git log -1

Inspect a specific commit

git show COMMIT_HASH

Shows the commit details and its changes.

View the last three commits

git log -3 --oneline

View who changed each line

git blame README.md

Useful when investigating changes in an existing file.

⸻

7. Branches

A branch is an independent line of development.

Developers use branches to build features without immediately changing the main branch.

List branches

git branch

The * identifies the current branch.

Create a branch

git branch feature/login

This creates a branch but does not switch to it.

Switch branches

git switch feature/login

Create and switch in one command

git switch -c feature/signup

This is a commonly used command.

Rename the current branch

git branch -m feature/new-name

Delete a merged local branch

git branch -d feature/login

Force-delete a local branch

git branch -D feature/login

Use -D carefully. It can delete a branch even when Git warns that its changes have not been merged.

Practical example

Create a feature branch:

git switch -c feature/profile

Create a file:

echo 'console.log("Profile page");' > profile.js

Commit it:

git add profile.js
git commit -m "Add profile page"

Return to the main branch:

git switch main

The committed profile.js file will not appear on main unless that branch already contains it.

⸻

8. Merge Branches

Merging integrates changes from another branch into your current branch.

Example

Create a feature branch:

git switch -c feature/contact

Create and commit a file:

echo "Contact page" > contact.txt
git add contact.txt
git commit -m "Add contact page"

Switch to the destination branch:

git switch main

Merge the feature:

git merge feature/contact

The changes are now integrated into main.

Two common merge outcomes

Fast-forward merge: Git moves the destination branch forward because it has no new diverging commits to combine.

Three-way merge: Git combines the histories using their common ancestor and the two branch tips. This may create a merge commit.

Abort a merge

If a merge has conflicts and you want to abandon the merge attempt:

git merge --abort

This attempts to restore the pre-merge state. Save any unrelated work before starting a merge.

⸻

9. Resolve Merge Conflicts

A merge conflict happens when Git cannot automatically combine changes.

This commonly happens when two branches modify the same lines differently.

Example

Suppose main contains:

App title: My Application

Branch A changes it to:

App title: Shopping Application

Branch B changes it to:

App title: Admin Dashboard

When Git tries to merge both changes, it may report a conflict.

Step 1: Inspect the conflict

git status

Step 2: Open the conflicting file

Git may show:

<<<<<<< HEAD
App title: Shopping Application
=======
App title: Admin Dashboard
>>>>>>> feature/admin

Meaning:

* <<<<<<< HEAD: the current branch’s version.
* =======: separates the conflicting versions.
* >>>>>>> feature/admin: the incoming version.

Step 3: Resolve it

Choose the correct content or combine both versions.

For example:

App title: Shopping Application Admin

Remove the conflict markers.

Step 4: Stage the resolved file

git add config.txt

Step 5: Complete the merge

git commit -m "Resolve configuration conflict"

Check:

git status

Remember: Resolve the actual code conflict before staging the file. Git cannot decide which business logic is correct for you.

⸻

10. GitHub Remote Operations

A remote is a reference to another Git repository.

The conventional remote name is origin.

View configured remotes

git remote -v

Add a remote

git remote add origin https://github.com/USERNAME/REPOSITORY.git

Replace the URL with your actual repository URL.

Change the remote URL

git remote set-url origin https://github.com/USERNAME/REPOSITORY.git

Remove a remote

git remote remove origin

This removes the local remote configuration. It does not delete the GitHub repository.

Push a branch for the first time

git push -u origin main

Meaning:

* push: upload commits.
* origin: destination remote.
* main: branch to push.
* -u: configure the upstream relationship.

After the upstream is configured, you can usually run:

git push

Fetch remote changes

git fetch origin

Fetch downloads remote information without integrating those changes into your current branch.

Pull remote changes

git pull

Pull fetches changes and integrates them into the current branch.

A useful explicit command is:

git pull --ff-only origin main

This only advances the current branch when the update can be performed as a fast-forward. It fails rather than creating a merge commit or rewriting history if the branches have diverged.

View local and remote-tracking branches

git branch -a

Example:

* main
  feature/login
  remotes/origin/main

Delete a remote branch

git push origin --delete feature/login

This deletes the branch on the remote repository, not the local branch.

⸻

11. Clone and Fork

Clone

Cloning downloads an existing Git repository.

git clone https://github.com/USERNAME/REPOSITORY.git

Use this when you want a local copy of a project.

Fork

A fork is a GitHub-hosted copy of another repository under your GitHub account.

Typical workflow:

1. Open the original repository on GitHub.
2. Click Fork.
3. Clone your fork.
4. Create a feature branch.
5. Commit and push your changes.
6. Open a pull request.

Configure the original repository as upstream

After cloning your fork, add the original repository:

git remote add upstream https://github.com/ORIGINAL_OWNER/REPOSITORY.git

Inspect the remotes:

git remote -v

You should see:

* origin: your fork.
* upstream: the original repository.

Fetch updates from the original repository

git fetch upstream

Update your local main if it is safe to fast-forward:

git switch main
git merge --ff-only upstream/main

Update your fork on GitHub:

git push origin main

Remember: A fork is hosted on GitHub. A clone is a local copy on your computer.

⸻

12. Pull Requests

A pull request (PR) asks others to review and merge your changes into a target branch.

Typical workflow

Create a feature branch:

git switch -c feature/login

Make changes and commit:

git add .
git commit -m "Add login feature"

Push the branch:

git push -u origin feature/login

Then, on GitHub:

1. Open the repository.
2. Select Compare & pull request, or create a pull request manually.
3. Choose the base branch, such as main.
4. Choose the feature branch as the compare branch.
5. Describe the changes.
6. Create the pull request.
7. Review feedback and make any requested changes.
8. Merge when approved.

After merging, synchronize your local repository:

git switch main
git pull --ff-only origin main

Delete the local feature branch if you no longer need it:

git branch -d feature/login

Why use pull requests?

* Code review.
* Team collaboration.
* Automated testing.
* Discussion about changes.
* Safer integration into the main branch.

Important: Git commands manage Git history. Pull requests are a GitHub collaboration feature.

⸻

13. Undo Changes

Different commands undo different kinds of changes.

A. Discard unstaged changes

Suppose you modify README.md but have not staged it.

git restore README.md

This restores the file from the staging area.

Warning: Uncommitted changes discarded this way may be unrecoverable.

B. Unstage a file

git restore --staged README.md

This removes the file’s changes from the staging area but keeps the changes in the working directory.

C. Restore a file from a commit

git restore --source=HEAD~1 -- README.md

This restores the file’s contents from the previous commit into your working directory. It does not automatically commit the restoration.

Inspect and commit the change if you want to keep it.

D. Rename a file

git mv old-name.txt new-name.txt

Stage and commit the change if necessary:

git commit -m "Rename file"

E. Delete a tracked file

git rm old-file.txt
git commit -m "Remove old file"

git rm removes the file from the working tree and stages its deletion.

⸻

14. Git Reset vs Revert

These commands are important when correcting mistakes.

A. Git reset

git reset moves the current branch to another commit.

It can also change the staging area and working directory, depending on the mode.

Soft reset

git reset --soft HEAD~1

Removes the latest commit from the current branch’s history while keeping its changes staged.

Mixed reset

git reset --mixed HEAD~1

Removes the latest commit from the current branch’s history and leaves its changes unstaged in the working directory.

--mixed is the default reset mode.

Hard reset

git reset --hard HEAD~1

Moves the current branch backward and resets the index and working tree to match.

Warning: This can destroy uncommitted changes and make the removed commit’s changes difficult to recover. Use it only when you understand what will be discarded.

B. Git revert

git revert HEAD

Creates a new commit that reverses the changes introduced by the latest commit.

Use a revert when you want to undo a commit while preserving existing history, especially on shared branches.

Reset vs Revert

Command	Main purpose
git reset --soft	Undo a commit but keep changes staged
git reset --mixed	Undo a commit but keep changes unstaged
git reset --hard	Reset the branch, index, and working tree
git revert	Create a new commit that reverses an earlier commit

Rule of thumb: Prefer git revert for published commits on shared branches. Use git reset when intentionally correcting local history.

⸻

15. Git Stash

git stash temporarily shelves changes so you can switch tasks without committing unfinished work.

Save changes

git stash push -m "WIP: unfinished login feature"

List saved stashes

git stash list

Restore the latest stash and remove it from the stash list

git stash pop

Restore a stash but keep it saved

git stash apply

Apply a specific stash

git stash apply stash@{1}

Delete a specific stash

git stash drop stash@{1}

Delete all stashes

git stash clear

Warning: git stash clear removes all saved stashes from the stash list.

Stash untracked files too

git stash push -u -m "Save unfinished work"

By default, ordinary stashing does not include untracked files.

Practical example

echo "Unfinished work" >> README.md
git stash push -m "Save README changes"
git status
git stash list
git stash pop

⸻

16. Git Cherry-Pick

git cherry-pick applies the changes introduced by a particular commit to your current branch.

Use it when you need a specific commit without merging the entire source branch.

Example

Create a branch:

git switch -c feature/notifications

Create and commit a file:

echo "Notification feature" > notification.txt
git add notification.txt
git commit -m "Add notifications"

Find the commit hash:

git log -1 --oneline

Switch to the destination branch:

git switch main

Apply the commit:

git cherry-pick COMMIT_HASH

Replace COMMIT_HASH with the actual hash.

Git creates a new commit on main containing the selected change.

Abort a cherry-pick

If the cherry-pick encounters conflicts and you want to cancel the operation:

git cherry-pick --abort

Remember: Cherry-picking copies a commit’s changes into the current branch’s history. It does not move the original commit.

⸻

17. Git Rebase

Rebase reapplies commits onto a new base commit.

It is commonly used to update feature branches and maintain a linear history.

Example

Create a feature branch:

git switch -c feature/search

Make a commit:

echo "Search feature" > search.txt
git add search.txt
git commit -m "Add search feature"

Suppose main receives new commits.

Update your local main first, if appropriate:

git switch main
git pull --ff-only origin main

Return to your feature branch:

git switch feature/search

Rebase:

git rebase main

Git reapplies the feature branch’s commits on top of main.

Inspect the history:

git log --oneline --graph --all

If a rebase has conflicts

1. Open the conflicting files.
2. Resolve the conflicts.
3. Stage the resolved files.
4. Continue the rebase.

git add .
git rebase --continue

To cancel the rebase:

git rebase --abort

Merge vs Rebase

Merge	Rebase
Combines branch histories	Reapplies commits onto another base
Can create a merge commit	Creates new commit IDs for the reapplied commits
Preserves existing commit ancestry	Rewrites the rebased portion of history

Important: Avoid rebasing commits that others rely on unless your team has agreed to that workflow.

⸻

18. Amend and Interactive Rebase

A. Amend the latest commit

Suppose you forgot to include a file in your last commit.

Stage the missing file:

git add missing-file.txt

Update the latest commit:

git commit --amend

Git opens an editor so you can edit the commit message.

To retain the existing message:

git commit --amend --no-edit

This creates a replacement for the latest commit.

Warning: Amend changes the commit ID. Avoid amending published commits that other people rely on.

B. Interactive rebase

Interactive rebase lets you edit, reorder, combine, or remove commits.

Inspect the last three commits:

git log --oneline -3

Start an interactive rebase:

git rebase -i HEAD~3

Git opens an editor with a list of commits.

Common actions:

Action	Meaning
pick	Keep the commit
reword	Change the commit message
edit	Stop to amend the commit
squash	Combine a commit with the previous commit and edit the resulting message
fixup	Combine a commit with the previous commit, discarding the fixup commit’s message
drop	Remove the commit from the rebased history

Save and close the editor to continue.

Important: Practice interactive rebase on a disposable local branch first. It rewrites history.

⸻

19. Git Reflog and Recovery

git reflog records recent movements of references such as HEAD and branch tips in your local repository.

It can help you recover from mistakes such as moving a branch backward with git reset.

View the reflog

git reflog

Example:

a12bc34 HEAD@{0}: reset: moving to HEAD~1
b56de78 HEAD@{1}: commit: Add login page

Suppose you accidentally reset a commit and want to recover it.

Inspect the reflog:

git reflog

Find the commit you want to recover.

Create a recovery branch:

git branch recovery/login COMMIT_HASH

Replace COMMIT_HASH with the appropriate hash from the reflog.

Inspect the recovered history:

git log --oneline recovery/login

Remember: Reflog is local. It is not a replacement for remote backups, and old entries may eventually expire.

⸻

20. Git Tags and Releases

Tags identify specific points in history, often corresponding to software versions.

Create a lightweight tag

git tag v1.0.0

Create an annotated tag

git tag -a v1.0.0 -m "Version 1.0.0"

Annotated tags store additional information, including a message and tagger details.

List tags

git tag

Inspect a tag

git show v1.0.0

Push one tag

git push origin v1.0.0

Push all tags

git push origin --tags

Delete a local tag

git tag -d v1.0.0

Delete a remote tag

git push origin --delete v1.0.0

GitHub Releases

On GitHub, you can create a release associated with a tag.

Releases are useful for publishing version notes, downloadable assets, and information about a specific version of your software.

⸻

21. .gitignore

.gitignore tells Git which untracked files it should ignore.

It is commonly used for dependencies, build output, environment files, and local configuration.

Example .gitignore

For a Node.js project:

node_modules/
.env
.env.local
dist/
build/
.DS_Store

Create the file:

touch .gitignore

Add the patterns above, save the file, then check:

git status

Important rule

.gitignore does not automatically stop tracking files that are already tracked.

If .env is already tracked, remove it from Git’s index:

git rm --cached .env

Then commit the change:

git add .gitignore
git commit -m "Ignore environment files"

This leaves the local .env file in place but removes it from the repository in the new commit.

Security warning: If a secret has already been pushed to GitHub, removing it in a later commit does not erase it from earlier history. Revoke or rotate the exposed secret immediately.

⸻

22. GitHub Issues and Actions

GitHub Issues

Issues help teams track bugs, features, and tasks.

Example issue:

Title: Fix login validation

Description:

* Validate the email field.
* Show an error for invalid input.
* Test the login form.

A typical workflow is:

1. Create an issue.
2. Create a branch to address it.
3. Commit the changes.
4. Open a pull request.
5. Link the pull request to the issue.
6. Merge the pull request and close the issue.

GitHub Actions

GitHub Actions automates workflows such as testing, linting, building, and deployment.

For example, a workflow can run tests whenever someone opens or updates a pull request.

Create this file in your repository:

.github/workflows/ci.yml

name: Basic CI
on:
  push:
    branches: [main]
  pull_request:
    branches: [main]
jobs:
  check:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4
      - name: Confirm workflow runs
        run: echo "GitHub Actions is working!"

Commit and push the file.

git add .github/workflows/ci.yml
git commit -m "Add basic CI workflow"
git push

Open the Actions tab on GitHub to inspect the run.

This is a minimal demonstration. Real projects should use appropriate test and build steps, and production workflows should follow current security recommendations for actions and permissions.

⸻

23. Daily Developer Workflow

This is a typical workflow for building a feature in a team.

Step 1: Update main

git switch main
git pull --ff-only origin main

Step 2: Create a feature branch

git switch -c feature/user-profile

Step 3: Write your code

Make changes in your editor.

Inspect them:

git status
git diff

Step 4: Stage the changes

git add .

Inspect the staged changes:

git diff --staged

Step 5: Commit

git commit -m "Add user profile"

Step 6: Push

git push -u origin feature/user-profile

Step 7: Create a pull request

Open GitHub, review the changes, and create a pull request into main.

Step 8: Merge and synchronize

After the pull request is merged:

git switch main
git pull --ff-only origin main

Step 9: Clean up

git branch -d feature/user-profile

This is a common workflow, although individual teams may use different branch names, merge strategies, and review requirements.

⸻

24. Common Errors and Solutions

Error 1: Nothing to commit

nothing to commit, working tree clean

Meaning: Git sees no pending changes to commit.

Check:

git status

Error 2: File is untracked

Solution:

git add filename
git commit -m "Add filename"

Error 3: Push rejected because remote has new commits

First inspect the situation:

git fetch origin
git status

If your local branch can safely fast-forward:

git pull --ff-only origin main

Resolve any divergence appropriately before pushing. Do not immediately force-push.

Error 4: Merge conflict

git status

Resolve the conflicting files, then:

git add .
git commit -m "Resolve merge conflict"

If the conflict happened during a rebase, use:

git rebase --continue

If it happened during a cherry-pick, use:

git cherry-pick --continue

Error 5: Wrong commit message

git commit --amend -m "Correct commit message"

Use this for the latest commit when rewriting it is appropriate.

Error 6: Wrong branch

Check your branch:

git branch --show-current

Switch branches:

git switch main

If you have uncommitted changes, Git may prevent the switch or carry compatible changes across. Inspect your status before switching.

Error 7: Remote already exists

error: remote origin already exists

Inspect the remote:

git remote -v

If the URL is wrong, update it:

git remote set-url origin YOUR_REPOSITORY_URL

Error 8: Accidentally committed a file

If the commit is still local and you want to undo it while retaining the changes:

git reset --soft HEAD~1

Review the staged files and recommit appropriately.

If the commit has already been shared, consider git revert instead.

Error 9: Lost a commit after reset

Inspect:

git reflog

Find the commit and create a recovery branch:

git branch recovery/backup COMMIT_HASH

Error 10: Authentication failed

Check the repository URL:

git remote -v

For HTTPS, authenticate using GitHub’s supported sign-in methods or a properly configured credential manager. For SSH, configure an SSH key and add its public key to your GitHub account.

Do not put passwords or access tokens directly in repository URLs or commit them to source control.

⸻

25. Essential Commands Reference

Setup

git --version
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --global --list

Create and inspect repositories

git init
git clone REPOSITORY_URL
git status
git rev-parse --show-toplevel

Stage and commit

git add filename
git add .
git commit -m "Message"
git commit --amend

Inspect changes

git diff
git diff --staged
git log --oneline
git log --oneline --graph --all
git show COMMIT_HASH
git blame filename

Branches

git branch
git branch feature/login
git switch main
git switch -c feature/login
git branch -m new-name
git branch -d feature/login

Merge and rebase

git merge feature/login
git merge --abort
git rebase main
git rebase --continue
git rebase --abort
git rebase -i HEAD~3

Remote operations

git remote -v
git remote add origin REPOSITORY_URL
git fetch origin
git pull
git push
git push -u origin main
git push origin --delete feature/login

Undo and recover

git restore filename
git restore --staged filename
git reset --soft HEAD~1
git reset --mixed HEAD~1
git reset --hard HEAD~1
git revert HEAD
git reflog

Stash and cherry-pick

git stash push -m "WIP"
git stash list
git stash apply
git stash pop
git stash drop stash@{0}
git cherry-pick COMMIT_HASH
git cherry-pick --abort

Tags

git tag
git tag -a v1.0.0 -m "Version 1.0.0"
git show v1.0.0
git push origin v1.0.0

⸻

26. Practice Projects

The best way to master Git is to practice these tasks in a disposable repository.

Beginner

* Initialize a repository.
* Create a README.
* Stage and commit files.
* Modify a file and inspect git diff.
* Make multiple commits.
* Inspect history using git log.
* Create a .gitignore.

Intermediate

* Create a feature branch.
* Make separate commits on two branches.
* Merge a feature branch.
* Create and resolve a merge conflict.
* Connect a local repository to GitHub.
* Push a feature branch.
* Open and merge a pull request.
* Clone a repository onto another directory.
* Fetch and pull remote changes.

Advanced

* Unstage a file without losing its changes.
* Undo a local commit using git reset --soft.
* Revert a commit.
* Save and restore changes using git stash.
* Cherry-pick one commit into another branch.
* Rebase a feature branch onto main.
* Amend a commit message.
* Squash commits using interactive rebase.
* Recover a commit using git reflog.
* Create and push a version tag.
* Fork a public repository and configure an upstream remote.
* Add a basic GitHub Actions workflow.

⸻

Final Rules to Remember

1. Check before acting: Use git status to understand the current state.
2. Inspect before committing: Use git diff and git diff --staged.
3. Commit logically: Keep commits focused on related changes.
4. Use branches: Develop features separately from main.
5. Understand your undo command: restore, reset, and revert have different effects.
6. Be careful with reset --hard: It can destroy uncommitted work.
7. Be careful with force-push: It can overwrite shared branch history.
8. Avoid rewriting shared history: Do not casually amend or rebase commits that teammates rely on.
9. Never commit secrets: Keep credentials and environment files out of Git.
10. Push regularly: Keep important work backed up remotely.
11. Use pull requests: Review changes before integrating them into shared branches.
12. Practice recovery: Learn how to use reflog before you need it.

The most important daily commands:

git status
git add .
git diff --staged
git commit -m "Describe changes"
git pull
git push
git switch -c feature/name
git merge feature/name
git log --oneline --graph --all

You don’t need to memorize every command at once. Keep this guide available, practice the workflows, and use the relevant section whenever you need a reminder.

Git mastery comes from understanding the state of your repository and choosing the right command—not from memorizing hundreds of commands.