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

`git reset HEAD~<Anzahl-Commits>`

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

