# Git Fuckup Workshop

## Seeing all your commits and commit numbers

`git log --oneline`


## Fuckup - not commited so far

`git reset` 
- takes already added changes away (but keeps them!)
- we can edit our faulty stuff and then commit it

`git reset --hard`
- remove all my changes i did since last commit

## Fuckup - already commited (but not pushed)

In the next sections We will now deal often with the so-called "HEAD" commit. That simply is the LATEST commit that was done in your current branch. 

Remove commits: 

`git reset HEAD~<Amount-of-Commits>`

Example: `git reset HEAD~2` (remove latest two commits, but keep the code to fix it)

Example: main branch got completeley messed up => restore local main branch back to latest state of main on GitHub 

`git checkout main`
`git reset --hard origin/main`

## Fuckup already pushed

Create revert commit for latest commit

`git revert HEAD`

This will NOT delete the last commit. It will UNDO this commit by creating a NEW commit which undoes the changes of that commit / restores them.

Revert specific commit

`git revert <Commit-Nr>` // revert the changes done in that specific commit

This will again create a new commit which undos the changes from the given commit (e.g. if you added 3 lines to README in that commit, that command will delete that 3 lines again).

### Caution

`git revert HEAD~3`

This will NOT undo the latest three commits. Revert always just addresses ONE commit. Instead we can do

`git revert --no-commit HEAD~3..HEAD`

This will revert all commit between LAST commit (=HEAD) and the last three commits.

The "--no-commit" command prevents that you create three new invert commits. Instead it just undoes all the changes and now you can add and commit them in ONE commit (which is a bit cleaner):

`git add . && git commit -m "I restored the world!" `


In case you want to revert multiple, specific commits, not just "the last ones", you have to revert EVERY SINGLE commit by its hash:

- `git revert --no-commit 17b787d784065c`
- `git revert --no-commit 1fefb57`
- `git revert --no-commit 8b3560b`

And afterwards: 

`git add . && git commit -m "I restored the world!" `

## File code wrong / outdated

At some point when we start our app or we work on a file in the project after some time, we realize something is wrong.

Some code on the file has an outdated state! Or code is completely missing. Maybe after a merge where we e.g. resolved the conflict wrong / deleting accidentally some code that was valid.

If one or several files have unexpected code or code in a file is suddenly missing, we can fortunately check the history of that file. And can restore every state it had in the past!

Therefore we can use the command "git log" which usually shows us the list of our commits in a branch.

Using the "--name-status" flag we can additionally list the FILES that where changed in each commit. 
And WHICH operation was done on the file (A - Added, M - Modified, D - deleted)

Example:
`git log --oneline --name-status`

Gives e.g. this output:
```
b967d3a (HEAD -> main) Added F3
A       f3.js
75a225a Deleted F2
D       f2.js
5e5034d Added F2, Update F1
M       f1.js
A       f2.js
102a5cc Added F1
A       f1.js
```

Aha! Now we see, how the files developed: E.g. f1.js was created and commited the first time to our branch in commit 102a5cc.

File f1.js then was modified the first time in commit 5e5034d. 
And f2.js was deleted in commit 75a225a.

Now often we are not interested in ALL the dozens of file changes, we usually check a specific file.

Using the "--" flag afterwards, we can search the history for a specific FILE. 

`git log --oneline --name-status -- *<filename>`

Example - We look for the history just of f1.js (because the last code change does not fit):

`git log --oneline --name-status -- *f1.js`

This gives us now just the history of f1.js changes:

```
5e5034d Added F2, Update F1
M       f1.js
102a5cc Added F1
A       f1.js
```

We see: 
In Commit 5e3034d the file was modified (=M) the last time.
In Commit 102a5cc ist was added (=A) the first time.

We can now check exactly the state the file had in these commits, e.g. in Commit 102a5cc - with the "git show" command:

`git show 102a5cc -- *f1.js`

Using git show we now see the exact code change on file f1.js that was done in Commit 102a5cc.

In case we wanna have these lines back, we could now simply copy & paste these lines and add them back in.

Alternatively we can restore the complete file from that commit:

`git checkout -f 102a5cc -- *f1.js`

Using the -- flag we can checkout not just a branch, we can also checkout an individual file (!) only. From any previous commit. Super Handy!

Now it replaces your current / messed up version of f1.js in your branch with that previous one. But you still need to add and commit that change, so tell git that you REALLY wanna get back to that old state of the file.

Fortunately in Git we can restore almost everything. If we know how :)

Happy Time Traveling!


## Completely messed up my local branch

Sometimes we somehow get into a situation where we have our branch completely messed up. Often after a merge with some outdated branch. Or we had unsolved conflicts and used "git add ." and accidentally commited all that conflicts to our repo! Or we deleted accidentally some commits. Or or or. Humans can be super creative when it comes to destruction.

In case we e.g. merged a branch, that had recent changes from our colleagues and we forgot to pull those changes before we merge that branch into ours.
Now we merged a completely oudated state of that branch into our current branch. 

We can now have two cases:
- We realize DURING the merge, that we merged something outdated and have not resolved all the conflicts so far
- We did NOT realize we deal with an outdated state. And merge all that oudated stuff in, fixed the merge conflicts and finalized the merge already. Nice work for the trashcan :)

Scenario 1 can easily be reverted. By simply ABORT the merge with all the crazy conflicts, using:

`git merge --abort`

This will simply cancel the merge completely. As if it did not happen. Nice!
But that only works, if the merge is still OPEN (=> usually if a merge is not successful / has open conflicts). This "merge in progress" state can always be aborted easily.

A bit trickier is becomes once we finalized that merge already, solving all the conflicts. And now we have that completely messed up state.

Or we did something else and that given branch is totally fucked up, for whatever reason.

In the worst case we cannot even pull from or push to the remote branch anymore. Because of a history diversion between your local (on your PC) and central branch (on GitHub).

And the only thing we want how is get BACK our local branch to the last state of that branch we have on Github! Our last safe haven so to say...

Fortunately, also for that scenario there is a way:

We checkout our messed up branch, e.g. dev: 

`git checkout dev`

Now we fetch the latest changes from GitHub using: 

`git fetch`

And now we harshly replace our LOCAL dev branch with the one on github (=> origin/dev)

We can do this using the git reset command:

`git reset --hard origin/<branchname>`

In this case:
`git reset --hard origin/dev`

WARNING!
This will completely wipe out the state of your local branch and REPLACE it with the branch code on GitHub.

So always make sure you are on the CORRECT branch before doing that.

E.g. you want to restore dev, then do these steps:
```
git checkout dev
git fetch
git reset --hard origin/dev
```

Other example: You want to restore branch "blog":
```
git checkout blog
git fetch
git reset --hard origin/blog
```


So this is usually what we want after a complete messed up state of our branch.
And can often get ourselves out of hell again! Finally!
