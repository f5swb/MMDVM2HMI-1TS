
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


Une fois votre hotspot pistar fonctionnel, vous allez déclarer votre écran Nextion :<br/>
- cliquez sur l'item expert puis MMDVMHost : <br/>

<img src = "https://github.com/f5swb/MMDVM2HMI-1TS/blob/master/conf%200.PNG" title = "conf 0">

<img src = "https://github.com/f5swb/MMDVM2HMI-1TS/blob/master/conf%202bis.PNG" title = "conf 1">

Choisissez alors dans la partie Afficheur MMDVM : <br/>

- sur le GPIO alors il faudra choisir : dev/ttyAMA0<br/>
- sur une clef USB il faudra choisir : dev/ttyUSB0<br/>
- pour l'affichage, sélectionner ON7LDS L3 HS<br/>

Redémarrer alors votre PISTAR, l'écran doit s'initialiser mais comme vous le constaterez de nombreuses informations sont absentes : <br/>
la vitesse du processeur du RPI, l'occupation processeur ainsi que le taux d'espace libre sur la carte sd. 


### 3 - Installation du driver Nextion du pistar :

loguez vous dans le pistar en ssh en cliquant sur EXPERT puis SSH Access :

<img src = "https://github.com/f5swb/MMDVM2HMI-1TS/blob/master/ssh.PNG" title = "conf 1">
https://github.com/f5swb/MMDVM2HMI-1TS/blob/master/ssh.PNG

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

Vous constaterez que dans le fichier MMDVMHost dans la partie Nextion de la page, il y a eu de nouvelles rubriques qui ont été ajoutées : <br/>

Rendez-vous sur l'item Expert Page => MMDVMHost : <br/>

- vérifiez la présence de /dev/ttyNextionDriver (adaptateur USB) ou /dev/ttyAMA0 (connecté au GPIO du RPi) ; <br/>

<img src = "https://github.com/f5swb/MMDVM2HMI-1TS/blob/master/control%201.PNG" title = "control 1">

- vérifiez dans l'item NextionDriver : <br/>
    Port: /dev/ttyUSB0 (pour un adaptateur USB)  ou /dev/ttyAMA0 (connecté au GPIO du RPi) <br/>
    LogLevel: 2  <br/>
    DataFilesPath: /usr/local/etc/  <br/>
    GroupsFile: groups.txt  <br/>
    DMRidFile: stripped.csv  <br/>
 
 
<img src = "https://github.com/f5swb/MMDVM2HMI-1TS/blob/master/control%202.PNG" title = "control 2">  
    
Si tout est correct, vous pouvez alors éteindre le pistar et le redémarrer.<br/>

### 5 - Utilsation de l'image MMDVM2HMI pour le pistar :<br/>

- démarrage de l'écran et controle de la présence du driver :<br/>



