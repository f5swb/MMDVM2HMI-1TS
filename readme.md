
# MMDVM2HMI DMR 1TS / PISTAR software 
(f5swb@hotmail.com 2021).<br/>
mailto:mmdvm2hmi+subscribe@groups.io

 <img src = "https://github.com/f5swb/MMDVM2HMI-1TS/blob/master/0_1.png" width="350" height="250" title = "boot"> <img src = "https://github.com/f5swb/MMDVM2HMI-1TS/blob/master/f5swb.jpg" title = "f5swb"> <img src = "https://github.com/f5swb/MMDVM2HMI-1TS/blob/master/DVmegaUHF_pr7813_1.jpg" title = "boot">

#### L'image proposée est compatible avec un écran NEXTION NX4832K035_11 et en Français uniquement pour le moment !!!<br/>



 
English version : https://github-com.translate.goog/f5swb/MMDVM2HMI-1TS/blob/master/readme.md?_x_tr_sl=fr&_x_tr_tl=en&_x_tr_hl=en&_x_tr_pto=nui,elem <br/>

# INFO INFO INFO INFO INFO INFO INFO INFO INFO INFO INFO INFO INFO INFO INFO INFO INFO INFO :

Une version de démonstration est dès à présent disponible (version 90° et version 270°). <br/>
#### Cette version ne peut être lancée que 5 fois. A l'issue celle-ci n'est plus fonctionnelle.<br/>

Une version enregistrée à votre callsign non limitée et complètement fonctionnelle dans le temps vous sera très prochainement proposée pour 10€.<br/>

Afin de me permettre de poursuivre le développement et de travailler sur une version DMR 2 Time slot, j'ai besoin pour cela de m'autofinancer afin d'investir dans une platine MMDVM 2 TS.<br/>

<img src = "https://github.com/f5swb/MMDVM2HMI-1TS/blob/master/duplex-mmdvm.jpg" title = "mmdvm">

https://www.passion-radio.fr/numerique/duplex-mmdvm-706.html


En fonction de la demande et l'engouement que cette version suscitera et procurera, j'étudierai peut-être le support également des modes DSTAR, CF4M, P25 et NXDN.<br/>


Group Email Addresses:

Post: mmdvm2hmi@groups.io <br/>
Subscribe: mmdvm2hmi+subscribe@groups.io <br/>

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

##### L'image proposée est compatible avec un écran NEXTION NX4832K035_11 uniquement !!!<br/>

<img src = "https://github.com/f5swb/MMDVM2HMI-1TS/blob/master/NEXTION.png" title = "nextion">  

Afin de disposer de la date et l'heure vous devez insérer une pile dans l'emplacement prévu à cet effet :

<img src = "https://github.com/f5swb/MMDVM2HMI-1TS/blob/master/rtc_battery.jpg" title = "rtc">  


Deux images (tft) sont disponibles au téléchargement :

- MMDVM2HMI_V1_Demo_90deg.tft : si l'encoche de votre écran est vers le bas ; <br/>

https://github.com/f5swb/MMDVM2HMI-1TS/blob/master/TFT_Files/mmdvm2hmi_v1.0_1TS_demo_90deg_final.tft

- MMDVM2HMI_V1_Demo_270deg.tft : si l'encoche de votre écran est vers le haut. <br/>

https://github.com/f5swb/MMDVM2HMI-1TS/blob/master/TFT_Files/mmdvm2hmi_v1.0_1TS_demo_270deg_final.tft

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

# 10 - Activer les informations réseaux : <br/>

cd /etc
sudo nano mmdvmhost

[NextionDriver]                                                             
Port=/dev/ttyUSB0                                                           
DataFilesPath=/usr/local/etc/                                               
LogLevel=2                                                                  
GroupsFile=groups.txt                                                       
DMRidFile=stripped.csv                                                      
#DMRidDelimiter=,                                                           
#DMRidId=1                                                                  
#DMRidCall=2                                                                
#DMRidName=3                                                                
#DMRidX1=4                                                                  
#DMRidX2=5                                                                  
#DMRidX3=7                                                                  
## ShowModesStatus=1                                                           
RemoveDim=0                                                                 
WaitForLan=1                                                                
SleepWhenInactive=0            

# 11 - Mise à jour de group.txt et user.csv : <br/>

1. rpi-rw
2. wget "https://api.brandmeister.network/v1.0/groups/" -O /tmp/groups.txt
3. sudo cp /tmp/groups.txt /usr/local/etc/

This is not a command only information # update DMR all users list infromation

4. wget "https://database.radioid.net/static/user.csv" -O /tmp/stripped.csv
5. sudo cp /tmp/stripped.csv /usr/local/etc/
6. sudo reboot
7. 


## 12 - Modem-connected displays

As of V1.03 the NextionDriver has support for Nextion displays which are connected to the modem ('Port=modem' in MMDVM.ini) For this, it is necessary to use the MMDVMHost code dated 20180815 or later (G4KLX GitID #f0ea25d or later). It surely is OK when the MMDVMHost version string is 20180910 or later.

NOTE: When connecting a Nextion to the Nextion port on a MMDVM_HS hat, the Nextion screen default baud rate must be set to 9600 unless you build custom firmware and define a higher UART2 speed. Send the following serial command in the Nextion simulator "bauds=9600"

In the MMDVM.ini file, you must enable 'Transparent Data' and it's option 'SendFrameType', i.e. :

[Transparent Data]
Enable=1
RemoteAddress=127.0.0.1
RemotePort=40094
LocalPort=40095
SendFrameType=1

Then you can instruct NextionDriver to use the Transparent Data to connect to the display. This is done by setting the 'Port' option in the NextionDriver section of MMDVM.ini to 'modem'

[NextionDriver]
Port=modem
...

Data from the Nextion (when pressing buttons) will be treated similar and will exit MMDVMHost as transparent data. IMPORTANT : the firmware of the modem has to pass data from the display to MMDVMHost for this to work!

If this is not (yet) the case, you could ask the developer of your modem to add this feature.
