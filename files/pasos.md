sudo mkdir imatge-joan
cd imatge-joan

sudo vi Dockerfile

```
# Utiliza Alpine Linux como base
FROM alpine

# Etiqueta con tu información de contacto (opcional)
LABEL maintainer="joanpardo@ginebro.cat"

# Ejecuta unos comandos para mostrar un mensaje al iniciar el contenedor
CMD echo "echo '¡Hola des del meu contenidor amb Linux Alpine!'" > hola
CMD chmod 777 hola
CMD /bin/sh hola
CMD sleep infinity
```
#CMD ["sh", "-c", "echo '¡Hola des del meu contenidor amb Linux Alpine!' && sleep infinity"]

```
sudo docker image build -t imatge-joan .
```

```
sudo docker container run --name cont-joan -d imatge-joan
```

```
sudo docker container log cont-joan
```



