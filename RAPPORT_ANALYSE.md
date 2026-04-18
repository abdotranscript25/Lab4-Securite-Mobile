# Rapport d'analyse statique - ProjetWS

## Informations générales
- **Date d'analyse :** 2026-04-18
- **Analyste :** El Hachimi Abdelhamid
- **APK analysé :** app-debug.apk
- **Version :** 1.0
- **Provenance :** Projet développé par mes soins (Android Studio)
- **Outils utilisés :** JADX GUI v1.5.0, dex2jar v2.4, JD-GUI v1.6.6

---

## Résumé exécutif

Cette analyse statique a révélé **6 vulnérabilités potentielles** dans l'application ProjetWS (Gestion d'étudiants).

Les principales préoccupations concernent :
- **Communications non chiffrées (HTTP)** : les données des étudiants circulent en clair
- **Configuration de débogage activée** : l'application est débuggable en production
- **Backup des données autorisé** : la base de données peut être extraite

Le niveau de risque global est évalué comme **ÉLEVÉ**.

### Actions prioritaires recommandées :
1. **Remplacer HTTP par HTTPS** et désactiver usesCleartextTraffic
2. **Désactiver le mode débogage** en production (debuggable=false)
3. **Désactiver le backup** (llowBackup=false)

---

## Constats détaillés

### Constat #1 : Communication HTTP non sécurisée
**Sévérité :** Élevée  
**Description :** L'application utilise le protocole HTTP (non chiffré) pour communiquer avec le serveur, exposant les données des étudiants (nom, prénom, ville, sexe) en clair sur le réseau.  
**Localisation :** AddEtudiant.java (ligne 26), ListEtudiant.java (ligne 22)  
**Impact potentiel :** Un attaquant sur le même réseau WiFi peut intercepter les requêtes (attaque MITM) et lire/modifier les données des étudiants.  
**Remédiation recommandée :** Remplacer HTTP par HTTPS, configurer un certificat SSL/TLS valide sur le serveur, désactiver usesCleartextTraffic="true".

---

### Constat #2 : Mode débogage activé
**Sévérité :** Élevée  
**Description :** Le manifeste Android contient ndroid:debuggable="true", ce qui permet le débogage de l'application en production.  
**Localisation :** AndroidManifest.xml (ligne 8)  
**Impact potentiel :** Un attaquant peut déboguer l'application en temps réel, accéder aux variables mémoire et extraire des données sensibles.  
**Remédiation recommandée :** Désactiver le débogage : ndroid:debuggable="false".

---

### Constat #3 : Backup autorisé
**Sévérité :** Moyenne  
**Description :** Le manifeste contient ndroid:allowBackup="true", permettant l'extraction des données via db backup.  
**Localisation :** AndroidManifest.xml (ligne 8)  
**Impact potentiel :** La base de données SQLite contenant les étudiants peut être extraite par un attaquant ayant accès au téléphone.  
**Remédiation recommandée :** Désactiver le backup : ndroid:allowBackup="false".

---

### Constat #4 : Trafic en clair autorisé
**Sévérité :** Élevée  
**Description :** Le manifeste contient ndroid:usesCleartextTraffic="true", autorisant les communications HTTP non chiffrées.  
**Localisation :** AndroidManifest.xml (ligne 8)  
**Impact potentiel :** Toute l'application communique en clair, facilitant l'interception des données.  
**Remédiation recommandée :** Désactiver : ndroid:usesCleartextTraffic="false".

---

### Constat #5 : IP serveur hardcodée
**Sévérité :** Moyenne  
**Description :** L'adresse IP du serveur 192.168.0.162 est écrite en dur dans le code source.  
**Localisation :** AddEtudiant.java (ligne 26), ListEtudiant.java (ligne 22)  
**Impact potentiel :** L'architecture interne est exposée. Si l'IP change, l'application nécessite une mise à jour.  
**Remédiation recommandée :** Utiliser un nom de domaine au lieu d'une IP, ou configurer l'URL dynamiquement.

---

### Constat #6 : Activité principale exportée
**Sévérité :** Moyenne  
**Description :** MainActivity a ndroid:exported="true", ce qui la rend accessible par d'autres applications.  
**Localisation :** AndroidManifest.xml  
**Impact potentiel :** Une application malveillante peut lancer l'activité principale sans autorisation.  
**Remédiation recommandée :** Mettre ndroid:exported="false" si l'accès externe n'est pas nécessaire.

---

## Annexes

### Permissions demandées
- ndroid.permission.INTERNET
- ndroid.permission.ACCESS_NETWORK_STATE

### Composants exportés
- MainActivity (exportée)
- ProfileInstallReceiver (exporté - bibliothèque AndroidX)

### URLs trouvées dans le code
- http://192.168.0.162/projet/ws/createEtudiant.php
- http://192.168.0.162/projet/ws/loadEtudiant.php

### Outils utilisés
- **JADX GUI v1.5.0** : Décompilation directe de l'APK (code + manifeste + ressources)
- **dex2jar v2.4** : Conversion des fichiers DEX en JAR
- **JD-GUI v1.6.6** : Visualisation du code Java décompilé à partir du JAR
