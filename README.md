# learning Git
## Ravi usual commands 
```
git log --oneline -n5
```

## Creating a Remote Branch 

First, you must create your branch locally
```
git checkout -b your_branch
```
After that, you can work locally in your branch, when you are ready to share the branch, push it. The next command push the branch to the remote repository origin and tracks it
```
git push -u origin your_branch
```
Teammates can reach your branch, by doing:
```
git fetch
git checkout origin/your_branch
```


## Tracking Remote Branch 
```
git checkout -b totallyNotMain o/main
```

### Way #2

Another way to set remote tracking on a branch is to simply use the git branch -u option. Running
```
git branch -u o/main foo
```

will set the foo branch to track o/main. If foo is currently checked out you can even leave it off:
```
git branch -u o/main

```
## Delete a Commit 

Careful: git reset --hard WILL DELETE YOUR WORKING DIRECTORY CHANGES. Be sure to stash any local changes you want to keep before running this command.
Assuming you are sitting on that commit, then this command will wack it...
``git reset --hard HEAD~1``
The HEAD~1 means the commit before head.
Or, you could look at the output of git log, find the commit id of the commit you want to back up to, and then do this:

``git reset --hard <sha1-commit-id>``
## How to add only modified files 
You can do ``git add -u``so that it will stage the modified and deleted files.
The git commit -a stands for all. This option automatically stages all modified files to be committed. If new files are added the -a option will not stage those new files. Only files that the Git repository is aware of will be committed
## How to remove local untracked files from the current Git branch
To remove directories, run 
``git clean -f -d`` or ``git clean -fd``.
To remove ignored files, ``run git clean -f -X`` or ``git clean -fX``.
To remove ignored and non-ignored files, ``run git clean -f -x`` or ``git clean -fx.
## Stashing 
```
git stash 
git stash --include-untracked
```
it stashes the files staged
```
git stash pop 
```
takes out the files previously stashed
you want ```git stash drop``` to drop the stashed staged files

## Gerrit Confluence page
```
> git diff                # Compare "working tree" against the last (HEAD) commit on this branch.
> git diff --cached       # Compare "staged files"/"index" against the last commit on this branch.
> git diff HEAD~1         # Compare "working tree" against the last-but-one commit on this branch (also ~2, ~3, etc).
> git diff <commit>       # Compare "working tree" against a specific commit.
> git diff <branch>       # Compare "working tree" against a specific branch.
> git diff <a> <b>        # Compare two branches, commits, tags.
```
if you want to see what you haven't git added yet:

git diff myfile.txt
or if you want to see already added changes

git diff --cached myfile.txt
Showing previous commits
```
> git log                 # View all commits on this branch.
> git log                 # View all commits on this branch.
> git log <branch>        # View all commits on another branch.
> git show                # Show details of the last commit on this branch.
> git show <commit>       # Show details of the given commit.
> git show <branch>       # Show details of the last commit on the given branch. 
```
Checkout out a branch
```
> git branch                    # List all local branches.
> git branch -a                 # List all branches (local and remote).
> git checkout develop          # Check out a branch.
```
Checkout a tag
```
> git tag -l                                    # List all tags
> git checkout weekly/2015-w47-develop-0        # Check out a specific tag.
```
Checkout out a specific commit
```
> git checkout f11d5963787e250168d7cb582c3313a6c7a5cb3a
```
Amending a commit
```
# Make edits...
> git status
> git add <list_of_files>
> git commit --amend            # Amends existing commit, instead of creating a new one.
```
Updating remote branches
```
> git fetch                     # Download commits made to origin branches.
> git fetch --all               # Download commits made to all remote branches.
```
Updating local branches
```
> git pull --rebase             # Download commits made to origin branches and rebase the current branch on top of the branch it tracks.
> git rebase <remote> <local>   # Rebase <local> branch onto <remote> branch.Updating remote branches
> git fetch                     # Download commits made to origin branches.
> git fetch --all               # Download commits made to all remote branches.
```
Updating local branches
```
> git pull --rebase             # Download commits made to origin branches and rebase the current branch on top of the branch it tracks.
> git rebase <remote> <local>   # Rebase <local> branch onto <remote> branch.
```
Develop feature on local branch and open a review
```
> git checkout -b watchdog_timer -t origin/feature/blah            # Check out a local branch (watchdog_timer) that tracks remote branch (origin/feature/blah).
# Make edits...
> git status                                                       # Show status of files (identify those which have been edited).
> git add <list_of_files>                                          # Add all the files you want to share (normally all edited files).
> git commit                                                       # Commit files.
> git pull --rebase                                                # Update the commit with remote changes.
> git push origin watchdog_timer:refs/for/feature/blah             # Open a review (n.b. refs/for/ magic prefix opens the review).
```
# Git Rebase
```
Git pull --rebase
Git rebase side1 side2 
Git rebase destination change
```


