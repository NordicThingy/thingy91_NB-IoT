# Programme de communication en NB-IoT/LTE-M avec le Thingy91

Ce projet permet de détecter les chocs et l'orientation du Thingy:91 de Nordic Semiconductor en utilisant des accéléromètres et un capteur environnemental. Le programme surveille en continu les données des capteurs et les transmets à un cloud en ligne via NB-IoT.


**Matériel requis:**
- Thingy:91 de Nordic Semiconductor
- nRF Connect for Desktop
- Visual Studio Code avec l'extension nRF Connect for VS Code
- nRF Cloud
- Câble USB-C


**Installation et Configuration:**
Pour exécuter ce projet, vous devez installer et configurer le nRF Connect for Desktop et Visual Studio Code (VS Code). 

Note : Assurez-vous que la chaîne d'outils (Toolchain) et le SDK sont installés sur le disque C:\ de l'ordinateur, dans un dossier dédié. Le dossier contenant le code pour le Thingy:91 doit également être placé dans un dossier de programmation sur le disque C:\.

Suivez les étapes ci-dessous pour la configuration :
1. Installation des outils en ligne de commande nRF
  - Téléchargez et installez les nRF Command Line Tools depuis le lien suivant : https://www.nordicsemi.com/Products/Development-tools/nRF-Command-Line-Tools/Download.
  - Les nRF Command Line Tools incluent nrfjprog, un outil essentiel pour flasher le firmware sur vos kits de développement Nordic.

2. Installation de Visual Studio Code
  - Rendez-vous sur https://code.visualstudio.com/download et installez la version de VS Code correspondant à votre système d'exploitation.

3. Installation du nRF Connect Extension Pack dans VS Code
  - Dans la barre d'activités de VS Code, cliquez sur l'icône Extensions.
  - Recherchez nRF Connect for VS Code Extension Pack, puis cliquez sur Installer.

Le nRF Connect Extension Pack dans VS Code permet de :
  - Développer, créer, déboguer et déployer des applications embarquées basées sur le SDK nRF Connect.
  - Interagir avec le compilateur, l'éditeur de liens, le système de construction complet, un débogueur compatible RTOS, et le SDK nRF Connect.
  - Utiliser un éditeur visuel pour les fichiers Devicetree et un terminal série intégré.

4. Installation de la chaîne d'outils (Toolchain) sur VS Code
- Lors du premier lancement de l'extension nRF Connect for VS Code (cliquez sur l'extension dans la barre de gauche), vous serez invité à installer une Toolchain. Si aucune n'est détectée, procédez ainsi :
    - Cliquez sur Installer la Toolchain.
    - Choisissez une version compatible avec la version du SDK nRF Connect que vous utiliserez (la dernière version recommandée).
    - L'installation peut prendre quelques minutes.

5. Installation du SDK nRF Connect

Dans nRF Connect pour VS Code, cliquez sur Gérer le SDK.

Dans cette section, vous pourrez installer, désinstaller et sélectionner la version active du SDK.
- Cliquez sur Installer le SDK pour afficher les versions disponibles et choisir celle que vous souhaitez utiliser et installer la, le mieux est de sélectionner la dernière sans parenthèse.
- Une fois ces étapes terminées, votre environnement est prêt pour le développement avec le SDK nRF Connect et Visual Studio Code.

**Utilisation du code:**
1. Chargement du code
- Ouvrir VS Code
- Télécharger et décompresser le dossier, puis ouvrez le dossier complet dans VS Code.

2. Build du code :
- Dans l'extension nRF Connect dans la barre d'activité, cliquez sur Add Build Configuration.
- Dans Board Target, choisissez thingy91_nrf9160_ns.
- Cliquez sur Build Configuration et attendez la fin du processus de compilation.

**Envoi du code au Thingy:91:**
- Connectez la carte Thingy:91 à votre ordinateur via un câble micro-USB.
- Allumez la carte en appuyant sur le bouton SW3 puis en activant l'interrupteur ON/OFF.
![image](https://github.com/user-attachments/assets/94f3a7b5-c8cf-49e6-ae4f-acffe8581d2b)
- Ouvrez nRF Connect for Desktop, puis l'outil Programmer (à installer si nécessaire).
- Cliquez sur Select a Device et sélectionnez le Thingy:91 dans la liste.
- Dans Add File, cliquez sur Browse, allez dans le dossier du code > build/zephyr, et sélectionnez app_signed.hex.
- Cliquez ensuite sur Write, puis Write à nouveau dans la fenêtre de confirmation pour flasher le code.

**Lire les données:**
⚠️Avant de faire cette étape, assurez vous d'avoir bien envoyé le programme dans le Thingy:91
- Inscrivez vous sur https://nrfcloud.com/
- Assure-toi d'avoir une carte SIM activée pour NB-IoT ou LTE-M. Tu peux en obtenir une auprès de ton opérateur ou de Nordic Semiconductor si elle est incluse dans le kit de développement.
- Sur le site, il vous ajouter votre carte SIM et votre Thingy:91
- Ajouter d'abord la carte SIM dans Device Management > SIM Card
-   Dans la page, ajouter le ICCID écris sur le support de la carte SIM
-   Ajouter le code PUK situé sous le gris a enlever avec une pièce pour lire le nombre et l'écrire
-   Cliquez sur Add Sim
-   Complétez ensuite les informations personnelles demandés (⚠️le numéro de téléphone doit être au format E164 (+XXYYYYYYYYY) XX correspond au code du pays (France = 33) et YYYYYYYYY correspond au numéro de téléphone sans le 0)
-   Faites save et la carte SIM est ajouté au site
- Ajouter maintenant le Thingy:91 dans Device Management > Devices
⚠️Assurez vous d'avoir inséré la carte SD dans le Thingy:91 et que celui-ci clignote en rouge et vert (4 secondes:1 seconde)
-   Appuyez sur Add Devices > LTE Device
-   Dans la nouvelle page, complétez Device ID avec : nrf-XXXXXXXXXXXXXXX (XXXXXXXXXXXXXXX Correspond au code IMEI écrit sur le Thingy:91 en enlevant l'opercule orange)
-   Complétez Pin avec le Pin écrit en dessous du numéro IMEI
-   Laissez Sub Type vide et vous avez fini de tout ajouter
- Pour lire les données, appuyez sur votre appareil dans Device Management > Devices et vous pouvez lire vos données
- Une fois que tout est bien paramétré, la carte devrait clignoter en vert puis en violet (cela signifie que la carte a réussi à détecter les données des capteurs puis à récupéré la localisation)
