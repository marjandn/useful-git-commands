# useful-git-commands
Most useful git commands:

## Undoing / Removing changes in all 3 areas:

### Remove Untracked Files ( In the WORKING DIRECTORY stage )
```
git clean -n    #  (Preview of what you'll discard)
git clean -f    #  (Discard only FILES)
git clean -fd   #  (Discard FILES and DIRECTORIES)
```


### Undoing Changes in the Staging Area
Unstages a file that has been added to the staging area, without changing the working directory.
```
git resset <file>
```

### Undoing a Commit ( Repository/History area )
Moves the HEAD pointer to the specified commit, keeping all changes in the staging area.
```
git resset --soft <commit>    # the <commit> code must be that commit you want to set the HEAD to
```

Moves the HEAD pointer to a the specified commit and *discards all changes in the staging area and working directory*.
```
git resset --hard <commit>    # the <commit> code must be that commit you want to set the HEAD to
```

### Undoing a Pushed Commit ( Repository/History area )
*Creates a new commit that reverses the changes made in the specified commit.* This is the safest way to "undo" a commit that has already been pushed to a shared repository because *it doesn’t rewrite history.*
```
git revert <commit>    # the <commit> code must be that commit you want to revert its changes
```

## Log
### Recovering commits
```
git reflog
```

```
git log --oneline
```

## Delete Branch
```
git branch -d feature-m  # Locally
git push origin --delete feature-m  # Remotely
```

## Apply the changes from a particular commit
```
git cherry-pick <hash-of-a-commit>
```

## Rebase / Interactive Rebase

#### Rebase
- Moves your current branch’s commits on top of another branch.
- It rewrites history by applying commits sequentially.
- Often used to keep a feature branch updated with the latest changes from main.
```
git checkout feature-branch
git rebase main
```
- Takes all commits from feature-branch, temporarily removes them.
- Updates feature-branch to the latest version of main.
- Reapplies the removed commits on top of the latest main, making history cleaner and linear.

```
git rebase --continue
```
To complete the process after resolving conflicts.

```
git checkout main
git merge feature-branch --ff-only  # Apply without more commit (if possible)
```

#### Interactive Rebase
```
git rebase -i
```
It allows you to:

- Reorder commits.
- Squash (combine) commits together.
- Edit commit messages.
- Drop commits (remove them from the history).


#### Remove some specific commits from history and discard their changes

1- This command opens an editor with the last 5 commits listed.

```
git rebase -i HEAD~5
```

2- You'll see a list of commits that looks something like this:
```
pick <hash_of_cm5> cm5
pick <hash_of_cm4> cm4
pick <hash_of_cm3> cm3
pick <hash_of_cm2> cm2
pick <hash_of_cm1> cm1
```

3- Remove the Unwanted Commits, Save and Exit.

4- if you want to change history on repository stage 
```
git push origin main --force
```
or the following command which checks if the remote branch has been updated since you last fetched. If someone else has pushed changes, the push will be rejected, preventing potential overwrites of others' work.
```
git push origin main --force-with-lease
```


## Tag
Tags used for making specific point in the project's hisotry as important, mostly used to mark release points or create a reference to an important points like completion of a major feature or the delivery of a critical bug fix.
```
git tag <TagName> <ReferenceCommit>
```
#### See all Tags
```
git tag
```
#### Push Tags
```
git push --tags # Will push all tags
git push origin <tag name> # Will push a certain tag
```
### Tags are Immutable
tags unlike branches are immutable and when you check out to them the HEAD will be detached it means you're not on any branch and you can't commit your changes so **you have to create a branch after checking out a tag** and do your changes on that branch.

#### Replace a Tag
Assume that you have a tag named v1.1.0 with 123 commit refrence number, now you want to change the refrence number of this tag name.
In this case you have to delete this tag (local and remote) and then create a new tag with this name

1- delete the tag locally
```
git tag -d v1.1.0
```

2- delete the tag from remote repository
```
git push origin --delete v1.1.0
```

then you won't have this tag name anymore, and you can create this tag with a new refrence number !


## Stash
Stash command let you to temporarily save changes in your working directory that you don't want to commit them yet, you can change your branch or work on other task while you won't lose your changes.

- Stash files
```
git stash push -m "name of stash"
```

- List of Stashes
```
git stash push -m "name of stash"
```

- Apply and Remove a stash
```
git stash pop stash@{n}
```

- Apply withou Removing
```
git stash apply stash@{n}
```

- Remove a Stash
```
git stash drop stash@{n}
```

- Show difference of Stash content with you working directory
```
git stash show -p stash@{n}
```



