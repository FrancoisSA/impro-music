

## CONFIGURATION
- Toutes les valeurs sensibles (tokens, clés API, secrets) → uniquement dans .env
- Jamais de valeur hardcodée dans le code (ports, URLs, timeouts)
- config.js est le seul point d'accès à la configuration — ne pas lire process.env ailleurs
- Ajouter toute nouvelle variable dans .env.example avec une description
- Valider les variables obligatoires au démarrage (fail-fast si manquantes)


## SÉCURITÉ
- Valider et assainir toutes les entrées utilisateur (paramètres de requête, corps POST)
- Ne jamais logger de tokens, mots de passe ou données personnelles
- Headers HTTP sécurisés via helmet.js
- Limiter les tentatives sur les endpoints sensibles (rate-limit)
- Uploads : vérifier extension ET contenu MIME réel (pas seulement le header)
- Signaler tout écart de sécurité avant de coder, pas après


## ERREURS & LOGS
- Chaque module préfixe ses erreurs avec son nom : `[module] message`
- Distinguer : erreurs utilisateur (4xx, message clair) vs erreurs système (5xx, log détaillé)
- Format de log : `2025-04-26T10:30:00Z [INFO] [wordpress] Événement publié: ID=42`
- Niveaux : ERROR (production), WARN (dégradation), INFO (actions métier), DEBUG (dev only)
- `catch` vide interdit — toujours logger ou propager
- QUand tu corrige un bug, vérifie que des bugs similaires ne sont pas présents


## GIT
- Branches : main (production), dev (intégration), feature/xxx (nouvelles fonctions)
- Commits en français, format : `type: description courte`
  Types : feat, fix, refactor, docs, chore, security
  ex. `feat: ajout publication Instagram Reels`
- Versioning sémantique : MAJOR.MINOR.PATCH
  MAJOR = rupture de compatibilité, MINOR = nouvelle fonctionnalité, PATCH = bug fix
- Toujours mettre à jour package.json + CHANGELOG avant un tag de release
- Ne jamais committer .env ou tout fichier contenant des secrets


## DOCUMENTATION
- Commenter le POURQUOI, pas le QUOI (le code dit déjà ce qu'il fait)
- JSDoc obligatoire sur les fonctions exportées : paramètres, retour, erreurs possibles
- Mettre à jour USERGUIDE.md pour toute modification visible par l'utilisateur

## REPOSITORY
- GitHub : https://github.com/FrancoisSA/impro-music
- Remote : git@github.com:FrancoisSA/impro-music.git (ou HTTPS)

## RELEASE
Lorsque je te demande de faire une release :
 - Relis le code pour trouver des problèmes de performance ou de sécurité et demande avant de modifier
 - Ajoute des commentaires pour qu'un humain puisse bien comprendre
 - Met à jour le manuel utilisateur qui porte le nom de l'appli et le numéro de version. Le format et en .MD il inclus la date et le numéro de version
 - Pousse une versio dans git. Si il n'y a pas de repository, demande si je veux le créer


## MEMORY
 Quand je te demande de mémoriser l'état du projet, ou que je te donne la commande MEMORY : Mémorise un ésumé des échanges dans MEMORY.md afin de pouvoir reprendre la conversation plus tard. Stocke les informations qui te permetrons de retrouver le contexte.