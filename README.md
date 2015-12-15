##Demo d'utilisation de HAProxy pour une exposition via des conteneur Docker.

Ce projet a pour but de monter un conteneur HAproxy pour démontrer la mise en place de test A/B sur la base de conteneurs et  la facilité que propose docker.

Cette composition expose 3 conteneurs, pour la lancer, exécutez la commande suivante : 

```
docker-compose up
```

Vous aurez à votre disposition les 3 conteneurs suivants :

###1. HAProxy

Ce qu'en dit wikipedia: 

> HAProxy is free, open source software that provides a high availability load balancer and proxy server for TCP and HTTP-based applications that spreads requests across multiple servers. It is written in C and has a reputation for being fast and efficient (in terms of processor and memory usage).

Ce proxy permet aussi de load balancer en affectant un poids à chacun des serveur permettant par exemple de proposer d'exposer (dans le cas de ce projet), un serveur 2 fois plus que l'autre.

La configuration estt défini dans le fichier ```haproxy/haproxy.cfg```, le load balancing est décrit dans la section ```backend nginx```, la section ```listen admin``` permet d'exposer une interface admin permettant de visualiser les accès aux serveurs exposés.

###2. Serveur nginx

Les serveur nginx sont configurés pour permettre de désactiver le cache nginx et de pouvoir modifier les fichiers du site en temps réel. Pour permettre cela, il faut intégrer dans la configuration l'instruction ```sendfile  off``` dans la section http du fichier de configuration nginx.
