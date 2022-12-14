# Previewgenerator richtig einrichten
[Hier](http://web.archive.org/web/20200513043150/https://ownyourbits.com/2019/06/29/understanding-and-improving-nextcloud-previews/) steht wie das geht. Kurzfassung:

1. Webserver stoppen von Nextcloud
2. In /var/www-data/html/appdata.. gibt es einen Ordner *Previews*. Den löschen (siehe [hier](https://help.nextcloud.com/t/fairly-new-with-nextcloud-but-preview-folder-has-huge-size/64390/3))
3. `occ files:scan-app-data` um Datenbank zu aktualisieren mit nun gelöschten Previews
4.  Die folgenden Settings ändern:
    ```
    occ config:app:set previewgenerator squareSizes --value="32 256"
    occ config:app:set previewgenerator widthSizes  --value="256 384"
    occ config:app:set previewgenerator heightSizes --value="256"
    occ config:system:set preview_max_x --value 2048
    occ config:system:set preview_max_y --value 2048
    occ config:system:set jpeg_quality --value 60
    occ config:app:set preview jpeg_quality --value="60"
    ```
5. mit `occ preview:generate-all` die previews neu generieren.

# Datenbankprobleme mit MariaDB
Wenn nextcloud nicht mehr geht kann dies an mariadb 10.6 liegen, das eine globale Variable 
defaultmässig anders setzt. Um das zu beheben mit 
`sudo docker exec -it mariadb1 bin/bash`
in den container gehen, dann
`mysql -p -u root`
und dann das mysql passwort eingeben.
Daraufhin
`SET GLOBAL innodb_read_only_compressed=OFF;`
schreiben, enter und beenden. Nun sollte es wieder gehen.
Solange dieser Bug besteht sollte Watchtower ausbleiben. 