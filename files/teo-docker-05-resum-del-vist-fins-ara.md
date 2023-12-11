# Resum del que hem vist fins ara

**1.** Totes les **comandes de ```docker```** segueixen el mateix patró.

> **```docker <objecte> [opcions] comanda```**

* Si volem fer alguna cosa relacionada amb una **imatge** **```docker image [opcions] comanda```**.

* Si volem fer alguna cosa relacionada amb un **contenidor** **```docker container [opcions] comanda```**.

* Si volem fer alguna cosa relacionada amb un **volum** (***volume***) **```docker volum [opcions] comanda```**.

* Si volem fer alguna cosa relacionada amb una **xarxa** (***network***) **```docker network [opcions] comanda```**.

**2.** **```nginx```** és un ***servidor web***

**3.** La comanda **```sudo docker image list```** mostra totes les imatges que tenim descarregades localment en el nostre servidor. Aportant informació dels següents camps:

* **```REPOSITORY```**: Mostra el **nom** de la imatge.

* **```TAG```**: Mostra l'etiqueta de la imatge.

* **```IMAGE ID```**: Mostra l'**ID** (***identificador únic***) de la imatge.

* **```CREATED```**: Mostra el moment en què es va crear la imatge.

* **```SIZE```**: Mostra la mida del disc que és ocupada per la imatge.

> [!TIP]
>
> #### Exemple
> 
> ```
> REPOSITORY     TAG       IMAGE ID       CREATED        SIZE
> nginx          latest    a6bd71f48f68   2 weeks ago    187MB
> ```
>
><hr>

**4.** La comanda **```sudo docker image pull [OPTIONS] NAME[:TAG|@DIGEST]```** descarrega la imatge amb el nom **```NAME[:TAG]```** del lloc web de [**```hub.docker.com```**](https://hub.docker.com/).

> [!TIP]
>
> #### Exemple
> 
> * **Comanda a executar**:
> 
> ```
> sudo docker image pull nginx
> ```
> 
> * **Sortida**:
> 
> ```
> profe@docker-sxm:~$ sudo docker image pull nginx
> Using default tag: latest
> latest: Pulling from library/nginx
> 1f7ce2fa46ab: Pull complete 
> 9b16c94bb686: Pull complete 
> 9a59d19f9c5b: Pull complete 
> 9ea27b074f71: Pull complete 
> c6edf33e2524: Pull complete 
> 84b1ff10387b: Pull complete 
> 517357831967: Pull complete 
> Digest: sha256:10d1f5b58f74683ad34eb29287e07dab1e90f10af243f151bb50aa5dbb4d62ee
> Status: Downloaded newer image for nginx:latest
> docker.io/library/nginx:latest
> profe@docker-sxm:~$_
> ```
>
><hr>

**5.** La comanda **```docker search [OPTIONS] TERM```** busca la imatge amb el nom **```TERM```** del lloc web de [**```hub.docker.com```**](https://hub.docker.com/). 

> [!TIP]
>
> #### Exemple
> 
> * **Comanda a executar**:
> 
> ```
> sudo docker search nginx
> ```
> 
> * **Sortida**:
> 
> ```
> profe@docker-sxm:~$ sudo docker search nginx
> NAME                               DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
> nginx                              Official build of Nginx.                        19311     [OK]       
> unit                               Official build of NGINX Unit: Universal Web …   19        [OK]       
> nginxinc/nginx-unprivileged        Unprivileged NGINX Dockerfiles                  136                  
> nginx/nginx-ingress                NGINX and  NGINX Plus Ingress Controllers fo…   86                   
> nginx/nginx-prometheus-exporter    NGINX Prometheus Exporter for NGINX and NGIN…   33                   
> nginxinc/nginx-s3-gateway          Authenticating and caching gateway based on …   3                    
> nginx/unit                         This repository is retired, use the Docker o…   64                   
> nginx/nginx-ingress-operator       NGINX Ingress Operator for NGINX and NGINX P…   2                    
> nginxinc/amplify-agent             NGINX Amplify Agent docker repository           1                    
> nginx/nginx-quic-qns               NGINX QUIC interop                              1                    
> nginxinc/ingress-demo              Ingress Demo                                    4                    
> nginxproxy/nginx-proxy             Automated Nginx reverse proxy for docker con…   119                  
> nginxproxy/acme-companion          Automated ACME SSL certificate generation fo…   127                  
> bitnami/nginx                      Bitnami nginx Docker Image                      180                  [OK]
> bitnami/nginx-ingress-controller   Bitnami Docker Image for NGINX Ingress Contr…   32                   [OK]
> ubuntu/nginx                       Nginx, a high-performance reverse proxy & we…   103                  
> nginxinc/nginmesh_proxy_debug                                                      0                    
> nginxproxy/docker-gen              Generate files from docker container meta-da…   14                   
> kasmweb/nginx                      An Nginx image based off nginx:alpine and in…   6                    
> nginxinc/mra-fakes3                                                                0                    
> rancher/nginx-ingress-controller                                                   11                   
> nginxinc/ngx-rust-tool                                                             0                    
> nginxinc/mra_python_base                                                           0                    
> nginxinc/nginmesh_proxy_init                                                       0                    
> profe@docker-sxm:~$ _
> ```
> <hr>

**6.** La comanda **```sudo docker container list```** llista de **TOTS els contenidors actius** o **que estan en marxa**, que hi ha en el nostre servidor.

Aportant informació dels següents camps:

* **```CONTAINER ID```**: Mostra l'**identificador únic** del contenidor.

* **```IMAGE```**: Mostra la imatge a partir de la quan s'ha creat el contenidor.

* **```COMMAND```**: Mostra la **comanda** executada en iniciar del contenidor.

* **```CREATED```**: **hora de creació**, hora en què es va crear el contenidor.

* **```STATUS```**: **Estat del contenidor** amb detalls sobre la durada i l'estat de salut (per exemple, **```created```** (***creat***), **```running```** (***en execució***), **```exited```** (***s'ha sortit***)).

