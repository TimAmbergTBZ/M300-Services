M300 - 35 Container-Sicherheit
=== 


Protokollieren & Überwachen
==

In der Informatik ist die Sicherheit immer wichtig. Darum sollte man ebenfalls bei den Container auf die Sicherheit schauen.

Einer der wichtigsten Punkte in der Informatik ist die Protokollierung. Wenn man keine Logging-Software angegeben hat, protokolliert Docker nur das was an STDOUT STDERR geschickt wird.

Wenn du eine Anwendung in einem Docker-Container startest, kannst du überwachen wie gut eine Anwendung läuft, indem du die Ausgabe auf die Standardausgabe (STDOUT) oder die Standardfehlerausgabe (STDERR) sendest. STDOUT und STDERR sind beides Kanäle, über die Anwendungen mit der Umgebung kommunizieren. STDOUT wird standartgemäss für die normale Ausgabe von Programmen verwendet, während STDERR für Fehlermeldungen und Warnungen reserviert ist.

Docker protokolliert standardmäßig alles, was an STDOUT oder STDERR geschickt wird, und speichert die Ausgabe in einem Container-Log-File. Dieses Log-File kann dann verwendet werden, um das Verhalten der Anwendung zu überwachen oder Probleme zu erkennen.

Sinnvoll ist natürlich, dass man diese Logs dann auch anschauen kann. Dazu muss man folgenden Behfel eingeben:

```
docker logs
```

| Logging-Methode | Beschreibung                                                                                     |
|----------------|-------------------------------------------------------------------------------------------------|
| json-file       | Diese Methode schreibt die Container-Logs als JSON-Datei auf die Festplatte des Host-Systems.   |
| syslog          | Diese Methode schickt die Logs an das System-Logging-Tool (syslog) des Host-Systems.           |
| journald        | Diese Methode schickt die Logs an das System-Logging-Tool (journald) des Host-Systems.         |
| splunk          | Diese Methode schickt die Logs an eine Splunk-Instanz. Splunk ist eine Software zur Analyse von Maschinendaten. |
| awslogs         | Diese Methode schickt die Logs an Amazon CloudWatch Logs. CloudWatch Logs ist ein verwalteter Log-Service von Amazon Web Services. |

Diese Liste ist nicht vollständig und es gibt noch weitere Logging-Methoden, die man über --log-driver auswählen kann. Man kann auch eigene Logging-Methoden implementieren, indem man ein Docker-Plugin erstellt.

### Wichtige Behfehle für Standard-Logging ###

| Befehl                                | Beschreibung                                                                                                                                                                      |
|--------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `$ docker run --name logtest ubuntu bash -c 'echo "stdout"; echo "stderr" >>2'` | Startet einen neuen Container `logtest` auf Basis des `ubuntu`-Images. Der Befehl gibt "stdout" auf STDOUT aus und gibt "stderr" auf STDERR aus. |
| `$ docker logs logtest`               | Zeigt die Logs des Containers `logtest` an.                                                                                                                                        |
| `$ docker rm logtest`                 | Entfernt den Container `logtest`.                                                                                                                                                  |
| `$ docker run -d --name streamtest ubuntu bash -c 'while true; do echo "tick"; sleep 1; done;'` | Startet einen neuen Container `streamtest` auf Basis des `ubuntu`-Images. Der Befehl gibt alle Sekunde "tick" aus. |
| `$ docker logs streamtest`            | Zeigt die Logs des Containers `streamtest` an.                                                                                                                                     |
| `$ docker logs streamtest \| wc -l`   | Zählt die Anzahl der Zeilen in den Logs des Containers `streamtest`.                                                                                                              |
| `$ docker rm streamtest`              | Entfernt den Container `streamtest`.                                                                                                                                                |

Protokollierung System-Log des Hosts:
```
    docker run -d --log-driver=syslog ubuntu bash -c 'i=0; while true; do i=$((i+1)); echo "docker $i"; sleep 1; done;'
```
```
    $ tail -f /var/log/syslog
```

### Überwachen und Benachrichtigen ###

Wenn man als System Administrator bei einem Microservices-System arbeitet, muss man sich auf vieles gefasst machen. Deswegen werden in Grossunternehmen immer ein Benachrichtungsdienst integriert. Damit man nicht dutzende Container aufeinmal im Hinterkopf haben muss, gibt es ein Program namens "Container Advisor". Dieses von Google entwicklte Tool gibt einem einen guten Überblick über seine Container. Somit ist die Warscheindlichkeit kleiner, dass ein System unbemerkt ausfällt.

 Da cAdvisor selbst als Container zur Verfügung steht, können wir das Tool in kürzester Zeit einrichten. Gestartet wird der cAdvisor-Container mit folgenden Argumenten:

    $ docker run -d --name cadvisor -v /:/rootfs:ro -v /var/run:/var/run:rw -v /sys:/sys:ro -v /var/lib/docker/:/var/lib/docker:ro -p 8080:8080


 
