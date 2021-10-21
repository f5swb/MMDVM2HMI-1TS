
# MMDVM2HMI 1TS / PISTAR software 
(f5swb@hotmail.com 2021).

<img src = "https://github.com/f5swb/MMDVM2HMI-1TS/blob/master/0_1.png" title = "boot">


### 1 - Télechargement de la dernière version PI-STAR : 

Rendez-vous sur le site de pistar puis allez dans le répertoire download :https://www.pistar.uk/downloads/

https://www.pistar.uk/downloads/Pi-Star_RPi_V4.1.5_21-Jun-2021.zip

(lors de la réalisation de ce tuto la dernière version datait du 21 juin 2021)

Une fois le fichier chargé vous devez l'écrire sur une carte sd.<br/>
ps : je considère que cette étape est acquise.

### 2 - Configuation du pistar :

Je vous invite à vous rendre sur le site suivant : http://f4dfq.fr/MMDVM-HS-DUAL-V1-3/


Une fois votre hotspot pistar fonctionnel, vous allez déclarer votre écran Nextion ici :

<img src = "https://github.com/f5swb/MMDVM2HMI-1TS/blob/master/nextion%201.PNG" title = "nextion 1">

Dans cet exemple, le driver est déjà disponible, si votre écran est branché :

sur le GPIO alors il faudra choisir : - dev/tty/AMA0<br/>
sur une clef USB il faudra choisir : - dev/tty/USB0<br/>

Pour l'affichage, sélectionner ON7LDS L3 HS<br/>

Redémarrer alors votre PISTAR, l'écran doit s'initialiser mais comme vous le constaterez de nombreuses informations sont absentes.


### 3 - Installation du driver Nextion du pistar :

loguez vous dans le pistar en ssh, 

puis entrez RPI-RW, (suivi de la touche enter),

entrez ensuite cette commande en respectant bien la casse :

sudo rm /usr/local/bin/NextionDriver to erase the old driver

Cette commande a pour action de supprimer le précédent driver de votre système.

get the software Then: cd /tmp

git clone https://github.com/on7lds/NextionDriverInstaller.git

go !

sudo NextionDriverInstaller/install.sh

Checking the installing (on Pi-Star)

You will notice that in the MMDVMHost beyond the Nextion part of that page, there are some additions regarding this Nextion Interface: Check your software settings in Pi-Star:

Goto the Expert Page => MMDVMHost Editor (or mmdvmhost.ini file) to the Nextion part

check/set in the Nextion part, the driver at /dev/ttyNextionDriver (USB adapter) or /dev/ttyAMA0 (connected to GPIO-RPi)
check/set in the NextionDriver part
    Port: /dev/ttyUSB0 (for USB adapter) or /dev/ttyAMA0 (connected to the GPIO pins of RPi)****
    LogLevel: 2
    DataFilesPath: /usr/local/etc/
    GroupsFile: groups.txt
    DMRidFile: stripped.csv
