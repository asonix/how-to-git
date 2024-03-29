## Getting Started with Git

_Authors: [Alice Werefox](https://werefox.cafe), [Nicholas Gilpin](https://github.com/nicholascgilpin), [asonix](https://git.asonix.dog/asonix)_

### What is Git?
_Torvald's fancy undo button_

Git is a _system_ which tracks the changes you make to files in a special folder called a _repository_. Each time you _commit_ to a significant file modification, Git will help you record when and why you made the change. Sometimes you're not sure which direction you want to take, so you make two _versions_. When this happens, Git can help you _branch_ off and control your different project versions. When working on large projects, Git can create online folders, called _remotes_, so that teams can _synchronize_ their files or post _requests_ for help. Lastly, if two friends make _conflicting_ changes to the same file, then Git can help them _differentiate_ between versions and _merge_ the changes back into one file.
### Creating a new repository

_Everybody starts somewhere_

When using a tool like GitHub or GitLab, often you won't need to create your own git repository, but we'll start from the beginning just in case. Skip to Cloning a Remote Repository if you don't care about this.

_syntax:_ `git init [[path/to/repository]]`

_example:_
```
asonix@asonix-gs60 ~/Downloads/Telegram Desktop
$ git init temp/
Initialized empty Git repository in /media/windows-data/Downloads/Telegram Desktop/temp/.git/
```

_note: this command creates the folder if it doesn't already exist_

### Setting Remotes

_Sharing is caring_

Once you've created your repository, it is likely that you will want to share it with someone. To do so, you must also initialize a repository in a public location.

Once you have a public repository, you can tell your local copy where you want to sync code using the `remote add` command.

_syntax:_ `git remote add [[remote name]] [[url]]`

_example:_
```
asonix@asonix-gs60 ~/git/temp
$ git remote add origin https://github.com/KayDevs/Project3.git
```

### Cloning a Remote Repository

_We stand on the shoulders of giants_

If there is already a repository for your project, you'll want to contribute to that rather than creating a new repository. In order to make a local copy of the code so you can make changes, you'll want to `clone` the repository.

_syntax:_ `git clone [[https://url.of/the/repository.git]]`

_example:_
```
asonix@asonix-gs60 ~/git
$ git clone https://github.com/Airblader/i3.git
Cloning into 'i3'...
remote: Counting objects: 31250, done.
remote: Total 31250 (delta 0), reused 0 (delta 0), pack-reused 31250
Receiving objects: 100% (31250/31250), 8.72 MiB | 366.00 KiB/s, done.
Resolving deltas: 100% (23935/23935), done.
Checking connectivity... done.
```
### Creating your branch

_You'll want your own copy of the code to modify to your heart's content_

It is important to note that cloning the repository is only the first step to getting your own code to work on. When you first clone the repository, you will want to create your own branch so you can make changes to your code without polluting the `main branch`.

The term **branch** comes from the idea that updates to the code should be seen as a tree. The Code can exist in multiple branches (versions) simultaneously, and the branches can split or merge freely. The `main branch` is at the base of the tree, and should be considered sacred._**The**_ `main branch` _**should only contain code that has been tested and is known to work.**_ This way, we have the ability to distribute copies of our code that we know will not fail.

_syntax:_ `git checkout -b [[your-branch-name]]`

_example:_
  ```
asonix@asonix-gs60 ~/git/i3 (main)
$ git checkout -b asonixdev
Switched to a new branch 'asonixdev'
  ```

It is typically a good idea to create a new branch for each new feature you want to add. This makes managing the repository much easier in the future.

### Switching branches

_When your first copy of the code is not enough_

You may want to create different branches for different features and bugs you are planning to add and fix (respectively). In order to switch between branches that have already been created, you use the following:
`git checkout [[branch-name]]`

`:: git checkout alicedev` changes your files to whatever is currently in your version of the branch you want to work on, in this case, alicedev

_syntax:_ `git checkout [[branch-name]]`

_example:_
  ```
asonix@asonix-gs60 ~/git/i3 (gaps)
$ git checkout main
Branch main set up to track remote branch main from origin.
Switched to a new branch 'main'
  ```

### Updating Your Branches

_Other people write code too, you should get it_

Always `pull` before you start working on new code. It will fetch any updates that have been pushed to the server on the branch you're on. It will also tell you which other branches you are tracking that are out of date and need to be pulled. You should do this on all branches you are tracking before you push commits to the server.

_syntax:_ `git pull`

_example:_
  ```
asonix@asonix-gs60 ~/git/i3 (main)
$ git pull
remote: Counting objects: 689, done.
remote: Total 689 (delta 319), reused 320 (delta 319), pack-reused 369
Receiving objects: 100% (689/689), 182.78 KiB | 0 bytes/s, done.
Resolving deltas: 100% (537/537), completed with 119 local objects.
From https://github.com/o4dev/i3
  c56403b..c922378  gaps       -> origin/gaps
  31c33df..4c878f4  main     -> origin/main
  * [new tag]         4.8        -> 4.8
Updating c56403b..c922378
Fast-forward
232 files changed, 9378 insertions(+), 5336 deletions(-)
  ```

### Making changes

_Programming ensues, changes are made. Whether they are right or wrong._

To check which files have been changed and need to be committed, or to see if your local code is outdated, you will want to get the repository's `status`.

_syntax:_ `git status`

_example:_
  ```
asonix@asonix-gs60 ~/git/i3 (main)
$ git status
On branch main
Your branch is up-to-date with 'origin/main'.
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

  modified:   Makefile

no changes added to commit (use "git add" and/or "git commit -a")
  ```

If you made changes, you will need to add those changes before you can commit them so Git knows what is being tracked and what to commit. To add files, just use `git add filename.extension` where filename is the name of the file and extension is the extension, if any.

```
asonix@asonix-gs60 ~/git/i3 (main)
$ git add Makefile
  ```
_**PROTIP: PLEASE DON'T ADD BIN FILES LIKE "a.out" BECAUSE YOU WILL MAKE ME MAD BECAUSE I'LL HAVE TO FIX IT BECAUSE THOSE DON'T MERGE WELL.** We'll cover methods to ensure this doesn't happen later_

### Committing Changes

_Committing changes solidifies a group of changes as a version of the code in git_

After you've added the changes so they are tracked, you can make sure everything is good by entering `git status` again and the output should tell you all the files which are being tracked. If something is not yet being tracked (like, you made a new file to be uploaded) you can 'git add' that as well or you can just ignore it if you don't want it pushed to the server.

To commit files to the LOCAL repository, use `git commit -m "enter message here on why you are committing"` if you want to force a commit for whatever reason or just don't feel like adding files (not recommended) use `git commit -a`.

_syntax:_ `git commit -m [[commit message]]`

_example:_
  ```
asonix@asonix-gs60 ~/git/i3 (main)
$ git commit -m "test commit"
[main ed9d6a7] test commit
1 file changed, 2 insertions(+)
  ```

_**PROTIP: If you don't put a message in, the thing will yell at you and not do the commit. using -a won't require a message, but I don't recommend using it unless you just really can't get the commit to work. It involves me having to go in afterwards and fix Github ruining things.**_

** Minor Troubleshooting **
If you accidentally added a file to be tracked and want to remove it, use `git rm filename.extension ..` (and other filenames if you want to do more). If you removed a file the normal way (rm, delete, etc.), it should be added to what is being committed automatically.

If you want to discard the changes you made (for example: someone else made them already and committed them, so your changes are useless now) use `git checkout --filename.extension ..`

### Pushing Changes To The Server

If all of that went well, all you need to do is use the push command. This pushes the commits you made on your local repository to the server's repository. This is why when you don't use the pull command often, the server won't let you push things. Your local repository needs to match what is in the server repository before you can make a push to the server, since it checks all of that and changes whatever is different. Otherwise, it'll yell at you for not having its updates.

_styntax:_ `git push`

_(authentication ensues)_

### Merging Branches using Pull Requests

_Having branches is nice, but we need all the features in the same place (when we ship our product)_

Many git frontends have a nice feature called Pull Requests, and since it helps us merge changes, we should probably use it. When you want to merge your feature branch into `main`, it is _incredibly_ important that you use a pull request. To ask to be merged in, you go to the repository's GitHub or GitLab or WhatEver page, you switch to the branch you want to merge from, and you click `New Pull Request`. This will bring you to a page where you can specify what changes have been made and why this `compare` branch should be merged with the `base` branch. Once you have explained yourself thoroughly, click `create pull request`. If the author of the `base` branch thinks your changes are important and needed, they can accept the pull request.

### Merging Branches Manually

_For when we don't want to use GitHub's/GitLab's pull request feature, when pull requests fail, or when we aren't dealing with a sane git frontend_

From here, since we pushed changes to our branch `alicedev` _and used pull requests to merge_ `alicedev` _into_ `main`, we want those changes on **every** feature branch to make sure we're working with updated code. To do this, we're going to use the merge command and them push those changes to the server. You have to push because when you merge it's doing that on your local repository first, then it needs to push those changes to the server.

`git merge main` merges what changes are in main into the current branch, git calls this "fast-forwarding"

_syntax:_
  - `git merge [[branch_with_changes]]`
  - `git merge [[branch_to_merge_into]] [[branch_with_changes]]`

_example:_
  ```
asonix@asonix-gs60 ~/git/i3 (main)
$ git merge main gaps
Merge made by the 'recursive' strategy.
33 files changed, 680 insertions(+), 58 deletions(-)
  ```
_Note: this example shows merging into main, please do not do this in any situation_

### Rebasing

_It comes to mind that main gets ahead of my branch a lot_

Bigger projects come with faster changes. There is always someone merging something into main, and often your feature or bug fix can get left behind. This is where `git rebase` comes in. Say you have a branch with 3 commits, and main has had a commit since you created this branch. In order to apply your changes to main, you might think to merge main into your branch.

There is another way, however, that doesn't add an extra commit where there doesn't need to be one. Since git keeps track of history in addition to branches, we can replay certain changes on top of a different starting point.

_syntax:_
  - `git rebase [[commit_id or branch_name]] [[commit_id or branch_name]]` for updating base on same branch
  - `git rebase [[commit_id or branch_name]] --onto [[commit_id or branch_name]]` for updating base to new branch

_example (borrowed from official documentation)_:
  ```
branches:
    A---B---C topic
   /
  D---E---F---G main

command:
$ git rebase main topic

branches:
                A'--B'--C' topic
               /
  D---E---F---G main
  ```
[source](https://git-scm.com/docs/git-rebase)

### Squashing

_Commits are good, but too many can be deafening_

When working on large projects, there will typically be thousands of commits across an entire team on various branches. In order to reduce the number of commits in the main branch and make it easier to find what changes introduced what features, you can squash a feature branch or bug fix branch into a single commit before merging.

_syntax:_
  - `git rebase -i [[commit_id]]` the `-i` makes it interactive

The commit_id is the full hash of the last commit before the commits you want to squash together.

_example:_
  ```
$ git checkout -b rebase-example
$ git log
  commit fb23fff41447f4f75d54255ff213baa783a9639b
  Author: Riley Trautman <asonix.dev@gmail.com>
  Date:   Thu May 12 23:36:54 2016 -0500

  remove all Map.{get,put}, replace with Map.update

  commit dbcafa1987d32cda1d8398947b8c1d59c7894b46
  Author: Riley Trautman <asonix.dev@gmail.com>
  Date:   Thu May 12 23:30:19 2016 -0500

  remove unneeded nil case

  commit 36a6cf5b9d62b4084d7db10c60a7ce2238110a6a
  Author: Riley Trautman <asonix.dev@gmail.com>
  Date:   Thu May 12 23:27:46 2016 -0500

  Initial arguments shouldn't be
  they should be an empty thing of the correct type (oops)

  commit 7cbbcf4d126da3b523984146190f96e91582bd61
  Author: Riley Trautman <asonix.dev@gmail.com>
  Date:   Thu May 12 22:07:27 2016 -0500

  Ensure node import test for multiple rounds is correct

  commit aacfc213a559668eafbdfb3a4f91c427edb0f72f
  Author: Riley Trautman <asonix.dev@gmail.com>
  Date:   Thu May 12 22:02:12 2016 -0500

  test inserting for multiple rounds

  commit 4d17080ac69590a27eda74fb9e0859cf0634e143 <- We want to squash onto this one
  Author: Riley Trautman <asonix.dev@gmail.com>
  Date:   Thu May 12 21:57:41 2016 -0500

  Fix formatting a bit

  commit a3ae709c412d14a19e1b49322378372640576eae <- so we pick this as our base
  Author: Riley Trautman <asonix.dev@gmail.com>
  Date:   Thu May 12 21:56:26 2016 -0500

  Inserting the first level of nodes works


$ git rebase -i a3ae709c412d14a19e1b49322378372640576eae

editor:
  1 pick 4d17080 Fix formatting a bit
  2 squash aacfc21 test inserting for multiple rounds
  3 squash 7cbbcf4 Ensure node import test for multiple rounds is correct
  4 squash 36a6cf5 Initial arguments shouldn't be they should be an empty thing of the correct type (oops)
  5 squash dbcafa1 remove unneeded nil case
  6 squash fb23fff remove all Map.{get,put}, replace with Map.update

editor:
  1 Some commit message
  2
  3 About what changed in this branch

output:
  [detached HEAD a8e0b22] Some commit message
  Date: Thu May 12 21:57:41 2016 -0500
  2 files changed, 66 insertions(+), 18 deletions(-)
  Successfully rebased and updated refs/heads/rebase-example.
  ```

This squashed commits `4d17080` through `fb23fff` into the same commit with the message "Some commit message". We can now open a merge request from the newly-squashed branch into the release branch.

### Other Things of Note

#### .gitignore
Git provides some other features that can be very helpful. Most importantly, the `.gitignore` file. `.gitignore` keeps track of files you _do not_ want to be committed and pushed to the repository. You can add files to `.gitignore` explicitly by stating the file path in reference to the location of `.gitignore`, or by specifying splats to cover multiple files (also in reference to the location of `.gitignore`).

A `.gitignore` may look like this:
  ```
a.out           # to avoid committing the compiled program
*.o             # to avoid committing other binaries
*~              # to avoid committing backups of files
*.swp           # to avoid committing swap files (created by vim)
.clang_complete # to avoid committing local clang configurations
tmp/*           # to avoid committing anything in the local temp folder
  ```

#### Stashing
If the branch you are on is updated by someone else, you will need to pull and merge your changes before you can push. In order to avoid conflicts during the merge, you can stash your local changes and play them back after you pull.

_syntax_:
 - `git stash` for stashing your changes onto a stack
 - `git stash pop` for popping the changes on the top of the stack back onto your branch

#### Colors
Sometimes (read: always) you want to make git output in a colorful manner because colors make things easy to read. You can easily enable this with `git --global color.ui true`
