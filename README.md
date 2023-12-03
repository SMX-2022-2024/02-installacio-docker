# Primer contenidor amb Docker

En aquesta activitat crearem un contenidor amb **```nginx```**.


> ### Què és nginx?
><hr>
>
> **```nginx```** (pronunciat **```engine-x```**) és un ***servidor intermediari invers*** (**```reverse proxy server```**) de ***codi obert*** (**```open source```**) per als protocols **```HTTP```**, **```HTTPS```**, **```SMTP```**, **```POP3```** i **```IMAP```**, així com un servidor per ***balancejar la càrrega*** (**```load balancer```**), ***memòria cau HTTP*** (**```HTTP cache```**) i un ***servidor web*** (l'origen d'aquest servidor).
> 
>El **projecte ```nginx```** va començar amb un fort enfocament en l'alta concurrència, alt rendiment i baix ús de memòria.
> 
>Té llicència sota la llicència de 2 clàusules tipus BSD ([2-clause BSD-like license](https://opensource.org/license/bsd-2-clause/)) i s'executa a Linux, variants BSD, Mac OS X, Solaris, AIX, HP-UX, així com en altres sabors **```*nix```**.
> 
>També té un port de prova de concepte per a Microsoft Windows.
> 
><hr>

<hr>
<br>

**Pas 1**: Creació de l'estructura de nostre primer projecte

* **Comandes a executar**:

```
sudo mkdir ~/c01-contenidor-nginx
sudo cd ~/c01-contenidor-nginx
```

* **Sortida**:

```
profe@docker-sxm:~$ sudo mkdir ~/c01-contenidor-nginx
profe@docker-sxm:~$ cd ~/c01-contenidor-nginx
profe@docker-sxm:~/c01-contenidor-nginx$ 
```

<hr>

**Pas 2**: Descarrega dels fitxers del web site.

* **Comandes a executar**:

```
cd ~/c01-contenidor-nginx
sudo wget https://github.com/SMX-2022-2024/02-installacio-docker/raw/main/web-exemple.zip
```

* **Sortida**:

```
profe@docker-sxm:~/c01-contenidor-nginx$ cd ~/c01-contenidor-nginx
profe@docker-sxm:~/c01-contenidor-nginx$ sudo wget https://github.com/SMX-2022-2024/02-installacio-docker/raw/main/web-exemple.zip
--2023-12-02 19:54:05--  https://github.com/SMX-2022-2024/02-installacio-docker/raw/main/web-exemple.zip
Resolving github.com (github.com)... 140.82.121.4
Connecting to github.com (github.com)|140.82.121.4|:443... connected.
HTTP request sent, awaiting response... 302 Found
Location: https://raw.githubusercontent.com/SMX-2022-2024/02-installacio-docker/main/web-exemple.zip [following]
--2023-12-02 19:54:06--  https://raw.githubusercontent.com/SMX-2022-2024/02-installacio-docker/main/web-exemple.zip
Resolving raw.githubusercontent.com (raw.githubusercontent.com)... 185.199.110.133, 185.199.109.133, 185.199.108.133, ...
Connecting to raw.githubusercontent.com (raw.githubusercontent.com)|185.199.110.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1547642 (1.5M) [application/zip]
Saving to: ‘web-exemple.zip’

web-exemple.zip                    100%[================================================================>]   1.48M  5.69MB/s    in 0.3s    

2023-12-02 19:54:06 (5.69 MB/s) - ‘web-exemple.zip’ saved [1547642/1547642]

profe@docker-sxm:~/c01-contenidor-nginx$ 
```

<hr>

**Pas 3**: Descomprimir el fitxer zip descarregat.

* **Comandes a executar**:

```
sudo unzip web-exemple.zip
sudo mv web-exemple html
sudo chmod -R 777 ~/c01-contenidor-nginx/html
```

* **Sortida**:

```
profe@docker-sxm:~/c01-contenidor-nginx$ sudo unzip web-exemple.zip
Archive:  web-exemple.zip
   creating: web-exemple/
  inflating: web-exemple/vitae-sed-condimentum.html  
   creating: web-exemple/assets/
...
  inflating: web-exemple/images/pic01.jpg  
  inflating: web-exemple/images/pic02.jpg  
  inflating: web-exemple/images/avatar.jpg  
  inflating: web-exemple/images/pic04.jpg  
  inflating: web-exemple/rutrum-neque-accumsan.html  
  inflating: web-exemple/magna-sed-adipiscing.html  
  inflating: web-exemple/odio-congue-mattis.html

root@docker-sxm:~/c01-contenidor-nginx# ls -l
total 1516
drwxrwxr-x 4 root root    4096 Dec  2 18:34 web-exemple
-rw-r--r-- 1 root root 1547642 Dec  2 19:40 web-exemple.zip

root@docker-sxm:~/c01-contenidor-nginx# mv web-exemple html

root@docker-sxm:~/c01-contenidor-nginx# ls -l
total 1516
drwxrwxr-x 4 root root    4096 Dec  2 18:34 html
-rw-r--r-- 1 root root 1547642 Dec  2 19:40 web-exemple.zip

root@docker-sxm:~/c01-contenidor-nginx# ls -ld html
drwxrwxr-x 4 root root 4096 Dec  2 18:34 html

root@docker-sxm:~/c01-contenidor-nginx# chmod -R 777 ~/c01-contenidor-nginx/html

root@docker-sxm:~/c01-contenidor-nginx# ls -ld html
drwxrwxrwx 4 root root 4096 Dec  2 18:34 html
```

<hr>

**Pas 4**: Comprovació de l'estructura de fitxers

* **Comandes a executar**:

```
cd ~/c01-contenidor-nginx
tree -L 2
```

* **Sortida**:

```
profe@docker-sxm:~/c01-contenidor-nginx$ cd ~/c01-contenidor-nginx
profe@docker-sxm:~/c01-contenidor-nginx$ tree -L 2
.
├── html
│   ├── assets
│   ├── images
│   ├── index.html
│   ├── magna-sed-adipiscing.html
│   ├── odio-congue-mattis.html
│   ├── rutrum-neque-accumsan.html
│   ├── unic.html
│   └── vitae-sed-condimentum.html
└── web-exemple.zip

3 directories, 7 files
profe@docker-sxm:~/c01-contenidor-nginx$
```

<hr>

**Pas 5**: Creació i posada en marxa del contenidor amb el servidor web **```nginx```**.

* **Comandes a executar**:

```
cd ~/c01-contenidor-nginx
docker run --name cont-prova1 -v /html:/usr/share/nginx/html:ro -p 80:80 -d nginx
```

* **Sortida**:

```
c01-contenidor-nginx# docker run --name cont-prova1 -v /web-exemple:/usr/share/nginx/html:ro -d nginx
7d3f36cde16a3a2bdf9267eaa7b5a1f03bbea05ad33090cd9e56fd8eddd58c5c
c01-contenidor-nginx# docker container ls
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS     NAMES
7d3f36cde16a   nginx     "/docker-entrypoint.…"   19 seconds ago   Up 18 seconds   80/tcp    cont-prova1
c01-contenidor-nginx# 
```


Allotjament d'algun contingut estàtic senzill


