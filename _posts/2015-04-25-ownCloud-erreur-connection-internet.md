---
layout: post
title: Installation ownCloud sous Debian, erreur de connection internet
---

## Contexte

* Debian 7/k3.14
* ownCloud 8.0.2, installé via [openSUSE Build Service packages](http://software.opensuse.org/download.html?project=isv:ownCloud:community&package=owncloud)

## Problème

Dans le menu d'administration du client web, la vérification de la configuration affiche l'erreur suivant:

	Ce serveur ne peut se connecter à internet. Cela signifie que certaines fonctionnalités, telles que le montage de supports de stockage distants, les notifications de mises à jour ou l'installation d'applications tierces ne fonctionneront pas. L'accès aux fichiers à distance, ainsi que les notifications par courriel ne fonctionneront pas non plus. Il est recommandé d'activer la connexion internet pour ce serveur si vous souhaitez disposer de l'ensemble des fonctionnalités offertes.
	Veuillez vous référer au guide d'installation.

*Erreur en VO:*

	This server has no working internet connection. This means that some of the features like mounting of external storage, notifications about updates or installation of 3rd party apps don´t work. Accessing files from remote and sending of notification emails might also not work. We suggest to enable internet connection for this server if you want to have all features.


## Cheminement

* ping `www.owncloud.org` depuis le serveur, OK
* essai d'échange enre le serveur **OC** & un client **OC** pour Android, OK
* édition du `php.ini`: `allow_url_fopen On`,
* édition du `php.ini`: `allow_url_include On`
* recherche de la fonction dans le code **OC** qui génère ce message d'erreur: `[OC_PATH]/lib/private/util.php`
* isolation de la fonction et essai sur plusieurs machines: `fsockopen()` à bien bien un comportement différant sur le serveur concerné
* suppression de `fsockopen()` dans la directive `disable_functions`  :-)

### Sources:

* Forum ownCloud:
	* [Internet connection not working](https://forum.owncloud.org/viewtopic.php?f=29&t=23700)
	* ["Internet connection not working" behind proxy](https://forum.owncloud.org/viewtopic.php?f=26&t=18623)
* 2by2host, [Warning: fsockopen() has been disabled for security reasons](http://www.2by2host.com/articles/php-errors-faq/disabled_fsockopen/)
