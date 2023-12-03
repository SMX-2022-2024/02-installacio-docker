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

## **Pas 1**: Creació de l'estructura de nostre primer projecte

* **Comandes a executar**:

```
sudo mkdir ~/c01-contenidor-nginx
cd ~/c01-contenidor-nginx
```

* **Sortida**:

```
profe@docker-sxm:~$ sudo mkdir ~/c01-contenidor-nginx
profe@docker-sxm:~$ cd ~/c01-contenidor-nginx
profe@docker-sxm:~/c01-contenidor-nginx$ _ 
```

<hr>

## **Pas 2**: Obtenció de la imatge del servidor web **```nginx```**.

### **Pas 2.1**: Primer cal comprovar <u>*si tenim descarregada localment*</u> la imatge de **```docker```** d'**```nginx```**.

* **Comanda a executar**:

```
sudo docker image ls
```

* **Sortida**:

```
REPOSITORY    TAG       IMAGE ID       CREATED        SIZE
....
nginx         latest    a6bd71f48f68   12 days ago    187MB
....
```

## [Més informació a **```docker image```**](./files/opcions-de-les-comandes-docker.md#comanda-1-docker-image-comandes)

### Descripció:

Per gestionar de les imatges de **```docker```**

### Ús:

```
docker image COMANDES
```

### Explicació de les opcions (**```[OPTIONS]```**) fetes servir amb la comanda **```docker image ls```**: 

```
docker image ls
```

> **```ls```**

La comanda **```ls```**: Llista les imatges que tenim al nostre servidor.

> #### Si la imatge **```nginx:latest```** apareix a la llista de les imatges descarregades, llavors ja tenim la tenim descarregada al nostre servidor.

Si no ens apareix a l'hora de llistar les imatges, llavors cal descarregar-la.

**Pas 2.2**: Per obtenir una imatge descarregant-la de [**```hub.docker.com```**](https://hub.docker.com/).

<hr>

**Pas 3**: Creació i posada en marxa del contenidor amb el servidor web **```nginx```**.

* **Comandes a executar**:

```
cd ~/c01-contenidor-nginx
sudo docker container run --name c01-nginx -d nginx
```

## [Més informació a **```docker container run```**](./files/opcions-de-les-comandes-docker.md#opcions-de-la-comanda-docker-container-run-options)

### Descripció:

Crea i executa un contenidor nou a partir d'una imatge

### Ús:

```
docker container run [OPTIONS] IMAGE [COMMAND] [ARG...]
```

### Explicació de les opcions (**```[OPTIONS]```**) fetes servir amb la comanda **```docker container run```**: 

```
docker container run --name c01-nginx -d nginx
```

> **```--name c01-nginx```**

El paràmetre **```--name <nom del contenidor>```**: Assigna un nom al contenidor


> **```-d, --detach```**

Executa el contenidor en **segon pla** i mostra per pantalla  l'identificador del contenidor.

> **```nginx => [IMAGE]```**
 
Indica la imatge de docker que es farà servir per crear el contenidor.
En aquest cas es tracta d'una imatge oficial de **```nginx```**. Si no porta cap etiqueta (**```tag```**) a continuació de la imatge, indica que és la darrera, la més actual (**```latest```**), de les imatges del proveïdor. 


* **Sortida**:

```
profe@docker-sxm:~/c01-contenidor-nginx$ sudo docker container run --name c01-nginx -d nginx
37f45d7ba037e9350d4efb10b7356759aab715e4103fdd299806d2541818809d
profe@docker-sxm:~/c01-contenidor-nginx$ sudo docker container ls
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS     NAMES
37f45d7ba037   nginx     "/docker-entrypoint.…"   7 seconds ago   Up 7 seconds   80/tcp    c01-nginx
profe@docker-sxm:~/c01-contenidor-nginx$ 
```

**Pas 3**: Comprovació del correcte funcionament del contenidor amb el servidor web **```nginx```**.

Per poder comprovar si funciona el contenidor amb el servidor web **```nginx```**, abans cal esbrinar quina és l'adreça IP que té en nostre servidor virtual.

* **Comandes a executar**:

```bash
ip a
```

Aquesta comanda ens mostra de **TOTA** la informació **totes** les **interfície de xarxa** del servidor.

```
profe@docker-sxm:~/c01-contenidor-nginx$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:67:51:5c brd ff:ff:ff:ff:ff:ff
    inet 10.0.2.15/24 metric 100 brd 10.0.2.255 scope global dynamic enp0s3
       valid_lft 65087sec preferred_lft 65087sec
    inet6 fe80::a00:27ff:fe67:515c/64 scope link 
       valid_lft forever preferred_lft forever
3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:d9:b8:85 brd ff:ff:ff:ff:ff:ff
    inet 192.168.56.122/24 metric 100 brd 192.168.56.255 scope global dynamic enp0s8
       valid_lft 597sec preferred_lft 597sec
    inet6 fe80::a00:27ff:fed9:b885/64 scope link 
       valid_lft forever preferred_lft forever
4: docker0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default 
    link/ether 02:42:f6:54:10:34 brd ff:ff:ff:ff:ff:ff
    inet 172.17.0.1/16 brd 172.17.255.255 scope global docker0
       valid_lft forever preferred_lft forever
    inet6 fe80::42:f6ff:fe54:1034/64 scope link 
       valid_lft forever preferred_lft forever
56: veth808d7e6@if55: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue master docker0 state UP group default 
    link/ether 7e:bb:61:c1:0e:ac brd ff:ff:ff:ff:ff:ff link-netnsid 0
    inet6 fe80::7cbb:61ff:fec1:eac/64 scope link 
       valid_lft forever preferred_lft forever
```

Pero a nosaltres, només ens interessa l'informació de l'**interfície de xarxa** que està configurada com **```Host-Only```**, i, si el Virtual Box està amb els valor per defecte, aquestes interfícies tenen una **adreça IP** que comença amb **```192.168.56```**.

* **Comanda a executar**:

```bash
ip a | grep 192.168.56
```

* **Sortida**:

```
profe@docker-sxm:~/c01-contenidor-nginx$ ip a | grep 192.168.56
    inet 192.168.56.122/24 metric 100 brd 192.168.56.255 scope global dynamic enp0s8
profe@docker-sxm:~/c01-contenidor-nginx$ 
```

L'adreça IP que ens interessa és aquella que comença és, en aquest és **```192.168.56.122```**.

Ara que ja coneixem l'**adreça IP** amb la que podem accedir al nostre servidor a taves de l'**interfície de xarxa** que està configurada com **```Host-Only```**, només cal escriure-la a un navegador web del nostre portàtil.


![Alt text](./images/image-001-welcome-nginx.png)

<!-- Allotjament d'algun contingut estàtic senzill -->

<!-- **Pas 2**: Descarrega dels fitxers del web site.

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

<hr>

**Pas 2**: Descomprimir el fitxer zip descarregat.

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

-->