Container sichern & beschränken
===


## Sicherheitsprobleme ##



## Berechtigungs-Verteilung ##

**Kernel Exploits** <br>
Im Gegensatz zu einer Virtual Machine wird der Kernel von Containern gemeinsam mit dem Host verwendet, wodurch Schwachstellen im Kernel grosse Auswirkungen haben können. Sollte ein Container eine sogennante Kernel Panic verursachen, führt das zum Absturz des gesamten Hosts. In VMs ist die Situation besser, da ein Angreifer den Host und VM Kernel ausser gefecht setzten müsste, um einen totalausfall zzu erzeugen.

**Denial-of-Service-(DoS-)Angriffe** <br>
Alle Container teilen sich die Ressourcen des Kernels. Wenn ein Container den Zugriff auf bestimmte Ressourcen für sich beansprucht, wie beispielsweise Speicher oder User IDs (UIDs), kann er die anderen Container auf dem Host blockieren und so einen Denial-of-Service-Angriff verursachen, bei dem berechtigte Benutzer das System nicht mehr nutzen können.

**Container-Breakouts** <br>
Wenn ein Angreifer Zugriff auf einen Container erhält, sollte er nicht in der Lage sein, auf andere Container oder den Host zuzugreifen. Da die Benutzer nicht durch Namensräume getrennt sind, erben alle Prozesse, die aus dem Container ausbrechen, auf dem Host dieselben Privilegien wie im Container. Wenn man im Container root-Zugriff hat, hat man auch auf dem Host root-Zugriff. Privilege-Escalation-Angriffe müssen ebenfalls berücksichtigt werden, bei denen ein Angreifer mehr Rechte erhält, als ihm zustehen – oft durch einen Fehler im Anwendungscode, der zusätzliche Berechtigungen erfordert. Da sich die Container-Technologie noch in der Anfangsphase befindet, sollte man davon ausgehen, dass Container-Breakouts unwahrscheinlich, aber möglich sind.

**Vergiftete Images** <br>
Es ist schwierig zu wissen, ob die verwendeten Images sicher sind, nicht manipuliert wurden und von der erwarteten Quelle stammen. Ein Angreifer kann einen dazu bringen, sein manipuliertes Image auszuführen und somit sowohl den Host als auch die eigenen Daten gefährden. Es ist auch wichtig sicherzustellen, dass die ausgeführten Images aktuell sind und keine bekannten Sicherheitslücken aufweisen.

**Offengelegte Geheimnisse** <br>
Wenn ein Container auf einen Service oder eine Datenbank zugreift, muss er möglicherweise ein Geheimnis wie einen API-Schlüssel oder Benutzername und Passwort kennen. Wenn ein Angreifer auf dieses Geheimnis zugreifen kann, kann er auch den Service oder die Datenbank verwenden. Dieses Problem wird in einer Microservices-Architektur verschärft, da Container häufig gestoppt und neu gestartet werden. Im Vergleich zu einer Architektur mit einer begrenzten Anzahl von langlebigen VMs ist dies ein erhöhtes Risiko.

## Container absichern ##

Natürlich können die konkreten Schritte zur Absicherung von Containern je nach Anwendungsfall und Umgebung variieren, aber hier sind einige konkrete Beispiele:

1. Verwenden von Images von vertrauenswürdigen Quellen oder von internen Registern, um sicherzustellen, dass die Images keine Malware oder andere bösartige Software enthalten.

2. Vermeiden von der Ausführung von Containern mit root-Privilegien, um zu verhindern, dass Angreifer auf Kernel-Ebene oder darüber hinaus gelangen können.

3. Begrenzen von Ressourcen (z.B. Speicher oder CPU) für jeden Container, um DoS-Angriffe und andere Arten von Ressourcenverbrauch zu verhindern.

4. Verwenden von Network Policies, um die Netzwerkkommunikation zwischen Containern oder von Containern zum Host-System zu beschränken.

5. Überwachen von Container-Logs und Ereignissen, um verdächtige Aktivitäten oder Anomalien zu erkennen und darauf zu reagieren.

6. Aktualisieren von Images und Containern auf die neuesten Versionen, um sicherzustellen, dass Sicherheitslücken oder Schwachstellen behoben wurden.

7. Verwendung von Verschlüsselung für die interne Kommunikation zwischen Containern oder für die Speicherung von Daten in Containern.

8. Einschränken des Zugriffs auf Host-Ressourcen wie Dateien oder Verzeichnisse durch die Verwendung von Volumes oder Bind Mounts mit gezielten Berechtigungen.


