**Git kurz erklärt:**

Git ist eine dezentrales Versionsverwaltungstools. D. h. jeder hat local eine komplette Kopie des Repos (im Gegensatz zu SVN).
Mann kann also ohne Internet Verbindung arbeiten (commiten, branches erstellen, etc.).

**Starten:**

`git clone https://github.com/Buntelrus/gso-eva.git Ordner-Name`

hiermit 'klonen' wir das Repository in einen beliebigen Ordner. Man kann letztere Angabe auch weglassen. Dann wird das Repository
nach 'gso-eva' geklont.

Nun haben wir eine Kopie des gesamten Repositories. In dem Ordner '.git' befinden sich alle Git relevanten Dateien. In unserem
Worktree (gso-eva) befinden sich nun die Dateien des Branches 'master'. Dieser repräsentiert i. d. R. den 'live Stand'.
Man kann andere Branches auschecken mit:

`git checkout branchname`

Neue branches erstellt man am besten mit:

`git checkout -b new-branchname`

dieses Komando erstellt auf Basis des aktuellen HEAD einen neuen Branch Namens 'new-branchname' und checkt diesen anschließend aus.


**Änderungen commiten:**

Git kennt 3 verschiedene Status von Dateien. Zum einen haben wir unversioniert Dateien. Dann Dateien, die zum Commit vorgemerkt
sind. Und die, die versioniert sind. Fügen wir eine neue Datei hinzu so ist diese unversioniert.

`git add file.txt`

fügt diese zum Index hinzu. Anschließend kann diese mit

`git commit`

commited werden. Mit

`git status`

können wir uns eine Liste der geänderten Dateien und ihren 'Status' anzeigen lassen.

**Fehler berichtigen:**

Achtung! folgende Befehle sollten nur nach Rücksprache mit dem Team angewendet werden, wenn Sie bereits gepushte commits betreffen.

Haben wir uns beim vorherigen commit vertan (bei d. commit message oder den Änderungen) können wir mit

`git commit --amend`

den letzten commit verbessern.

Wollen wir Änderungen bis zu einem Zeit Punkt x rückgängig machen so können wir das mit 

`git reset`

machen. Dabei unterscheidet 'git reest' 3 Verhaltensweisen:

`git reset --soft` setzt das Repository auf commit x zurück und behält Änderungen im Index.

`git reset [--mixed]` setzt das Repository auf commit x zurück und behält Änderungen **nicht** im Index.

`git reset --hard` setzt das Repository auf commit x zurück und ändert die Dateien im Workingtree.

Beispiel: `git reset --hard HEAD~3` würde die letzten 3 commits ungeschehen machen.

**Branches zusammenführen:**

wir möchten branch 'feature-ABC' mit branch 'develop' zusammenführen:

Dafür haben wir zwei Möglichkeiten:

1. `git merge` git merged die branches und erzeugt einen merge commit(ggf. muss fastforward ausgeschaltet werden).

`git checkout develop` checke 'develop' aus

`git merge feature-ABC` merge Änderungen aus 'feature-ABC' in den 'develop'

2. `git rebase` git erzeugt neue commits und wendet diese auf einen branch oder commit an.

`git checkout feature-ABC` checke 'feature-ABC' aus

`git rebase develop` wende Änderungen von 'feature-ABC' auf 'develop' an.

**Änderungen für alle zugänglich machen**

Bisher haben wir nur lokal gearbeitet. Damit wir unsere Arbeit nun anderen Teammitgliedern zur Verfügung stellen können,
stelle ich euch nun die Befehle `git push` und `git pull` vor. Bevor wir Änderungen 'pushen', 'pullen' wir. Dazu wechseln
wir in den Branch den wir pushen möchten.

`git checkout feature-EveryTeamateNeeds`

anschließend holen wir alle Änderungen, die andere Teammitglieder gemacht haben.

`git pull` dabei ist zu beachten, dass der upstream branch richtig gesetzt ist. Genauere Infos darüber erhaltet ihr von git.
oder:

`git pull origin feature-EveryTeamateNeeds` origin ist der name des remote repositories.

`git commit -am 'some changes'` -a fügt geänderte Dateien dem Index hinzu. -m definiert eine commit message.

`git push` überträgt die Änderungen 'some changes' ins remote repository.
oder:

`git push origin feature-EveryTeamateNeeds feature-XY` überträgt die Änderungen von 'EveryTeamateNeeds' und 'feature-XY'
ins 'origin' repository

Vorsicht! mit den hier vorgestellten Befehlen
`git commit --amend`
`git reset`
`git rebase`
lassen sich commits bearbeiten, die bereits im remote repository sind. Diese Änerungen sollten nur nach Rücksprache mit den
anderen Teammitgliedern gepusht werden. A natürlich können so bei anderen unnötige Konflikte enstehen und B verweisen Branches
immer auf den commit, wo sie erstellt wurden. Ändert sich nun dieser commit zeigt der branch quasi aufs Nichts. Das lässt sich
zwar auch alles wieder beheben. Aber besser nicht machen ;). Falls es doch mal notwenig wird:

`git push -f` für force

**Sonstiges**

Ich weiß das git auch eine GUI unter Windows mit bringt. Diese benutze ich allerdings nicht, daher kann ich dazu nicht viel sagen.
Für die Linux nutzer unter uns kann ich gitg empfehlen. Dies ist ein Tool, welches die git history ganz gut grafisch darstellt.
Die IDEs von JetBrains haben ebenfalls eine hervoragende Git Integration (auch mit Grafischer Ansicht). Wie das mit Eclipse aussieht weiß ich nicht.
Für diejenigen, die sich die Historie lieber in der Konsole angucken, denen rate ich mal ein Blick auf `git log` zu werfen.

Ich hoffe das hilft um einen kleinen Einstieg in git zu bekommen. Ich nehme keinerlei Gewähr für Tippfehler und vollständig
ist das ganze hier natürlich auch nicht. Wenn ihr mehr wissen wollt, tut die Git Dokumentation, wie ich finde, einen sehr guten Job.
Sollte ich etwas wichtiges vergessen haben, könnt ihr dieses Dokument natürlich gerne erweitern.