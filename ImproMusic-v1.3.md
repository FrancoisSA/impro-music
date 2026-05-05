# ImproMusic — Manuel utilisateur v1.3
**Date** : 2026-05-05
**Version** : 1.3.1
**Plateforme** : Chrome Android (tablette) — fonctionne aussi sur Chrome desktop

---

## Présentation

ImproMusic est une régie son pour spectacle vivant. Elle fonctionne **sans serveur**, directement depuis le fichier `impromusic.html` ouvert dans Chrome. Les projets sont sauvegardés en fichiers `.json` sur votre disque.

---

## Démarrage rapide

1. Ouvrir `impromusic.html` dans Chrome
2. Charger un projet via **🎭 Spectacle → 📂 Charger**
3. Si des sons ou des dossiers playlist manquent, un bandeau orange apparaît — cliquer les boutons **📁** pour lier les dossiers
4. La prochaine ouverture retrouve les dossiers automatiquement (1 clic de permission Chrome)

---

## Interface

### En-tête
| Élément | Rôle |
|---------|------|
| **🎭 Spectacle** | Créer, charger ou sauvegarder un spectacle |
| **🪲** | Journal des erreurs (contour rouge = erreur présente) |
| **⚙** | Panneau Couleurs, thème et **police** |
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

La colonne droite accueille des **playlists** : listes de morceaux streamés depuis un dossier audio, **sans chargement en RAM**. Idéal pour une bibliothèque musicale entière.

### Ajouter une playlist
1. Cliquer **✏ Éditer** dans l'en-tête Playlists
2. Cliquer **＋ Ajouter une playlist**
3. Sélectionner un dossier — tous les fichiers audio sont importés et triés alphabétiquement
4. Les vignettes d'album art (tags ID3) s'extraient automatiquement en arrière-plan

### Lier un dossier à une playlist existante
Au chargement du spectacle, si des playlists n'ont pas de dossier lié, un **bandeau orange** liste les boutons **📁 NomPlaylist**. Cliquer chaque bouton pour sélectionner le dossier correspondant. Cette association est mémorisée pour les sessions suivantes.

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
- **Rescan automatique au démarrage** si le dossier est déjà lié et accessible

### Redimensionner
Glisser la barre verticale entre la séquence et les playlists.

### Persistance
Les playlists sont sauvegardées dans le fichier `.json` du spectacle (noms et réglages). Les dossiers audio sont retrouvés automatiquement à la session suivante si la permission Chrome est accordée.

---

## Gestion des dossiers audio

### Séquence
Au chargement, si des sons de séquence manquent, le bandeau affiche **📁 Musiques** → sélectionner le dossier contenant les MP3.

### Sessions suivantes
Chrome redemande la permission (1 clic). Pour ne plus être redemandé, choisir **"Autoriser à chaque visite"** dans la popup Chrome.

---

## Compatibilité tablette Android *(amélioré en v1.3)*

Sur Android Chrome, `showDirectoryPicker` n'est pas disponible. L'application utilise automatiquement un sélecteur de fichiers alternatif (`<input webkitdirectory>`) pour :
- Lier ou relancer un dossier de séquence
- Ajouter une nouvelle playlist
- Rescanner une playlist existante
- Lier un dossier manquant depuis le bandeau

> **Limitation Android** : les handles de dossiers ne peuvent pas être persistés entre sessions. Il faut re-sélectionner les dossiers à chaque rechargement de page.

---

## Noms de fichiers avec accents

Les chemins de fichiers contenant des caractères accentués (é, è, ü, ñ…) sont normalisés automatiquement en Unicode NFC, aussi bien à l'import qu'à la lecture. Cela garantit la cohérence entre macOS (qui retourne parfois NFD) et Android.

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

### v1.3.1 (2026-05-05)

#### Corrections
- **Playlists bloquées au chargement** : quand Chrome a besoin d'une confirmation de permission sur un dossier playlist déjà connu, l'application affichait silencieusement les morceaux sans pouvoir les jouer. Désormais un bouton **🔒 NomPlaylist** apparaît dans le bandeau orange ; un clic (geste utilisateur requis par Chrome) accorde la permission et charge les fichiers immédiatement.

---

### v1.3.0 (2026-05-05)

#### Nouvelles fonctionnalités
- **Compatibilité Android** : toutes les actions de sélection de dossier (séquence, playlists, rescan) fonctionnent sur Android Chrome via `<input webkitdirectory>`
- **Demande de dossiers au chargement** : si des playlists n'ont pas de dossier lié, le bandeau orange apparaît immédiatement avec un bouton par playlist — plus besoin de cliquer sur un morceau pour déclencher la demande
- **Rescan automatique au démarrage** : les playlists dont le dossier est déjà accessible sont rescannées silencieusement (nouveaux fichiers intégrés, supprimés retirés)
- **Noms de fichiers accentués** : normalisation Unicode NFC systématique sur Android (`webkitRelativePath`)
- **Logs détaillés de diagnostic** : `_resolvePlaylistFile` log chaque étape (handle, permission, scan, candidats) dans le journal 🪲

#### Suppressions
- **Sons libres (pads)** supprimés : colonne, styles, fonctions `triggerPad`, `renderPads`, `guessEmoji`, picker emoji — fonctionnalité retirée pour simplifier l'interface
- Import de dossier : destination unique (séquence), menu de choix supprimé

#### Format JSON
- Version bumped `1.2` → `1.3`
- Clés `pads` et `audioRootPads` supprimées du payload (rétrocompatibilité lecture maintenue)

---

### v1.2.0 (2026-05-04)
- Playlists libres, album art, choix de police, bouton Stop par cue

### v1.1.0
- Colonne notes, deux dossiers audio, journal d'erreurs

### v1.0.0
- Version initiale
