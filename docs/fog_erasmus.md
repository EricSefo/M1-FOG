# El servidor FOG

![imatge](./CAPTURES%20M1%20FOG/fog.png)

Benvingut a la introducció del servidor FOG! En aquest treball, explorarem el funcionament i els beneficis d'aquest sistema per a la clonació de imatges de disc i la gestió centralitzada en una xarxa d'ordinadors.

Un servidor FOG és una plataforma basada en programari lliure i de codi obert que permet automatitzar la implementació de sistemes operatius, clonar imatges de disc, gestionar ordinadors de forma remota i administrar l'inventari del maquinari. Aquesta solució és àmpliament utilitzada en entorns educatius, empresarials i d'altres organitzacions que requereixen gestionar grans quantitats d'ordinadors.

Amb un servidor FOG, és possible crear una imatge mestra d'un sistema operatiu, que inclou totes les configuracions i programes desitjats, i després clonar aquesta imatge en múltiples ordinadors de la xarxa de manera eficient i ràpida. Això permet una implementació massiva i consistent dels sistemes operatius, estalviant temps i recursos.

A més, el servidor FOG facilita la gestió remota d'ordinadors. Des de la interfície d'usuari del servidor, els administradors poden realitzar tasques com l'apagat o l'arrencada remota d'ordinadors, la instal·lació de programes i actualitzacions en múltiples equips, o la supervisió de l'estat dels sistemes. Això ofereix un control centralitzat i eficient sobre els recursos informàtics.

# Instal·lació i configuració del servidor FOG

En el nostre cas hem utilitzat Ubuntu Server 20.04.6 per instal·lar el servidor FOG.

Primarament configurarem la xarxa del servidor Ubuntu Server amb l'IP 192.168.0.2, porta d'enllaç 192.168.0.1, com a servidors DNS 192.168.0.1 com a principal i com a DNS secundaris 8.8.8.8 i 8.8.4.4 .

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-20 14-54-37.png)
![imatge](./CAPTURES%20M1%20FOG/captura1.png)

Seguidament, apliquem l'arxiu .yaml amb la comanda **sudo netplan apply**, comprovem que s'ha aplicat amb la comanda **ip a** i comprovem la connectivitat realitzant un ping a www.google.com.

![imatge](./CAPTURES%20M1%20FOG/Captura%20de%20pantalla%20de%202023-05-21%2012-52-07.png)

Actualitzem la informació dels paquets disponibles a través dels repositoris d'Ubuntu.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-20 14-59-02.png)

Instal·larem l'entorn d'escriptori d'Ubuntu per realitzar l'administració gràficament, això ens falicitarà molt les tasques.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-20 14-59-52.png)

Al finalitzar l'instal·lació reiniciarem el servidor amb la comanda **reboot**.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-20 15-11-26.png)

A l'iniciar de nou el servidor d'Ubuntu veurem que tenim l'entorn d'escriptori d'Ubuntu.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-20 15-12-08.png)

A continuació, descargarem l'arxiu comprimit del servidor FOG des de la web oficial https://www.fogproject.org/download.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-20 15-37-09.png)

Accedim al directori "Descargas" i comprovem el checksum sha256 de l'arxiu descarregat coincideix amb el que hi ha la seva web per verificar l'integritat del fitxer.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-20 15-41-06.png)

Després, amb la comanda **sudo -i** accedim com a root per accedir al directori /home/erasmus/Descargas/ i descomprimir l'arxiu fogproject-1.5.10.tar.gz.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-20 15-41-50.png)

Accedirem al directori fogproject-1.5.10/bin i executarem l'arxiu **installfog.sh**.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-20 15-42-46.png)

Indicarem que volem una instal·lació **"Normal"**, indiquem que no volem canvia l'interfície per defecte, introduïm l'adreça IP del nostre router que realitzarà la funció d'un servidor DHCP encara que l'instal·lador la detecti, diem que volem "handle DHCP to DNS" que significa asumir la responsabilitat de gestionar i configurar la informació de DNS a través del servei DHCP, també indiquem que volem instal·lar paquets d'idiomes adicionals, per finalitzar, indiquem que no volem que utilitze https en el servidor web i que no volem canviar el hostname.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 13-13-00.png)

Indiquem que volem continuar i s'inicialitzarà el prcoés d'instal·lació del servidor FOG.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 13-14-54.png)

L'instal·lador ens fa accedir a la direcció http://192.168.0.2/fog/management per instal·lar la base de dades, aquesta captura també inclou el procés que es realitza despŕes d'instal·lar la base de dades.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 13-18-30.png)

En el navegador farem clic a "Install/Update Now".

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 13-17-49.png)

Ens apareix que s'ha instal·lat correctament.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 13-18-00.png)

