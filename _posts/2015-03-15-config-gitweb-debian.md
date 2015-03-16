---
layout: post
title: Config du paquet debian [gitweb](http://www.git-scm.com/book/fr/v1/Git-sur-le-serveur-GitWeb) avec Apache2
---

Installer via aptitude
`aptitude install gitweb`

Adapter la config locale:
1. `vi /etc/gitweb.conf`
2. `vi /etc/apache2/conf.d/gitweb`

Redémarrer apache2
`service apache2 restart`
