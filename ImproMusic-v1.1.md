# ImproMusic — Manuel utilisateur v1.1
**Date** : 2026-05-03
**Version** : 1.1.0
**Plateforme** : Chrome Android (tablette) — fonctionne aussi sur Chrome desktop

---

## Présentation

ImproMusic est une régie son pour spectacle vivant. Elle fonctionne **sans serveur**, directement depuis le fichier `impromusic.html` ouvert dans Chrome. Les sons sont stockés dans le navigateur (IndexedDB) et rechargés automatiquement à chaque ouverture.

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
| **⚙** | Panneau de personnalisation des couleurs |
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

La modale regroupe tous les paramètres sur une seule page :

| Zone | Paramètres |
|------|-----------|
| **En-tête** | Nom · Type (Musique / Effet / Ambiance / Boucle) |
| **Volume** | Slider 0–100% avec valeur en temps réel |
| **↗↘ Timing** | Fade in · Fade out · Boucle |
| **↦↤ Plage** | Débuter à (mm:ss) · Finir à (mm:ss ou -30s) |
| **Fichier audio** | Bouton 📂 Choisir + nom du fichier sélectionné |
| **Notes** | Zone de texte libre (plusieurs lignes) |

---

## Gestion des dossiers audio

Les fichiers musicaux de la **séquence** et les **sons libres** peuvent être dans des dossiers différents.

### Première utilisation
1. Charger un spectacle → bandeau rouge si des sons manquent
2. Cliquer **📁 Musiques** → sélectionner le dossier contenant les MP3 de séquence
3. Cliquer **📁 Sons libres** → sélectionner le dossier des sons libres
4. Sauvegarder le projet pour mémoriser les noms de dossiers dans le JSON

### Sessions suivantes
Chrome redemande la permission d'accès (1 clic). Si le dossier a le même nom que celui enregistré dans le JSON, les sons sont rechargés automatiquement.

### Sous-dossiers
Les dossiers sont scannés récursivement. Les `filepath` dans le JSON incluent le chemin relatif : `"PL-RECONSTITUTION/son.mp3"`.

### Fichier JSON du spectacle
```json
{
  "audioRootSeq":  "PL-RECONSTITUTION",
  "audioRootPads": "sounds"
}
```

---

## Journal des erreurs (🪲)

Le bouton 🪲 dans l'en-tête s'entoure d'un contour rouge quand une erreur est détectée (fichier introuvable, erreur d'import…).

Cliquer 🪲 pour ouvrir le journal :
- Entrées du plus récent au plus ancien
- Niveaux : **ERROR** (rouge) · **WARN** (orange) · **INFO** (gris)
- **↺ Actualiser** relit les entrées · **🗑 Vider** efface le journal

Le journal est en mémoire — il est perdu au rechargement de la page.

---

## Gestion des spectacles

### Sauvegarder
1. **🎭 Spectacle → 💾 Sauvegarder**
2. Première fois : choisir l'emplacement du fichier `.json`
3. Fois suivantes : écrit directement dans le fichier ouvert

L'indicateur **✓** après le nom du projet confirme la sauvegarde.

### Charger
**🎭 Spectacle → 📂 Charger** puis sélectionner un fichier `.json`.

### Nouveau
**🎭 Spectacle → ✦ Nouveau** remet l'application à zéro.

### Importer un dossier audio
**🎭 Spectacle → 🎵 Importer un dossier audio** pour ajouter des sons en séquence ou en sons libres.

---

## Personnalisation du thème

**⚙** ouvre le panneau de couleurs. Toutes les couleurs sont personnalisables. Le thème est sauvegardé dans le navigateur.

---

## Conseils pour la représentation

- Utiliser Chrome en **mode plein écran** (F11 desktop / "Ajouter à l'écran d'accueil" Android)
- L'écran reste allumé tant qu'un son est joué (Wake Lock automatique)
- **🔉 Sourdine** : baisser discrètement sans stopper la lecture
- **🔇 Silence** : couper instantanément, reprendre au niveau normal en retappant

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

- Aucune donnée envoyée sur internet
- Fichiers audio stockés localement (IndexedDB)
- Projets sauvegardés en fichiers `.json` sur votre disque
- Thème sauvegardé en `localStorage`

---

## Changelog v1.1.0 (2026-05-03)

- **Colonne Notes** : notes de mise en scène alignées sur chaque cue, colonne redimensionnable par glissement
- **Deux dossiers audio** : séquence et sons libres peuvent être dans des dossiers distincts (`audioRootSeq` / `audioRootPads`)
- **Journal des erreurs** : bouton 🪲 avec badge rouge, liste horodatée ERROR/WARN/INFO
- **Modale redessinée** : slider volume, blocs Timing/Plage, textarea notes, type inline
- **Bouton ＋ en mode édition** : ajouter un cue directement depuis la colonne séquence
- **Fix NFD/NFC** : noms de fichiers accentués correctement reconnus sur macOS
- **Fix `_prevState`** : champ interne non sauvegardé dans le JSON
- **Fix `handleGo`** : "cue suivant" ne se pose plus sur une section
- **Fix suppression** : stopper le son avant de supprimer un cue en cours de lecture
