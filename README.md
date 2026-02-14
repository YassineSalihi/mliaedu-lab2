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

# Etape 7 : Verified Boot

> [!NOTE]
> Green : Tout est normal, système vérifié et intègre
> Yellow/Orange : Avertissement, système modifié mais fonctionnel 
> Red : Danger, intégrité compromise

![](https://github.com/user-attachments/assets/7a1ba00b-867c-4b66-a976-85324ec7b45c)

# Etape 9 : Définir le Rooting

 Le rooting est le processus par lequel les utilisateurs d'appareils Android peuvent obtenir un contrôle privilégié (appelé accès root) sur divers sous-systèmes de l'appareil, généralement des smartphones et des tablettes.
 Android étant basé sur une version modifiée du noyau Linux, le rooting d'un appareil Android donne accès à des autorisations administratives (superutilisateur) similaires à celles de Linux ou de tout autre système d'exploitation de type Unix tel que FreeBSD ou macOS. 

# Etape 11 : Matrice de risques

* **Intégrité non garantie** : Les conclusions peuvent être biaisées car le système d'exploitation ne se comporte plus de manière standard et les mécanismes de protection natifs sont désactivés.
* **Surface d'attaque accrue** : Si l'appareil quitte le périmètre sécurisé du laboratoire, il devient vulnérable aux menaces externes en l'absence de ses barrières de sécurité d'origine.
* **Exposition de données** : Risque de violation de la confidentialité si des données sensibles transitent ou sont stockées sur un appareil dont le cloisonnement est rompu.
* **Instabilité système** : Les modifications peuvent rendre les tests non reproductibles et entraîner des résultats incohérents.
* **Mélange de comptes** : Risque de fuite d'informations personnelles si les comptes de test et les comptes personnels ne sont pas strictement isolés.
* **Nettoyage insuffisant** : Persistance de données sensibles entre deux sessions de test si une procédure de remise à zéro (reset) complète n'est pas appliquée.
* **Réseau non isolé** : Risque d'effets de bord ou d'attaques involontaires sur des systèmes tiers ou des infrastructures externes.
* **Traçabilité insuffisante** : Difficulté majeure pour auditer précisément les manipulations effectuées ou pour fournir une preuve de concept (PoC) fidèle.

# Etape 12 : Mesures Défensives

Pour atténuer les risques liés au rooting et sécuriser l'environnement de test, les mesures suivantes doivent être appliquées :

* **Réseau isolé** : Utiliser un segment réseau dédié pour éviter toute communication non contrôlée vers l'extérieur.
* **Données fictives** : Manipuler exclusivement des données de test pour éliminer tout risque de fuite d'informations réelles.
* **Équipement dédié** : Utiliser un appareil physique ou un émulateur (AVD) réservé uniquement aux audits de sécurité.
* **Snapshots et Wipe** : Effectuer une remise à zéro complète ou restaurer un instantané propre après chaque séance de test.
* **Journal de configuration** : Tenir un registre détaillé des modifications système pour assurer la reproductibilité des résultats.
* **Isolation des comptes** : Proscrire l'usage de comptes personnels afin d'éviter tout mélange accidentel de données privées.
* **Contrôle des APK** : Restreindre strictement l'installation aux seules applications cibles pour limiter les vecteurs d'attaque.
* **Traçabilité complète** : Systématiser l'horodatage et les captures d'écran à chaque étape pour garantir un audit transparent.

# Étape 13 : OWASP MASVS (Référence de Sécurité)

L'**OWASP** (Open Web Application Security Project) est l'organisation de référence mondiale en cybersécurité. Le **MASVS** (Mobile Application Security Verification Standard) est leur standard spécifique pour évaluer la sécurité des applications mobiles.

### Exigences clés (Extraits)

* **MASVS-STORAGE-1** : Les données sensibles (clés d'API, mots de passe, tokens) doivent être stockées de manière sécurisée en utilisant les mécanismes de chiffrement natifs du système.
* **MASVS-NETWORK-1** : Toutes les communications réseau doivent utiliser le protocole TLS avec une configuration robuste et une vérification stricte des certificats.

### Application pratique
Grâce aux **privilèges root** obtenus lors des étapes précédentes, vous pouvez auditer ces exigences en :
1. Explorant les répertoires de stockage privés pour vérifier l'absence de secrets en clair (Storage).
2. Utilisant un proxy d'interception pour valider la robustesse du chiffrement du trafic (Network).

## Étape 14 : OWASP MASTG (Méthodologie de Test)

Le **MASTG** (Mobile Application Security Testing Guide) est le manuel technique qui explique **comment** vérifier les exigences posées par le MASVS. C'est votre guide pratique pour réaliser des tests d'intrusion sur mobile.

### Idées de tests appliquées à DIVA

* **Analyse du stockage local** : Examiner les fichiers de préférences dans `/data/data/jakhar.aseem.diva/shared_prefs/` pour vérifier si des informations sensibles (comme le login ou les clés) y sont stockées en clair. 
* **Surveillance des logs système** : Utiliser la commande `adb logcat` pendant l'utilisation de l'application pour détecter des fuites d'informations sensibles (mots de passe, numéros de carte) envoyées vers la console de débogage.



### Astuce technique (Privilèges Root)
Sur Android, le dossier `/data/data/` est normalement protégé par le "bac à sable" (sandbox) applicatif. Grâce à vos **privilèges root**, vous pouvez briser cet isolement pour accéder aux données privées de DIVA et valider si l'application respecte les standards de sécurité.

> [!NOTE]
> On a utilisé strings et la décompilation pour trouver la clé hardcodée (Analyse statique).
> On a utilisé adb logcat pour voir les fuites d'informations (Analyse dynamique, préconisée par le MASTG).

# Etape 16 : Traçabilité (Fiche Environnement)

> [!IMPORTANT]
> En sécurité, la documentation est aussi importante que le test lui-même. Sans traçabilité, un test n'a pas de valeur probante et ne peut être ni reproduit, ni vérifié.

## 📋 Fiche de l'Environnement de Test

| Champ | Informations |
| :--- | :--- |
| **Date / Auteur** | 14/02/2026 - addseen |
| **Support de test** | AVD (Android Virtual Device) - Pixel_6 |
| **Version Android / API** | Android [Version, ex: 13] / API [ex: 33] |
| **Application (APK)** | DIVA (Damn Insecure Vulnerable App) v1.0 |
| **Environnement réseau** | LAN de test isolé via machine hôte (Kali Linux) |

## 🧪 Résumé des Scénarios de Test

1. **Scénario 1 : Hardcoding Issue** - Analyse statique via décompilation (JADX) pour extraire des secrets en dur dans le code Java.
2. **Scénario 2 : SQL Injection** - Test d'injection sur les entrées de recherche pour bypasser la logique de la base de données locale.
3. **Scénario 3 : WebView Vulnerability** - Exploitation de `loadUrl` pour accéder à des fichiers locaux via le schéma `file://`.

## 🔍 Observations Factuelles & Limites
* **Observations** : L'utilisation d'**adb root** a permis de confirmer l'exposition des données dans `/data/data/`. L'absence de vérification du certificat (MASTG) facilite l'interception.
* **Limites** : Tests effectués sur émulateur x86_64 ; certains comportements liés au matériel réel (TEE, StrongBox) n'ont pas été audités.

## 🛡️ Clôture et Preuves
* **Reset effectué** : [x] Oui / [ ] Non
* **Preuve du Reset** : [Copie d'écran du wipe ou commande `adb shell rm -rf`]

---

### 📸 Captures de Traçabilité à Inclure

* **Accès Root** : Capture du terminal montrant la commande `adb root` et le changement du prompt (`#`).
* **Intégrité Boot** : Capture du résultat de `adb shell getprop ro.boot.verifiedbootstate` (valeur `orange` ou `yellow`).
* **Diva en exécution** : Capture d'écran de l'application lancée sur l'AVD Pixel_6.
* **Logs Dynamiques** : Capture de `adb logcat | grep -i "diva"` montrant une fuite d'information.

---
**Conseil de documentation** : Utilisez un outil comme *Flameshot* ou *Spectacle* pour annoter vos captures avec des flèches rouges sur les adresses mémoires ou les secrets révélés.

