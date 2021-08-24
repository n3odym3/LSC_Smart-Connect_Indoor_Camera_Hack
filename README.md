# LSC_Smart-Connect_Indoor_Camera_Hack
Hack to enable the ONVIF (and RTSP) on the LSC Smart connect indoor camera from Action

## Tuto de base 
https://github.com/guino/BazzDoorbell/issues/2

## Rooter la caméra
- Placer le ficher ppsFactoryTool.txt dans une carte SD (FAT32)
- Setup le SSID et PASSWORD du WiFi
- Placer la carte SD dans la caméra
- Lancer la caméra
- Trouver son adresse ip avec [ONVIF Device Manager](https://sourceforge.net/projects/onvifdm/)
- Réaliser les requêtes HTTP Suivantes
  - http://admin:admin@CAMERA.IP:8090/devices/deviceinfo => Réponse : ppstrong-a3-tuya2_lsc-4.0.6.20210311
  - http://admin:admin@CAMERA.IP:8090/proc/cmdline => Sauvegarder réponse
  - http://admin:admin@CAMERA.IP:8090/proc/self/root/etc/init.d/S90PPStrong => S'assurer que MTDNUM=5 est bien décommenté (sans #)
- Si tout est OK éteindre la caméra et récupérer la carte SD
- Placer les fichier de ToRoot sur la SD
  - env
  - initrun.sh
  - ppsMmcTool.txt
- Placer la SD dans la caméra
- Appuyer sur le boutton reset
- Brancher la caméra (en gardant le boutton reset enfoncé)
- Maintenir le boutton enfoncé pendant 5 secondes (la caméra devrait clignotter entre rouge et bleu)
- La caméra devrait ensuite booter
- Tester si le hack a fonctionné avec la requête HTTP suivante 
  - http://admin:admin@CAMERA.IP:8090/proc/self/root/mnt/mmc01/hack => Réponse : done
- Placer les fichier de ToHack sur le carte SD
  - cgi-bin
  - busybox
  - custom.sh
  - dropbearmulti
  - httpd.conf
  - index.html
  - jpeg-arm
  - passwd
  - set
  - upload.html
- Copier le fichier ppsapp présent dans /home/app
- Sassurer que le md5 correspond à celui présent [ici](https://github.com/guino/ppsapp-rtsp/issues/1) (chercher ppstrong-a3-tuya2_lsc-4.0.6.20210311) 
- Aller sur https://www.marcrobledo.com/RomPatcher.js/
- Sélectionner le fichier ppsapp
- Sélectionner le patch téléchargé [ici](https://github.com/guino/ppsapp-rtsp/files/6880255/ppsapp-onvif.zip)
- Renommer le fichier ppsapp.txt téléchargé après le patch en ppsapp
- Placer le fichier ppsapp patché à la racine de la carte SD
- Placer la carte SD dans la caméra et brancher la caméra
- La caméra devrait booter deux fois !
- Bravo la caméra est patchée
- Essayer d'ouvrir le flux RTSP dans ONVIF Device Manager
