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

Beispiel: `git reset HEAD~2` (letzte zwei Commits rückgängig machen)

Beispiel: main branch lokal zerstört => auf letzten Stand auf GitHub / der Kollegen zurücksetzen

`git reset --hard origin/main`

## Fuckup already pushed

Create revert commit for latest commit

`git revert HEAD`

This will NOT delete the last commit. It will UNDO this commit by creating a NEW commit which undoes the changes of that commit / restores them.

Revert specific commit

`git revert <Commit-Nr>` // revert the changes done in that specific commit

### Caution:

`git revert HEAD~3`

This will NOT undo the latest three commits. 

In case you want to revert multiple commits, You have to revert EVERY SINGLE commit:

- `git revert --no-commit 17b787d784065c`
- `git revert --no-commit 1fefb57`
- `git revert --no-commit 8b3560b`

The "--no-commit" command prevents that you create three new invert commits. Instead it just undoes all the changes and now you can add and commit them in ONE commit (which is a bit cleaner):

`git add . && git commit -m "I restored the world!" `


