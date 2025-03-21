# Git-Advanced-Exercises
## Part 1: Refining Git History (10 Challenges)
### 1.Missing File Fix:
```bash
Run git status and git log to assess the current state of your repository.
From the status you will see that you forgot to add test4.md in the last commit.

Challenge: Recover from this error by staging/adding test4.md and amending the commit message with an appropriate description.

#SOLUTION
acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git add test4.md

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git commit --amend -m " adding test4 to Creating third and fourth files"
[main 73d75be]  adding test4 to Creating third and fourth files
 Date: Mon Mar 3 12:57:10 2025 +0200
 2 files changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 test3.md
 create mode 100644 test4.md

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git log --oneline
73d75be (HEAD -> main)  adding test4 to Creating third and fourth files
44b99b0 chore: Create another file
6a39ab3 chore: Create initial file
0804bf4 first commit
```

### 2.Editing Commit History:
```bash

It's crucial to maintain accurate commit messages. Modify the message from "Create another file" to "Create second file".

Challenge: Utilize interactive rebasing (git rebase -i HEAD~2) to edit the commit message and ensure clarity. learn more about git rebase

# SOLUTION

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git rebase -i HEAD~3
[detached HEAD 2f77402] chore: Create Second file
 Date: Mon Mar 3 12:57:09 2025 +0200
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 test2.md
Successfully rebased and updated refs/heads/main.

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git log --oneline
268f541 (HEAD -> main)  adding test4 to Creating third and fourth files
2f77402 chore: Create Second file
6a39ab3 chore: Create initial file
0804bf4 first commit

 ```

 ### 3.Keeping History Tidy - Squashing Commits:
 ```bash 

 Squashing combines multiple commits into a single one. Let's merge "Create second file" into "Create initial file" for a cleaner history.

Challenge: Use interactive rebasing with the squash command to achieve this. learn more about squash

#SOLUTION

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git rebase -i HEAD~3
[detached HEAD e1c34b2] chore: Merging initial and second file commits
 Date: Mon Mar 3 12:57:09 2025 +0200
 2 files changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 test1.md
 create mode 100644 test2.md
Successfully rebased and updated refs/heads/main.

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git log --oneline
f1047c6 (HEAD -> main)  adding test4 to Creating third and fourth files
e1c34b2 chore: Merging initial and second file commits
0804bf4 first commit
 ```

 ### 4.Splitting a Commit:
 ```bash 
 acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git reset --soft HEAD~1

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   test3.md
        new file:   test4.md


acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git reset HEAD .
acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git add test3.md && git commit -m "chore: Create third file"
[main 91a1a2d] chore: Create third file
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 test3.md

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git add test4.md && git commit -m "chore: Create fourth file"
[main 24653c2] chore: Create fourth file
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 test4.md
 ```

 ### 5.Advanced Squashing:
 ```bash 
 Let's explore more complex squashing. Can you combine the last two commits ("Create third file" and "Create fourth file") into a single commit named "Create third and fourth files"?

Challenge: Utilize interactive rebasing with the squash command to achieve this advanced squash. Check step 4
# SOLUTION
      Steps
      1.use git rebase -i HEAD~2
      2.change pick for creating fourth file to squash and then set it to Creating third and fourth files
acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git rebase -i HEAD~2
[detached HEAD 0ea49c4] chore: Create third and fourth files
 Date: Mon Mar 3 13:32:45 2025 +0200
 2 files changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 test3.md
 create mode 100644 test4.md
Successfully rebased and updated refs/heads/main.

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git log --oneline
0ea49c4 (HEAD -> main) chore: Create third and fourth files
e1c34b2 chore: Merging initial and second file commits
0804bf4 first commit
 ```

 ### 6.Dropping a Commit:
 ```bash 
 We all make mistakes. Imagine needing to completely remove an unwanted commit from your history.

Create a new file named unwanted.txt add some changes and commit it with a message like "Unwanted commit".

Challenge: Use git rebase -i to identify and remove the "Unwanted commit" commit, cleaning up your history. learn more about dropping commits

# SOLUTION

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ touch unwanted.txt

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ echo 'this is unwanted file ' > unwanted.txt

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git add unwanted.txt
warning: in the working copy of 'unwanted.txt', LF will be replaced by CRLF the next time Git touches it

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git commit -m 'unwanted commit'
[main d38279e] unwanted commit
 1 file changed, 1 insertion(+)
 create mode 100644 unwanted.txt

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git rebase -i HEAD~1
Successfully rebased and updated refs/heads/main.

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git log --oneline
0ea49c4 (HEAD -> main) chore: Create third and fourth files
e1c34b2 chore: Merging initial and second file commits
0804bf4 first commit


 ```
