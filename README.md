# Creació del primer contenidor amb Docker

**Pas 1**: Creació de l'estructura de nostre primer projecte

Comandes a executar:

```
mkdir ~/c01-pagina-web
cd ~/c01-pagina-web
```

**Pas 2**: Descarrega dels fitxers del web site.

Comandes a executar:

```
mkdir ~/c01-pagina-web/web-exemple
cd ~/c01-pagina-web/web-exemple
wget https://github.com/SMX-2022-2024/02-installacio-docker/raw/main/web-example.zip
unzip web-example.zip
Archive:  web-example.zip
   creating: assets/
   creating: assets/webfonts/
  inflating: assets/webfonts/fa-regular-400.woff 
...
  inflating: images/pic04.jpg        
  inflating: index.html
```




```
root@docker-sxm:/home/profe/pagina-web# tree
.
└── pagina-web
    └── web-example
        ├── assets
        ├── images
        ├── index.html
        ├── single.html
        └── web-example.zip
```

