






1 - télechargement de la dernière version PI-STAR : 

Rendez-vous sur le site de pistar :

https://www.pistar.uk/downloads/

puis allez dans le répertoire download :

https://www.pistar.uk/downloads/Pi-Star_RPi_V4.1.5_21-Jun-2021.zip

Une fois le fichier chargé vous devez l'écrire sur une carte sd.
ps : je considère que cette étape est acquise.

2 - Configuation du pistar :

Je vous invite à vous rendre sur le site suivant : 


Une fois votre hotspot pistar fonctionnel, vous allez déclarer votre écran Nextion ici :








HOW TO INSTALL THE NEXTION DRIVER

First install the Nextion driver from ON7LDS L3 HS

log in to your Pi-Star with SSH

RPI-RW

sudo rm /usr/local/bin/NextionDriver to erase the old driver

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