### 7. Reordering Commits:

```bash

Challenge : swapping  chore: Merging initial and second file commits with Create third and fourth files
#SOLUTION 
acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git log --oneline --graph
* 0ea49c4 (HEAD -> main) chore: Create third and fourth files
* e1c34b2 chore: Merging initial and second file commits
* 0804bf4 first commit

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git rebase -i HEAD~2
Successfully rebased and updated refs/heads/main.

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git log --oneline 
5471e4a (HEAD -> main) chore: Merging initial and second file commits
18a8d5d chore: Create third and fourth files
0804bf4 first commit
 ```

 ### 8. Cherry-Picking Commits:
 ```bash 
 Create a branch, call it ft/branch, and add a new file named test5.md with some content. Commit these changes with a message like "Implemented test 5".

Imagine you only desire a specific commit from ft/branch. Research and use git cherry-pick to selectively bring that commit into your current branch which is main.

#SOLUTION

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git checkout -b ft/branch
Switched to a new branch 'ft/branch'

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (ft/branch)
$ echo "This is test 5" > test5.md

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (ft/branch)
$ git add test5.md
warning: in the working copy of 'test5.md', LF will be replaced by CRLF the next time Git touches it

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (ft/branch)
$ git commit -m 'Implemented test 5'
[ft/branch 574dded] Implemented test 5
 1 file changed, 1 insertion(+)
 create mode 100644 test5.md
 
 acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (ft/branch)
$ git checkout main
Switched to branch 'main'

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git cherry-pick 574dded
[main 6fe9e16] Implemented test 5
 Date: Mon Mar 3 14:05:08 2025 +0200
 1 file changed, 1 insertion(+)
 create mode 100644 test5.md

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git log --oneline
6fe9e16 (HEAD -> main) Implemented test 5
5471e4a chore: Merging initial and second file commits
18a8d5d chore: Create third and fourth files
0804bf4 first commit
 ```
 ### 9. Visualizing Commit History (Bonus):
 ```bash 
 Tools like git log --graph or a graphical Git client can help visualize your commit history. Explore these tools for a clearer understanding of your workflow

 acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git log --graph
* commit 6fe9e163559586a772dc2e330ca6bfda73a440b8 (HEAD -> main)
| Author: Gervais Ngabo <stemgerlamo@gmail.com>
| Date:   Mon Mar 3 14:05:08 2025 +0200
|
|     Implemented test 5
|
* commit 5471e4a0b783f0cc7fdbdd0e24cd6af5da6f16d0
| Author: Gervais Ngabo <stemgerlamo@gmail.com>
| Date:   Mon Mar 3 12:57:09 2025 +0200
|
|     chore: Merging initial and second file commits
|
* commit 18a8d5d1dab9f0b7839e912b55ae1c059e06745c
| Author: Gervais Ngabo <stemgerlamo@gmail.com>
| Date:   Mon Mar 3 13:32:45 2025 +0200
 ```

 ### 10.Understanding Reflogs (Bonus):
```bash
acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git reflog

6fe9e16 (HEAD -> main) HEAD@{0}: cherry-pick: Implemented test 5
5471e4a HEAD@{1}: checkout: moving from ft/branch to main
574dded (ft/branch) HEAD@{2}: commit: Implemented test 5
5471e4a HEAD@{3}: checkout: moving from main to ft/branch
5471e4a HEAD@{4}: rebase (finish): returning to refs/heads/main
5471e4a HEAD@{5}: rebase (pick): chore: Merging initial and second file commits
18a8d5d HEAD@{6}: rebase (pick): chore: Create third and fourth files
0804bf4 HEAD@{7}: rebase (start): checkout HEAD~2
0ea49c4 HEAD@{8}: rebase (finish): returning to refs/heads/main
0ea49c4 HEAD@{9}: rebase (start): checkout HEAD~2
0ea49c4 HEAD@{10}: rebase (finish): returning to refs/heads/main
0ea49c4 HEAD@{11}: rebase (start): checkout HEAD~1
d38279e HEAD@{12}: commit: unwanted commit
0ea49c4 HEAD@{13}: rebase (finish): returning to refs/heads/main
0ea49c4 HEAD@{14}: rebase (squash): chore: Create third and fourth files
91a1a2d HEAD@{15}: rebase (start): checkout HEAD~2
24653c2 HEAD@{16}: commit: chore: Create fourth file
91a1a2d HEAD@{17}: commit: chore: Create third file
e1c34b2 HEAD@{18}: reset: moving to HEAD~1
f1047c6 HEAD@{19}: rebase (finish): returning to refs/heads/main
f1047c6 HEAD@{20}: rebase (pick): adding test4 to Creating third and fourth files
e1c34b2 HEAD@{21}: rebase (squash): chore: Merging initial and second file commits
6a39ab3 HEAD@{22}: rebase (start): checkout HEAD~3
268f541 HEAD@{23}: rebase (finish): returning to refs/heads/main
268f541 HEAD@{24}: rebase (pick): adding test4 to Creating third and fourth files
2f77402 HEAD@{25}: rebase (reword): chore: Create Second file
44b99b0 HEAD@{26}: rebase: fast-forward
6a39ab3 HEAD@{27}: rebase (start): checkout HEAD~3
73d75be HEAD@{28}: commit (amend): adding test4 to Creating third and fourth files
e6ce277 HEAD@{29}: commit: chore: Create third and fourth files
44b99b0 HEAD@{30}: commit: chore: Create another file
6a39ab3 HEAD@{31}: commit: chore: Create initial file
0804bf4 HEAD@{32}: Branch: renamed refs/heads/main to refs/heads/main
0804bf4 HEAD@{34}: commit (initial): first commit
(END)
```

