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