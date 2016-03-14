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

	(
		git clone https://github.com/openstack/python-novaclient.git
		cd python-novaclient
		python ./setup.py build
		sudo python ./setup.py install
	)

	https://pypi.python.org/packages/source/r/rackspace-novaclient/rackspace-novaclient-1.5.tar.gz#md5=c41cca1e9405b47ca199f2c169711be5
	cd rackspace-novaclient
	python ./setup.py build
	sudo python ./setup.py install


	sudo pip install cffi
	sudo pip install pyopenssl
	sudo pip install ndg-httpsclient
	sudo pip install python-novaclient
	sudo pip install urllib3
	sudo pip install setuptools --upgrade
	sudo pip install pyrax --upgrade

	wget https://code.launchpad.net/duplicity/0.7-series/0.7.04/+download/duplicity-0.7.04.tar.gz
	tar -xvzf duplicity-0.7.04.tar.gz
	cd duplicity-0.7.04

	(`dépendance` ? aptitude install : sudo pip install `dépendance`; re-build)



## Erreurs:

* `UserWarning: Module novaclient.v1_1 is deprecated` => si
* [InsecurePlatformWarning](https://urllib3.readthedocs.org/en/latest/security.html#insecureplatformwarning) => pyopenssl ndg-httpsclient python-pyasn1



## Sources:

* Blog de Yvan Godard:
	* [Utiliser HubiC comme espace de backup avec Duplicity](http://www.yvangodard.me/hubic-backup-duplicity-backend-pyrax/)
	* [Utiliser Hubic comme backup pour Duplicity avec le backend pyrax](http://www.yvangodard.me/utiliser-hubic-comme-espace-de-backup-avec-duplicity/)
	* []()

* Sources:
	* [duplicity v0.7.04](https://code.launchpad.net/duplicity/0.7-series/0.7.04)
	* [python-novaclient v2.27.0](https://github.com/openstack/python-novaclient/tree/stable/kilo) aka _kilo_
	* []()