## Part 2.Branching Basics (10 Challenges)
###  1.Feature Branch Creation:
```bash 
Imagine working on a new feature named ft/new-feature. Let's establish a dedicated branch for it
.
Challenge: Create a new branch named ft/new-feature and switch to that branch.
#SOLUTION 
1.git Checkout -b ft/new-feature

#SOLUTION

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git checkout -b ft/new-feature
Switched to a new branch 'ft/new-feature'

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (ft/new-feature)
```
### 2.Working on the Feature Branch
```bash 
Create a new file named feature.txt in this branch and add some content to it.
Commit these changes with a descriptive message like "Implemented core functionality for new feature".

#SOLUTION
acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (ft/new-feature)
$ echo "This is the core functionality for the new feature." > feature.txt

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (ft/new-feature)
$ git add feature.txt && git commit -m "Implemented core functionality for new feature"
warning: in the working copy of 'feature.txt', LF will be replaced by CRLF the next time Git touches it
[ft/new-feature 0d24c2f] Implemented core functionality for new feature
 1 file changed, 1 insertion(+)
 create mode 100644 feature.txt
```

### 3. Switching Back and Making More Changes
```bash 
It's common to switch between branches during development.

Challenge: Switch back to the main branch (previously master) and create a new file named readme.txt with some introductory content. Commit these changes with a message like "Updated project readme".

# SOLUTION

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (ft/new-feature)
$ git switch main
Switched to branch 'main'
Your branch is up to date with 'origin/main'.

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ echo "This is the project README file. It contains important information about the project." > readme.txt

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git add readme.txt
warning: in the working copy of 'readme.txt', LF will be replaced by CRLF the next time Git touches it

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git commit -m "Updated project readme"
[main 34337c8] Updated project readme
 1 file changed, 1 insertion(+)
 create mode 100644 readme.txt

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git log --oneline
34337c8 (HEAD -> main) Updated project readme
29ac187 (origin/main) deleting gitignore
6fe9e16 Implemented test 5
5471e4a chore: Merging initial and second file commits
18a8d5d chore: Create third and fourth files
0804bf4 first commit

```

### 5.Branch deletion
```bash
After merging or completing work on a feature branch, it's good practice to remove it.

Challenge: Delete the ft/new-feature branch once you're confident the changes are integrated into main.
 
 #SOLUTION
 acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git merge ft/new-feature
Merge made by the 'ort' strategy.
 feature.txt | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 feature.txt

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git branch -d ft/new-feature
Deleted branch ft/new-feature (was 0d24c2f).

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git branch
  ft/branch
* main

```
 ### 6.Creating a Branch from a Commit
 ```bash
 You can also create a branch from a specific commit in your history.

Challenge: Use git checkout -b ft/new-branch-from-commit commit-hash (adjust the commit hash as needed) to create a new branch named ft/new-branch-from-commit starting from the commit two positions back in your history
 
 # SOLUTION
 acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git log --oneline
1e6a27a (HEAD -> main) Merge branch 'ft/new-feature'
34337c8 Updated project readme
0d24c2f Implemented core functionality for new feature
29ac187 (origin/main) deleting gitignore
6fe9e16 Implemented test 5
5471e4a chore: Merging initial and second file commits
18a8d5d chore: Create third and fourth files
0804bf4 first commit

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git checkout -b ft/new-branch-from-commit HEAD~2
Switched to a new branch 'ft/new-branch-from-commit'

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (ft/new-branch-from-commit)
$ git branch
  ft/branch
* ft/new-branch-from-commit
  main

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (ft/new-branch-from-commit)
$ git log --oneline
29ac187 (HEAD -> ft/new-branch-from-commit, origin/main) deleting gitignore
6fe9e16 Implemented test 5
5471e4a chore: Merging initial and second file commits
18a8d5d chore: Create third and fourth files
0804bf4 first commit
  ```

  ### 7.Branch Merging
  ```bash
  Now that you've completed work on your feature branch, it's time to integrate it into main.

Challenge: Merge the ft/new-branch-from-commit branch into the main branch. Address any merge conflicts that might arise.

# SOLUTION
 git switch main
Switched to branch 'main'
Your branch is ahead of 'origin/main' by 3 commits.
  (use "git push" to publish your local commits)

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git merge ft/new-branch-from-commit
Already up to date.
  ```

