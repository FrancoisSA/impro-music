# ImproMusic — Manuel utilisateur v1.4
**Date** : 2026-05-07
**Version** : 1.4.0
**Plateforme** : Chrome Android (tablette) — fonctionne aussi sur Chrome desktop

---

## Présentation

ImproMusic est une régie son pour spectacle vivant. Elle fonctionne **sans serveur**, directement depuis le fichier `impromusic.html` ouvert dans Chrome. Les projets sont sauvegardés en fichiers `.json` sur votre disque.

---

## Structure des dossiers audio

Depuis la v1.4, **tous les fichiers audio** sont regroupés sous un seul dossier racine, que l'on appellera ici `PLAYLISTS/` :

```
PLAYLISTS/
  SEQUENCE/        ← sons de la séquence
  IMPRO DANCE/     ← sons de la playlist "Impro Dance"
  IMPRO FILMS/     ← sons de la playlist "Impro Films"
  …
```

Au chargement, l'application scanne récursivement ce dossier en une seule passe. Séquence et playlists partagent le même index de fichiers.

> **Important :** les dossiers doivent être de **vrais dossiers** sur le disque. Les alias macOS (raccourcis) ne sont pas suivis par Chrome.

---

## Démarrage rapide

1. Ouvrir `impromusic.html` dans Chrome
2. Charger un projet via **🎭 Spectacle → 📂 Charger**
3. Si un bandeau orange/rouge apparaît, cliquer **📁 Sélectionner PLAYLISTS/** et pointer vers le dossier racine
4. La prochaine ouverture retrouve le dossier automatiquement (1 clic de permission Chrome)

---

## Interface

### En-tête
| Élément | Rôle |
|---------|------|
| **🎵 ImproMusic v1.4.0** | Titre et version |
| **🎭 Spectacle** | Créer, charger ou sauvegarder un spectacle |
| **🪲** | Journal des erreurs (contour rouge = erreur présente) |
| **⚙** | Panneau Couleurs, thème et police |
| **🔊 Volume** | Volume master global |

### Bandeau "En cours"
| Bouton | Action |
|--------|--------|
| **▶** | Lecture |
| **⏸** | Pause / Reprise |
| **■** | Stop immédiat |
| **🔉** | Sourdine : cycle −50% → −75% → −90% → Off |
| **🔇** | Silence total (volume à 0, lecture continue) |
| **↘** | Fade out en 2 secondes puis stop |
| **⏭** | Jouer le cue suivant |

---

## Séquence + Notes (colonne principale)

La vue principale est divisée en deux colonnes redimensionnables :

- **Séquence** (gauche) — liste ordonnée des cues
- **Notes** (droite) — notes de mise en scène alignées sur chaque cue

### Redimensionner
Glisser la barre de séparation entre les deux colonnes. La position est mémorisée entre les sessions.

### États des cues
- **Contour orange** = en cours de lecture
- **Contour vert** = cue suivant prêt
- **Contour bleu** = en pause
- **Opacité réduite** = déjà joué
- **⊙ vert** = fichier audio chargé · **○ gris** = pas de fichier

### Jouer un cue
- **Tap sur la carte** = jouer (ou pause si en cours)
- **▶ / ⏸ / ■** sur la carte = contrôles individuels
- **»** = marquer comme "cue suivant"
- **🔁** = activer/désactiver la boucle

### Sections
- En mode édition : **+ Section** insère un séparateur nommé
- Hors édition : tap sur le séparateur réduit/développe la section

---

## Mode édition

Activer via **✏ Éditer** dans l'en-tête de la séquence.

En mode édition :
- **＋** ajoute un nouveau cue (ouvre la modale)
- **+ Section** insère un séparateur
- **↑ ↓** réordonnent les cues
- **✏** ouvre la modale de modification
- **👁** masque/affiche un cue
- **✕** supprime (confirmation inline)

---

## Modale d'édition d'un cue

| Zone | Paramètres |
|------|-----------|
| **En-tête** | Nom · Type (Musique / Effet / Ambiance / Boucle) |
| **Volume** | Slider 0–100% avec valeur en temps réel |
| **↗↘ Timing** | Fade in · Fade out · Boucle |
| **↦↤ Plage** | Débuter à (mm:ss) · Finir à (mm:ss ou -30s) |
| **Fichier audio** | Bouton 📂 Choisir + nom du fichier sélectionné |
| **Notes** | Zone de texte libre (plusieurs lignes) |

---

## Playlists libres

La colonne droite accueille des **playlists** : listes de morceaux streamés depuis un sous-dossier de `PLAYLISTS/`, **sans chargement en RAM**.

### Ajouter une playlist
1. Cliquer **✏ Éditer** dans l'en-tête Playlists
2. Cliquer **＋ Ajouter une playlist**
3. Sélectionner un sous-dossier — tous les fichiers audio sont importés et triés alphabétiquement
4. Les vignettes d'album art (tags ID3) s'extraient automatiquement en arrière-plan

### Importer un morceau dans la séquence *(nouveau en v1.4)*
En mode édition des playlists, chaque carte de morceau affiche un bouton **←** (flèche bleue vers la gauche). Cliquer ce bouton insère le morceau dans la séquence juste après le cue sélectionné en dernier. Si aucun cue n'est sélectionné, le morceau est ajouté en fin de séquence. Le buffer audio est chargé immédiatement — le cue est jouable sans délai.

### Lire un morceau
- **Tap** sur la carte ou **▶** pour lire
- **■** pour stopper
- **🔁** pour activer la boucle

### Organisation
- **▾ / ▸** (chevron gauche de l'en-tête) : tout replier / déplier
- Chaque playlist dispose de son propre chevron de repli
- En mode édition : **↑ ↓** réordonnent les playlists, **↺** rescanne le dossier, **✕** supprime

### Rescan du dossier
Cliquer **↺** en mode édition pour mettre à jour une playlist :
- Nouveaux fichiers ajoutés avec réglages par défaut
- Fichiers supprimés retirés (arrêt automatique si en cours)
- Réglages des morceaux existants conservés

### Redimensionner
Glisser la barre verticale entre la séquence et les playlists.

---

## Gestion des dossiers audio

### Premier chargement ou dossier manquant
Si le bandeau orange/rouge apparaît au chargement, cliquer **📁 Sélectionner PLAYLISTS/** et pointer vers le dossier racine. L'application scanne immédiatement tous les sous-dossiers en récursif et charge les sons.

### Sessions suivantes
Chrome redemande la permission (1 clic). Pour ne plus être redemandé, choisir **"Autoriser à chaque visite"** dans la popup Chrome.

### Rescan automatique au démarrage
Si le dossier racine est déjà connu et accessible, les playlists sont rescannées silencieusement (nouveaux fichiers intégrés, supprimés retirés).

---

## Compatibilité tablette Android

Sur Android Chrome, `showDirectoryPicker` n'est pas disponible. L'application utilise automatiquement un sélecteur de fichiers alternatif (`<input webkitdirectory>`) pour toutes les actions de sélection de dossier.

> **Limitation Android** : les handles de dossiers ne peuvent pas être persistés entre sessions. Il faut re-sélectionner le dossier racine à chaque rechargement de page.

---

## Noms de fichiers avec accents

Les chemins de fichiers contenant des caractères accentués sont normalisés automatiquement en Unicode NFC, aussi bien à l'import qu'à la lecture. Cela garantit la cohérence entre macOS et Android.

---

## Personnalisation

**⚙** ouvre le panneau de réglages :

### Couleurs
Toutes les couleurs de l'interface sont personnalisables. Le thème est sauvegardé dans le navigateur.

### Police d'affichage
5 polices optimisées pour tablette 11" :

| Police | Caractère |
|--------|-----------|
| **Inter** | Référence UI moderne, lisible à toutes tailles *(défaut)* |
| **DM Sans** | Géométrique, aérée |
| **Nunito** | Arrondie, douce sur tactile |
| **Roboto** | Standard Android/Chrome |
| **Source Sans** | Conçue spécifiquement pour les écrans |

---

## Journal des erreurs (🪲)

Le bouton 🪲 s'entoure d'un contour rouge quand une erreur est détectée.

- Niveaux : **ERROR** (rouge) · **WARN** (orange) · **INFO** (gris)
- **↺ Actualiser** · **🗑 Vider** efface le journal
- Journal en mémoire — perdu au rechargement

---

## Gestion des spectacles

### Sauvegarder
**🎭 Spectacle → 💾 Sauvegarder** — première fois : choisir l'emplacement du `.json`.

### Charger
**🎭 Spectacle → 📂 Charger** → sélectionner un fichier `.json`.

### Nouveau
**🎭 Spectacle → ✦ Nouveau** remet l'application à zéro.

---

## Conseils pour la représentation

- Utiliser Chrome en **mode plein écran** (F11 desktop / "Ajouter à l'écran d'accueil" Android)
- L'écran reste allumé tant qu'un son est joué (Wake Lock automatique)
- **🔉 Sourdine** : baisser discrètement sans stopper la lecture
- **🔇 Silence** : couper instantanément
- Les playlists sont streamées depuis le disque — latence ≈ 300 ms au démarrage, pas d'impact mémoire

---

## Compatibilité navigateurs

| Navigateur | Support |
|------------|---------|
| Chrome Android 86+ | ✅ Complet |
| Chrome desktop | ✅ Complet |
| Safari iOS | ⚠ Partiel (File System Access non supporté) |
| Firefox | ⚠ Partiel |

---

## Données et vie privée

- Aucune donnée envoyée sur internet (sauf chargement des polices Google Fonts)
- Projets sauvegardés en fichiers `.json` sur votre disque
- Thème et police sauvegardés en `localStorage`

---

## Changelog

### v1.4.0 (2026-05-07)

#### Architecture
- **Modèle audio unifié** : un seul dossier racine `PLAYLISTS/` couvre séquence et playlists. Un seul scan au démarrage, un seul index (`_globalFileMap`) partagé par toute l'application. Fini les handles multiples et les demandes de permission par dossier.
- **Résolution de fichiers robuste** : recherche d'abord par chemin exact, puis par nom de fichier seul (migration automatique des anciens projets qui stockaient des chemins sans sous-dossier).
- **Format JSON v1.4** : champ `folderName` remplace `audioRoot` (rétrocompatibilité assurée).

#### Nouvelles fonctionnalités
- **Importer un morceau de playlist dans la séquence** : bouton **←** en mode édition sur chaque carte de morceau — insère le morceau dans la séquence après le cue sélectionné en dernier, buffer audio chargé immédiatement.
- **Numéro de version** affiché dans le titre de l'application.

#### Corrections
- **`openFolderImport`** : utilise `isSameEntry()` pour détecter si le dossier choisi est la racine déjà enregistrée, sans ambiguïté sur le nom du dossier.
- **Message d'erreur clair** si le dossier racine n'a pas encore été sélectionné lors d'une tentative de lecture.
- Suppression du code mort `_pendingImportHandle`.

---

### v1.3.1 (2026-05-05)
- **Playlists bloquées au chargement** : bouton 🔒 dans le bandeau orange pour accorder la permission Chrome et charger les fichiers.

### v1.3.0 (2026-05-05)
- Compatibilité Android, demande de dossiers au chargement, rescan automatique, normalisation Unicode NFC, suppression des sons libres.

### v1.2.0 (2026-05-04)
- Playlists libres, album art, choix de police, bouton Stop par cue.

### v1.1.0
- Colonne notes, deux dossiers audio, journal d'erreurs.

### v1.0.0
- Version initiale.
