# CHRONO EPS — PWA

Application web progressive pour chronométrer des courses en EPS, enregistrer jusqu'à 30 coureurs, capturer la vidéo du passage, revoir les essais et classer les meilleurs temps.

## Tester en local
Ouvrez `index.html` dans un navigateur pour tester les coureurs, le chronomètre et le classement. L'accès caméra et l'installation PWA nécessitent normalement une origine sécurisée HTTPS (ou localhost). Le mode fichier peut limiter ces fonctions.

## Héberger gratuitement (HTTPS)
1. Créez un compte sur GitHub et un dépôt public `chrono-eps`.
2. Téléversez tous les fichiers de ce dossier à la racine du dépôt.
3. Dans **Settings → Pages**, choisissez **Deploy from a branch**, la branche `main` et le dossier `/ (root)`, puis **Save**.
4. Attendez l'URL HTTPS affichée par GitHub Pages. Ouvrez-la sur le téléphone.

Autre option : déposer ce dossier sur Netlify ou Cloudflare Pages. Il faut conserver les fichiers à la même racine.

## Installer
- **Android / Chrome** : ouvrez l'URL HTTPS, menu ⋮, **Installer l'application** ou **Ajouter à l'écran d'accueil**.
- **iPhone / iPad / Safari** : ouvrez l'URL dans Safari, bouton Partager, **Sur l'écran d'accueil**.

## Fonctionnalités
- Jusqu'à 30 prénoms, avec suppression individuelle.
- 5 essais maximum par coureur, chronomètre au bouton départ/arrivée.
- Caméra arrière si disponible, trait de visée vertical et vidéo arrêtée environ 1 s après le chrono.
- Relecture avec curseur, commandes ±0,1 s, avance/recul image par image (approx. 1/30 s) et repère manuel de l’image du franchissement.
- Classement croissant par meilleur temps et export CSV/JSON, import JSON.
- Sauvegarde locale des noms et des temps ; service worker pour cache hors ligne.

## Protocole conseillé sur Android
1. Hébergez sur HTTPS et ouvrez dans Chrome sur la tablette Android.
2. Autorisez la caméra et choisissez la caméra arrière ; faites un essai de 5 à 10 secondes avant la séance.
3. Fixez la tablette sur un support stable, en sécurité et hors de la trajectoire. Alignez le trait vert sur le plan de la ligne d’arrivée et vérifiez que le torse est bien visible.
4. Appuyez au départ, puis à l’arrivée. Après l’arrêt, attendez la fin de l’enregistrement, puis ouvrez la relecture.
5. Pour revoir le passage, faites glisser le curseur près de l’arrivée, mettez en pause et utilisez « Image − » / « Image + ». Marquez la première image où le torse atteint le plan de la ligne.
6. Comparez le temps manuel et le repère vidéo. Le repère vidéo est une aide d’analyse après course : il ne fait pas de détection automatique et ne recalcule pas le temps officiel.
7. Testez la stabilité et la fréquence d’images sur votre modèle Android ; certains appareils/navigateurs limitent les formats vidéo.

## Limites importantes
- Les vidéos sont conservées temporairement en mémoire de la session pour éviter de remplir le stockage de l'appareil. Elles ne sont pas incluses dans l'export JSON et ne sont pas restaurées après fermeture/actualisation.
- Le temps mesuré est le temps entre les deux appuis humains, pas une détection automatique du franchissement. La latence de réaction et de déclenchement vidéo peuvent influencer le résultat.
- La caméra/MediaRecorder varie selon navigateur et appareil. Tester sur la tablette cible avant une séance. Le pas image par image est une estimation de 1/30 seconde ; la cadence vidéo réelle peut être différente et les commandes de navigateur ne garantissent pas un vrai accès à chaque image décodée. La première visite en ligne est nécessaire pour mettre en cache l'application.
- Les données sont locales à ce navigateur/appareil ; exportez régulièrement une sauvegarde. Aucune donnée n'est envoyée à un serveur par cette application.

## Fichiers
- `index.html` : interface, style et logique de l'application.
- `manifest.webmanifest` : nom, mode autonome et icônes PWA.
- `sw.js` : cache pour accès hors ligne.
- `icon-192.png`, `icon-512.png` : icônes de l'application.
