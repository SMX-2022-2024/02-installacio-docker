<!-- https://www.cherryservers.com/blog/install-lamp-on-ubuntu-22-04 -->

## Actualització del servidor

Actualització dels fitxers d'**índex de paquets del sistema**, que contenen informació sobre els paquets disponibles i les seves versions.

```bash
sudo apt-get update
```

Un cop actualitzats els fitxers, cal descarregar i instal·lar les actualitzacions de cada paquet obsolet i dependència del vostre sistema.

```bash
sudo apt-get -y upgrade
```
Reiniciem el servidor

```bash
sudo reboot now
```

Comprovem l'espai en disc que tenim:

```bash
df -h
```

## Comanda per veure tots els paquets instal·lats

```bash
sudo apt list --installed
```


# Cal instal·lar LAMP

* Linux

* Apache

* Mysql

* PHP

## Pas 1: Instal·lar servidor web **Apache**

```bash
sudo apt-get install -y apache2
```

<pre>
profe@docker-smx:~$ sudo apt-get install -y apache2
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
apache2 is already the newest version (2.4.52-1ubuntu4.7).
0 upgraded, 0 newly installed, 0 to remove and 4 not upgraded.
profe@docker-smx:~$ 
</pre>

![alt text](image.png)

```bash
sudo systemctl status apache2
```

<pre>
profe@docker-smx:~$ sudo systemctl status apache2
● apache2.service - The Apache HTTP Server
     Loaded: loaded (/lib/systemd/system/apache2.service; enabled; vendor preset: enabled)
     Active: active (running) since Fri 2024-03-01 08:54:27 UTC; 5min ago
       Docs: https://httpd.apache.org/docs/2.4/
   Main PID: 2182 (apache2)
      Tasks: 55 (limit: 4558)
     Memory: 5.2M
        CPU: 51ms
     CGroup: /system.slice/apache2.service
             ├─2182 /usr/sbin/apache2 -k start
             ├─2219 /usr/sbin/apache2 -k start
             └─2220 /usr/sbin/apache2 -k start

Mar 01 08:54:27 docker-smx systemd[1]: Starting The Apache HTTP Server...
Mar 01 08:54:27 docker-smx apachectl[2181]: AH00558: apache2: Could not reliably determine the server's fully qual>
Mar 01 08:54:27 docker-smx systemd[1]: Started The Apache HTTP Server.
profe@docker-smx:~$ 
</pre>

Per permetre el trànsit HTTP, heu de permetre connexions al port 80.

```bash
sudo ufw allow 80/tcp
```

<pre>
profe@docker-smx:~$ sudo ufw allow 80/tcp
Rules updated
Rules updated (v6)
profe@docker-smx:~$ 
</pre>


### Habilitar el FW

```bash
sudo ufw enable
```

<pre>
profe@docker-smx:~$ sudo ufw enable
Command may disrupt existing ssh connections. Proceed with operation (y|n)? y
Firewall is active and enabled on system startup
profe@docker-smx:~$ 
</pre>


Per aplicar els canvis, torneu a carregar el tallafoc.

```bash
sudo ufw reload
```

Per confirmar l'estat del tallafoc, executeu l'ordre següent:

```bash
sudo ufw status
```

<pre>
profe@docker-smx:~$ sudo ufw status
Status: active

To                         Action      From
--                         ------      ----
80/tcp                     ALLOW       Anywhere                  
80/tcp (v6)                ALLOW       Anywhere (v6)             

profe@docker-smx:~$ 
</pre>

## Pas 2: Instal·lar servidor base de dades **`MariaDB`**

En aquest pas, instal·larem el servidor de bases de dades **`MariaDB`** en lloc de **`MySQL`**. **`MariaDB`** ofereix un conjunt de funcions ric i un rendiment millorat.

```bash
sudo apt-get install -y **`MariaDB`**-server **`MariaDB`**-client
```

<pre>
profe@docker-smx:~$ sudo apt-get install -y **`MariaDB`**-server **`MariaDB`**-client
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  galera-4 libcgi-fast-perl libcgi-pm-perl libclone-perl libconfig-inifiles-perl libdaxctl1 libdbd-mysql-perl
  libdbi-perl libencode-locale-perl libfcgi-bin libfcgi-perl

