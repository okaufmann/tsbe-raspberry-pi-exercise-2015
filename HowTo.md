#Anpassungen vom Musterbeispiel

*Image bei mir verlangen*

###Namen ersetzen
Als erstes empfehle ich nach dem login über ssh sich als root einzulogen, damit muss man nicht immer sudo verwenden
(Folgender Befehl ist in der Konsole einzugeben):
```
su -
```
Im folgenden muss im Prinzip nur hans muster mit dem eigenen vornamen und nachnamen ersetzt werden.

1) Pi Finder name ändern 
```
/usr/lib/node_modules/pi-finder/config.js
```
2) Pi hostname wie folgt ändern:
```
raspy-config
```
(8 Advanced -> A2 Hostname --> vorname-nachname.int)

3) Zonenfiles umbenennen:
```
mv /etc/bind/db.hans-muster.int /etc/bind/db.vorname-nachname.int
mv /etc/bind/db.hans-muster.dmz /etc/bind/db.vorname-nachname.dmz
```
4) Zonennamen, Dateinamen (wie im vorherigen schritt umbenannt) anpassen: 
```
nano /etc/bind/named.conf.local
```
5) Webseitenordner umbennen
```
mv /home/sites/hans-muster.int /home/sites/vorname-nachname.int
```
6) Pfad zum Webseitenordner, hostname und alias entsprechend anpassen (vorname-nachname.int)
```
/etc/apache2/sites-available/hans-muster.int
```
7) Folgende alte Seitenkonfiguration entfernen
```
rm /etc/apache2/sites-enabled/hans-muster.int
rm /etc/apache2/sites-available/hans-muster.int
```
8) Neue Seite im Apache2 wie folgt einschalten
```
a2ensite vorname-nachname.int
service apache2 restart
```
9) Einen neuen Zugang für den privaten Bereich erstellen mit
```
htpasswd /etc/apache2/passwords/.htpasswd VornameNachname
```

10) Den gerade erstellen Benutzer der richtigen Gruppe (TsbeStudents) hinzufügen:
```
nano /etc/apache2/passwords/.htgroup
```
11) Die Html Startseite und privater Bereich entsprechend (Namen ersetzen) anpassen:
```
nano /home/sites/vorname-nachname/index.html
nano /home/sites/vorname-nachname/privat/index.html
```
12) Nun muss man die IP des Pi in den Netzwerk Einstellungen als DNS eintragen und die Seite
```
http://www.vorname-nachname.int aufrufen.
```

###In jedem neuen Netzwerk

Das Folgende muss immer neu konfiguriert werden, da der PI immer eine neue IP bekommt(dhcp).
1) Reverse Lookup Zone anpassen:
```
nano /etc/bind/named.conf.local
```
2) forwarders und allow-query anpassen unter:
```
nano /etc/bind/named.conf.options
```
3) IPs vom pi in den SOA Records (Dateinamen beachten!) 
```
nano /etc/bind/db.vorname-nachname.int
```

###Fehleranalyse

Probleme mit Bind oder sontstiges:
```
tail /var/log/syslog
```

Probleme mit Apache
```
tail /var/log/apache2/error.log
```

###Zugang

IP gemäss `https://pi.strebl.ch` (Name gemäss Punkt 1)
Username: pi
Passwort: raspberry (auch für root)

