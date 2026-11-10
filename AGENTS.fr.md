[English](AGENTS.md) · [Español](AGENTS.es.md) · [Português](AGENTS.pt.md) · **Français** · [Deutsch](AGENTS.de.md)

# AGENTS.md

Guide pour les agents d'IA et les contributeurs qui modifient ce dépôt.

## Ce que c'est

Un site statique d'une seule page pour tester et diagnostiquer les écrans (téléphone, ordinateur et TV). Tout se trouve dans `index.html` : HTML, CSS et JavaScript sans dépendances, sans bundler et sans requêtes réseau.

## Structure

- `index.html` : le site complet.
- `README.md` (et `README.es.md`, `README.pt.md`, `README.fr.md`, `README.de.md`) : description et fonctionnalités pour les utilisateurs.
- `AGENTS.md` (et `AGENTS.es.md`, `AGENTS.pt.md`, `AGENTS.fr.md`, `AGENTS.de.md`) : guide pour les contributeurs. Gardez toutes les versions linguistiques synchronisées lorsque vous en modifiez une.
- `LICENSE` : GPL v3.

Dans `index.html`, le script comprend ces parties : utilitaires, noyau de langue (`DICT`, `tr`, `applyLang`), outils (`TOOLS`), grille et filtres, visionneuse plein écran, clavier et entrées, page d'accueil, menus de thème et de langue, favicon et démarrage.

## Exécuter et tester

Il n'y a pas de build. Ouvrez `index.html` dans un navigateur ou servez le dossier avec `python3 -m http.server`.

Avant de publier des modifications, vérifiez au minimum :

- Aucune erreur dans la console.
- Téléphone (~390 px), ordinateur (~1280 px) et TV (~1920 px) sans défilement horizontal.
- Thèmes clair, sombre, noir pur et automatique. Avec l'automatique désactivé, le thème fixe reste en place.
- Un navigateur sans `matchMedia` revient au thème clair.
- Chaque outil s'ouvre en plein écran, ses contrôles répondent et `Échap` le ferme.
- Géométrie, mode calibrage : la boîte est centrée dans le cercle sur mobile, ordinateur et TV, et affiche la résolution, la densité et l'échelle (avec `H` pour masquer le panneau et pouvoir le lire).
- Langues : si le système est dans une langue non prise en charge, le site utilise l'anglais ; le menu affiche l'anglais en premier, puis la langue du système, puis les autres ; le choix est conservé après un rechargement.
- Les entrées fonctionnent et les indications changent : clavier, tactile (glissement), télécommande de TV (`ChannelUp`, `Info`, `GoBack`, et événements uniquement par code 37–40/13 avec un User Agent de TV), manette (simulable en remplaçant `navigator.getGamepads`).
- Grille de glissement : faire glisser peint des cases et ne change ni de test ni ne ferme la visionneuse.

Playwright avec Chromium permet d'automatiser ces vérifications.

## Conventions

