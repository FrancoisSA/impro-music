# Spécification — Application de régie son pour spectacle
**Version** : 1.0 — 2026-05-01  
**Contexte** : Application statique HTML/CSS/JavaScript, sans serveur, tournant sur Chrome Android (tablette)

---

## 1. Analyse du marché — Applications existantes

### Référence professionnelle

| Application | Plateforme | Prix | Points forts |
|-------------|-----------|------|-------------|
| **QLab** | macOS uniquement | Freemium (~399$/an pro) | Standard de l'industrie, cues chainables, OSC, vidéo |
| **Show Cue System** | Windows | Payant | Cues ordonnés, volume/pan par piste, sélection haut-parleurs |
| **SoundQ Studio** | Navigateur (offline-ready) | Gratuit (freemium) | Cues embarqués dans le script, cross-platform, offline |
| **SoundShow** | Win/Mac/Linux | Freemium | Soundboard théâtre, pistes simultanées |
| **Linux Show Player (LiSP)** | Linux | Gratuit open-source | Cue player complet, sans GUI moderne |
| **Cue Player Premium** | Windows | Payant | Fades, cross-fades, delays, autostarts |

### Applications Android spécialisées

| Application | Plateforme | Points forts |
|-------------|-----------|-------------|
| **Audio Cues** (Radial Theater) | Android | Cues simples, pistes d'accompagnement, effets, mise à jour fév. 2026 |
| **Impro Sound System** | Android (gratuit) | Interface onglets/dossiers, boutons sons, lecture en boucle |
| **Séquenceur Histoires** (Odéon) | Web/mobile | Créé par le Théâtre National de l'Odéon, usage pro depuis 1998 |

---

## 2. Fonctionnalités les plus répandues

### 2.1 Gestion des cues (incontournable)
- Liste ordonnée de cues numérotés (1, 2, 3... ou 1.0, 1.5...)
- Déclenchement manuel : bouton **GO** unique (barre espace ou tap)
- Navigation : précédent / suivant / aller à un cue précis
- Nommage de chaque cue (ex. : "Entrée personnage A", "Fin acte 1")
- Indicateur du cue **en cours** et du cue **suivant** bien visible

### 2.2 Lecture audio
- Lecture de fichiers MP3, WAV, OGG, M4A
- Volume individuel par cue (0–100%)
- Fade in / fade out configurable (durée en secondes)
- Cross-fade entre deux cues
- Lecture en boucle (loop) par cue
- Stop immédiat / stop avec fade out

### 2.3 Organisation des sons
- Import de fichiers audio locaux (depuis le stockage de la tablette)
- Regroupement par catégories / scènes / actes
- Recherche par nom
- Prévisualisation avant déclenchement ("test")

### 2.4 Interface régisseur
- Mode **plein écran** (éviter les interruptions)
- Grande lisibilité (contraste élevé, gros boutons) pour conditions de lumière faible
- Mode **nuit** (thème sombre)
- Affichage du titre, durée et progression de la piste en cours
- Barre de progression visuelle

### 2.5 Contrôle pendant la représentation
- Pause / reprise de la piste en cours
- Ajustement du volume master en temps réel
- Sauter à un cue spécifique (mode urgence)
- Historique des cues joués

### 2.6 Sauvegarde / chargement de projet
- Sauvegarde du projet (liste de cues + configurations) en local
- Export/import du projet (fichier JSON)
- Plusieurs projets/spectacles

### 2.7 Fonctions avancées (présentes dans les outils pro)
- Déclenchement automatique (auto-follow : enchaîner après N secondes)
- Routage audio multi-canaux (selon la régie)
- Contrôle OSC/MIDI (synchronisation avec éclairagiste)
- Notes de mise en scène par cue

---

## 3. Analyse de faisabilité — Application statique HTML/CSS/JS sur Chrome Android

### 3.1 Architecture proposée

```
index.html          — coque principale (PWA)
css/
  app.css           — styles, thème sombre, responsive tablette
js/
  app.js            — orchestrateur principal
  cueList.js        — gestion de la liste de cues
  audioEngine.js    — moteur audio (Web Audio API)
  projectStore.js   — sauvegarde/chargement (IndexedDB + JSON)
  ui.js             — gestion de l'interface
manifest.json       — PWA manifest (icône, fullscreen)
service-worker.js   — cache offline
```

### 3.2 Technologies clés — Faisabilité

#### Web Audio API ✅ Supportée sur Chrome Android
- Lecture multi-pistes simultanées via `AudioContext`
- Volume par piste : `GainNode`
- Fade in/out : `GainNode.linearRampToValueAtTime()`
- Analyse de niveau : `AnalyserNode`
- **Contrainte** : Chrome Android exige un geste utilisateur avant le premier `AudioContext.resume()` — gérable avec un bouton "Démarrer la session"

#### File System Access API ✅ Chrome Android 86+
- Import de fichiers audio locaux directement depuis la tablette
- `showOpenFilePicker()` pour sélectionner les fichiers
- **Alternative si non supporté** : `<input type="file" multiple accept="audio/*">`

