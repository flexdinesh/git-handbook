# Git Handbook

Handbook on how to use git commands and strategies that make life easier.

## Sections

- [Useful commands](#useful-commands)
    - [Log](#log)
    - [Branch](#branch)
    - [Rebase](#rebase)
    - [Push](#push)
    - [Commit](#commit)
    - [Stash](#stash)
    - [Reset](#reset)
    - [Cherry Pick](#cherry-pick)
- [Merge strategies](#merge-strategies)
    - [Rebasing](#rebasing)

## Useful commands

### Log
`git log --oneline --graph --decorate`

View the log in a useful and concise way

### Branch
`git checkout -b branch-name-goes-here`

Create a new branch from current branch

`git checkout branch-name`

Checkout the code of existing branch

`git checkout -`

Checkout previous branch 

### Rebase
`git rebase main`

Rebase current branch against main

`git rebase --abort`

Abort current rebase in progress and revert to the state before rebase

`git rebase --continue`

After resolving merge conflicts during a rebase, continue with rebasing.

`git rebase -i HEAD~3`

Enter into interactive rebase mode with top 3 commits in current branch. This is how you squash/reword/discard commits in local branch.

### Push

`git push origin HEAD`

Push the current branch to remote (the command will auto create remote ref if it doesn't exist)

`git push origin HEAD --force-with-lease`

Force push current branch to remote but don't override remote if someone else's changes are there. Need to do this after rebase, amend or anything that rewrites history

### Commit
`git commit --amend --no-edit`

Amend the last commit (HEAD) with new changes. This will rewrite history so you will have to force push after this.

`git commit --amend -m "new desc"`

Amend the last commit (HEAD) with a new commit message. This will rewrite history so you will have to force push after this.

### Stash

`git stash save`

Save all current tracked (staged and unstaged) files to stash. If you want to stash an untracked file (newly created file).

`git stash save stash-name-goes-here`

Save to stash with a descriptive name

`git stash apply n`

Apply a particular stash index (0-n)

### Reset

`git reset --hard origin/main`

Reset current branch to the state of remote main

`git reset --mixed HEAD~2`

Pop the last two commits in the current branch but preserve the changes from those commits in the staging area

`git checkout .`

Discard all tracked local changes. Untracked files (newly created files) won't be affected.

### Cherry Pick

`git cherry-pick commit-hash`

Cherry pick that commit and apply it to current branch

`git cherry-pick commit-hash commit-hash`

Cherry pick all listed commits and apply it on current branch

## Merge Strategies

### Rebasing

**Step 1:** Make sure you don't have any merge commits in your current branch. If you do, please don't rebase or you'll have a hard time resolving conflicts repeatedly.

**Step 2:** Make sure you don't have any uncommitted local changes. If you do, stash or commit them.

**Step 3:** (from current branch) `git checkout main`

**Step 4:** `git pull`  (This will fetch latest from origin/main and auto merge to local main. `pull` is just a shorthand for `fetch` and fast-forward `merge`)

**Step 5:** `git checkout -` (This will take you back to your previous branch)

**Step 6:** `git rebase main`

(If you run into conflicts you will need to resolve it manually and stage the changes)

**Step 7:** (once you stage the changes after resolving conflicts) `git rebase --continue`

**Step 8:** Voila! You've now successfully rebased your branch against main.

(If you need to cancel your rebase at any point and revert to old state, you can always run `git rebase --abort` to do that)

## License

MIT © Dinesh Pandiyan