- Un seul fichier, sans dépendances externes ni requêtes réseau. Il doit s'ouvrir par un double-clic.
- Le texte de l'interface passe par `tr(texte)`. La clé est le texte en espagnol, en minuscules sauf les noms propres et sigles, et sans point d'exclamation. Les traductions sont dans `DICT` (une table par langue). Si une traduction manque, l'espagnol s'affiche. Pour ajouter une langue : ajoutez-la à `SUP`, `NATIVE` et `DICT` avec toutes les clés, puis ajoutez son README et son AGENTS.
- Couleurs et thème via des variables CSS dans `:root`. Ne codez jamais de couleurs en dur dans l'interface ; les motifs de test utilisent des couleurs exactes, car ce sont eux le produit.
- Thèmes : clair, sombre (gris), noir pur (`data-theme="black"`, fond #000) et automatique. En automatique avec un système sombre, le thème sombre gris est utilisé ; la case **Utiliser le noir pur en mode sombre** du menu de thème remplace le sombre par le noir pur (`dt-oled` dans `localStorage`). Aucune API web ne détecte l'OLED, donc le choix revient à l'utilisateur.
- Le thème par défaut est le clair. L'automatique dépend de `prefers-color-scheme`, avec `data-theme="light|dark|black"` sur `<html>` uniquement lorsque l'utilisateur fixe le thème.
- Les motifs statiques sont dessinés en SVG avec `viewBox` et reçoivent la largeur et la hauteur (`W`, `H`) pour s'adapter au rapport réel de l'écran. La miniature utilise 160×90.
- Les motifs animés (`kind:"cv"`) sont dessinés sur un `canvas` avec `init` et `frame`, et leur miniature est un SVG statique (`thumb`).
- Accessibilité : vrais boutons, `aria-pressed` sur les sélecteurs, focus visible, `aria-label` sur les miniatures et respect de `prefers-reduced-motion`.
- La persistance avec `localStorage` est toujours entourée de `try/catch` ; le site doit fonctionner sans elle. Elle conserve le thème (`dt-theme`) et la langue (`dt-lang`, `auto` ou un code).
- Langue : l'automatique suit `navigator.languages`, avec l'anglais en repli. Les éléments statiques utilisent `data-i18n`, `data-i18n-aria` et `data-i18n-title`. Un changement de langue appelle `applyLang()`.
- Les icônes sont des SVG en ligne avec `currentColor`. N'utilisez ni polices d'icônes ni images externes : le site est un fichier unique et doit s'afficher à l'identique à l'ouverture par double-clic.
- Le thème se choisit dans un menu déroulant à partir d'une icône (`#themeBtn`, `#themeMenu`) avec `role="menu"`, la navigation au clavier (flèches, Échap), et l'icône reflète le mode. Le menu de langue (`#langBtn`, `#langMenu`) fonctionne de la même façon.
- Le pied de page a été retiré volontairement. Ne le remettez pas.
- Tests tactiles : le compteur de contacts crée un cercle par point et efface les anciens lorsque l'écran est de nouveau touché ; la grille de glissement peint les cases traversées par le doigt ou la souris. Dans la grille, les gestes de glissement (naviguer, fermer) et le toucher pour afficher ou masquer le panneau sont désactivés volontairement.
- Luminosité de crête : le mode HDR utilise `color(rec2100-pq 1 1 1)` uniquement si `CSS.supports` l'accepte ; sinon, il affiche un avis et du blanc SDR. Le champ `help` d'un outil (ici `HDR_HELP`) s'affiche dans une section repliable de la visionneuse (`#vhelp`).
- `colorScale(x,y,w,h,noGray)` dessine les lignes de couleur ; avec `noGray`, la bande de gris est omise. Le test RGB et CMJN possède un sélecteur `Échelle` qui utilise `ramp1` pour n'afficher qu'une seule échelle.
- Lecture/pause : le bouton se trouve dans la ligne `#vnav`, entre Précédent et Suivant (classe `playbtn`), et non dans le panneau de contrôles. `clickPlay()` le cherche à cet endroit.
- L'en-tête ne contient pas de navigation par catégories ; les filtres forment une rangée de boutons au-dessus de la grille, quelle que soit la taille de l'écran, sans barre latérale. Ne les réintroduisez pas.
- Démarrage automatique : `AUTO` (`dt-auto` dans `localStorage`) décide si les tests avec un contrôle `play` démarrent en lecture (`showTool` définit `p.play`). Le débloqueur de pixels est inclus. Le mode Ghosting de `respuesta` bouge toujours, comme avant la fusion ; les autres modes suivent `AUTO`.
- Panneau de la visionneuse : `kick()` masque `#vc` après 5 s sans action, sauf dans la grille de glissement. Toute touche ou mouvement de souris le réaffiche.
- Contrôles conditionnels : un contrôle avec `when:{k,v}` n'apparaît que si `p[k]===v`. Un choix avec `rb:true` reconstruit le panneau lors d'un changement ; c'est ainsi que fonctionnent les modes.
- Utilitaires partagés pour les motifs : `smpteSvg`, `grayStrip`, `colorScale`, `contrastSvg`, `geoBase`, `screenInfo`, `starCount` et `newStar`. Réutilisez-les plutôt que de dupliquer le code de dessin.
- Toutes les entrées (clavier, souris, tactile, télécommande, manette et joystick) passent par le répartiteur `act(action, natif)`, avec les actions `left`, `right`, `up`, `down`, `confirm`, `back`, `next`, `prev`, `toggle` et `playpause`. Pour prendre en charge un nouvel appareil, faites-le correspondre à ces actions ; n'ajoutez pas de gestionnaires isolés.
- `INPUT` garde la dernière entrée détectée (`keyboard`, `mouse`, `touch`, `remote`, `gamepad`) et est reflétée dans `data-input` de `<html>`. Les indications de la visionneuse (`hintHtml`) en dépendent. Si vous ajoutez une action, ajoutez son indication pour toutes les entrées.
- Touches de la télécommande : `keyAction` accepte le nom (`ArrowLeft` ou `Left`) et le code numérique (37–40, 13). Certaines TV n'envoient que le code ; ne supprimez pas ce repli.
- Avis de photosensibilité : l'avis général se place au-dessus de la grille. Les tests de mouvement ou de changement de couleur ont un `warn` et l'affichent dans la visionneuse (`#vwarn`) avec la même classe `.warn` que la page d'accueil.
- Boutons de la visionneuse (`#vc .btn`), bouton pause et boutons sélectionnés : bleu des curseurs `#85b7eb` avec texte noir (les autres, blancs avec texte noir). Les touches d'indication (`kbd`) sont blanches avec texte noir et plates, sans relief inférieur.
- Favicon : icône de moniteur identique à celle de l'en-tête. `setFav()` la régénère en `data:` selon `prefers-color-scheme` (noire en clair, blanche en sombre) et la met à jour lorsque le système change. N'utilisez pas `media` sur les liens d'icône : les navigateurs ne l'appliquent pas de façon fiable.
- Les touches dans les indications sont écrites avec `<kbd>` (classes `r` pour la télécommande et `g` pour la manette) pour apparaître dans un encadré.
- La navigation spatiale (`spatial`) ne s'active que lorsqu'un élément a le focus (clavier et souris) ou toujours (télécommande et manette), afin que les utilisateurs du clavier conservent le défilement avec les flèches.

## Règles de sécurité

- Pas de flashs ni de clignotement automatique. Le mouvement reste modéré et l'avis de photosensibilité doit rester visible.
- La vitesse du ghosting est limitée à 2–6 s par passage. Ne descendez pas sous 2 s.
- Le débloqueur de pixels démarre en pause, sauf si le démarrage automatique est activé. Chaque case change de couleur au hasard et de façon autonome, avec un intervalle moyen allant de 10 s à 0,1 s (vitesses 1–16) et une variation de ±40 % ; les cases sont reprogrammées lorsque la vitesse change, afin qu'elles ne changent jamais ensemble. Au-delà de 3 changements par seconde (vitesse 13 ou plus), au moins 8 colonnes sont imposées pour que le scintillement ne se concentre pas sur quelques cases, et l'étiquette indique « rapide ». Ne supprimez pas cette limite et n'augmentez pas la vitesse sans en informer le responsable du projet.
- Le test ghosting et smearing (`respuesta`) bouge toujours en mode Ghosting (`m` = 0). Le mode Smearing démarre en pause, sauf si le démarrage automatique est activé. Les deux affichent l'avis de photosensibilité.
- Les vignettes sont dessinées avec les paramètres par défaut (`thumbOf` utilise `t.p0`), donc ajuster un test ne change jamais sa vignette. Ne les redessine pas avec les valeurs actuelles.
- L'en-tête, l'avis de photosensibilité et les filtres forment un seul bloc `.sticky` en haut de la page d'accueil. Le guide et la grille défilent en dessous.
- Les contrôles de la visionneuse doivent pouvoir être masqués, pour ne pas polluer les tests d'uniformité.

## Ajouter un outil

1. Ajoutez un objet à `TOOLS` avec `id`, `name`, `cat`, `desc`, `p` (paramètres par défaut), `ctl` (contrôles, facultatif) et `draw(p, W, H, live)` qui renvoie le SVG. S'il est animé, utilisez `kind:"cv"` avec `init`, `frame` et `thumb`.
2. Si c'est une nouvelle catégorie, ajoutez-la à `CATS`.
3. Les contrôles peuvent être `range` (`min`, `max`, `step`, `fmt`), `choice` (`opts`), `preset` (raccourcis vers une valeur) ou `play` (démarrer et mettre en pause).
4. Ajoutez chaque texte visible en espagnol à toutes les langues de `DICT`, et mettez à jour le tableau des outils de `README.md` et de ses traductions.
5. Vérifiez le site avec la liste de tests ci-dessus.

## Commits

Messages courts en espagnol ou en anglais, à l'impératif, avec une ligne de résumé. Une modification par commit lorsque c'est possible.