### 8.Branch Rebasing
```bash
Challenge: Try rebasing the ft/new-branch-from-commit branch onto the main branch. Remember, rebasing rewrites history, so use it with caution, especially in shared repositories
# SOLUTION
acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git checkout ft/new-branch-from-commit
Switched to branch 'ft/new-branch-from-commit'

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (ft/new-branch-from-commit)
$ git rebase main
Successfully rebased and updated refs/heads/ft/new-branch-from-commit.
```

### 9.Renaming Branches
```bash
Branch names can sometimes evolve. Let's rename ft/new-branch-from-commit to a more descriptive name.

Challenge: Use git branch -m ft/new-branch-from-commit ft/improved-branch-name to rename your branch.

# SOLUTION

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (ft/new-branch-from-commit)
$ git branch -m ft/new-branch-from-commit ft/improved-branch-name

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (ft/improved-branch-name)
```
### 10.Checking Out Detached HEAD
```bash 

Chalenge: detaching HEAD means checking out 0d24c2f commit without affecting any branch or being on that 

# SOLUTION

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git checkout 0d24c2f
Note: switching to '0d24c2f'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at 0d24c2f Implemented core functionality for new feature

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises ((0d24c2f...))
$ ls
feature.txt  README.md  test1.md  test2.md  test3.md  test4.md  test5.md
```

## Part 3: Advanced Workflows (10+ Challenges)
### Stashing Changes
```bash 
Imagine you're working on some changes in the main branch but need to attend to something urgent. You don't want to lose your uncommitted work.
Challenge: Stash your current changes in the main branch using git stash

# SOLUTION
acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git stash save 'save your uncommitted changes '
Saved working directory and index state On main: save your uncommitted changes 

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git stash list
stash@{0}: On main: save your uncommitted changes

```
### 2.Retrieving Stashed Changes
```bash
Challenge: Apply the most recent stash back onto the main branch using git stash pop

# SOLUTION

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git stash pop
On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
Dropped refs/stash@{0} (a0f4b59d0638d74e6581cfc1f2100d515b71c787)

```

### 3.Branch Merging Conflicts (Continued)
  ```bash
  Challenge: Simulate a merge conflict scenario (you can create conflicting changes in a file on both main and a new feature branch). Then, try merging again and resolve the conflicts manually using your text editor.

  # Steps
  acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (feature-branch)
$ echo "Hello from Feature Branch" > conflict.txt
git add conflict.txt
git commit -m "Updated conflict.txt in feature branch"
warning: in the working copy of 'conflict.txt', LF will be replaced by CRLF the next time Git touches it
[feature-branch 35f08d7] Updated conflict.txt in feature branch
 1 file changed, 1 insertion(+)
 create mode 100644 conflict.txt

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (feature-branch)
$ git switch main
Switched to branch 'main'
Your branch is up to date with 'origin/main'.

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ echo "Hello from Main Branch" > conflict.txt

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git add conflict.txt
warning: in the working copy of 'conflict.txt', LF will be replaced by CRLF the next time Git touches it

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git commit -m 'Updated conflict.txt in main branch'
[main 2078b5a] Updated conflict.txt in main branch
 1 file changed, 1 insertion(+)
 create mode 100644 conflict.txt

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git merge feature-branch
Auto-merging conflict.txt
CONFLICT (add/add): Merge conflict in conflict.txt
Automatic merge failed; fix conflicts and then commit the result.

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main|MERGING)

#CONFLICT IN FILE
<<<<<<< HEAD
Hello from Main Branch
=======
Hello from Feature Branch
>>>>>>> feature-branch

   # SOLUTION
1. I changed manual remove what was not needed and then 
 $ git add conflict.txt

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main|MERGING)
$ git commit -m 'resolving conflict from main and feature branch'
[main 0ed1444] resolving conflict from main and feature branch

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
  ```

  ### 5.Ignoring Files/Directories
  ```bash 
  You might have files or directories you don't want to track in Git. Create a .gitignore file to specify these exclusions.

Challenge: Add a pattern like /tmp to your .gitignore file to exclude all temporary files and directories from version control. more about ignoring files
# SOLUTION

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ touch .gitignore
acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ touch .gitignore

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git add .

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git commit - m 'adding gitignore '
error: pathspec '-' did not match any file(s) known to git
error: pathspec 'm' did not match any file(s) known to git
error: pathspec 'adding gitignore ' did not match any file(s) known to git

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git commit -m 'adding gitignore '
[main 7156552] adding gitignore
 1 file changed, 1 insertion(+)
 create mode 100644 .gitignore

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git status --ignored
On branch main
Your branch is ahead of 'origin/main' by 4 commits.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ cat .gitignore
/tmp
  ```