* **```PORTS```**: **Ports exposats** en crear el contenidor.

* **```NAMES```**: Mostra el **nom** del contenidor.

> [!TIP]
>
> #### Exemple
> 
> ```
> profe@docker-sxm:~$ sudo docker container list 
> CONTAINER ID   IMAGE       COMMAND                  CREATED        STATUS        PORTS                                   NAMES
> df4d7d30b752   wordpress   "docker-entrypoint.s…"   38 hours ago   Up 38 hours   0.0.0.0:8085->80/tcp, :::8085->80/tcp   c02-wp-wordpress-1
> a4ca320542fb   mysql:5.7   "docker-entrypoint.s…"   38 hours ago   Up 17 hours   3306/tcp, 33060/tcp                     c02-wp-db-1
> profe@docker-sxm:~$ _
> ```
>
><hr>

**7.** La comanda **```sudo docker container list -a```** llista **TOTS els contenidors** que hi ha en el nostre servidor. Fins i tot aquells que **NO estan actius o en marxa**.

> [!TIP]
>
> #### Exemple
> 
> ```
> profe@docker-sxm:~$ sudo docker container list -a
> CONTAINER ID   IMAGE       COMMAND                  CREATED          STATUS                    PORTS                                   NAMES
> 6ba80d4798c6   nginx       "/docker-entrypoint.…"   22 seconds ago   Exited (0) 1 second ago                                           c01-nginx-web-1
> df4d7d30b752   wordpress   "docker-entrypoint.s…"   38 hours ago     Up 38 hours               0.0.0.0:8085->80/tcp, :::8085->80/tcp   c02-wp-wordpress-1
> a4ca320542fb   mysql:5.7   "docker-entrypoint.s…"   38 hours ago     Up 17 hours               3306/tcp, 33060/tcp                     c02-wp-db-1
> profe@docker-sxm:~$ $ _
> ```
>
><hr>

**8.** La comanda **```sudo docker container list -q```** ens mostra només el **```CONTAINER ID```** de **TOTS els contenidors** que hi ha en el nostre servidor.

