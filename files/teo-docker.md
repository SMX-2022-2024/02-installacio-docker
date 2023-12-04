# Visió general de *Docker*

**Docker** és una **plataforma oberta** per **desenvolupar**, **enviar** i **executar aplicacions**

**Docker** permet separar les aplicacions de la infraestructura perquè es pugui lliurar programari ràpidament.

Amb Docker, es pot gestionar la infraestructura de la mateixa manera que es gestionen les aplicacions.

Aprofitant les metodologies de Docker per enviar, provar i desplegar codi, podeu reduir significativament el retard entre escriure el codi i executar-lo en producció.

## La plataforma *Docker*

**Docker** ofereix la possibilitat d'**empaquetar** i **executar** una aplicació en un entorn poc aïllat anomenat **contenidor**.

L'aïllament i la seguretat permeten executar molts contenidors simultàniament en un host determinat.

Els contenidors són lleugers i contenen tot el necessari per executar l'aplicació, de manera que no cal confiar en el que està instal·lat a l'amfitrió.

Es poden compartir contenidors mentre es treballa i s'assegur que tothom amb es comparteix tingui el mateix contenidor que funcioni de la mateixa manera.

Docker ofereix eines i una plataforma per gestionar el cicle de vida dels vostres contenidors:

* Desenvolupar una aplicació i els seus components de suport mitjançant contenidors.

* El contenidor es converteix en la unitat per distribuir i provar l'aplicació.

* Quan estigui preparada l'aplicació, cal implementar-la en en entorn de producció, com a contenidor o servei orquestrat. 

Això funciona igual tant si l'entorn de producció és un centre de dades local, un proveïdor de núvol o un híbrid dels dos.

## Per a què utilitzar Docker?

### Lliurament ràpid i coherent de les aplicacions

**Docker** racionalitza el **cicle de vida del desenvolupament** permetent als desenvolupadors treballar en entorns estandarditzats mitjançant contenidors locals que proporcionen les vostres aplicacions i serveis.

Els contenidors són ideals per a la integració contínua i els fluxos de treball de lliurament continu (**CI/CD**).

Considereu el següent exemple d'escenari:

* Els col·laboradors i desenvolupadors escriuen codi localment i comparteixen el seu treball amb els seus col·legues mitjançant contenidors **Docker**.

* Utilitzen **Docker** per introduir les seves aplicacions a un entorn de prova i executar proves manuals i automatitzades.

* Quan els desenvolupadors troben errors, poden corregir-los a l'entorn de desenvolupament i tornar-los a desplegar a l'entorn de prova per provar-los i validar-los.

* Quan s'hagi completat la prova, aconseguir la solució al client és tan senzill com enviar la imatge actualitzada a l'entorn de producció.

### Desplegament sensible i escalat

La plataforma basada en **contenidors de Docker** permet càrregues de treball altament portàtils. Els **contenidors de Docker** es poden executar a l'ordinador portàtil local d'un desenvolupador, en màquines físiques o virtuals d'un centre de dades, en proveïdors de núvol o en una barreja d'entorns.

La portabilitat i la lleugeresa de **Docker** també faciliten la gestió dinàmica de les càrregues de treball, augmentant o eliminant aplicacions i serveis segons les necessitats empresarials, gairebé en temps real.

### Executant més càrregues de treball al mateix maquinari

**Docker** és lleuger i ràpid.

Proporciona una alternativa viable i rendible a les màquines virtuals basades en hipervisor, de manera que podeu utilitzar més de la capacitat del vostre servidor per assolir els vostres objectius empresarials.

**Docker** és perfecte per a entorns d'alta densitat i per a implementacions petites i mitjanes on necessiteu fer més amb menys recursos.
