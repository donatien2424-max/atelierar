# AtelierAR — application pour menuisier (PWA)

Trois outils dans une seule application installable (Android et iOS) :

1. **Mesurer (AR)** : mesure de distance, de pavé/cube (L × l × H) et de cylindre (Ø × H) avec la caméra, volume en litres, historique.
2. **Photo** : prise de photo, étalonnage sur un objet de taille connue (mètre, feuille A4), tracé manuel des lignes de cotation en cm, export PNG.
3. **Atelier 3D** : modélisation paramétrique du meuble (pavés et cylindres, en cm), liste de débit, enregistrement, import/export JSON, puis **pose en AR à l'échelle 1:1** chez le client.

## Lancer

La caméra et la AR exigent **HTTPS** (sauf `localhost`).

- Test rapide sur ordinateur : `npx serve .` puis ouvrir `http://localhost:3000`.
- Sur téléphone : déposer les 4 fichiers sur un hébergement HTTPS (Netlify Drop, GitHub Pages, Cloudflare Pages), ouvrir l'adresse, puis « Ajouter à l'écran d'accueil ».

## Compatibilité

| Fonction | Android (Chrome + Services Google Play pour la RA) | iPhone / iPad (Safari) |
|---|---|---|
| Atelier 3D | oui | oui |
| Photo-cotation | oui | oui |
| Mesure AR et pose AR | oui (WebXR) | non : Safari ne fournit pas WebXR |

## Limites à connaître

- La mesure AR repose sur des points touchés à l'écran (détection de plans). Elle ne reconnaît pas automatiquement un meuble : sans capteur de profondeur, aucune application ne le fait de façon fiable. Précision typique : ± 1 à 2 cm, à vérifier au mètre pour les coupes.
- La photo-cotation n'est exacte que pour des points situés dans le même plan que la référence d'étalonnage, photo prise bien de face.

## Pour une version native complète (iOS + Android)

- **iOS** : ARKit + RealityKit (SwiftUI). Avec un iPhone Pro (LiDAR), mesure de volume automatique via les maillages de scène, et export USDZ du meuble pour l'affichage AR (AR Quick Look).
- **Android** : ARCore + Sceneform/Filament ou Jetpack XR, avec l'API Depth.
- **Multiplateforme** : Unity AR Foundation (un seul code pour ARKit et ARCore), ou Flutter/React Native avec un module AR.
- Le format JSON du meuble de cette application peut être repris tel quel comme modèle de données.
