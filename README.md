# OSINT Mobile avec BeVigil & Yaazhini
## Laboratoire d'Analyse de Surface d'Attaque

**Cours :** Sécurité des applications mobiles  
**Analyste :** Omar Haouani  
**Outils :** BeVigil (CloudSEK), Yaazhini  
**Date :** 17 mai 2026

---

## Table des matières

1. Introduction
2. Environnement Technique
3. Phase 1 : BeVigil - Connexion
4. Phase 2 : BeVigil - Upload APK
5. Phase 3 : BeVigil - Résultats
6. Phase 4 : BeVigil - Certificat
7. Phase 5 : Yaazhini - Configuration
8. Phase 6 : Yaazhini - Installation Certificat
9. Phase 7 : Yaazhini - Procédure d'analyse
10. Synthèse des Découvertes
11. Corrélation OWASP
12. Checklist
13. Conclusion

---

## 1. Introduction

Ce laboratoire porte sur l'analyse OSINT d'une application mobile avec **BeVigil** (analyse externe) et **Yaazhini** (analyse interne). Objectif : identifier expositions, secrets codés en dur et vulnérabilités.

---

## 2. Environnement Technique

| Outil     | Rôle                     |
|-----------|--------------------------|
| BeVigil   | OSINT externe (CloudSEK) |
| Yaazhini  | Analyse interne APK      |
| APK cible | app-debug.apk            |

---

## 3. Phase 1 : BeVigil - Connexion

<img width="950" height="461" alt="1" src="https://github.com/user-attachments/assets/ed1e2707-54ee-4d5d-bd3a-afbb055ccee0" />


---

## 4. Phase 2 : BeVigil - Upload APK

<img width="941" height="425" alt="2" src="https://github.com/user-attachments/assets/c80350ed-652b-4c24-8c47-933877c3d4b6" />

<img width="811" height="437" alt="3" src="https://github.com/user-attachments/assets/ee1296fb-3bb9-4079-bd72-2a8b8f8bbeb9" />

<img width="371" height="203" alt="4" src="https://github.com/user-attachments/assets/be2b72cb-2507-415c-aa76-4bac21fcdc1b" />


---

## 5. Phase 3 : BeVigil - Résultats

<img width="844" height="392" alt="5" src="https://github.com/user-attachments/assets/bd8df1e7-85e2-4cba-a091-7e6037003b90" />


**Observations :**
- Permissions : 0 dangereuses
- Secrets possibles détectés (REST API, IP Address)
- 23 bibliothèques tierces identifiées

<img width="946" height="443" alt="6" src="https://github.com/user-attachments/assets/f26b7b8b-68fe-48df-b8dd-fc6d1c86d13d" />


**Score : 9.2/10 (Excellent)**

**Issues :**
- Exported Activity (MED - 94.6%)
- Possible Secret Detected (LOW - 5.4%)

---

## 6. Phase 4 : BeVigil - Certificat

<img width="299" height="227" alt="7" src="https://github.com/user-attachments/assets/10be1ccd-bad3-4293-8eec-3805f47686a3" />


| Description                                   | Status |
|-----------------------------------------------|--------|
| APK is signed with a code signing certificate | GOOD   |
| APK is signed with a debug certificate        | BAD    |

**Public Key Algorithm :** RSA — Bit Size : 2048  
**Hardcoded Keys :** Not Available

---

## 7. Phase 5 : Yaazhini - Configuration

<img width="671" height="446" alt="9" src="https://github.com/user-attachments/assets/86194c81-aa1d-443b-b31c-e11141e0bc27" />


- **IP :** 172.29.32.1  
- **Port :** 8088

---

## 8. Phase 6 : Yaazhini - Installation Certificat

<img width="824" height="451" alt="8" src="https://github.com/user-attachments/assets/f9fa4b8a-a03b-4659-84a4-16cbd268019f" />


- **Valide du :** 20/03/2026 **au :** 22/06/2028

---

## 9. Phase 7 : Yaazhini - Procédure d'analyse

<img width="959" height="503" alt="10" src="https://github.com/user-attachments/assets/c414f6ed-385e-4bbf-b8da-7a2b9b016965" />

<img width="178" height="359" alt="11" src="https://github.com/user-attachments/assets/52da1826-5679-4b3a-8c1b-bd02ec1c992a" />



**Étapes :**

1. Configurer le proxy Android (`172.29.32.1:8088`)
2. Installer le certificat
3. Parcourir toutes les écrans
4. Lancer le scan
5. Générer le rapport

---

## 10. Synthèse des Découvertes

| Élément           | Sévérité | Recommandation               |
|-------------------|----------|------------------------------|
| Certificat debug  | BAD      | Utiliser certificat release  |
| Exported Activity | MED      | Vérifier composants exportés |
| Secret détecté    | LOW      | Nettoyer le code             |

---

## 11. Corrélation OWASP

| Découverte        | Référence MASVS    |
|-------------------|--------------------|
| Certificat debug  | MASVS-RESILIENCE-4 |
| Exported Activity | MASVS-CODE-3       |
| Secrets dans code | MASVS-STORAGE-2    |

---

## 12. Checklist

- [x] Périmètre défini
- [x] Traçabilité complète
- [x] Export BeVigil sauvegardé
- [x] Rapport Yaazhini sauvegardé
- [x] Mapping OWASP réalisé
- [x] Rapport final rédigé

---

## 13. Conclusion

Score BeVigil : **9.2/10**. Points à corriger : certificat debug et activités exportées.

---