### 7.Working with Tags
```bash
Tags act like bookmarks in your Git history. Create a tag to mark a specific point in your development.
Challenge: Use git tag v1.0 to create a tag named v1.0 on the current commit in your main branch

# SOLUTION
acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git tag v1.0

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git tag
v1.0
```

### 8.Listing and Deleting Tags
```bash 
acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git tag show v1.0

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git tag
list
show
v1.0

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git tag -d list
Deleted tag 'list' (was 41d22a3)

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git tag -d show
Deleted tag 'show' (was 41d22a3)

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git tag
v1.0

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git show v1.0
commit 41d22a3dc9311af3d0496b88e94e561070bbdb0c (HEAD -> main, tag: v1.0)
Author: Gervais Ngabo <stemgerlamo@gmail.com>
Date:   Tue Mar 4 10:54:52 2025 +0200

    adding gitignore

diff --git a/.gitignore b/.gitignore
new file mode 100644
index 0000000..cad2309
--- /dev/null
+++ b/.gitignore
@@ -0,0 +1 @@
+/tmp
\ No newline at end of file
```

### 9.Pushing Local Work to Remote Repositories:
```bash
Once you're happy with your local changes and branches, it's time to share them with others.
Challenge: Assuming you've set up a remote repository on a Git hosting platform (like GitHub), push the changes with the actual branch you want to push to push your local branch to the remote repository

# SOLUTION
acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git push
Enumerating objects: 14, done.
Counting objects: 100% (14/14), done.
Delta compression using up to 4 threads
Compressing objects: 100% (9/9), done.
Writing objects: 100% (12/12), 3.48 KiB | 508.00 KiB/s, done.
Total 12 (delta 5), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (5/5), completed with 2 local objects.
To https://github.com/Stemgerlamo/Git-Advanced-Exercises.git
   e506d1b..9a4a9ec  main -> main

```
### 10.Pulling Changes from Remote Repositories
```bash
Challenge: Navigate to Github and make some changes inside your README file that you created on your main branch and in your local environment use git pull origin <branch-name> (replace <branch-name> with the actual branch you want to pull) to fetch changes from the remote repository's main branch and merge them into your local main branch. Address any merge conflicts that might arise.
THERE WAS CHANGES ON BOTH SIDES

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git commit -m 'adding changes on readme'
[main b599e3b] adding changes on readme
 1 file changed, 0 insertions(+), 0 deletions(-)

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git pull
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 3 (delta 1), reused 0 (delta 0), pack-reused 0 (from 0)
Unpacking objects: 100% (3/3), 6.89 KiB | 414.00 KiB/s, done.
From https://github.com/Stemgerlamo/Git-Advanced-Exercises
   32e209e..d53c9a1  main       -> origin/main
warning: Cannot merge binary files: README.md (HEAD vs. d53c9a1ca231e489d6176c1c0a4be418598ccdef)
Auto-merging README.md
CONFLICT (content): Merge conflict in README.md
Automatic merge failed; fix conflicts and then commit the result.
Auto-merging README.md
CONFLICT (content): Merge conflict in README.md
Automatic merge failed; fix conflicts and then commit the result.
CONFLICT (content): Merge conflict in README.md
Automatic merge failed; fix conflicts and then commit the result.
Automatic merge failed; fix conflicts and then commit the result.

acer@NBI MINGW64 ~/Desktop/gym/Git Advance Exercises (main)
$ git pull
Already up to date.
```
