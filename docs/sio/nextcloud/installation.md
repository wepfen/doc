# Installation




## Mises à jour
Les mises à jours doivent être effectuées avant d'installer le reste:
>### **Important**

>Toutes les commandes sont à faire en **root**
```
zypper refresh 
```

```
zypper update 
```
```
zypper dist-upgrade
```
Les commandes précédentes mettent à jours respectvement les sources des paquets, les packets et le système.

<br><br>
## Installation de Nextcloud

```
zypper install nextcloud
```
>### **Au cas où**
>Choisir `r` lorsqu'il y a cette invite: `Abandoner, réessayer, ignorer ? [a,r,i...? affiche toutes les options] >(a):`

<br><br>
## Installation de Mariadb
MariaDB a été en même temps que Nextcloud grâce à la commande précédente, mais voici la 
commande pour l'installer:
```
zypper install mariadb
```
<br><br>
## Installation d'apache
Intslallation de notre serveur web
```
zypper install apache2
```

