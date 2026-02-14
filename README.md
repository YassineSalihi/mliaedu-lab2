# Définition : 
> Rooting s'agit d'obtenir les privilèges les plus 
> élèvé dans un système.

> [!NOTE]
> ADB est l'outil principal pour communiquer avec 
> votre appareil Android depuis votre ordinateur.

# Etape 1 : Rooting AVD
Active le serveur adb en mode root si supporté par l'image
 
 ![root&remount](https://github.com/user-attachments/assets/bd24b686-e58b-460c-92fc-1c25f92ca047)

![ids](https://github.com/user-attachments/assets/f570bcd7-8080-429a-b606-689835758d25)

![verify](https://github.com/user-attachments/assets/006259f4-7c19-4a5f-9fc6-98303bf6c933)

![Logs](https://github.com/user-attachments/assets/ad2a2dbf-bf83-4d73-a18c-08a45eb534b0)

# Etape 2 : Fiche Périmètre de l'Audit
 - Application & Version : 
 - Support (Cible) : Emulateur Android Studio (AVD) : Pixel_6
 - Objectif du test : 
 - Nature des Données : 
 - Environnement Réseau : Réseau local de test isolé (via machine hôte Kali Linux).

# Etape 3 : Démarrer AVD 
 
![adb devices](https://github.com/user-attachments/assets/35129add-99fe-46da-8d51-f06df8ade4a9)

# Etape 4 : Installer et lancer l'app de test

~~~sh 
git clone https://github.com/0xArab/diva-apk-file.git
~~~
 
![](https://github.com/user-attachments/assets/d6370948-ac2c-4e76-bd0b-1fdbedc3cf29)

# Etape 5 : 3 Scénarios

![diva open](https://github.com/user-attachments/assets/e79e6fd6-29d7-4071-a163-cba25a521728)

## Scénario 1 :

 On a utilisé un décompilateur pour avoir le source code,
diva_decompiler_to_source/sources/jakhar/aseem/diva/HardcodeActivity.java,
on a trouvé le code secret : 

![source code](https://github.com/user-attachments/assets/0a134ae0-fa6f-4083-b1ac-df16fa6327ef) 

## Scénario 2 : SQL injection

![](https://github.com/user-attachments/assets/76055981-c737-44b0-b3ab-4007eb381114)

## Scénario 3 : WebURL

![](https://github.com/user-attachments/assets/45152b70-7b8c-4e08-aa3d-6b2c490894a6)

# Etape 6 : Lire Android Security

<https://source.android.com/docs/security> 

Le programme de sécurité d'Android repose sur une architecture multicouche conçue pour protéger les données et la confidentialité des utilisateurs tout en offrant un environnement ouvert aux développeurs. Cette approche inclut des fonctionnalités natives comme le sandboxing des applications, le chiffrement des données et le Verified Boot. La plateforme assure une protection continue grâce à la publication régulière de bulletins de sécurité et à l'application de meilleures pratiques couvrant aussi bien le matériel que le réseau. 
Enfin, des outils de test et de diagnostic rigoureux permettent de détecter et de corriger les vulnérabilités avant qu'elles ne soient exploitées.



