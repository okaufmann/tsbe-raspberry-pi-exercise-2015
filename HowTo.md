#Anpassungen vom Musterbeispiel

*Image bei mir verlangen*

###Zugang

IP gemäss `https://pi.strebl.ch` (Zuerst Name in Punkt 1 wechseln)
Username: pi
Passwort: raspberry (auch für root)

###Tipp
Als erstes empfehle ich nach dem login über ssh sich als root einzuloggen, damit muss man nicht immer sudo verwenden
(Folgender Befehl ist in der Konsole einzugeben; Passwort: Siehe oben):
```
su -
```

###Pi Umbenennen
Damit es keine Netzwerk konflikte gibt sind folgende Schritte notwendig:

**1) Pi Finder name ändern**
```
nano /usr/lib/node_modules/pi-finder/config.js
```
**2) Pi hostname ändern:**
```
raspy-config
```
(8 Advanced -> A2 Hostname --> vorname-nachname.int)

###IP anpassen und Webseiten Zugang erstellen
**1) Einen neuen Zugang für den privaten Bereich der eingerichteten Webseite erstellen (Und sich die Daten merken!):**
```
htpasswd /etc/apache2/passwords/.htpasswd GewuenschterUsername
```
**2) Den gerade erstellen Benutzer der richtigen Gruppe (TsbeStudents) hinzufügen:**
```
nano /etc/apache2/passwords/.htgroup
```
**3) Die Html Startseite und privater Bereich entsprechend (Namen ersetzen) anpassen:**
```
nano /home/sites/vorname-nachname/index.html
nano /home/sites/vorname-nachname/privat/index.html
```
**4) Nun muss man die IP die der PI erhaltent hat in den folgenden Files anpassen:**
```
http://www.vorname-nachname.int aufrufen.
```
**5) Dienste neustarten**
```
service apache2 restart
service bind9 restart
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


