# LAB 4 : Analyse statique d'un APK avec JADX GUI + dex2jar + JD-GUI

## 📌 Objectif du lab

Apprendre à analyser la sécurité d'une application Android (APK) **sans l'exécuter** en utilisant des outils de décompilation et d'analyse statique. Identifier les vulnérabilités potentielles : secrets en clair, permissions dangereuses, configurations exposées.

---

## 🎯 Ce que nous avons appris

| Concept | Définition |
|---------|-------------|
| **APK** | Android Package Kit = fichier d'installation Android (c'est un ZIP) |
| **DEX** | Dalvik Executable = bytecode Android (code compilé) |
| **JAR** | Java Archive = format standard pour les bibliothèques Java |
| **Décompilation** | Transformer du bytecode en code source lisible |
| **Manifest** | Fichier XML qui déclare les permissions et composants |
| **Exported** | Composant accessible par d'autres applications |

---

## 🛠️ Outils utilisés

| Outil | Type | Rôle |
|-------|------|------|
| **JADX GUI** | Décompilateur | Visualisation complète (manifeste + code + ressources) |
| **dex2jar** | Convertisseur | Transforme les fichiers `.dex` en `.jar` |
| **JD-GUI** | Décompilateur Java | Affiche le code Java à partir du `.jar` |

---

## 🛠️ Environnement de test

| Élément | Valeur |
|---------|--------|
| **APK analysé** | ProjetWS (app-debug.apk) |
| **Package** | `com.example.projetws` |
| **Version** | 1.0 |
| **Min SDK** | 24 (Android 7.0) |
| **Target SDK** | 36 |
| **Taille APK** | 11.1 MB |

---

## 📊 Vulnérabilités découvertes

| # | Constat | Sévérité | Localisation |
|---|---------|----------|--------------|
| 1 | Communication HTTP non sécurisée | **Élevée** | `AddEtudiant.java`, `ListEtudiant.java` |
| 2 | Mode débogage activé | **Élevée** | `AndroidManifest.xml` |
| 3 | Trafic en clair autorisé | **Élevée** | `AndroidManifest.xml` |
| 4 | Backup autorisé | Moyenne | `AndroidManifest.xml` |
| 5 | IP serveur hardcodée | Moyenne | `AddEtudiant.java`, `ListEtudiant.java` |
| 6 | Activité principale exportée | Moyenne | `AndroidManifest.xml` |

---
## 📊 Comparaison JADX GUI vs JD-GUI

| Aspect | JADX GUI | JD-GUI |
|--------|----------|--------|
| **Format d'entrée** | APK directement | JAR (nécessite conversion) |
| **Affichage ressources** | ✅ Oui (XML, manifeste) | ❌ Non |
| **AndroidManifest.xml** | ✅ Visible | ❌ Non |
| **Lisibilité du code** | ✅ Très bonne | ⚠️ Moyenne (obfusqué) |
| **Facilité d'utilisation** | ✅ Très simple | ⚠️ Nécessite conversion |

**Conclusion :** JADX GUI est plus adapté pour l'analyse d'APK Android.

## 📸 Screenshots

## Task 1  

<img width="757" height="213" alt="T1" src="https://github.com/user-attachments/assets/f29eaa13-2bbe-4dd7-8290-d77943c33eb0" />
<img width="993" height="723" alt="T1_2" src="https://github.com/user-attachments/assets/523ca938-bd2d-4ea0-83c3-be194f406d41" />

## Task 3

<img width="1600" height="837" alt="T3" src="https://github.com/user-attachments/assets/f29e1d98-1af8-4dc2-b579-4902fe35ad93" />
<img width="1599" height="789" alt="T3_1" src="https://github.com/user-attachments/assets/0bff2d07-dc42-492f-8847-c86264292b58" />
<img width="1249" height="715" alt="T3_2" src="https://github.com/user-attachments/assets/75d3fd06-dc3a-4032-860d-d92596a6a503" />
<img width="1265" height="676" alt="T3_4" src="https://github.com/user-attachments/assets/4c7c1c90-0a32-46dc-9ce7-a98ce0dcf89d" />
<img width="1153" height="746" alt="T3_5" src="https://github.com/user-attachments/assets/7752171e-b58d-4f9b-bf14-091ca7914a3e" />

## Task 4

<img width="858" height="136" alt="T4" src="https://github.com/user-attachments/assets/56b80236-3274-42fb-87dc-e28f6dcfaf0d" />
<img width="864" height="193" alt="T4_1" src="https://github.com/user-attachments/assets/7dff723e-ed4d-4c45-917c-237c065fb253" />
<img width="1386" height="743" alt="T4_2" src="https://github.com/user-attachments/assets/72a3e35b-8c42-44b2-ad6d-088e3ea79c2f" />
<img width="1128" height="704" alt="T4_3" src="https://github.com/user-attachments/assets/06913b6e-a2db-41bd-b948-6cce1a31ef56" />
<img width="1499" height="707" alt="T4_4" src="https://github.com/user-attachments/assets/3066c3c8-d70e-4801-bb23-2907e95e73ce" />

## Task 5

<img width="771" height="641" alt="T5" src="https://github.com/user-attachments/assets/6b754ece-01fc-4ff6-9fc5-7d88e9740914" />
<img width="1030" height="676" alt="T5_1" src="https://github.com/user-attachments/assets/3fb3c120-df27-4506-886e-76e73dd8385e" />
<img width="676" height="417" alt="T5_2" src="https://github.com/user-attachments/assets/3c209d88-ec97-438f-8ade-c469044c5fe9" />

## Task 6

<img width="1595" height="855" alt="T6" src="https://github.com/user-attachments/assets/e72506fc-c70c-42a4-b447-12e9ee41dbcd" />
<img width="1580" height="779" alt="T6_1" src="https://github.com/user-attachments/assets/a8deae55-4254-412b-8459-9629e8437992" />
<img width="1589" height="834" alt="T6_2" src="https://github.com/user-attachments/assets/95da1398-749f-469c-bd1a-6f32b771de70" />
<img width="1325" height="404" alt="T6_3" src="https://github.com/user-attachments/assets/c949c0f6-ea5d-4e85-be1c-da1c37454e3d" />

## Task 8

<img width="796" height="633" alt="T8" src="https://github.com/user-attachments/assets/b16d1862-6eb0-42be-bb95-128f55069095" />



## ✅ Checklist

### Début de lab

| Vérification | Statut |
|--------------|--------|
| APK disponible (ProjetWS) | ✅ |
| Outils installés (JADX, dex2jar, JD-GUI) | ✅ |
| Workspace créé | ✅ |

### Pendant le lab

| Vérification | Statut |
|--------------|--------|
| APK vérifié (hash SHA256) | ✅ |
| Analyse avec JADX GUI | ✅ |
| Recherche chaînes sensibles | ✅ |
| Conversion DEX → JAR | ✅ |
| Analyse avec JD-GUI | ✅ |
| Comparaison des outils | ✅ |

### Fin de lab

| Vérification | Statut |
|--------------|--------|
| Mini-rapport rédigé (6 constats) | ✅ |
| Screenshots pris | ✅ |
| Aucune donnée sensible exposée | ✅ |


## 👤 Auteur

**El Hachimi Abdelhamid**  
Date : 2026-04-18  
Cours : Sécurité des applications mobiles
