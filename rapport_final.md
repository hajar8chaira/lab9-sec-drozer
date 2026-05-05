# Rapport Final de Synthèse (Format Standard)

## Informations générales
- **Application** : Sieve (VulnerableApp)
- **Package** : com.withsecure.example.sieve
- **Version** : 1.0
- **Date d'audit** : 06 Mai 2026
- **Auditeur** : Hajar Chaira

## Résumé exécutif
L'application Sieve présente des vulnérabilités critiques de type **Broken Access Control**. La surface d'attaque est largement surexposée, permettant à n'importe quelle application malveillante de contourner le verrouillage par code PIN et de lire l'intégralité des mots de passe stockés en clair dans le Content Provider. Une remédiation immédiate est nécessaire pour protéger les données utilisateur.

## Méthodologie
- Analyse statique du manifeste Android via Drozer.
- Cartographie des composants exposés (Activities, Services, Providers).
- Vérification des protections (Permissions nulles, debug flag).
- Exploitation Proof-of-Concept (PoC) des Content Providers.

## Découvertes principales
1. **Accès non protégé aux mots de passe** via `DBContentProvider`.
2. **Contournement de l'authentification** via l'activité `PWList` exportée.
3. **Extraction des clés de chiffrement** via URI vulnérable.
4. **Application Debuggable**, facilitant l'exploitation dynamique.

## Recommandations prioritaires
1. Positionner `android:exported="false"` pour tous les composants internes.
2. Implémenter des permissions de niveau `signature`.
3. Désactiver le flag `debuggable` pour la version de production.
4. Utiliser le Android KeyStore pour le stockage des clés sensibles.

## Annexes
- Annexe A : Tableau de triage complet
- Annexe B : Captures d'écran des preuves (1.png à 14.png)
- Annexe C : Mapping OWASP MASVS
