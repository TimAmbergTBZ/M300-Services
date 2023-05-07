# Container #
## Was ist ein Container: ##
Container-Virtualisierung ist eine Technik der Virtualisierung auf Betriebssystemebene, bei der eine Anwendung und ihre Abhängigkeiten in einem Container-Image zusammengefasst werden und dann in einer isolierten Umgebung, die als Container bezeichnet wird, ausgeführt werden.

Ein Container ist ein leichtgewichtiges und portables ausführbares Paket, das alle erforderlichen Dateien, Bibliotheken und Abhängigkeiten enthält, die zum Ausführen einer Anwendung benötigt werden. Es isoliert die Anwendung vom Host-System und anderen Containern und stellt sicher, dass sie über eigene dedizierte Ressourcen wie CPU, Arbeitsspeicher und Festplattenspeicher verfügt.

Die Containerisierungstechnologie ermöglicht es Anwendungen, konsistent über verschiedene Umgebungen wie Entwicklung, Test und Produktion hinweg auszuführen, ohne Änderungen vornehmen zu müssen. Es erleichtert auch Entwicklern das Erstellen und Bereitstellen von Anwendungen, indem der Bereitstellungsprozess vereinfacht und der Overhead bei der Verwaltung komplexer Infrastrukturen reduziert wird.

Die Containerisierungstechnologie hat in den letzten Jahren immense Popularität erlangt, da sie Unternehmen dabei hilft, Softwareanwendungen schneller, zuverlässiger und mit größerer Skalierbarkeit zu entwickeln und bereitzustellen. Zu den beliebten Containerisierungstechnologien gehören Docker, Kubernetes und Docker Swarm.

 ### Wichtigste Merkmale von Containern: ###

 - Container teilen sich Ressourcen mit dem Host-Betriebssystem
 - Container können im Bruchteil einer Sekunde gestartet und gestoppt werden
Anwendungen, die in Containern laufen, verursachen wenig bis gar keinen Overhead
- Container sind portierbar --> Fertig mit "Aber bei mir auf dem Rechner lief es doch!"
 - Container sind leichtgewichtig, d.h. es können dutzende parallel betrieben werden.
 - Container sind "Cloud-ready"!
  ### MicroServices ###
Microservices sind eine Architektur für Softwareanwendungen, bei der eine Anwendung aus kleinen, unabhängigen und leichtgewichtigen Komponenten besteht, die als Services bezeichnet werden. Jeder Service hat seine eigene spezifische Funktionalität und kann unabhängig von anderen Services entwickelt, bereitgestellt und skaliert werden. Die Services kommunizieren über eine klare, standardisierte Schnittstelle miteinander und können in verschiedenen Programmiersprachen und Technologien entwickelt werden. Die Verwendung von Microservices ermöglicht es Entwicklern, schneller und effektiver auf Änderungen und Anforderungen zu reagieren, da sie nur den Service aktualisieren müssen, der betroffen ist, anstatt die gesamte Anwendung zu aktualisieren.
## Docker ##
Docker ist eine Software-Plattform für die Erstellung, Bereitstellung und Ausführung von Anwendungen in Containern. Mit Docker können Entwickler Anwendungen in einer isolierten Umgebung entwickeln und testen und dann diese Anwendungen einfach auf verschiedenen Servern bereitstellen, ohne sich um die unterschiedliche Umgebung kümmern zu müssen.
## Docker Architektur ##
Nachfolgend sind die wichtigsten Komponenten von Docker aufgelistet:
 - ### Docker Deamon ### 

Erstellen, Ausführen und Überwachen der Container
Bauen und Speichern von Images

Der Docker Daemon wird normalerweise durch das Host-Betriebssystem gestartet.
 - ### Docker Client ### 

Docker wird über die Kommandozeile (CLI) mittels des Docker Clients bedient
Kommuniziert per HTTP REST mit dem Docker Daemon

