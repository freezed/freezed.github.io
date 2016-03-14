---
layout: post
title: Relier duplicity à une instance HubiC
---

## Contexte

* Debian 7 wheezy (oldstable)
* kernel 3.14

## Problème

* [HubiC](https://hubic.com/) est basé sur une version modifié de [openStack](http://www.openstack.org), notament au niveau de l'authentification.
* [pyrax](https://developer.rackspace.com/sdks/python/) est le SDK , Python/openStack
* [Duplicity](https://code.launchpad.net/duplicity), intègre [pyrax](https://github.com/rackspace/pyrax) à partir de sa version 0.6.23
* les versions minimum respectives de ces paquets et de certaines dépendances ne sont pas dispo dans le repo debian/wheezy

## Cheminement

	sudo aptitude install python-pip python-setuptools python-dev
	sudo aptitude install librsync1 librsync-dev
	sudo aptitude install python-lockfile
	sudo aptitude install python-pyasn1
	sudo aptitude install libffi-dev

	sudo apt-get -t wheezy-backports install "python-cffi"

	sudo pip2 install cffi
	sudo pip2 install pyopenssl
	sudo pip2 install ndg-httpsclient
	sudo pip2 install urllib3
	sudo pip2 install setuptools --upgrade
	sudo pip2 install python-novaclient --upgrade
	sudo pip2 install pyrax --upgrade

	wget https://code.launchpad.net/duplicity/0.7-series/0.7.06/+download/duplicity-0.7.06.tar.gz
	tar -xvzf duplicity-0.7.06.tar.gz
	cd duplicity-0.7.06
	python ./setup.py build
	sudo python ./setup.py install

	(`dépendance` ? aptitude install : sudo pip2 install `dépendance`; re-build)


## Erreurs:

1. [InsecurePlatformWarning](https://urllib3.readthedocs.org/en/latest/security.html#insecureplatformwarning) : install pyopenssl ndg-httpsclient python-pyasn1
2. `UserWarning: Module novaclient.v1_1 is deprecated` : disparu avec le lot de MàJ du 20160314 (python-novaclient 1.5?)
3. `Connection failed, please check your credentials: JSONDecodeError Expecting value: line 1 column 1 (char 0)` : upgrade setuptools 18.3.1 -> 20.2.2


## Ressources:

* Tuto:
	* [Utiliser HubiC comme espace de backup avec Duplicity](http://www.yvangodard.me/hubic-backup-duplicity-backend-pyrax/) (lien mort)
	* [Utiliser Hubic comme backup pour Duplicity avec le backend pyrax](http://www.yvangodard.me/utiliser-hubic-comme-espace-de-backup-avec-duplicity/) (lien mort)
	* [Backups dans le cloud hubic avec duplicity et rclone(rsync)](http://nogues.pro/blog/backup-hubic-duplicity-rsync.html)
	* [Hubic and Duplicity](https://www.tiernanotoole.ie/2015/04/01/Duplicity_Hubic.html)
	* [How-to backup your data on hubic using duplicity](http://www.monperrus.net/martin/backup-hubic)
	* []()

* Sources:
	* [duplicity v0.7.06](https://launchpad.net/duplicity/0.7-series/0.7.06/+download/duplicity-0.7.06.tar.gz)

## Changelog
* 20160314 :
	* MàJ de la version de duplicity
	* MàJ pip -> pip2
	* MàJ python-novaclient 2.28.2.dev3
	* MàJ rackspace-novaclient 1.5
	* Erreur #2 & #3

