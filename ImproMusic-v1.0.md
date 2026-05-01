# ImproMusic — Manuel utilisateur v1.0
**Date** : 2026-05-01  
**Version** : 1.0.0  
**Plateforme** : Chrome Android (tablette) — fonctionne aussi sur Chrome desktop

---

## Présentation

ImproMusic est une régie son pour spectacle vivant. Elle fonctionne **sans serveur**, directement depuis le fichier `impromusic.html` ouvert dans Chrome. Les sons sont stockés dans le navigateur (IndexedDB) et rechargés automatiquement à chaque ouverture.

---

## Démarrage rapide

1. Ouvrir `impromusic.html` dans Chrome (double-clic ou glisser dans Chrome)
2. Importer des sons via **📂 Dossier**
3. Choisir la destination : **Séquence** ou **Sons libres**
4. Sauvegarder le spectacle via **🎭 Spectacles → 💾 Sauver**
5. Lors des représentations suivantes, le dernier spectacle se recharge automatiquement

---

## Interface

### En-tête
| Élément | Rôle |
|---------|------|
| **🎭 Spectacles** | Créer, charger ou supprimer un spectacle |
| **📂 Dossier** | Importer un dossier de fichiers audio |
| **+Seq** | Ajouter un cue manuellement dans la séquence |
| **+Pad** | Ajouter un son libre manuellement |
| **⚙** | Panneau de personnalisation des couleurs |
| **🔊 Volume** | Volume master global (affecte tous les sons) |

### Bandeau "En cours" (barre centrale)
Affiche le son en cours de lecture et les commandes de transport.

| Bouton | Action |
|--------|--------|
| **▶** | Lecture (si rien ne joue) |
| **⏸** | Pause / Reprise |
| **■** | Stop immédiat |
| **🔉** | Sourdine : cycle −50% → −75% → −90% → Off |
| **🔇** | Silence total (volume à 0) |
| **↘** | Fade out en 2 secondes puis stop |
| **⏭** | Jouer le cue suivant dans la séquence |

---

## Séquence (colonne gauche)

La séquence est une liste ordonnée de cues, jouée dans l'ordre pendant le spectacle.

### États des cues
- **Contour orange** = en cours de lecture
- **Contour vert** = cue suivant prêt
- **Contour bleu** = en pause
- **Opacité réduite** = déjà joué
- **⊙ vert** = fichier audio chargé · **○ gris** = pas de fichier

### Jouer un cue
- **Tap sur la carte** = jouer (ou mettre en pause si en cours)
- **▶** sur la carte = lecture directe
- **⏸** sur la carte = pause / reprise
- **■** sur la carte = stop (remet le cue en "en attente")
- **»** sur la carte = marquer comme "cue suivant"

### Boucle
Le bouton **🔁** sur chaque carte active/désactive la lecture en boucle sans ouvrir la modale.

### Sections
En mode édition, cliquer **+ Section** pour insérer un séparateur nommé.  
Hors édition, taper sur le séparateur réduit/développe la section.

---

## Sons libres (colonne droite)

Boutons déclenchables à tout moment, indépendants de la séquence.  
Un tap joue le son ; un second tap l'arrête.  
Les sons libres sont regroupés par type : Effets, Musiques, Ambiances, Boucles.

---

## Importer des sons

### Via 📂 Dossier
1. Cliquer **📂 Dossier**
2. Sélectionner un dossier sur la tablette
3. Cocher les fichiers à importer
4. Choisir la destination : **Séquence** ou **Sons libres**
5. Cliquer **Importer**

Les fichiers sont stockés dans le navigateur. Ils ne disparaissent pas entre les sessions.

**Formats supportés** : MP3, WAV, OGG, M4A, AAC

### Manuellement (+Seq / +Pad)
Permet d'ajouter un son avec des réglages précis :
- Nom, type, volume (%)
- Fade in / fade out (secondes)
- Démarrer à (mm:ss) — commence la lecture à une position précise
- Finir à (mm:ss ou −30) — arrête avant la fin réelle du fichier
- Boucle
- Notes de mise en scène

---

## Paramètres d'un cue

| Paramètre | Description |
|-----------|-------------|
| **Volume** | Volume individuel du cue (0–100%) |
| **Fade in** | Montée progressive au démarrage (secondes) |
| **Fade out** | Descente progressive à l'arrêt (secondes) |
| **Démarrer à** | Position de départ dans le fichier (ex: `1:30`) |
| **Finir à** | Position de fin (ex: `3:00`) ou offset depuis la fin (ex: `-30` = 30s avant la fin) |
| **Boucle** | Rejoue automatiquement en fin de piste |
| **Notes** | Mémo affiché dans le bandeau "En cours" |

---

## Gestion des spectacles

### Sauvegarder
1. Cliquer **🎭 Spectacles**
2. Saisir un nom
3. Cliquer **💾 Sauver**

La sauvegarde automatique est active : toute modification (ajout, déplacement, loop…) est enregistrée instantanément (indicateur **✓** après le nom).

### Charger
Cliquer **🎭 Spectacles** puis **📂 Charger** sur le spectacle souhaité.

### Fichiers audio manquants
Si des sons ne sont pas retrouvés au chargement, un bandeau rouge s'affiche avec le bouton **📂 Charger le dossier**. Pointer vers le dossier contenant les fichiers audio pour les réinjecter.

---

## Mode édition

Activer via le bouton **✏ Éditer** (colonne gauche).

En mode édition :
- **↑ ↓** réordonnent les cues
- **✏** ouvre la modale de modification
- **👁** masque/affiche un cue dans la séquence
- **✕** supprime (avec confirmation)
- **+ Section** ajoute un séparateur de section

---

## Personnalisation du thème

Cliquer **⚙** pour ouvrir le panneau de couleurs.  
Toutes les couleurs (fond, texte, accent, types de sons) sont personnalisables.  
Le thème est sauvegardé dans le navigateur et restauré automatiquement.  
**↺ Réinitialiser** remet les couleurs par défaut.

---

## Conseils pour la représentation

- Utiliser Chrome en **mode plein écran** (F11 sur desktop, ou "Ajouter à l'écran d'accueil" sur Android)
- L'écran reste allumé tant qu'un son est joué (Wake Lock automatique)
- Le **volume master** dans l'en-tête permet d'ajuster rapidement le niveau global sans toucher aux réglages individuels
- La **sourdine** (🔉) permet de baisser discrètement le volume pour parler à quelqu'un
- Le **silence** (🔇) coupe instantanément tout son sans stopper la lecture (reprend au niveau normal en retappant)

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

- Aucune donnée n'est envoyée sur internet
- Les fichiers audio sont stockés localement dans le navigateur (IndexedDB)
- Les projets sont sauvegardés localement (IndexedDB)
- Le thème est sauvegardé localement (localStorage)
- Pour effacer toutes les données : vider le cache du navigateur pour ce fichier