L'instal·lació del servidor FOG ha acabat i ens indica les credencials per defecte per iniciar sessió.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 13-18-37.png)

Ens loguegem amb l'usuari fog i la contrasenya password amb el llenguatge Español.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 13-18-14.png)

Estan en root i amb la comanda **systemctl disable systemd-resolved.service** desactivem el servei systemd-resolved que és el responsable de la resolució de noms de domini (DNS), aturem el servei systemd-resolved amb l'ordre **systemctl stop systemd-resolved.service**, eliminem l'arxiu /etc/resolv.conf i el tornem a crear amb la línia "nameserver 8.8.8.8". Seguidament, instal·lem el paquet **dnsmasq**.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 13-21-10.png)

El paràmetre **port=0** s'utilitzem per indicar que no actui com a servidor DNS, **log-dhcp** per rebre més informació sobre les transaccions DHCP, **tftp-root:/tftpboot** per indicar el directori arrel per als arxius disponibles al FTP, **dhcp-no-override** desactiva la reutilització dels camps de nom de servidor DHCP i nom de fitxer, **dhcp-boot=undionly.kpxe,,192.168.0.2** que indica el fitxer boot, el nom del servidor FOG que no està escrit i l'adreça IP del servidor FOG, **pxe-prompt="Booting FOG Client", 1** que serà el text mostrat a l'usuari sent el segon paràmetre el timeout en segons, per acabar **dhcp-range=192.168.0.2,proxy** indicant el rang especificat és des de 192.168.0.2 fins a l'adreça IP del servidor intermediari.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 13-23-39.png)

Reiniciarem el servei dnsmasq i mostrarem l'estat amb les comandes **service dnsmasq restart i service dnsmasq status**.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 13-24-10.png)

Amb això finalitzarem l'instal·lació i la configuració.

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

# Captura de la imatge d'un client Ubuntu 22.04

Aquest és el client Ubuntu 22.04 que té instal·lat el Skype, el navegador Brave i Visual Studio Code.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 15-37-13.png)

Aquest és l'aplicació de skype amb el compte de Nasim loguejat.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 15-42-05.png)

Aquest és el navegador brave.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 15-42-25.png)

I aquest és el Visual Studio Code.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 15-42-37.png)

Crearem una nova imatge amb el tipus de sistema operatiu Linux, en aquest cas utilitzarem el tipus d'imatge "Single Disk - Resizable" que permet ajustar la mida de les particions contingudes al disc, la qual cosa significa que es pot expandir o reduir l'espai assignat a cada partició segons calgui.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 15-59-05.png)

La imatge del client Ubuntu s'ha creat correctament.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 15-59-19.png)

Iniciem el client Ubuntu amb la prioritat d'arrencada per xarxa.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 16-00-17.png)

Ens detectarà el nostre servidor FOG.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 16-03-05.png)

Seleccionem l'opció **Quick Registration and Inventory** per registrar el host d'Ubuntu.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 16-03-21.png)

A continuació, el servidor FOG està intentant registrar el host.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 16-03-47.png)

L'ha registrat i ens indica diverses informacions sobre la màquina com el UUID del disc.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 16-03-51.png)

El host d'Ubuntu és el 080027eabf2a que s'ha registrat correctament.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 16-04-28.png)

A la configuració del host indiquem que la imatge ha de ser la que hem creat anteriorment per a l'Ubuntu client.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 16-05-57.png)

Triem l'opció "Capture".

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 16-06-10.png)

Creem una nova tasca per captura la imatge del client d'Ubuntu per xarxa.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 16-06-15.png)

La tasca ha sigut creada correctament.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 16-06-24.png)

Accedim al client Ubuntu arrancant per xarxa.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 16-07-00.png)

S'està intentant connectar-se o registrar un dispositiu client al servidor FOG per realitzar operacions de clonació.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 16-07-10.png)

Realitzar una serie de comprovacions i preparacions per realitzar la clonació.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 16-08-06.png)

S'ha finalitzat la captura de la imatge d'un client d'Ubuntu, seguidament, ens reiniciarà.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 16-11-43.png)

Com podem comprovar en la següent captura la imatge Ubuntu Client 22.04 té un espai de 17,3 GB amb la data en la que s'ha realitzat la captura.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 16-13-22.png)

# Instal·lar una imatge Windows

Crearem una nova màquina virtual de Windows 10 amb 4 GB de RAM que inicie l'arrencada per xarxa.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 16-17-01.png)

Aquesta màquina l'he posat 50 GB d'espai.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 16-17-07.png)

Iniciem la màquina virtual arrencant amb xarxa.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 16-18-48.png)