It is carried out on the destination, and once the change is done the branch changes to the one specified in change
## Detaching Head
First we have to talk about "HEAD". HEAD is the symbolic name for the currently checked out commit 
Detaching HEAD just means attaching it to a commit instead of a branch.
Specify this commit by its hash. The hash for each commit is displayed on the circle that represents the commit.
## Relaltive Commits
Relative commits are powerful, but we will introduce two simple ones here:
	• Moving upwards one commit at a time with ^
	• Moving upwards a number of times with ~<num>

Saying main^ is equivalent to "the first parent of main".
main^^ is the grandparent (second-generation ancestor) of main!

```
Git checkout main^
Git checkout mainˆˆ
```

## Git Merge 

Checkout the branch where you want to merge into and then use the merge command 
```
> git checkout B                  # Check out the target branch.
> git pull --rebase               # Rebase (to ensure your branch is up-to-date).
> git merge origin/A --no-ff      # Merge branch origin/A into branch B (without fast-forwarding).
> git mergetool                   # Resolve conflicts...
> git add <resolved_files>        # Add fixed files.
> git merge --continue
# Test...
> git push origin B:refs/for/B    # Push back to Gerrit.
```

## Branch Forcing 
You're an expert on relative refs now, so let's actually use them for something.
One of the most common ways I use relative refs is to move branches around. You can directly reassign a branch to a commit with the -f option. So something like:
git branch -f main HEAD~3
moves (by force) the main branch to three parents behind HEAD.


## Git Reset
git reset reverts changes by moving a branch reference backwards in time to an older commit. In this sense you can think of it as "rewriting history;" git reset will move a branch backwards as if the commit had never been made in the first place.

## Git Revert
While resetting works great for local branches on your own machine, its method of "rewriting history" doesn't work for remote branches that others are using.
In order to reverse changes and share those reversed changes with others, we need to use git revert. Let's see it in action.

git cherry-pick. It takes on the following form:
```
	• git cherry-pick <Commit1> <Commit2> <...>

```
It's a very straightforward way of saying that you would like to copy a series of commits below your current location (HEAD). I personally love cherry-pick because there is very little magic involved and it's easy to understand.


## Git Interactive Rebase
Git cherry-pick is great when you know which commits you want (and you know their corresponding hashes) -- it's hard to beat the simplicity it provides.
But what about the situation where you don't know what commits you want? Thankfully git has you covered there as well! We can use interactive rebasing for this -- it's the best way to review a series of commits you're about to rebase.
```
Git commit --ammend
```

## Git Tags
As you have learned from previous lessons, branches are easy to move around and often refer to different commits as work is completed on them. Branches are easily mutated, often temporary, and always changing.
If that's the case, you may be wondering if there's a way to permanently mark historical points in your project's history. For things like major releases and big merges, is there any way to mark these commits with something more permanent than a branch?
You bet there is! Git tags support this exact use case -- they (somewhat) permanently mark certain commits as "milestones" that you can then reference like a branch.
More importantly though, they never move as more commits are created. You can't "check out" a tag and then complete work on that tag -- tags exist as anchors in the commit tree that designate certain spots.

## Git Describe
Because tags serve as such great "anchors" in the codebase, git has a command to describewhere you are relative to the closest "anchor" (aka tag). And that command is called git describe!
Git describe can help you get your bearings after you've moved many commits backwards or forwards in history; this can happen after you've completed a git bisect (a debugging search) or when sitting down at a coworkers computer who just got back from vacation.

Git describe takes the form of:
git describe <ref>
Where <ref> is anything git can resolve into a commit. If you don't specify a ref, git just uses where you're checked out right now (HEAD).
The output of the command looks like:
<tag>_<numCommits>_g<hash>
Where tag is the closest ancestor tag in history, numCommits is how many commits away that tag is, and <hash> is the hash of the commit being described.


