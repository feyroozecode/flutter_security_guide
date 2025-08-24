# flutter_security_guide

# Guide de Sécurité Flutter  
**2025**

---

## par IBRAHIM AHMAD  
*Consultant en Développement d’Application et Sécurité Mobile*

---

## Introduction et Vue d'ensemble  

Dans le paysage numérique actuel, où les applications mobiles sont devenues omniprésentes, la sécurité est une préoccupation primordiale. Flutter, le framework de développement d'applications multiplateformes de Google, offre une flexibilité et une rapidité de développement inégalées.  

Cependant, cette agilité ne doit pas se faire au détriment de la sécurité. Ce guide est conçu pour les consultants et les développeurs Flutter qui cherchent à intégrer les meilleures pratiques de sécurité dans leurs applications mobiles (Android et iOS) afin de protéger les données sensibles et de garantir une expérience utilisateur fiable et sécurisée.  

La sécurisation d'une application Flutter nécessite une approche de défense en profondeur :  

- **Mise à jour régulière des dépendances**  
- **Éviter les secrets codés en dur**  
- **Chiffrement et stockage sécurisé**  
- **Validation des entrées**  
- **Authentification forte**  
- **Chiffrement du trafic réseau**  
- **Minimisation de la surface d’attaque**  

Les normes **OWASP Mobile (MASVS/Top-10)** rappellent l’importance :  
- du stockage sécurisé  
- de la cryptographie  
- de l’authentification  
- de la sécurité réseau  
- de la qualité du code  
- de la résistance à l’ingénierie inverse [1, 2]  

Ce document fournit des solutions pratiques et actualisées en 2025 pour renforcer la sécurité des applications Flutter.  

---

## Sécurité du Code et de la Compilation  

### Mises à Jour Régulières des Dépendances  
- Garder le SDK Flutter et les packages à jour.  
- Ne pas « épingler » indéfiniment les versions.  
- Vérifier régulièrement les correctifs de sécurité [3].  

### Analyse Statique du Code (SAST)  
- Intégrer **SonarQube** ou **Veracode** dans la CI/CD [4, 5].  
- Utiliser `flutter analyze` et les **linters Dart**.  

### Gestion des Secrets  
- Ne jamais coder en dur **mots de passe** ou **API keys**.  
- Utiliser `--obfuscate` et `--split-debug-info` lors de la compilation release [7].  

### Résistance à l’Ingénierie Inverse  
- Activer **ProGuard/R8** (Android).  
- Supprimer les symboles de debug.  
- Vérifier les signatures à l’exécution [8].  

---

## Stockage Sécurisé (Données au Repos)  

- Utiliser **flutter_secure_storage** (Keychain iOS, Keystore Android) [9, 10].  
- Chiffrer bases de données avec **Hive** ou **sqlcipher**.  
- Intégrer **authentification biométrique** via `local_auth`.  
- Ne stocker que le minimum de données nécessaires.  

---

## Sécurité Réseau (Données en Transit)  

### HTTPS Obligatoire  
- Toutes les communications via **TLS (HTTPS)**.  
- Ne jamais désactiver la validation SSL [11].  

### Épinglage de Certificats SSL  
```dart
await HttpCertificatePinning.check(
  serverURL: 'https://api.example.com',
  sha: SHA.SHA256,
  allowedSHAFingerprints: ['<empreinte_sha256>'],
  timeout: 50,
);
```

Utiliser http_certificate_pinning ou ssl_pinning_plugin [12, 13].

Validation des Endpoints

Vérifier les domaines approuvés.

Désactiver les ponts JS non sécurisés.

TLS Supplémentaire

Forcer TLS 1.2/1.3.

Activer HSTS et transparence des certificats [16].

Authentification et Autorisation

Utiliser OAuth2/OIDC, Firebase Auth, AWS Cognito [17].

Stocker les jetons dans Keychain/Keystore.

Secrets API uniquement côté serveur.

Utiliser PKCE pour OAuth2 mobile.

Valider les JWT côté serveur [18].

Protections Spécifiques à Android

Créer network_security_config.xml [14].

Activer Google Play App Signing + Play Integrity [19].

Limiter les permissions.

Détecter les appareils rootés avec SafetyNet/Play Integrity.

Protections Spécifiques à iOS

ATS (App Transport Security) activé par défaut [20].

Utiliser Keychain et Data Protection.

Activer App Attest / DeviceCheck.

Vérifier le jailbreak (optionnel).

Toujours compiler avec dernière version de Xcode/iOS SDK.

Outils et Bibliothèques Essentiels

Analyse statique : SonarQube, Veracode, Dart analyze [4, 5].

Stockage sécurisé : flutter_secure_storage [9].

SSL Pinning : http_certificate_pinning, ssl_pinning_plugin [12, 13].

Vérification des dépendances : Dependabot, pub outdated.

Tests sécurité mobile : MobSF, OWASP MASTG [23, 24].

Bonnes Pratiques

Injecter secrets avec --dart-define et CI/CD secure store [25].

Chiffrer SharedPreferences avec EncryptedSharedPreferences.

Toujours valider les entrées utilisateur [26].

Ne pas exposer d’erreurs sensibles en prod [27].

Implémenter un timeout de session.

Activer la journalisation d’audit sur serveur sécurisé.

Ressources Supplémentaires

Flutter Security Documentation
 [28]

OWASP MASVS
 [1]

OWASP Mobile Top 10 (2024)
 [2]

Android Network Security Config
 [14]

Apple ATS Guidelines
 [20]

MobSF - Mobile Security Framework
 [23]

Références

(liste complète en fin du document avec liens numérotés [1-28])
