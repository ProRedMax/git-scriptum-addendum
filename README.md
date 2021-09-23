# Entfernen von Files aus vorgänger commits in Git

Sollte man unabsichtlich **.class** Files committed haben, welche vom remote als __forbidden__ gelten, kann man diese recht einfach mit wenigen kommandos wieder entfernen.

## Überprüfen der commits

Als erstes müssen wir herausfinden in welchem commit die .class Files committed worden sind.
Dazu verwenden wir den command:

```git
gitk
```

dannach sollte so ein Fenster mit allen commits auftauchen.

Mit einem linksklick auf einen commit kann man ablesen welche Files jeweils committed worden sind. Hat man nun den fehlerhaften commit gefunden, so muss man sich den Commit Hash
des Vorgänger commits kopieren.

## Rebase

Mit dem Kommando:

```git
git rebase -i <Hash des Vorgängercommits>
```
öffnet sich nun ein VI Editor. Ganz oben sind die Nachfolgercommits, mit jeweils einem Prefix __pick__, eingetragen.
Man ersetzt jetzt das Wort __pick__ mit dem Wort __edit__ (Mit I schaltet man in den Insert mode und mit Escape verlässt man diesen wieder)
Schließen erfolgt mit __:wq__

## Entfernen der Class files mit Hilfe des Git GUIs

Nach dem rebase müssen wir die .class Files herausnehmen. Mit dem

```git
git gui
```
ist dies am einfachsten. In dem GUI wählt man nun die Checkbox 'Amend Last Commit' aus. Jetzt erscheinen auf der linken Seite alle Files welche committed worden sind.
Mit einem Linksklick auf das Fileicon kann man das File als unstaged markieren. Wenn man alle .class Files entfernt hat kann man das Fenster wieder schließen.

## Rebase fertigstellen

Mit

```git
git rebase --continue
```

schließen wir unseren __rebase__ ab, und können nun fehlerfrei auf den remote pushen.
Jetzt sollte ein .gitignore File angelegt werden um erneute .class File pushes zu vermeiden.
