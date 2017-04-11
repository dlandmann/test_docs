# Dokumentation - CronJobs




Versionen:
Nummer
Änderungen
Autor
Datum
1.0
Erste Fassung
Dierk Landmann
06.04.2017







##Todo
Regelmäßig die CronJob und die Serverlast prüfen und gegebenenfalls neue Gruppen anlegen.
Inhaltsverzeichnis

Todo
Inhaltsverzeichnis
Allgemeines
CronGroups
Aktive CronGroups
Anpassung Crontab -e
Modul ICMAA_CronPool


##Allgemeines  
Ziel ist es alle Jobs mit dem Modul AOE-Scheduler zu verwalten. Dazu wurden aus Performancegründen die CronGroups eingeführt und ein neues Modul “ICMAA_CronPool” entwickelt.


##CronGroups
Mittels CronGroups können mehrere Job bzw. Gruppen parallel ausgeführt werden. Es werden die “Lücken” in der Timeline verhindert.


##Aktive CronGroups

Die Gruppen können im Scheduler (Job Configuration) zugewiesen werden. 

Gruppenname
Verwendung
followupemails
Zusammensammeln und Senden der Mails
→ dauert früh ca. 30 Min und dann im Stundentakt nur wenige Minuten
googlemerchant
Google Shopping 
→ dauert pro Storeview ca 60 Minuten!
→ noch nicht eingetaktet - wahrscheinlich Samstag 
amazonshopping
AMZ Shopping un
→ dauert früh um 9 ca. 60 Minuten 









Anpassung Crontab -e

```
* * * * * /bin/bash pfad/scheduler_cron.sh --mode always
# alle Gruppen als einzelnen Prozess starten
* * * * * /bin/bash pfad/scheduler_cron.sh --mode default --includeGroups followupemails
* * * * * /bin/bash pfad/scheduler_cron.sh --mode default --includeGroups amazonshopping
* * * * * /bin/bash pfad/scheduler_cron.sh --mode default --includeGroups googlemerchant
# alle Jobs ausführen, welche nicht den Gruppen sind
* * * * * /bin/bash pfad/scheduler_cron.sh --mode default --excludeGroups followupemails,amazonshopping,googlemerchant
```
! Bei excludeGroups und includeGroups dürfen KEINE Leerzeichen nach dem Komma folgen. 



Modul ICMAA_CronPool
Alle individuellen CronJobs wurden in ein Modul ausgelagert und können nun über den AOS_Scheduler geplant und angepasst werden.


Job
Verwendung


Stand
cron_test
Testcronjob


fertig
drop_products_in_outlet




test lief durch
refresh_sale_products






test lief durch
productalert_send


wahrscheinlich nicht notwendig

Es gibt bereits zwei jobs im scheduler, welche aktiv sind und 15:00 Uhr laufen.
Das sind "catalog_product_alert" mit dem Return Mage_ProductAlert_Model_Observer 
und 
"catalog_product_alert_clean" mit den Return Impericon_ExtendedProductAlert_Model_Observer
price






zugangsdaten fehlen noch

Weitere Jobs können einfach im Modul hinzugefügt werden. Falls es sind um zeitlich umfangreiche Jobs handelt sollte eine neue Gruppe definiert werden und der Crontab erweitert werden.

Ausblick
Integration der Chartmeldungen in das Modul

