# Creació del primer contenidor amb Docker

**Pas 1**: Creació de l'estructura de nostre primer projecte

* **Comandes a executar**:

```
mkdir ~/c01-pagina-web
cd ~/c01-pagina-web
```

<br><hr><br>

**Pas 2**: Descarrega dels fitxers del web site.

* **Comandes a executar**:

```
mkdir ~/c01-pagina-web/web-exemple
cd ~/c01-pagina-web/web-exemple
wget https://github.com/SMX-2022-2024/02-installacio-docker/raw/main/web-exemple.zip
```

* **Sortida**:

```
# wget https://github.com/SMX-2022-2024/02-installacio-docker/raw/main/web-exemple.zip
--2023-12-02 18:46:16--  https://github.com/SMX-2022-2024/02-installacio-docker/raw/main/web-exemple.zip
Resolving github.com (github.com)... 140.82.121.3
Connecting to github.com (github.com)|140.82.121.3|:443... connected.
...
Length: 1547642 (1.5M) [application/zip]
Saving to: ‘web-exemple.zip’

web-exemple.zip                    100%[================================================================>]   1.48M  1.25MB/s    in 1.2s    

2023-12-02 18:46:19 (1.25 MB/s) - ‘web-exemple.zip’ saved [1547642/1547642]

root@docker-sxm:/home/profe/c01-pagina-web# ls -l
total 1512
-rw-r--r-- 1 root root 1547642 Dec  2 18:46 web-exemple.zip
```

<br><hr><br>

**Pas 3**: Descomprimir el fitxer zip descarregat.

* **Comandes a executar**:

```
unzip web-exemple.zip
```

* **Sortida**:

```
unzip web-exemple.zip
Archive:  web-exemple.zip
   creating: assets/
   creating: assets/webfonts/
  inflating: assets/webfonts/fa-regular-400.woff 
...
  inflating: images/pic04.jpg        
  inflating: index.html
```

<br><hr><br>

**Pas 4**: Comprovació de l'estructura de fitxers

* **Comandes a executar**:

```
root@docker-sxm:/home/profe/c01-pagina-web# tree -L 2
```

* **Sortida**:

```
.
├── web-exemple
│   ├── assets
│   ├── images
│   ├── index.html
│   ├── magna-sed-adipiscing.html
│   ├── odio-congue-mattis.html
│   ├── rutrum-neque-accumsan.html
│   ├── unic.html
│   └── vitae-sed-condimentum.html
└── web-exemple.zip
```