Triem l'opció **Deploy Image** per desplegar la imatge de Windows 10 que tenim capturada en aquesta nova màquina.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 16-19-02.png)

Introduïm les credencials de login del servidor FOG.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 16-19-34.png)

Escollim quina imatge volem instal·lar, en aquest cas triem la de Windows 10 Pro.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 16-19-46.png)

S'inicialitza l'instal·lació.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 16-19-56.png)

A continuació, realitza una serie de comprovacions abans de començar a instal·lar la nostra imatge.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 16-24-22.png)

Em restaurat la nostra imatge capturada del Windows 10 en aquesta nova màquina.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 16-44-39.png)

Es reinicia automàticament la màquina virtual realitzant una serie de tasques abans.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 16-44-42.png)

Després, iniciarem la màquina virtual "Windows 10 - FOG" amb el disc dur i desactivem la xarxa com a mètode d'arrencada.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 16-45-18.png)

Accedim al sistema i comprovem que el nostre sistema capturat és el mateix que acavem d'instal·lar en aquesta nova màquina virtual incloent els programes Firefox i Zoom.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 16-46-34.png)

Comprovem que el compte de Nasim està loguejat al zoom.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 16-46-56.png)

Comprovem també que el navegador Firefox funciona correctament.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 16-46-47.png)

# Instal·lar una imatge Ubuntu

Primerament, crearem una nova màquina virtual amb 4 GB de RAM i 50 GB d'espai, indiquem com a prioritat d'arranc per xarxa.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 16-48-53.png)

S'inicia la connexió amb el servidor FOG.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 16-49-12.png)

Seleccionem l'opció **Deploy Image** per aplicar la imatge capturada del client Ubuntu 22.04 en aquesta nova màquina d'Ubuntu.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 16-49-28.png)

Indiquem les credencials del servidor FOG.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 16-49-37.png)

Triem la imatge **Ubuntu Client 22.04**.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 16-49-43.png)

Realitza una serie de comprovacions i configuracions per instal·lar la imatge.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 16-50-08.png)

S'ha finalitzat la restauració de la imatge en la nova màquina.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 16-53-35.png)

La clonació s'ha realitzat correctament, seguidament, es reinicia la màquina virtual.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 16-53-53.png)

A continuació, iniciarem amb el disc al nou client Ubuntu.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 16-54-54.png)

Ens apareix l'usuari del sistema.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 17-02-50.png)

Introduïm les credencials de l'usuari erasmus-client.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 17-02-59.png)

Ens apareix l'escriptori i podem comprovar que tenim el fons que vam configurar amb les tres aplicacions que vam instal·lar (Skype, Brave, Visual Studio Code).

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 17-03-13.png)

L'usuari de Skype de Nasim està loguejat al Skype.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 17-03-23.png)

El navegador web Brave funciona correctament.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 17-03-34.png)

I l'editor de codi Visual Studio Code també funciona correctament.

![imatge](./CAPTURES%20M1%20FOG/Captura de pantalla de 2023-05-21 17-03-44.png)

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

# Conclusió

En conclusió, la implementació i configuració d'un servidor FOG proporciona una solució eficient per a la gestió centralitzada d'ordinadors en una xarxa. Amb el servidor FOG, és possible capturar i instal·lar imatges de disc tant de sistemes operatius Windows com Ubuntu, oferint flexibilitat per als diferents entorns de treball.

La captura d'un sistema Windows des del client permet crear una imatge mestra de Windows amb totes les configuracions i programes necessaris, facilitant la implementació massiva i consistent d'aquest sistema operatiu en múltiples ordinadors de la xarxa.

De manera similar, capturar un sistema Ubuntu des del client ofereix la possibilitat de crear una imatge mestra d'Ubuntu personalitzada, amb les preferències i els programes específics per al seu entorn. Això simplifica la implementació i estandarditza els sistemes Ubuntu en la xarxa.

Amb el servidor FOG, és fàcil instal·lar imatges de Windows i Ubuntu en múltiples clients de forma simultània i eficient. Aquest procés estalvia temps i recursos, ja que no és necessari instal·lar manualment cada sistema operatiu en cada màquina individualment.

Una altra funcionalitat destacada és la capacitat de llançar paquets d'instal·lació als clients. Això permet implementar i actualitzar programes i paquets de software en múltiples equips de manera ràpida i eficient, evitant la necessitat d'accedir a cada màquina individualment.

En resum, la utilització d'un servidor FOG simplifica i automatitza la gestió dels sistemes operatius Windows i Ubuntu en una xarxa d'ordinadors. Des de la captura d'imatges fins a la instal·lació dels sistemes operatius i l'aplicació de paquets, aquesta solució proporciona una plataforma centralitzada per a una administració eficient i ràpida dels recursos informàtics.