https://docs.docker.com/compose/

## Què és **```docker compose```**

**```docker compose```** és una eina per definir i executar aplicacions Docker de diversos contenidors. Amb Compose, utilitzeu un fitxer YAML per configurar els serveis de la vostra aplicació. Aleshores, amb una única comanda, creeu i inicieu tots els serveis des de la vostra configuració.

**```docker compose```** funciona en tots els ambients: **producció**, **posada en escena** (***staging***), **desenvolupament**, **proves**, així com fluxos de **treball CI** (***workflow CI***) . També té ordres per gestionar tot el **cicle de vida** de la vostra aplicació:

* Iniciar, aturar i reconstruir els serveis

* Veure l'estat dels serveis en execució

* Transmetre la sortida del registre dels serveis en execució

* Executar una comanda única en un servei

## Provem **```docker compose```**

Aquest tutorial està dissenyat per introduir els conceptes clau de **```docker compose```** mentre es construeix una aplicació web senzilla de **Python**. L'aplicació utilitza el marc **Flask** i manté un comptador de visites a **Redis**.

**Els conceptes que es mostren aquí són comprensibles encara que no estigueu familiaritzat amb Python.**

## Pas 1: definir les dependències de l'aplicació

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

