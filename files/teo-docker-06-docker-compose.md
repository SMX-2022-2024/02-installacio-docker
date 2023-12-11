## [Enllaç documentació oficial (docs.docker.com/compose)](https://docs.docker.com/compose/)

# Què és **```docker compose```**

La comanda **```docker compose```** és una eina per definir i executar aplicacions **Docker** de diversos contenidors. **docker compose**, es fa servir un fitxer **```YAML```** per configurar els serveis del **vostre sistema**. Fins al punt, que amb una única comanda, es crea i s'inicien tots els serveis del **vostre sistema**.

**```docker compose```** funciona en tots els ambients: **producció**, **posada en escena** (***staging***), **desenvolupament**, **proves**, així com fluxos de **treball CI** (***workflow CI***). També té ordres per gestionar tot el **cicle de vida** de la vostra aplicació:

* Iniciar, aturar i reconstruir els serveis

* Veure l'estat dels serveis en execució

* Transmetre la sortida del registre dels serveis en execució

* Executar una comanda única en un servei

## Provem **```docker compose```**

Aquest tutorial està dissenyat per introduir els conceptes clau de **```docker compose```** mentre es construeix una aplicació web senzilla de **Python**. L'aplicació utilitza el marc **Flask** i manté un comptador de visites a **Redis**.

**Els conceptes que es mostren aquí són comprensibles encara que no estigueu familiaritzat amb Python.**

### Requisits previs

**1.** Cal tenir **Docker Engine** a la vostra màquina.

Validació que tenim **Docker Engine** instal·lat:

* **Comandes a executar**:

```
sudo docker --version
```

* **Sortida**:

```
profe@docker-sxm:~$ sudo docker --version
Docker version 24.0.7, build afdd53b
profe@docker-sxm:~$ _
```

Si no el teniu instal·lat, el podeu instal·lar seguint l'enllaç [Install Docker Engine on Ubuntu](https://docs.docker.com/engine/install/ubuntu/)

**2.** Cal tenir **Docker Compose** a la vostra màquina.

Validació que tenim **Docker Compose** instal·lat:

* **Comandes a executar**:

```
sudo docker compose version
```

* **Sortida**:

```
profe@docker-sxm:~$ sudo docker compose version
Docker Compose version v2.21.0
profe@docker-sxm:~$ _
```

Si no el teniu instal·lat, el podeu instal·lar seguint l'enllaç [Install Compose standalone](https://docs.docker.com/compose/install/standalone/)


**3.** No cal que instal·leu **Python** o **Redis**, ja que tots dos els proporcionen les **imatges de ```Docker```**.

## **Pas 1**: definir les dependències de l'aplicació

Creem un directori per al projecte:

* **Comandes a executar**:

```
sudo mkdir ~/teo-compose
cd ~/teo-compose
```

* **Sortida**:

```
profe@docker-sxm:~$ sudo mkdir ~/teo-compose
profe@docker-sxm:~$ cd ~/teo-compose
profe@docker-sxm:~/teo-compose$ _ 
```