Da die gesamte Kommunikation über HTTP abläuft, ist es einfach, sich mit entfernten Docker Daemons zu verbinden und Bindings an Programmiersprachen zu entwickeln.
 - ### Images ### 

Images sind gebuildete Umgebungen welche als Container gestartet werden können
Images sind nicht veränderbar, sondern können nur neu gebuildet werden.
Images bestehen aus Namen und Version (TAG), z.B. ubuntu:16.04.

Wird keine Version angegeben wird automatisch :latest angefügt.



### Container ### 

Container sind die ausgeführten Images
Ein Image kann beliebig oft als Container ausgeführt werden
Container bzw. deren Inhalte können verändert werden, dazu werden sogenannte Union File Systems verwendet, welche nur die Änderungen zum original Image speichern.

![DockerTechVisualized](1.png)

### Docker Registry ### 

In Docker Registries werden Images abgelegt und verteilt

Die Standard-Registry ist der Docker Hub, auf dem tausende öffentlich verfügbarer Images zur Verfügung stehen, aber auch "offizielle" Images.
Viele Organisationen und Firmen nutzen eigene Registries, um kommerzielle oder "private" Images zu hosten, aber auch um den Overhead zu vermeiden, der mit dem Herunterladen von Images über das Internet einhergeht.
Ein Dockerfile ist eine Textdatei, die eine Reihe von Anweisungen enthält, die Docker verwenden kann, um ein Docker-Image zu erstellen. Mit einem Dockerfile können Entwickler und Systemadministratoren eine Standardkonfiguration für ihre Anwendungen definieren und das Erstellen und Verteilen von Container-Images automatisieren. Das Dockerfile enthält Informationen wie die Ausgangsbasis für das Image, die erforderlichen Abhängigkeiten, die Anwendungskonfiguration und andere relevante Details. Mit diesem einfachen Textformat können komplexe Container-Images erstellt und verwalten werden, was zu einer effizienten und zuverlässigen Bereitstellung von Anwendungen führt.
## Docker Commands ##

- **Image Commands**
  - `docker build`: Build an image from a Dockerfile
  - `docker pull`: Pull an image from a registry
  - `docker push`: Push an image to a registry
  - `docker images`: List images on your system
  - `docker rmi`: Remove one or more images from your system

- **Container Commands**
  - `docker run`: Create a new container and start it
  - `docker start`: Start a stopped container
  - `docker stop`: Stop a running container
  - `docker rm`: Remove one or more containers from your system
  - `docker ps`: List running containers
  - `docker logs`: View the logs of a container
  - `docker exec`: Run a command in a running container

- **Networking Commands**
  - `docker network create`: Create a new network
  - `docker network ls`: List all networks
  - `docker network connect`: Connect a container to a network
  - `docker network disconnect`: Disconnect a container from a network

- **Volume Commands**
  - `docker volume create`: Create a new volume
  - `docker volume ls`: List all volumes
  - `docker volume rm`: Remove one or more volumes from your system
  - `docker run -v`: Mount a volume to a container

- **Other Commands**
  - `docker login`: Log in to a registry
  - `docker logout`: Log out of a registry
  - `docker info`: Display system-wide information about Docker

## Docker Configuration ##
Stellen Sie sich vor, Sie lassen einen Webserver in einem Container laufen. Wie können Sie dann der Aussenwelt darauf Zugriff gewähren?

Man muss Ports nach aussen mit folgendem Command öffnen:

```
docker -p
``` 
Danach führen wir diesen Command aus, um den Container neuzustarten.
```
docker run --rm -d -P mysql
```

ich habe ein SQL Container Image wiefolgt heruntergeladen:
```bash
sudo docker pull mcr.microsoft.com/mssql/server:2022-latest
```
 Danach habe ich folgenden Command ausgeführt:
 ```bash
 sudo docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong@Passw0rd>" \
   -p 1433:1433 --name sql1 --hostname sql1 \
   -d \
   mcr.microsoft.com/mssql/server:2022-latest
```
Hiermit habe ich das Image gestartet.

