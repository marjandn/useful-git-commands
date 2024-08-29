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

Reapply Commits on a New Base: It allows you to move or "reapply" a series of commits from one base commit to another.
Linearize Commit History: Rebasing rewrites the commit history by creating new commits with the same changes as the original ones, but with different parent commits. This results in a linear commit history, as opposed to the sometimes complex history produced by merging branches.

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
### Tags are Immutable
tags unlike branches are immutable and when you check out to them the HEAD will be detached it means you're not on any branch and you can't commit your changes so **you have to create a branch after checking out a tag** and do your changes on that branch.
