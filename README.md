# Git Fuckup Workshop

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

Revert latest n commits

`git revert HEAD~3` // revert latest three commits

`git revert <Commit-Nr>` // revert INCLUDING the commit hash stated
