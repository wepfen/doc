# Sécurité

## Fail2ban

La plateforme nextcloud peut être hébergée en interne ou ouverte à l'extérieur. Dans les deux cas elle peut être sujette à des attaques par force brute. Cependant elle intègre une fonction de protection contre cette attaque. 

### Attaque par force brute

Je vais mener une attaque par force brute pour sur ma plateforme en localhost sur un compte crée pour l'occasion afin de montrer que l'attaque par force brute n'est pas interrompue.
<br>`Login: test_brute`
avec la commande:
```
$ hydra -V -f -l test_brute -P rockyou.txt -s 80 http-get://localhost/nextcloud/index.php/login
```
Sur cette image on voit que ma tentative a été interceptée au bout de 16 tentatives
![tenative_hydra](https://github.com/1Tyron140/doc/raw/main/images/nextcloud/hydra.jpg "tentative brute force")


Le serveur a renvoyé un mauvais mot de passe comme mot de passe valide pour bloquer l'attaque.

Dans cette table on voit le journal des attaques:
![tenative_hydra](https://github.com/1Tyron140/doc/raw/main/images/nextcloud/bruteforce_attempts.jpg "table bruteforce")

et on ne peut plus se connecter:
![tenative_hydra](https://github.com/1Tyron140/doc/raw/main/images/nextcloud/connexion_refusee.jpg "accès bloqué")
La commande `sudo -u wwwrun php /srv/www/htdocs/nextcloud/occ security:bruteforce:reset <adresse ip>`
### Qu'est ce que fail2ban

On peut installer fail2ban pour renforcer cette sécurité. Cette outil opensource va venir bloquer une adresse ip grâce à iptables selon certaines conditions (exemple: 5 tentatives échouées). 

### Installation

On ajoute le dépôt d'abord pour pouvoir récupérer le paquet:
```
sudo zypper addrepo https://download.opensuse.org/repositories/security/openSUSE_Leap_15.3_Update/security.repo
sudo zypper refresh
sudo zypper install fail2ban
```
Et l'activer: `sudo systemctl enable fail2ban.serice --now`
### Création d'un filtre et d'une prison

__Les filtres__ servent à définir les cas qui activeront la prison, ici: les cas d'échecs d'authentification.

Dans `/etc/fail2ban/filter.d/` il y a plein d'autre filtres comme `nagios.conf` ou `bitwarden.conf` alors on crée nextcloud.conf dans le repertoire: `sudo nano nextcloud.conf`.

Et coller ces lignes de regex: 
```
[Definition]
_groupsre = (?:(?:,?\s*"\w+":(?:"[^"]+"|\w+))*)
failregex = ^\{%(_groupsre)s,?\s*"remoteAddr":"<HOST>"%(_groupsre)s,?\s*"message":"Login failed:
datepattern = ,?\s*"time"\s*:\s*"%%Y-%%m-%%d[T ]%%H:%%M:%%S(%%z)?"
```

__Les prisons__ (ou jail) sont les punitions qui vont être appliquées, comme un bannissement de 50000 secondes.

Dans `/etc/fail2ban/jail.d/`, créer `nextcloud.local` avec ce contenu:

```
[nextcloud]
backend = auto
enabled = true
port = 80,443
protocol = tcp
filter = nextcloud
maxretry = 5
bantime = 86400
findtime = 43200
logpath = /srv/www/htdocs/nextcloud/data/nextcloud.log
```
On lit qu'au bout de 5 tentatives, un ban de 86400 secondes (24 heures) est appliqué.

Relancer le service : `sudo systemctl restart fail2ban.service`

Ensuite la commande `fail2ban-client status` nous affiche les prisons activées:

```
Status
|- Number of jail:    1
 - jail list: nextcloud
```
Après quelques tentatives échouées, les logs de fail2ban montrent que les filtres foncitonnent correctemen, mais a été ignorée car il s'agit des requêtes du serveur.

![image log fail2ban](https://github.com/1Tyron140/doc/raw/main/images/nextcloud/fail2ban_log.jpg)

## Utiliser HTTPS

Pour ne pas que les mots de passes circulent en clair, je vais rediriger les requêtes HTTP en HTTPS.


`sudo nano /etc/apache2/conf.d/nextcloud.conf`

```
<VirtualHost *:80>
   ServerName cloud.nextcloud.com
   Redirect permanent / https://cloud.nextcloud.com/
</VirtualHost>
```
Puis, redémmarer le serveur web:
`sudo systemctl restart apache2.service`