...

Setting up **`MariaDB`**-server (1:10.6.16-0ubuntu0.22.04.1) ...
Processing triggers for man-db (2.10.2-1) ...
Processing triggers for libc-bin (2.35-0ubuntu3.6) ...
Scanning processes...                                                                                              
Scanning linux images...                                                                                           
Running kernel seems to be up-to-date.
No services need to be restarted.
No containers need to be restarted.
No user sessions are running outdated binaries.
No VM guests are running outdated hypervisor (qemu) binaries on this host.
profe@docker-smx:~$ 
</pre>

Tanmateix, el repositori d'Ubuntu no proporciona la versió més recent de **`MariaDB`**, que instal·la **`MariaDB 10.6`**. Per instal·lar la darrera versió, instal·leu-la des dels repositoris **`MariaDB`**.

Per fer-ho, assegureu-vos d'afegir la **`clau de signatura GPG`**.

```bash
sudo apt-key adv --fetch-keys 'https://mariadb.org/mariadb_release_signing_key.asc'
```

<pre>
profe@docker-smx:~$ sudo apt-key adv --fetch-keys 'https://mariadb.org/mariadb_release_signing_key.asc'
Warning: apt-key is deprecated. Manage keyring files in trusted.gpg.d instead (see apt-key(8)).
Executing: /tmp/apt-key-gpghome.v4F4aVI3RU/gpg.1.sh --fetch-keys https://mariadb.org/mariadb_release_signing_key.asc
gpg: requesting key from 'https://mariadb.org/mariadb_release_signing_key.asc'
gpg: key F1656F24C74CD1D8: public key "MariaDB Signing Key <signing-key@mariadb.org>" imported
gpg: Total number processed: 1
gpg:               imported: 1
profe@docker-smx:~$ 
</pre>


Actualització dels fitxers d'**índex de paquets del sistema**, que contenen informació sobre els paquets disponibles i les seves versions.

```bash
sudo apt-get update
```
<pre>
profe@docker-smx:~$ sudo apt-get update
Hit:1 http://es.archive.ubuntu.com/ubuntu jammy InRelease
Hit:2 https://download.docker.com/linux/ubuntu jammy InRelease              
Hit:3 http://es.archive.ubuntu.com/ubuntu jammy-updates InRelease           
Hit:4 http://es.archive.ubuntu.com/ubuntu jammy-backports InRelease
Hit:5 http://es.archive.ubuntu.com/ubuntu jammy-security InRelease
Reading package lists... Done
profe@docker-smx:~$ 
</pre>


Un cop actualitzat l'**índex de paquets**, instal·leu el servidor i el client **MariaDB** tal com es mostra.

```bash
sudo apt-get -y install mariadb-server mariadb-client
```

<pre>
profe@docker-smx:~$ sudo apt-get -y install mariadb-server mariadb-client
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
mariadb-client is already the newest version (1:10.6.16-0ubuntu0.22.04.1).
mariadb-server is already the newest version (1:10.6.16-0ubuntu0.22.04.1).
0 upgraded, 0 newly installed, 0 to remove and 4 not upgraded.
profe@docker-smx:~$ 
</pre>

En aquest punt, el servidor MariaDB, juntament amb el client, s'ha instal·lat correctament. Podeu confirmar la versió instal·lada de la següent manera.

```bash
mariadb --version
```

<pre>
profe@docker-smx:~$ mariadb --version
mariadb  Ver 15.1 Distrib 10.6.16-MariaDB, for debian-linux-gnu (x86_64) using  EditLine wrapper
profe@docker-smx:~$ 
</pre>

## Pas 3: assegura el servidor de bases de dades MariaDB

La instal·lació predeterminada de MariaDB inclou una configuració feble, que suposa un risc potencial per a les vostres bases de dades. Per tant, és molt recomanable realitzar algunes operacions d'enduriment per protegir el servidor de bases de dades.

Per millorar la seguretat de MariaDB, executeu l'script de seguretat, que s'inclou com a part de la instal·lació de MariaDB.

