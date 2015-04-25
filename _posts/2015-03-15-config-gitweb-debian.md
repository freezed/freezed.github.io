---
layout: post
title: Configurer le paquet gitweb provenant du dépot Debian
---

Pour visualiser via HTTP les projets [git](http://www.git-scm.com/) et leur état depuis le serveur, il existe [gitweb](http://www.git-scm.com/book/fr/v1/Git-sur-le-serveur-GitWeb). La doc n'ayant pas précisé comment adapter la config après l'installation, voici où ça se passe:

Installer via aptitude

`aptitude install gitweb`

Adapter la config locale:

1. `vi /etc/gitweb.conf`
2. `vi /etc/apache2/conf.d/gitweb`

Redémarrer apache2

`service apache2 restart`
