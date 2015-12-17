#Anpassungen vom Musterbeispiel

*Image bei mir verlangen*

##Wichtige Infos
- Ich übernehme **keine Haftung** wenns dann nicht läuft, das hier soll eine gut gemeinte Hilfestellung sein, keine Verpflichtung!
- Die Datei Struktur (etc, home) ist identisch mit der auf dem raspi (wie sie sein sollte), so können die "Vorlagen-Dateien" jederzeit wiedergefunden werden und allenfalls neu kopiert werden.
- Bei Fragen, fragen ;)

###Zugang

IP gemäss [https://pi.strebl.ch](https://pi.strebl.ch) (Zuerst aber umbenennen)
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
service pi-finder restart
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
nano /home/sites/aba.int/index.html
nano /home/sites/aba.int/privat/index.html
```
**4) In folgenden Dateien XXX mit letztem Teil der IP vom Raspi ersetzen:**
```
/etc/bind/db.10.23.3
/etc/bind/db.aba.int
/etc/bind/named.conf.options
```
**5) DNS Server `dns-nameservers` auf Raspi selbst anpassen**
```
/etc/network/interfaces
```
**5) Bind und Apache neustarten**
```
service apache2 restart
service bind9 restart
```

###Fehleranalyse

**Probleme mit Bind oder sontstiges:**
```
tail /var/log/syslog
```

**Probleme mit Apache**
```
tail /var/log/apache2/error.log
```