```bash
sudo mysql_secure_installation
```

<pre>
profe@docker-smx:~$ sudo mysql_secure_installation

NOTE: RUNNING ALL PARTS OF THIS SCRIPT IS RECOMMENDED FOR ALL MariaDB
      SERVERS IN PRODUCTION USE!  PLEASE READ EACH STEP CAREFULLY!

In order to log into MariaDB to secure it, we'll need the current
password for the root user. If you've just installed MariaDB, and
haven't set the root password yet, you should just press enter here.

Enter current password for root (enter for none): <p>profe</p>
OK, successfully used password, moving on...

Setting the root password or using the unix_socket ensures that nobody
can log into the MariaDB root user without the proper authorisation.

You already have your root account protected, so you can safely answer 'n'.

Switch to unix_socket authentication [Y/n] <kbd>enter</kbd>
Enabled successfully!
Reloading privilege tables..
 ... Success!


You already have your root account protected, so you can safely answer 'n'.

Change the root password? [Y/n] <kbd>enter</kbd>
New password: <kbd>profe</kbd>
Re-enter new password: <kbd>profe</kbd>
Password updated successfully!
Reloading privilege tables..
 ... Success!


By default, a MariaDB installation has an anonymous user, allowing anyone
to log into MariaDB without having to have a user account created for
them.  This is intended only for testing, and to make the installation
go a bit smoother.  You should remove them before moving into a
production environment.

Remove anonymous users? [Y/n] <kbd>enter</kbd>
 ... Success!

Normally, root should only be allowed to connect from 'localhost'.  This
ensures that someone cannot guess at the root password from the network.

Disallow root login remotely? [Y/n] <kbd>enter</kbd>
 ... Success!

By default, MariaDB comes with a database named 'test' that anyone can
access.  This is also intended only for testing, and should be removed
before moving into a production environment.

Remove test database and access to it? [Y/n] <kbd>enter</kbd>
 - Dropping test database...
 ... Success!
 - Removing privileges on test database...
 ... Success!

Reloading the privilege tables will ensure that all changes made so far
will take effect immediately.

Reload privilege tables now? [Y/n] <kbd>enter</kbd>
 ... Success!

Cleaning up...

All done!  If you've completed all of the above steps, your MariaDB
installation should now be secure.

Thanks for using MariaDB!
profe@docker-smx:~$ 
</pre>

### Per accedir a **`mariadb`**

```bash
mariadb -u root -pprofe
```

<pre>
profe@docker-smx:~$ mariadb -u root -pprofe
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 54
Server version: 10.6.16-MariaDB-0ubuntu0.22.04.1 Ubuntu 22.04

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
4 rows in set (0.001 sec)

MariaDB [(none)]> exit
Bye
profe@docker-smx:~$ 
</pre>

## Per comprovar el que ja tenim instal·lat

```bash
sudo lsof -i TCP
```

<pre>
profe@docker-smx:~$ sudo lsof -i TCP
COMMAND    PID            USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
(...)
sshd       695            root    3u  IPv4  20563      0t0  TCP *:ssh (LISTEN)
sshd       695            root    4u  IPv6  20593      0t0  TCP *:ssh (LISTEN)
(...)
apache2   2182            root    4u  IPv6  26196      0t0  TCP *:http (LISTEN)
apache2   2219        www-data    4u  IPv6  26196      0t0  TCP *:http (LISTEN)
apache2   2220        www-data    4u  IPv6  26196      0t0  TCP *:http (LISTEN)
mariadbd  4005           mysql   18u  IPv4  35217      0t0  TCP localhost:mysql (LISTEN)
profe@docker-smx:~$ 
</pre>


## Pas 4: instal·leu els mòduls PHP i PHP

L'últim component de la pila LAMP és instal·lar PHP. Ubuntu 22.04 ja proporciona PHP 8.1 al seu repositori. Podeu instal·lar-lo de la següent manera.


```bash
sudo apt-get -y install php
```

<pre>
profe@docker-smx:~$ sudo apt-get -y install php
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  libapache2-mod-php8.1 php-common php8.1 php8.1-cli php8.1-common php8.1-opcache php8.1-readline
Suggested packages:
  php-pear
