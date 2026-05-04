# ImproMusic — Manuel utilisateur v1.2
**Date** : 2026-05-04
**Version** : 1.2.0
**Plateforme** : Chrome Android (tablette) — fonctionne aussi sur Chrome desktop

---

## Présentation

ImproMusic est une régie son pour spectacle vivant. Elle fonctionne **sans serveur**, directement depuis le fichier `impromusic.html` ouvert dans Chrome. Les projets sont sauvegardés en fichiers `.json` sur votre disque.

---

## Démarrage rapide

1. Ouvrir `impromusic.html` dans Chrome
2. Charger un projet via **🎭 Spectacle → 📂 Charger**
3. Si les sons sont manquants, cliquer **📁 Musiques** et/ou **📁 Sons libres** dans le bandeau rouge
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
- **■** en haut à gauche de la carte = stopper uniquement ce cue
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

## Playlists libres *(nouveau en v1.2)*

La colonne droite accueille des **playlists** : listes de morceaux streamés depuis un dossier audio, **sans chargement en RAM**. Idéal pour une bibliothèque musicale entière.

### Ajouter une playlist
1. Cliquer **✏ Éditer** dans l'en-tête Playlists
2. Cliquer **＋ Ajouter une playlist**
3. Sélectionner un dossier — tous les fichiers audio sont importés et triés alphabétiquement
4. Les vignettes d'album art (tags ID3) s'extraient automatiquement en arrière-plan

### Lire un morceau
- **Tap** sur la carte ou **▶** pour lire
- **■** pour stopper
- **🔁** pour activer la boucle

### Organisation
- **▾ / ▸** (chevron gauche de l'en-tête) : tout replier / déplier
- Chaque playlist dispose de son propre chevron de repli
- En mode édition : **↑ ↓** réordonnent les playlists, **↺** rescanne le dossier (ajoute les nouveaux fichiers, retire les disparus, conserve les réglages), **✕** supprime

### Rescan du dossier
Cliquer **↺** en mode édition pour mettre à jour une playlist :
- Nouveaux fichiers ajoutés avec réglages par défaut
- Fichiers supprimés retirés (arrêt automatique si en cours)
- Réglages des morceaux existants conservés
- Un toast confirme : `+2 ajoutés, 1 supprimé`

### Redimensionner
Glisser la barre verticale entre la séquence et les playlists.

### Persistance
Les playlists sont sauvegardées dans le fichier `.json` du spectacle (noms et réglages). Les dossiers audio sont retrouvés automatiquement à la session suivante si la permission Chrome est accordée.

---

## Gestion des dossiers audio (séquence)

Les fichiers de la **séquence** et les **sons libres** peuvent être dans des dossiers différents.

### Première utilisation
1. Charger un spectacle → bandeau rouge si des sons manquent
2. Cliquer **📁 Musiques** → sélectionner le dossier contenant les MP3 de séquence
3. Cliquer **📁 Sons libres** → sélectionner le dossier des sons libres
4. Sauvegarder le projet pour mémoriser les noms de dossiers dans le JSON

### Sessions suivantes
Chrome redemande la permission (1 clic). Si le dossier a le même nom que celui enregistré dans le JSON, les sons sont rechargés automatiquement.

---

## Personnalisation *(étendu en v1.2)*

**⚙** ouvre le panneau de réglages :

### Couleurs
Toutes les couleurs de l'interface sont personnalisables (fonds, texte, accent, boutons, types de sons). Le thème est sauvegardé dans le navigateur.

### Police d'affichage *(nouveau)*
5 polices optimisées pour tablette 11" :

| Police | Caractère |
|--------|-----------|
| **Inter** | Référence UI moderne, lisible à toutes tailles *(défaut)* |
| **DM Sans** | Géométrique, aérée |
| **Nunito** | Arrondie, douce sur tactile |
| **Roboto** | Standard Android/Chrome |
| **Source Sans** | Conçue spécifiquement pour les écrans |

La sélection est mémorisée entre les sessions. "↺ Réinitialiser" remet Inter.

> Nécessite une connexion internet au premier chargement pour télécharger la police.

---

## Journal des erreurs (🪲)

Le bouton 🪲 s'entoure d'un contour rouge quand une erreur est détectée.

- Niveaux : **ERROR** (rouge) · **WARN** (orange) · **INFO** (gris)
- **↺ Actualiser** · **🗑 Vider** efface le journal
- Journal en mémoire — perdu au rechargement

---

## Gestion des spectacles

### Sauvegarder
**🎭 Spectacle → 💾 Sauvegarder** — première fois : choisir l'emplacement du `.json`. L'indicateur **✓** confirme la sauvegarde.

### Charger
**🎭 Spectacle → 📂 Charger** → sélectionner un fichier `.json`.

### Nouveau
**🎭 Spectacle → ✦ Nouveau** remet l'application à zéro.

---

## Conseils pour la représentation

- Utiliser Chrome en **mode plein écran** (F11 desktop / "Ajouter à l'écran d'accueil" Android)
- L'écran reste allumé tant qu'un son est joué (Wake Lock automatique)
- **🔉 Sourdine** : baisser discrètement sans stopper la lecture
- **🔇 Silence** : couper instantanément, reprendre au niveau normal en retappant
- Les playlists sont streamées depuis le disque — latence ≈ 300 ms au démarrage, pas d'impact mémoire

---

## Compatibilité

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

## Changelog v1.2.0 (2026-05-04)

### Nouvelles fonctionnalités
- **Playlists libres** : 3e colonne avec playlists audio streamées depuis un dossier (zéro RAM), grille 2 colonnes, vignettes album art extraites des tags ID3v2
- **Album art** : extraction automatique au chargement de la playlist et au lancement (si permission déjà accordée)
- **Rescan de dossier** : bouton ↺ pour mettre à jour une playlist sans perdre les réglages
- **Chevron global** : replier/déplier toutes les playlists en un clic
- **Choix de police** : 5 polices optimisées tablette dans le panneau ⚙ (Inter, DM Sans, Nunito, Roboto, Source Sans 3)
- **Bouton Stop par cue** : stopper uniquement un cue spécifique sans affecter les autres

### Améliorations
- Titres de playlists en couleur accent (orange), chevrons plus grands
- Tri alphabétique automatique des morceaux dans les playlists
- Vignettes album art carrées à gauche des cartes (layout row)
- Colonne playlists redimensionnable par glissement

### Corrections
- XSS : `nextCue.name` désormais échappé dans le bandeau "En cours"
- `endAt` correctement appliqué dans le lecteur playlist (arrêt dur à la position définie)
- `isPaused()` corrigé (faux négatif à position 0)
- Suppression du double `playlistDirHandles.set()` dans `addPlaylist`
- `engine.loadFile` retiré de l'édition de morceau playlist (pas d'AudioBuffer pour les playlists)
