# Installation sur OpenSUSE 15.4

en root ou avec sudo

## OpenSSH server

On aura besoin de d'activer le service ssh côté serveur.

* Faire les Màj:

```
zypper ref
zypper update -f
```

* Vérifier si le paquet openssh est déjà installé avec la commande suivante:

`zypper info --type package -s openssh-server`

* Sinon l'installer:

`zypper install openssh-server`

* L'activer: 

`systemctl start sshd`


