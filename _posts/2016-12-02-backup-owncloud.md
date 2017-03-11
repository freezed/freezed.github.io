# backup owncloud

## Preventif

### Backup /data & /config

	rsync -e "ssh -p 22" -arzv --stats --delete-after -f"- thumbnails/" host:/path/to/owncloud/data /path/to/backup/owncloud/

	rsync -e "ssh -p 22" -arzv host:/path/to/owncloud/config /path/to/backup/owncloud/

### [Backup DB][7]

	mysqldump --lock-tables -h [server] -u [username] -p[password] [db_name] > owncloud-dbbackup_`date +"%Y%m%d"`.bak

## Curatif

### Restore /data & config

	rsync -e "ssh -p 42" -arzv --stats -f"- thumbnails/" host:/path/to/backuup/owncloud/data/ /home/owncloud/data

### Restore DB
[Créer le nouvel user et sa base][8]:

	CREATE USER 'owncloud'@'localhost' IDENTIFIED BY 'password'
	CREATE DATABASE IF NOT EXISTS owncloud;
	GRANT ALL PRIVILEGES ON owncloud.* TO 'owncloud'@'localhost' IDENTIFIED BY 'password';
	-
### Déménagement SSL

### MàJ DNS

	10800 IN A [new.IP]
	@ 10800 IN A [new.IP]
	imap 10800 IN CNAME access.mail.gandi.net.
	pop 10800 IN CNAME access.mail.gandi.net.
	smtp 10800 IN CNAME relay.mail.gandi.net.
	webmail 10800 IN CNAME agent.mail.gandi.net.
	@ 10800 IN MX 50 fb.mail.gandi.net.
	@ 10800 IN MX 10 spool.mail.gandi.net.

## Surprises

### Changement de Debian/Wheezy -> Debian/Jessie

#### Apache2: [v2.2 -> v2.4][9]

##### site-avaiable
Les noms des fichiers se terminent [par .conf][10]

##### PhpMyAdmin

__Erreur__: `Fatal error:  require_once(): Failed opening required '/usr/share/php/php-gettext/gettext.inc' (include_path='.') in /usr/share/phpmyadmin/libraries/select_lang.lib.php on line 463`

__Remède__: Ajout de  _/usr/share/php/php-gettext/_ dans la directive _php_admin_value open_basedir_ du fichier de conf apache. (_Ref. :  [phpmyadmin symlinks error after ubuntu upgrade - superuser.com][10]_)

##### Owncloud logging

(Re)mettre en place les logs dans [_/var/log/owncloud/_ et le logrotate][11]

##### Manipulation des données ownCloud en local via CLI

Mise en place de [davfs2][14] pour le montage via _fstab_. Attention [doc.owncloud][13] est incomplète, voir aussi la [doc.ubuntu][12]

__erreur__: /sbin/mount.davfs: warning: the server does not support locks

/etc/fstab

~/.davfs2/secrets

/etc/davfs2/cert

/etc/davfs2/davfs2.conf



_ _ _

[7]: https://doc.owncloud.org/server/latest/admin_manual/maintenance/backup.html#backup-database "Backup Database - doc.owncloud"
[8]: https://doc.owncloud.org/server/9.1/admin_manual/maintenance/restore.html#restore-database  "Restore Database - doc.owncloud"
[9]: http://httpd.apache.org/docs/2.4/fr/upgrading.html "Mise à jour de la version 2.2 vers la version 2.4 - doc.apache"
[10]: http://superuser.com/questions/590208/phpmyadmin-symlinks-error-after-ubuntu-upgrade/590565#590565 "phpmyadmin symlinks error after ubuntu upgrade - superuser.com"
[11]: http://www.jouvinio.net/wiki/index.php/OwnCloud_Fichier_log "OwnCloud Fichier log - jouvinio.net"
[12]: https://doc.ubuntu-fr.org/davfs2 "davfs2 - doc.ubuntu"
[13]: https://doc.owncloud.org/server/9.1/user_manual/files/access_webdav.html#creating-webdav-mounts-on-the-linux-command-line "Creating WebDAV Mounts on the Linux Command Line - doc.owncloud"
[14]: https://packages.debian.org/jessie/davfs2 "mount a WebDAV resource as a regular file system - package.debian"


Ressources:

* [Configuring a MySQL or MariaDB Database - doc.owncloud](https://doc.owncloud.org/server/latest//admin_manual/configuration_database/linux_database_configuration.html#configuring-a-mysql-or-mariadb-database)
* [rsync - doc.ubuntu](https://doc.ubuntu-fr.org/rsync)
* [MySQL - doc.ubuntu](https://doc.ubuntu-fr.org/mysql)
