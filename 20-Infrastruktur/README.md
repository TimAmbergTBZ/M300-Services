# 20-Infrastruktur #

## Vagrant ##


Die Vagrant Installation ist grundsätzlich simpel, Vagrant benötigt Konfigurationsfiles, welche einfach über einen command erstellt werden können. Mit diesen Konfigurationsfiles können eine  beliebige Anzahl VMs erstellt werden.












## Vorgefertigte Boxen/Vagrant Boxen ##

Alternative Boxen sind  bereits vorgefertigte VM-Vorlagen:
Vagrant ist ein Vorraussetztung für boxen.
Zum Beispiel die Vagrant Box: ubuntu/xenial64, welche wir vorhin verwendet haben.

Für die Boxen Erstellung benötigt man 2 Files:
base.sh und
vagrant.sh


Mit "vagrant up" können neue virtuelle Maschienen initialisiert werden. Die Box/das Image (falls es noch nicht lokal verfügbar ist) wird heruntergeladen und installiert.Eine virtuelle Maschine wird erstellt. Dabei werden alle im Vagrantfile festgelegten Konfigurationen berücksichtigt, zum Beispiel Webserver Installation.
vagrant up --provider virtualbox
Mit dem Parameter "--provider virtualbox" wird deklariert, dass Vagrant Virtualbox als Provider verwendet wird. Vagrant unterstützt diverse Virtualisierungssoftwares wie Vmware oder Hyper-V.


### Wichtigste Vagrant Befehle ###

 Befehl       | Beschreibung                                                                  |
|--------------|-------------------------------------------------------------------------------|
| vagrant up     | Startet und provisioniert eine neue virtuelle Maschine                   |
| vagrant ssh      | Verbindet sich per SSH zur laufenden VM         |
| vagrant halt   | Stoppt die laufende VM              |
| vagrant destroy    | Löscht die VM und alle zugehörigen Ressourcen                           |
| vagrant status    | Zeigt den Status aller VMs im aktuellen Verzeichnis an   |
| vagrant init     | Initialisiert ein neues Vagrant-Projekt im Verzeichnis                                |
| vagrant reload   | Neustartet die VM und lädt die Vagrant-Konfiguration                            |
| vagrant suspend    | Pausiert die laufende VM                   |
| vagrant resume   | Nimmt eine pausierte VM wieder auf          |
| vagrant provision      | Führt eine erneute Provisionierung auf der VM durch                               |


## packer ##

Packer hat sehr oft Schwierigkeiten mit Windows Systemen, da Packer nur mit Linux und macOS-Systemen zu funktionieren scheint. Dies liegt daran, dass Packer für Unix-Systeme entwickelt wurde und einige der notwendigen Abhängigkeiten nicht standardmäßig in Windows enthalten sind. Wenn Sie also Packer verwenden möchten, empfehle ich Ihnen eine Linux- oder macOS-Maschine zu verwenden, damit das Programm reibungslos und frustfrei funktioniert. Ich persönlich habe selber versucht, Packer auf Windows zum laufen zu bringen, jedoch führt das Programm seine Grundfunktionen einfach nicht aus, da ihm vermutlich eine wichtige Funktion fehlt.

Ich habe jedoch eine gute Anleitung gefunden, welche die Installation von packer auf unix-basierten Systemen schildert:

Bevor man beginnt, sollte man immer sichergehen, dass das Paket-Repository aktuell ist.
```bash
sudo apt-get update
```
Das Paket "unzip" wird für Packer benötigt, um Archivdateien zu extrahieren. Desshalb sollten sie es installieren.
```bash
sudo apt-get install unzip
```
Unter diesem Link können Sie Packer herunterladen. Nehmen Sie jeweils die neuste stabile Version. Sie können den Download-Link auf der Seite https://www.packer.io/downloads finden
```bash
wget https://www.packer.io/downloads
```
Entpacken Sie das heruntergeladene Packer-Archiv hier: 
```
/usr/local/bin/
```
```bash
sudo unzip packer_*_linux_amd64.zip -d /usr/local/bin/
```
```bash
packer version
```
Wenn alles richtig funktioniert hat, sollte im terminal nun die Packer version angeziegt werde, welche Sie installiert haben. Falls nicht, hat es ein Installationsfehler gegeben.

Packer funktioniert mit .json files. Wenn Sie ein solches File haben, können Sie dies mit Packer öffnen. Jetzt sollte die respektive VM erstellt werden.
## AWS ##

Auch die Installation bei der AWS Aufgabe hat Probleme mit Windows. 
Das AWS Plugin wird leider nicht mehr weiterentwickelt und ist desswegen nicht mit Windows kompatibel. Eine ältere Version des Plugins hat anscheindend zu einem Zeitpunkt mit Windows funktioniert, diese Version ist leider nicht mehr erhältlich.
