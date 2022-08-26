# Git Fuckup Workshop

## Fuckup not commited so far

`git reset` => takes already added changes away (but keeps them!)
`git reset --hard` => alle meine Changes seit letztem Commit wegmachen!

## Fuckup - already commited (but not pushed)

`git reset HEAD~<Anzahl-Commits>`
Beispiel: `git reset HEAD~2` (letzte zwei Commits rückgängig machen)

Beispiel main branch auf remote Stand der Kollegen zurücksetzen
`git reset --hard origin/main`

## Fuckup already pushed