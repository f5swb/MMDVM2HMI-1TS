
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

Redémarrer alors votre PISTAR, l'écran doit s'initialiser mais comme vous le constaterez de nombreuses informations sont absentes : <br/>
la vitesse du processeur du RPI, l'occupation processeur ainsi que le taux d'espace libre de la carte sd. 


### 3 - Installation du driver Nextion du pistar :

loguez vous dans le pistar en ssh, 

puis entrez : <br/>
RPI-RW, (suivi de la touche enter),

entrez ensuite cette commande en respectant bien la casse : <br/>

sudo rm /usr/local/bin/NextionDriver 

Cette commande a pour action de supprimer le précédent driver de votre système.

Ensuite nous allons installer la dernière version du driver pour le Nextion : <br/>

cd /tmp <br/>

git clone https://github.com/on7lds/NextionDriverInstaller.git <br/>

sudo NextionDriverInstaller/install.sh <br/>

### 4 - Vérification de la présence du driver Nextion  pour le pistar :

Vous constaterez que dans le fichier MMDVMHost dans la partie Nextion part de la page, il y a eu de nouvelles rubriques qui ont été ajoutées : <br/>

Rendez-vous sur l'item Expert Page => MMDVMHost Editor : <br/>

- vérifiez la présence de /dev/ttyNextionDriver (adaptateur USB) ou /dev/ttyAMA0 (connecté au GPIO du RPi) ; <br/>

- vérifiez dans l'item NextionDriver : <br/>
    Port: /dev/ttyUSB0 (pour un adaptateur USB)  ou /dev/ttyAMA0 (connecté au GPIO du RPi) <br/>
    LogLevel: 2  <br/>
    DataFilesPath: /usr/local/etc/  <br/>
    GroupsFile: groups.txt  <br/>
    DMRidFile: stripped.csv  <br/>
Si tout est correct, vous pouvez alors éteindre le pistar et le redémarrer.

### 5 - Utilsation de l'image MMDVM2HMI pour le pistar :

