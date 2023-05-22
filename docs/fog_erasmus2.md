# Captura de la imatge d'un client Windows 10

Hem instal·lat el zoom en el client Windows 10.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-20 17-38-06.png)

També hem instal·lat el navegador Firefox.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-20 17-38-15.png)

Indiquem la xarxa com a prioritat d'arrencada.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-20 17-53-23.png)

Creem una nova imatge en el servidor FOG per a un client Windows 10 indicant com a tipus d'imatge Multiple Partition Image - Single Disk (Not Resizable) té particions amb mides fixes que no es poden modificar i el gestor d'imatges en **Partclone Gzip**.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 13-27-27.png)

Arranquem el client de Windows i aquest menú seleccionem l'opció **Quick Registration and Inventory** per registrar el host en el servidor FOG.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 13-29-00.png)

Despŕes, apareix el logo de FOG i ens indica que està intentant registrar el host.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 13-31-47.png)

Ens registra el host i ens mostra quin disc està utilitzant el client de Windows juntament amb més informació...

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 13-31-54.png)

Tornem el servidor FOG i visualitzem que s'ha registrat el host.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 13-30-39.png)

Entrem a la configuració del host Windows 10 i assignem l'imatge de host **Windows 10 Pro** que hem creat anteriorment al host.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 13-33-52.png)

Després, ens dirigim a l'apartat **Basic Tasks** dins del host i triem l'opció "Capture".

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 13-35-24.png)

Seleccionem les opcions "Wake on lan?" i "Schedule instant", fem clic a "Task" per finalitzar.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 13-35-38.png)

S'ha creat la tasca correctament.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 13-35-46.png)

Tornem a iniciar per xarxa des del client Windows 10.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 13-36-20.png)

Ens mostra el log del servidor FOG i ens indica quin sistema operatiu és, quants processadors té i el sistema de communicació que utilitzarà per enviar la imatge que capturarem que és **NFS**.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 13-36-29.png)

S'ha completat la captura de la imatge del client de Windows 10.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 13-46-26.png)

Ens indica que s'ha finalitzat la clonació, que la imatge s'ha capturat, que la tasca s'ha completat, s'ha actualitzat la base de dades i que la màquina es reiniciarà.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 13-46-30.png)

Ens dirigim al servidor FOG i visualitzem que la imatge ara té una mida de 50 GB i la data quan s'ha fet la captura.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 15-16-15.png)