Wenn wir jetzt den command:
```bash
sudo docker ps
```
ausführen, dann gilt es zu erwarten, das wir nun unseren gestarteten Container in der Liste sehen würden:
![List_Of_Containers](Screenshots/WorkingContainer.png)

Und wie wir sehen, wird der Container richtig angezeigt.

## 03 - Netzwerk-Anbindung ##
Jetzt wollen wir den mySQL Container permanent an den Hostport 3306 weiterleiten:
```bash
docker run --rm -d -p 3306:3306 mysql
```



Volumes
===

[&uarr; nach oben](https://github.com/Silvan-Mattig/M300-Services/tree/main/30-Container#m300---30-container)

Bisher gingen alle Änderungen im Dateisystem verloren, wenn der Docker-Container gelöscht wurde. Um Daten auch über das Löschen des Containers hinaus zu erhalten, bietet Docker verschiedene Optionen:

* Daten auf dem Host ablegen: Man kann die Daten auf dem Hostsystem speichern, auf dem Docker läuft. Dadurch bleiben die Daten auch erhalten, wenn der Container gelöscht wird.

* Daten zwischen Containern teilen: Man kann Daten zwischen verschiedenen Containern teilen. Dadurch können mehrere Container auf dieselben Daten zugreifen und die Daten bleiben erhalten, auch wenn einer der Container gelöscht wird.

* Eigene Volumes erstellen: Man kann eigene Volumes erstellen, um Daten zu speichern. Diese Volumes sind unabhängig vom Container und können auch von anderen Containern genutzt werden. Dadurch bleiben die Daten erhalten, auch wenn der Container gelöscht wird.

Diese Optionen erlauben es, Daten auch über das Löschen eines Containers hinaus zu behalten und erleichtern die Verwaltung von Daten in Docker-Containern.

## Volume - Verzeichnis ##

Ein Volume ist ein spezielles Verzeichnis auf dem Hostsystem, in dem ein oder mehrere Docker-Container ihre Daten speichern können. Volumes bieten verschiedene nützliche Funktionen für die Verwaltung von persistenter oder gemeinsam genutzter Daten.

## Wie erstellt man ein neues Volume /data Verzeichnis? ##

Man muss den Folgenden Befehl einggeben, dass ein neues Docker Volume angelegt wird.

```
docker volume create data
```

Mit dem Folgenden Befehl kann man Überprüfen, ob der Befehl funktioniert hat. Somit werden alle verfügbaren Docker-Volumes aufgelistet.
```
docker volume ls
```

Damit man das Volume verwenden kann, muss man die folgenden Zeilen im Docker-Compose hinzufügen. Smoit wird "my-data" durch den gewünschten Namen des Volumes ersetzt.
```
volumes:
  my-data:
```

## Datencontainer ##

Wie starten man einen Container? Und wie kommen andere Personen darauf?

Um den Container zu starten, muss man den folgenden Befehl eingeben:
```
docker run
```
Um auf ein Container zugreifen zukönnen, muss man folgenden Behfel eingeben:
```
--volumes-from
```

## Named Volumes ##

Docker Volume ist seit Version 1.9 ein wichtiger Befehl, zur Verwaltung von Volumes auf einem Docker Host. Mit dem Befehl kann man ganz viele Sachen verwalten. Alle diese hier aufzuzählen macht aber keinen Sinn.


Image-Bereitstellung
===

[&uarr; nach oben](https://github.com/Silvan-Mattig/M300-Services/tree/main/30-Container#m300---30-container)

Es existieren zahlreiche Optionen, um Images bereitzustellen. Man kann sie durch das Erstellen von Dockerfiles erstellen, von einer Registry mit "docker pull" herunterladen oder mithilfe von "docker load" aus einer Archivdatei installieren.

## Namensgebung für Images ##

Images bestehen aus einem Namen und einer Version, wobei bei fehlender Angabe automatisch ":latest" hinzugefügt wird. Um Images bereitzustellen, sind präzise und beschreibende Namen und Tags von entscheidender Bedeutung. Die Namen und Tags werden entweder beim Bauen der Images oder durch den Befehl "docker tag" festgelegt.

Bei den Tag-Namen muss man auf ein Paar Sachen achten:

* Gross- und Kleinbuchstaben
* Zahlen
* Symbolen . und -
* nicht länger als 128 Zeichen
* erstes Zeichen kein . oder -

Bei der Entwicklung eines Workflows ist es äußerst wichtig, sinnvolle Namen für Repositories und Tags zu verwenden. Docker hat nur wenige Einschränkungen bezüglich der Namensgebung und erlaubt jederzeit die Erstellung oder Löschung von Namen. Es obliegt also dem Entwicklungsteam, ein angemessenes Namensschema zu entwerfen und anzuwenden

## Warnung vor dem latest-Tag ##

Wenn bei einem "docker run" oder "docker pull" Befehl kein spezifischer Tag angegeben wird, verwendet Docker standardmäßig das Image, das mit "latest" gekennzeichnet ist. Wenn kein solches Image vorhanden ist, wird eine Fehlermeldung ausgegeben.

# Docker Hub #

[&uarr; nach oben](https://github.com/Silvan-Mattig/M300-Services/tree/main/30-Container#m300---30-container)

Ein eigenes Images bereitzustellen ist am einfachsten, wenn man Dockers Hub verwendet.

Das Hub ist soweit kostenlos, man kann aber auch für Repositories von privaten Personen zahlen.

## Docker Hub einrichten ##

1. Zuerst muss man achten, dass man einen Docker Hub Account hat.
2. Image erstellen

```
docker tag mysql username/mysql
```

3. Um das Image hochzuladen, muss man den Befehl push mit verwenden.

```
docker push username/mysql
```

Dannach muss das Image noch beschrieben werden.

## Weitere Befehle ##

Nach einem Image kann man suchen mit folgendem Befehl:

```
docker search mysql
```
Um ein Image herunterzuladen, muss man den befehl pull verwenden:

```
docker pull ubuntu
```

# Export/Import von Container und Images #

[&uarr; nach oben](https://github.com/Silvan-Mattig/M300-Services/tree/main/30-Container#m300---30-container)

Damit man Images zwischen zwei Hots hin und her verschieben kann, braucht man die Befehle docker export und docker import. Damit man Verzeichnisse hin und her kopieren kann, verwenden wir docker save und docker load.
```
docker export
```

```
docker import
```


Um seine eigenen Images sehen zu können, muss man folgenden Befehl ausführen:

```
/vagrant/mysql$ docker images
```
Wie kann ich mein Images wiederherstellen?

```
docker load
```


## TAR-Format ##

Das TAR-Format dient der Archivierung und Komprimierung von Dateien und Verzeichnissen und hat seinen Ursprung in der Sicherung von Daten auf Magnetbändern. Heutzutage wird es oft verwendet, um Dateien in einer einzelnen, komprimierten Datei für die Übertragung oder Speicherung zu archivieren. Um die Dateigröße weiter zu reduzieren, können TAR-Dateien mit verschiedenen Komprimierungsverfahren wie Gzip, bzip2 oder XZ komprimiert werden. Im Bereich von Docker-Images werden TAR-Dateien häufig als Archivdateien verwendet.

# Private Registry #

[&uarr; nach oben](https://github.com/Silvan-Mattig/M300-Services/tree/main/30-Container#m300---30-container)

Es gibt verschiedene Möglichkeiten, Images neben dem Docker Hub bereitzustellen, aber die manuelle Erstellung oder der Export/Import von Images sind suboptimale Optionen. Das Erstellen von Images aus Dockerfiles auf jedem Host ist langsam und kann zu unterschiedlichen Images führen, während das Exportieren und Importieren von Images knifflig und fehleranfällig sein kann. Stattdessen wird empfohlen, eine andere Registry zu verwenden, die selbst gehostet oder von einem anderen Unternehmen betrieben wird.