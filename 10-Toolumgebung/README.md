# 10-Toolumgebung 

## GitHub ##

### GitHub Account erstellen###

Ein GitHub Account kann unter www.github.com erstellt werden. Ein GitHub Account ist eine Voraussetztung für die folgenden Schritte.

## SSH Key ##

### SSH Key erstellen ###

Wir benötigen ein SSH Key, um den Austausch zwischen unserem lokalen GitHub Repository zu ermöglichen. Der lokale SSH Key lässt sich wie folgt einfach im Terminal generieren:

ssh-keygen -t rsa -b 4096 -C "beispiel@beispiel.com"

Danach muss man ein Passwort für den Key festlegen.

### SSH-Key dem SSH-Agent hinzufügen ###

Datei %HOME%/.ssh/id_rsa.pub in die Zwischenablage kopieren.

### SSH Key hinzufügen ###

Man melde sich auf GitHub an.
Jetzt auf new key klicken und den genrierten Key einfügen.








## Vagrant und VirtualBox ##

Mit Vagrant kann man virtuelle Maschienen erstellen.

Eine normale VM kann man mit folgenden Befehlen erstellen:

vagrant init %Betriebsystem%

zum Beispiel: 

vagrant init ubuntu/xenial64

### Wo sind Probleme aufgetreten ###

Die von Hand installierte Ubuntu VM musste mehrmals installiert werden, bevor diese richtig korrekt eingerichtet wurde.

Der SSH Key in Gitlab hatte anfangs ein Fehler, sodass ich immer das Passwort eingeben musste, nach einer neueinrichtung hat das jedoch funktioniert.





