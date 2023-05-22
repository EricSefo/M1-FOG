# Llençar un paquet per a que s’instal·li als clients

Primerament ens dirigim al client Windows el qual hem realitzat la captura del client Windows i introduïm les credencials del servidor FOG. Ens haurem de fixar en l'opció de debaix de tot on apareix **FOG Client** perquè l'utilitzarem per llençar el paquet per la xarxa.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 17-13-31.png)

Connectats ja al servidor fem clic a l'apartat que es troba abaix de tot de la pàgina "**FOG Client**"

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 17-13-39.png)

Fem clic a **FOG Client**.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 17-08-43.png)

Seleccionem l'opció **Smart Intaller (Recomended)**.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 17-13-51.png)

Donem permisos d'administrador per poder executar l'instal·lador de l'aplicació.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 17-14-09.png)

Al camp "Server Address" indiquem l'adreça IP del servidor FOG, la resta de camps els deixem per defecte.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 17-15-39.png)

Finalitzem l'instal·lació.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 17-15-49.png)

A continuació, ens dirigim a "Servicios" de Windows i busquem el servei **FOGService** i fem clic a "Propiedades", seguidament, iniciem el servei i posem al tipus d'inici del servei en "Automático".

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 17-17-19.png)

Apliquem els canvis i anem al servidor Ubuntu.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 17-17-29.png)

Després, al servidor Ubuntu descargarem un instal·lador amb l'extensió **.msi**, en aquest cas volem instal·lar Google Chrome.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 17-46-21.png)

Ens dirigim a **Snapin management** i creem un nou "Snapin" (complement). Indicarem el nom, la descripció, en **Snaping Template** posarem MSI i en **Snaping File** indicarem la ruta del fixer .msi del Google Chrome.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 17-47-19.png)

Seguidament, ens dirigim al host de Windows 10 que tenim registrat de l'apartat **Captura de la imatge d'un client Windows 10**. En l'apartat **Snapins** del host fem clic a "Check here to see what snapins can be added".

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 17-48-09.png)

Després, triem el snapin creat anteriorment de Google Chrome i l'afegim.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 17-48-20.png)

A continuació, fem clic a **Basic Tasks** i després a **Advanced**.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 17-48-45.png)

Fem clic abaix de tot en **Single Snapin**.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 17-49-15.png)

Triem el snaping que volem instal·lar que en aquest cas és el de Google Chrome i indiquem que és realitzi la tasca a l'instant triant l'opció **Schedule instant**.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-22 12-11-00.png)

La tasca s'ha creat correctament.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 17-49-37.png)

A l'iniciar el client Windows 10 al qual vam registrar i capturar la seva imatge, podrem comprovar que l'aplicació Google Chrome s'haurà instal·lat a l'iniciar el sistema automàticament.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 17-50-24.png)