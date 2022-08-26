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

