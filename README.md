# Drift King (Col du Drift)

Jeu de drift 3D sur une route de montagne au coucher du soleil, jouable dans le navigateur.

**▶ Démo en ligne : [https://yoannservices.github.io/drift-king/](https://yoannservices.github.io/drift-king/)**

## Fonctionnalités

- Entrez en virage avec de la vitesse et tenez la glisse le plus longtemps possible
- Score et combo, perdu si vous touchez la glissière
- Meilleur score enregistré (`localStorage`)

## Commandes

| Touche | Action |
|---|---|
| ↑ / Z / W | Accélérer |
| ↓ / S | Freiner |
| ← → / Q D | Tourner |
| Espace | Frein à main |
| R | Replacer la voiture |
| C | Changer de vue (poursuite, éloignée, capot) |
| Clic + glisser | Tourner la caméra autour de la voiture |

## Lancer en local

Aucune installation : ouvrez `index.html` dans un navigateur, ou servez le dossier :

```bash
python -m http.server 8000
```

puis allez sur http://localhost:8000 (dans le dossier `web/` de Mes Projets : http://localhost:8000/loisirs/drift-king/).

## Structure

- `index.html`, `style.css`
- `js/main.js` : le jeu

## Technologies

HTML, CSS et JavaScript ; rendu 3D avec [Three.js](https://threejs.org/) r186 (chargé depuis un CDN par `assets/three-compat.js`). Sans étape de build.

---

Fait partie de [Mes Projets](https://yoannservices.github.io/) · [Portfolio](https://yoannservices.github.io/portfolio/) · par [@yoannservices](https://github.com/yoannservices)

## Fiche technique

Résumé de ce que fait le code, tenu à jour à chaque modification : le lire suffit pour vérifier une information sans relire tout le jeu.

- **Code** : un seul fichier, `js/main.js` (script classique chargé par `../../assets/three-compat.js`, Three.js r186).
- **Voiture** : `assets/models/ferrari-458.glb` (Ferrari 458 Italia 2015, Tyler_Dave, CC-BY), cadrée par `fitGLB(g, 4.53, 0)` : avant du modèle sur +Z = avant du jeu. Carrosserie = matériau `Material.001`, teinte `0x1fb5b0`. Roues : `rigWheels` (nœuds `bone_wheel_*`) puis `poseWheel` : rotation `f1·dt/0.38`, braquage `steer × 0.5` (× 0.6 au-dessus de 25 m/s).
- **Caméras (C, fonction `cam()`)** : 0 Poursuite (distance 7,2 + vitesse × 0,05, hauteur 2,6 ; roulis et champ de vision qui suivent la vitesse) ; 1 Éloignée (distance et hauteur × 1,7) ; 2 Capot (point (0 ; 1,12 ; 0,75) du repère voiture, regard vers (0 ; 0,95 ; 12), champ 70°). Clic + glisser = orbite, retour derrière la voiture après 1,5 s sans glisser.
- **Sauvegarde** : meilleur score dans `localStorage` clé `cdd_best`.
- **Aide à l'écran** : `#help` dans `index.html` ; liste des touches du menu = `data-controls` du script `loader.js`.

## Crédits

Modèle de voiture : [2015 Ferrari 458 Italia](https://sketchfab.com/3d-models/2015-ferrari-458-italia-e0e86e4a9b25412badfa5c4b7e78c659) par Dave Bored (@Tyler_Dave), licence CC-BY 4.0, fichier `assets/models/ferrari-458.glb` (voir `assets/models/CREDITS.md`).