#### IndexedDB ✅ Supportée partout
- Stockage persistant des projets, configurations et **fichiers audio** (en Blob)
- Capacité : plusieurs Go selon l'espace disque disponible
- Pas besoin de serveur

#### PWA / Service Worker ✅
- Mode offline complet
- Ajout à l'écran d'accueil (icône, lancement plein écran)
- Évite le navigateur Chrome qui se ferme accidentellement
- Cache des assets statiques

#### Web MIDI API ⚠️ Partielle sur Android
- Non supportée nativement sur Chrome Android sans flag
- Contournement : application tierce MIDI over WiFi (hors scope v1)

### 3.3 Limites identifiées et solutions

| Limite | Impact | Solution |
|--------|--------|----------|
| Geste utilisateur requis pour AudioContext | Bloque le premier son | Bouton "Démarrer" affiché à l'ouverture |
| Latence audio Android : 12–150ms selon tablette | Décalage léger possible | Pré-charger les pistes (`AudioBuffer`), éviter `<audio>` |
| Pas d'accès système au volume | Pas de contrôle du volume système | Volume master via GainNode |
| Verrouillage d'écran suspend les sons | Spectacle interrompu | Wake Lock API (`navigator.wakeLock`) |
| Stockage limité si quota dépassé | Projets lourds refusés | Alerter l'utilisateur, proposer fichiers externes |
| File System Access API non dispo sur certains Android | Impossible d'ouvrir fichiers | Fallback `<input type="file">` |

### 3.4 Wake Lock API ✅ Chrome Android 84+

```javascript
// Empêche la tablette de se mettre en veille pendant la représentation
const wakeLock = await navigator.wakeLock.request('screen');
```

### 3.5 Performances attendues

- **Latence de déclenchement** : < 30ms sur tablette Android récente (pistes pré-chargées en AudioBuffer)
- **Nombre de pistes simultanées** : 4–8 pistes sans problème sur tablette mid-range
- **Stockage projet** : 500 Mo typique pour un spectacle (musiques + effets) — bien dans les limites IndexedDB
- **Format recommandé** : MP3 128–192kbps (bon compromis taille/qualité) ou OGG pour meilleure compatibilité

### 3.6 Ce qui n'est PAS faisable sans serveur

- Synchronisation multi-postes en temps réel (ex. régie son + éclairagiste sur tablette séparée) → nécessite WebRTC ou WebSocket
- Streaming de fichiers lourds depuis un NAS → nécessite un serveur
- OSC réseau vers une console → nécessite un bridge serveur

---

## 4. Périmètre recommandé pour la v1

### Inclus (faisable 100% statique)
- [x] Liste de cues ordonnée avec bouton GO
- [x] Import audio local (MP3/WAV/OGG)
- [x] Volume par cue + fade in/out
- [x] Lecture en boucle par cue
- [x] Stop avec fade
- [x] Thème sombre, interface tablette optimisée
- [x] Sauvegarde projet en IndexedDB
- [x] Export/import JSON du projet
- [x] Mode plein écran + Wake Lock
- [x] Prévisualisation des sons
- [x] Indicateur cue en cours / cue suivant

### Reporté v2
- [ ] Auto-follow (enchaînement automatique)
- [ ] Plusieurs sorties audio (multi-canal)
- [ ] Synchronisation OSC/MIDI
- [ ] Collaboration multi-postes

---

## 5. Recommandation technique

Une application **100% statique** (zéro serveur) est **pleinement faisable** pour le cas d'usage régie son spectacle sur tablette Android Chrome, en utilisant :

- **Web Audio API** pour le moteur audio précis et sans latence
- **IndexedDB** pour le stockage persistant des projets et fichiers
- **PWA** (manifest + service worker) pour le mode offline et plein écran
- **Wake Lock API** pour maintenir l'écran actif
- **Fallback `<input type="file">`** pour l'import audio si File System Access non disponible

L'application peut être livrée comme un simple dossier de fichiers statiques, ouvert directement dans Chrome Android via `file://` ou hébergé gratuitement sur GitHub Pages / Netlify.

---

## Sources et références

- [QLab Alternatives — AlternativeTo](https://alternativeto.net/software/qlab/)
- [Theatrecrafts — Sound Playback Software](http://theatrecrafts.com/pages/home/topics/sound/sound-playback-software/)
- [SoundQ Studio — Browser-based QLab alternative](https://soundq.studio/)
- [Audio Cues — Google Play](https://play.google.com/store/apps/details?id=org.radialtheater.audiocues&hl=en_US)
- [Impro Sound System (blog)](https://improetc.wordpress.com/2015/12/04/impro-sound-system-lappli-qui-simplifie-la-regie-son/)
- [3 apps pour spectacle — Dramaction](https://www.dramaction.qc.ca/fr/3-apps-pour-gerer-la-musique-les-effets-speciaux-en-spectacle/)
- [Web Audio API — MDN](https://developer.mozilla.org/en-US/docs/Web/API/Web_Audio_API)
- [Web Audio FAQ — Chrome Developers](https://developer.chrome.com/blog/web-audio-faq)
- [Web Audio API Best Practices — MDN](https://developer.mozilla.org/en-US/docs/Web/API/Web_Audio_API/Best_practices)
