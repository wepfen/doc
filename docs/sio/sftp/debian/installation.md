# Installation d'un serveur SFTP sur Debian 11

en root ou avec sudo

## OpenSSH server

On aura besoin de d'activer le service ssh côté serveur.

* Faire les Màj:

```
apt update
apt upgrade -f
```

* Vérifier si le paquet openssh est déjà installé avec la commande suivante:

`dpkg -l openssh-server``

> Si la mention 'ii' apparaît au début de la ligne c'est que le paquet est installé

* Sinon l'installer:

`apt install openssh-server`

* L'activer: 

`systemctl start sshd`