The following NEW packages will be installed:
  libapache2-mod-php8.1 php php-common php8.1 php8.1-cli php8.1-common php8.1-opcache php8.1-readline
0 upgraded, 8 newly installed, 0 to remove and 4 not upgraded.
(...)
Processing triggers for php8.1-cli (8.1.2-1ubuntu2.14) ...
Processing triggers for libapache2-mod-php8.1 (8.1.2-1ubuntu2.14) ...
Scanning processes...                                                                                              
Scanning linux images...                                                                                           

Running kernel seems to be up-to-date.

No services need to be restarted.

No containers need to be restarted.

No user sessions are running outdated binaries.

No VM guests are running outdated hypervisor (qemu) binaries on this host.
profe@docker-smx:~$ 
</pre>

Tanmateix, PHP 8.2 és l'última versió estable de PHP en el moment d'escriure aquesta guia. Per tenir aquesta versió, cal instal·lar-la des del **Ondrej Sury PPA**. Que és un repositori que proporciona les últimes versions de PHP, com ara la sèrie PHP 8.x.

De nou a la línia d'ordres, afegiu l'Ondrej PPA tal com es mostra.

```bash
sudo add-apt-repository ppa:ondrej/php
```

<pre>
profe@docker-smx:~$ sudo add-apt-repository ppa:ondrej/php
PPA publishes dbgsym, you may need to include 'main/debug' component
Repository: 'deb https://ppa.launchpadcontent.net/ondrej/php/ubuntu/ jammy main'
Description:
Co-installable PHP versions: PHP 5.6, PHP 7.x, PHP 8.x and most requested extensions are included. Only Supported Versions of PHP (http://php.net/supported-versions.php) for Supported Ubuntu Releases (https://wiki.ubuntu.com/Releases) are provided. Don't ask for end-of-life PHP versions or Ubuntu release, they won't be provided.

Debian oldstable and stable packages are provided as well: https://deb.sury.org/#debian-dpa

You can get more information about the packages at https://deb.sury.org

IMPORTANT: The <foo>-backports is now required on older Ubuntu releases.

BUGS&FEATURES: This PPA now has a issue tracker:
https://deb.sury.org/#bug-reporting

CAVEATS:
1. If you are using php-gearman, you need to add ppa:ondrej/pkg-gearman
2. If you are using apache2, you are advised to add ppa:ondrej/apache2
3. If you are using nginx, you are advised to add ppa:ondrej/nginx-mainline
   or ppa:ondrej/nginx

PLEASE READ: If you like my work and want to give me a little motivation, please consider donating regularly: https://donate.sury.org/

WARNING: add-apt-repository is broken with non-UTF-8 locales, see
https://github.com/oerdnj/deb.sury.org/issues/56 for workaround:

# LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php
More info: https://launchpad.net/~ondrej/+archive/ubuntu/php
Adding repository.
Press [ENTER] to continue or Ctrl-c to cancel. <kbd>enter</kbd>
Adding deb entry to /etc/apt/sources.list.d/ondrej-ubuntu-php-jammy.list
Adding disabled deb-src entry to /etc/apt/sources.list.d/ondrej-ubuntu-php-jammy.list
Adding key to /etc/apt/trusted.gpg.d/ondrej-ubuntu-php.gpg with fingerprint 14AA40EC0831756756D7F66C4F4EA0AAE5267A6C
Hit:1 https://download.docker.com/linux/ubuntu jammy InRelease                                                    
Hit:2 http://es.archive.ubuntu.com/ubuntu jammy InRelease                                                         
Get:3 http://es.archive.ubuntu.com/ubuntu jammy-updates InRelease [119 kB]       
Get:4 https://ppa.launchpadcontent.net/ondrej/php/ubuntu jammy InRelease [23.9 kB]
Get:5 https://ppa.launchpadcontent.net/ondrej/php/ubuntu jammy/main amd64 Packages [122 kB]
Get:6 https://ppa.launchpadcontent.net/ondrej/php/ubuntu jammy/main Translation-en [37.5 kB]
Hit:7 http://es.archive.ubuntu.com/ubuntu jammy-backports InRelease       
Get:8 http://es.archive.ubuntu.com/ubuntu jammy-security InRelease [110 kB]
Fetched 413 kB in 2s (169 kB/s)   
Reading package lists... Done
profe@docker-smx:~$ 
</pre>

Quan se us demani que continueu, premeu <pre>INTRO</pre>. L'ordre afegeix el repositori **`OndreJ`** al directori **`/etc/apt/sources.list.d`** i la clau de signatura **`GPG`**.

A continuació, instal·leu PHP 8.2 mitjançant el gestor de paquets APT.

```bash
sudo apt-get -y install php8.2
```

<pre>
profe@docker-smx:~$ sudo apt-get -y install php8.2
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  libapache2-mod-php8.2 php8.2-cli php8.2-common php8.2-opcache php8.2-readline
Suggested packages:
  php-pear
The following NEW packages will be installed:
  libapache2-mod-php8.2 php8.2 php8.2-cli php8.2-common php8.2-opcache php8.2-readline
0 upgraded, 6 newly installed, 0 to remove and 15 not upgraded.
(...)
Creating config file /etc/php/8.2/apache2/php.ini with new version
libapache2-mod-php8.2: php8.1 module already enabled, not enabling PHP 8.2
Setting up php8.2 (8.2.15-1+ubuntu22.04.1+deb.sury.org+1) ...
Processing triggers for man-db (2.10.2-1) ...
Processing triggers for php8.2-cli (8.2.15-1+ubuntu22.04.1+deb.sury.org+1) ...
Processing triggers for libapache2-mod-php8.2 (8.2.15-1+ubuntu22.04.1+deb.sury.org+1) ...
Scanning processes...                                                                                              
Scanning linux images...                                                                                           

Running kernel seems to be up-to-date.

No services need to be restarted.

No containers need to be restarted.

No user sessions are running outdated binaries.

No VM guests are running outdated hypervisor (qemu) binaries on this host.
</pre>


L'ordre instal·la **`PHP 8.2`** juntament amb altres paquets addicionals i extensions **PHP**, com ara **`php8.2-cli`**, una interfície de línia d'ordres per executar scripts **PHP** des de la línia d'ordres, i **`php8.2-common`**, que inclou fitxers comuns per a paquets PHP.

Per veure la versió de PHP instal·lada, executeu l'ordre:

```bash
php --version
```

<pre>
profe@docker-smx:~$ php --version
PHP 8.2.15 (cli) (built: Jan 20 2024 14:17:05) (NTS)
Copyright (c) The PHP Group
Zend Engine v4.2.15, Copyright (c) Zend Technologies
    with Zend OPcache v8.2.15, Copyright (c), by Zend Technologies
profe@docker-smx:~$ 
</pre>


Utilitzeu la sintaxi següent per instal·lar extensions PHP addicionals.

<pre>
sudo apt install php8.2-[extname]
</pre>


```bash
sudo apt-get -y install php8.2-{mbstring,mysql,zip}
```


<pre>
profe@docker-smx:~$ sudo apt-get -y install php8.2-{mbstring,mysql,zip}
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  libonig5 libzip4
The following NEW packages will be installed:
  libonig5 libzip4 php8.2-mbstring php8.2-mysql php8.2-zip
0 upgraded, 5 newly installed, 0 to remove and 15 not upgraded.
Need to get 924 kB of archives.
After this operation, 2,598 kB of additional disk space will be used.
(...)
Creating config file /etc/php/8.2/mods-available/mbstring.ini with new version
Processing triggers for libapache2-mod-php8.2 (8.2.15-1+ubuntu22.04.1+deb.sury.org+1) ...
Processing triggers for libc-bin (2.35-0ubuntu3.6) ...
Processing triggers for php8.2-cli (8.2.15-1+ubuntu22.04.1+deb.sury.org+1) ...
Scanning processes...                                                                                              
Scanning linux images...                                                                                           

Running kernel seems to be up-to-date.

No services need to be restarted.

No containers need to be restarted.

No user sessions are running outdated binaries.

No VM guests are running outdated hypervisor (qemu) binaries on this host.
profe@docker-smx:~$ 
</pre>
