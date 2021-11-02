
# MMDVM2HMI 1TS / PISTAR software 
(f5swb@hotmail.com 2021).

<img src = "https://github.com/f5swb/MMDVM2HMI-1TS/blob/master/0_1.png" title = "boot">

English version : https://github-com.translate.goog/f5swb/MMDVM2HMI-1TS/blob/master/readme.md?_x_tr_sl=fr&_x_tr_tl=en&_x_tr_hl=en&_x_tr_pto=nui,elem <br/>

# INFO INFO INFO INFO INFO INFO INFO INFO INFO INFO INFO INFO INFO INFO INFO INFO INFO INFO :

Ce projet est encore au stade de développement. Une version de démonstration sera bientot disponible (5 démarrages). <br/>
Afin de me permettre de poursuivre le développement et de travailler sur une version DMR 2 Time slot, j'ai besoin pour cela de m'autofinancer afin d'investir dans une platine MMDVM 2 TS.<br/>

<img src = "https://github.com/f5swb/MMDVM2HMI-1TS/blob/master/duplex-mmdvm.jpg" title = "mmdvm">

https://www.passion-radio.fr/numerique/duplex-mmdvm-706.html


En fonction de la demande et l'engouement que cette version procurera, j'étudierai peut-être le support également des modes DSTAR, CF4M, P25 et NXDN.<br/>
Une version enregistrée à votre callsign non limitée dans le temps sera alors proposée à 10€ d'ici quelques semaines (en phase de test actuellement).<br/>

73's QRO.
F5SWB Dimitri.


### 1 - Télechargement de la dernière version PI-STAR : 

Rendez-vous sur le site de pistar puis allez dans le répertoire download :https://www.pistar.uk/downloads/

https://www.pistar.uk/downloads/Pi-Star_RPi_V4.1.5_21-Jun-2021.zip

(lors de la réalisation de ce tuto la dernière version datait du 21 juin 2021)

Une fois le fichier chargé vous devez l'écrire sur une carte sd.<br/>
ps : je considère que cette étape est acquise.

### 2 - Configuation du pistar :

Je vous invite à vous rendre sur le site suivant : http://f4dfq.fr/MMDVM-HS-DUAL-V1-3/


Une fois votre hotspot pistar fonctionnel, vous allez déclarer votre écran Nextion :<br/>
- cliquez sur Configuration : <br/>

<img src = "https://github.com/f5swb/MMDVM2HMI-1TS/blob/master/conf%200.PNG" title = "conf 0">

<img src = "https://github.com/f5swb/MMDVM2HMI-1TS/blob/master/conf%202bis.PNG" title = "conf 1">

Choisissez alors dans la partie Afficheur MMDVM : <br/>

- sur le GPIO alors il faudra choisir : /dev/ttyAMA0<br/>
- sur une clef USB il faudra choisir : /dev/ttyUSB0<br/>
- pour l'affichage, sélectionner ON7LDS L3 HS<br/>

Redémarrer alors votre PISTAR, l'écran doit s'initialiser mais comme vous le constaterez de nombreuses informations sont absentes : <br/>
la vitesse du processeur du RPI, l'occupation processeur ainsi que le taux d'espace libre sur la carte sd. 


### 3 - Installation du driver Nextion du pistar :

loguez vous dans le pistar en ssh en cliquant sur EXPERT puis SSH Access :

<img src = "https://github.com/f5swb/MMDVM2HMI-1TS/blob/master/ssh.PNG" title = "ssh">

le login est : pi-star<br/>
le mot de passe est : raspberry

<img src = "https://github.com/f5swb/MMDVM2HMI-1TS/blob/master/rpi-rw.PNG" title = "rpi-rw 1">

puis entrez : <br/>
rpi-rw, (suivi de la touche enter),

<img src = "https://github.com/f5swb/MMDVM2HMI-1TS/blob/master/git.PNG" title = "git">

entrez ensuite cette commande en respectant bien la casse : <br/>

sudo rm /usr/local/bin/NextionDriver 

Cette commande a pour action de supprimer le précédent driver de votre système.

Ensuite nous allons installer la dernière version du driver pour le Nextion : <br/>
cd /tmp <br/>

git clone https://github.com/on7lds/NextionDriverInstaller.git <br/>

sudo NextionDriverInstaller/install.sh <br/>
<img src = "https://github.com/f5swb/MMDVM2HMI-1TS/blob/master/nextiondriver.PNG" title = "nextion driver">

A l'issue le système vous propose un redémarrage, entrez Y puis enter.

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

### 5 - Utilisation de l'image MMDVM2HMI pour le pistar :<br/>

L'image proposée est compatible avec un écran NEXTION NX4832 35K uniquement !!!<br/>

<img src = "https://github.com/f5swb/MMDVM2HMI-1TS/blob/master/NEXTION.png" title = "nextion">  

Afin de disposer de la date et l'heure vous devez insérer une pile dans l'emplacement prévu à cet effet :

<img src = "https://github.com/f5swb/MMDVM2HMI-1TS/blob/master/rtc_battery.jpg" title = "rtc">  




- démarrage de l'écran et controle de la présence du driver :<br/>


<img src = "https://github.com/f5swb/MMDVM2HMI-1TS/blob/master/boot.gif " title = "boot">  

Une fois le système initialisé, l'affichage de l'item Driver Nextion 1.22 vous confirme le bon fonctionnement.<br/>

### 6 - Ecran MMDVM :<br/>

<img src = "https://github.com/f5swb/MMDVM2HMI-1TS/blob/master/Animated_gif/mmdvm_screen_start.gif" title = "start">  

<img src = "https://github.com/f5swb/MMDVM2HMI-1TS/blob/master/pictures/mmdvm_screen_help.png" title = "help">  

### 7 - Page réglages :<br/>

<img src = "https://github.com/f5swb/MMDVM2HMI-1TS/blob/master/Animated_gif/mmdvm_r%C3%A9glages.gif" title = "réglages">  


<img src = "https://github.com/f5swb/MMDVM2HMI-1TS/blob/master/pictures/mmdvm_r%C3%A9glages.png" title = "réglages">  

### 8 - Page informations :<br/>

<img src = "https://github.com/f5swb/MMDVM2HMI-1TS/blob/master/Animated_gif/informations.gif" title = "informations">  

<img src = "https://github.com/f5swb/MMDVM2HMI-1TS/blob/master/pictures/informations.PNG" title = "informations">  

### 9 - Page world Time :<br/>

<img src = "https://github.com/f5swb/MMDVM2HMI-1TS/blob/master/Animated_gif/world%20time.gif" title = "world time">  