> [!TIP]
>
> #### Exemple
> 
> ```
> profe@docker-sxm:~$ sudo docker container list -q
> df4d7d30b752
> a4ca320542fb
> profe@docker-sxm:~$ _
> ```
>
><hr>


**9.** La comanda **```sudo docker container stop [OPTIONS] CONTAINER [CONTAINER...]```** **atura un o més contenidors actius** o que estan en marxa en el nostre servidor. Cal que li indiquem l'identificador o el nom del contenidor, i podem passar-li més d'un identificador o més d'un nom del contenidor.

> [!TIP]
>
> #### Exemple
> 
> ```
> profe@docker-sxm:~ sudo docker container list
> CONTAINER ID   IMAGE       COMMAND                  CREATED          STATUS          PORTS                                   NAMES
> 6ba80d4798c6   nginx       "/docker-entrypoint.…"   12 seconds ago   Up 12 seconds   0.0.0.0:8080->80/tcp, :::8080->80/tcp   c01-nginx-web-1
> df4d7d30b752   wordpress   "docker-entrypoint.s…"   38 hours ago     Up 38 hours     0.0.0.0:8085->80/tcp, :::8085->80/tcp   c02-wp-wordpress-1
> a4ca320542fb   mysql:5.7   "docker-entrypoint.s…"   38 hours ago     Up 17 hours     3306/tcp, 33060/tcp                     c02-wp-db-1
> 
> profe@docker-sxm:~ sudo docker container stop 6ba80d4798c6
> 6ba80d4798c6
 > 
> profe@docker-sxm:~ sudo docker container list
> CONTAINER ID   IMAGE       COMMAND                  CREATED          STATUS                    PORTS                                   NAMES
> df4d7d30b752   wordpress   "docker-entrypoint.s…"   38 hours ago     Up 38 hours               0.0.0.0:8085->80/tcp, :::8085->80/tcp   c02-wp-wordpress-1
> a4ca320542fb   mysql:5.7   "docker-entrypoint.s…"   38 hours ago     Up 17 hours               3306/tcp, 33060/tcp                     c02-wp-db-1
> profe@docker-sxm:~ 
> ```
>
><hr>

**10.** La comanda **```sudo docker container remove [OPTIONS] CONTAINER [CONTAINER...]```** **elimina del nostre servidor un o més contenidors**. Cal que li indiquem l'identificador o el nom del contenidor, i podem passar-li més d'un identificador o més d'un nom de contenidor i que **el contenidor estigui aturat**.

> [!TIP]
>
> #### Exemple
> 
> ```
> profe@docker-sxm:~ sudo docker container list -a
> CONTAINER ID   IMAGE       COMMAND                  CREATED         STATUS                     PORTS                                   NAMES
> 6ba80d4798c6   nginx       "/docker-entrypoint.…"   4 minutes ago   Exited (0) 4 minutes ago                                           c01-nginx-web-1
> df4d7d30b752   wordpress   "docker-entrypoint.s…"   38 hours ago    Up 38 hours                0.0.0.0:8085->80/tcp, :::8085->80/tcp   c02-wp-wordpress-1
> a4ca320542fb   mysql:5.7   "docker-entrypoint.s…"   38 hours ago    Up 17 hours                3306/tcp, 33060/tcp                     c02-wp-db-1
> profe@docker-sxm:~ sudo docker container remove 6ba80d4798c6
> 6ba80d4798c6
> profe@docker-sxm:~ sudo docker container list -a
> CONTAINER ID   IMAGE       COMMAND                  CREATED        STATUS        PORTS                                   NAMES
> df4d7d30b752   wordpress   "docker-entrypoint.s…"   38 hours ago   Up 38 hours   0.0.0.0:8085->80/tcp, :::8085->80/tcp   c02-wp-wordpress-1
> a4ca320542fb   mysql:5.7   "docker-entrypoint.s…"   38 hours ago   Up 17 hours   3306/tcp, 33060/tcp                     c02-wp-db-1
> profe@docker-sxm:~ 
> ```
>
><hr>

[Següent **Què és **```docker compose```**?](./teo-docker-06-docker-compose.md)