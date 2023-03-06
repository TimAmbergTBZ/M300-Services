# Sicherheit #

## Firewall ##
Eine Firewall kann in einer VM erstellt werden. Wir benutzen dafür UFW (Uncomplicated FireWall).

Die Firewall kann ganz einfach mit: sudo apt-get install ufw installiert werden.

Danach muss man diese Firewall nur noch aktivieren, und dann kann sie schon Traffic filtern.

Der Status der Firewall kann mit sudo ufw status überprüft werden.

Die Firewall kann man mit sudo ufw enable aktivieren.

So können die Firewall Regeln eingeben:
    Port 80 (HTTP) öffnen für alle
    vagrant ssh web
    sudo ufw allow 80/tcp
    exit

    # Port 22 (SSH) nur für den Host (wo die VM laufen) öffnen
    vagrant ssh web
    w
    sudo ufw allow from [Meine-IP] to any port 22
    exit

    # Port 3306 (MySQL) nur für den web Server öffnen
    vagrant ssh database
    sudo ufw allow from [IP der Web-VM] to any port 3306
    exit

Bei diesen Anfragen erhalte ich momentan leider noch keine Antwort:
    $ curl -f 192.168.55.101
    $ curl -f 192.168.55.100:3306
