[English](README.md) · [Español](README.es.md) · [Português](README.pt.md) · **Français** · [Deutsch](README.de.md)

# DisplayTests

Site web proposant des outils pour tester et diagnostiquer les écrans de téléphones, d'ordinateurs et de téléviseurs. C'est un seul fichier, `index.html`, sans dépendances ni étape de compilation.

## Utilisation

Ouvrez `index.html` dans un navigateur (double-clic) ou publiez-le sur n'importe quel hébergement statique, par exemple GitHub Pages. Touchez une vignette pour ouvrir le test en plein écran.

Pour mesurer, réglez la luminosité de l'écran, utilisez le plein écran et, pour les tests de noir, une pièce sombre. Les couleurs affichées sont une approximation.

## Points forts

**Outils de test**

| Outil | Catégorie | À quoi il sert |
| --- | --- | --- |
| Barres SMPTE | Couleur | Vérifier la couleur, la luminosité et les niveaux de noir |
| Échelles de couleurs et de gris | Couleur | Échelle de gris et six échelles de couleur à dix paliers (rouge, vert, bleu, cyan, magenta et jaune). Utilisez l'option Échelle pour toutes les voir ou une seule |
| Noirs foncés | Couleur | Barres de 0 à 8 % sur noir pour voir si la TV écrase les ombres ou relève le noir (pièce sombre) |
| Luminosité crête | Couleur | Fenêtre blanche de 10 à 100 % de la surface sur noir, pour mesurer la luminosité crête ; plage SDR ou HDR. Le HDR exige un navigateur et un écran compatibles, et la visionneuse explique comment l'activer |
| Contraste | Couleur | Blocs de 5 % à 95 % avec niveau réglable |
| Uniformité grise | Uniformité | Gris de 0 à 100 % avec raccourcis vers le noir et le blanc : taches, vignetage, fuites de lumière, nuages et bandes |
| Uniformité RVB et CMJN | Uniformité | Une couleur en plein écran à la fois (rouge, vert, bleu, cyan, magenta, jaune, blanc et noir), choisie à la main. Sert aussi à trouver les pixels morts |
| Compteur de contacts | Tactile | Un cercle numéroté et coloré par point de contact ; les cercles restent après le relâchement et sont effacés quand l'écran est de nouveau touché. Compte les contacts simultanés et le maximum |
| Grille de glissement | Tactile | Grille réglable qui peint les carrés traversés par le doigt ou la souris, avec le pourcentage couvert |
| Débloqueur de pixels | Pixels | Grille carrée adaptative dont les carrés changent au hasard entre RVB, CMJN, blanc et noir, chacun à son rythme ; taille (4–25 % de la largeur) et vitesse (1–16, de toutes les 10 s à toutes les 0,1 s) réglables |
| Gradation locale | Mouvement | Étoiles de plusieurs tailles qui se déplacent sur noir pour détecter les halos et la gradation locale ; vitesse, densité et taille des étoiles réglables |
| Ghosting et smearing | Mouvement | Choisissez un mode. Ghosting : un bloc traverse l'écran pour montrer les traînées d'une réponse lente (passage de 2 à 6 s). Smearing (VA) : une barre blanche laisse une traînée sombre ou claire sur les dalles VA ; vitesse et fond réglables |
| Texte en mouvement | Mouvement | Lignes de texte qui défilent en sens opposés, à l'horizontale ou à la verticale, en taille uniforme ou variée ; comparez la netteté à l'arrêt et en mouvement |
| Géométrie | Netteté | Grille, ou calibrage avec un cadre central dans le cercle qui réunit barres SMPTE, échelles de gris, RVB et CMJN, et contraste, et affiche la résolution, la densité et l'échelle de l'écran ; avec la diagonale saisie, il calcule les ppp |
| Convergence | Netteté | Grilles rouge, verte et bleue, avec des points près des coins de chaque carré ; le désalignement apparaît en bords ou points colorés. Pour tubes CRT et projecteurs à trois panneaux ; sur les écrans plats à panneau unique, la convergence est réglée en usine |
| Format d'image et overscan | Netteté | Mode : cercle et cadres 4:3, 16:9, 21:9 et 32:9, chacun touchant le bord le plus proche et nommé ; ou Overscan, avec des cadres à 0, 2, 5 et 10 % des bords pour voir si l'image est rognée (surtout sur TV) |
| Carrés | Netteté | Damier de carrés ; des carrés rectangulaires révèlent une mise à l'échelle inégale |
| Lignes fines | Netteté | Lignes d'un pixel réel pour détecter la mise à l'échelle, le flou et le moiré |
| Netteté du texte | Netteté | Texte en nombreuses tailles, avec empattement, à chasse fixe et en couleur, sur blanc et sur noir, pour vérifier la netteté sur les écrans à pixel blanc (comme le W-OLED) |

**Site**

- **Adaptatif :** 2 colonnes sur mobile, 3 sur tablette, 4 sur ordinateur et 5 sur TV avec un texte plus grand. Les filtres forment une rangée de boutons quelle que soit la taille de l'écran, comme sur mobile. L'en-tête, l'avis de photosensibilité et les filtres restent en haut en faisant défiler la page.
- **Visionneuse plein écran :** chaque test s'adapte au format réel de l'écran. Les contrôles s'affichent et se masquent avec `H` ou un clic de souris (sur écran tactile, double toucher), et disparaissent aussi seuls après 5 secondes sans action, pour ne pas polluer les tests d'uniformité. Bouger la souris ne les affiche pas.
- **Plusieurs entrées :** clavier, souris, écrans tactiles, télécommandes de TV, manettes et joysticks. Les indications de commande de la visionneuse s'adaptent à l'entrée détectée, et les touches s'affichent dans une case pour bien ressortir. Voir la section Commandes.
- **Thème automatique :** suit le mode clair ou sombre du système sur Android, iPhone, Windows, macOS et Linux. Avec le système en sombre, il utilise le thème sombre gris, ou le noir pur si vous cochez l'option du menu de thème. Si l'appareil ne le signale pas, il utilise le thème clair.
- **Menu de thème :** une seule icône dans l'en-tête ouvre un menu Automatique, Clair, Sombre et Noir pur, et l'icône reflète l'état. Clair, Sombre et Noir pur fixent le thème et désactivent le suivi du système. En dessous, la case **Utiliser le noir pur en mode sombre** fait utiliser le noir pur au thème sombre, idéal pour les écrans OLED. La préférence est mémorisée dans le navigateur.
- **En-tête :** lien vers GitHub, un bouton qui active ou désactive le démarrage automatique des tests de mouvement (désactivé par défaut ; le choix est mémorisé) et les menus de thème et de langue.
- **Langues :** anglais, espagnol, portugais, français et allemand. La langue est choisie automatiquement d'après la langue du système ; si elle n'est pas prise en charge ou ne peut pas être détectée, l'anglais est utilisé. L'icône globe, à gauche de l'icône de thème, permet de la changer à la main.
- **Filtres par catégorie :** Couleur, Uniformité, Pixels, Mouvement, Netteté et Tactile.
- **Sécurité :** avertissement pour les personnes photosensibles, mouvement sans flashs, et un débloqueur de pixels qui démarre en pause, avec des changements de couleur aléatoires et indépendants pour chaque carré. À partir de la vitesse 13 (plus de 3 changements par seconde), la grille compte au moins 8 colonnes et un avertissement s'affiche.

## Commandes

Le site détecte la dernière entrée utilisée et adapte les indications de la visionneuse en conséquence.

| Action | Clavier | Tactile | Télécommande | Manette ou joystick |
| --- | --- | --- | --- | --- |
| Changer de test | `←` `→` | Glisser sur les côtés, ou boutons Précédent et Suivant | `◀` `▶`, `CH+` `CH−` | `◀` `▶`, `LB` `RB` |
| Aller aux commandes | `↓` (et `↑` pour revenir) | Toucher la commande | `▼` (et `▲` pour revenir) | `▼` (et `▲` pour revenir) |
| Régler une commande | `←` `→` sur un curseur | Faire glisser | `◀` `▶` | `◀` `▶` ou stick gauche |
| Afficher ou masquer le panneau | `H` | Cliquer sur l'écran (tactile : double toucher) | `OK` ou `Info` | `Start` |
| Démarrer ou mettre en pause | `Espace` | Bouton Pause/Démarrer entre Précédent et Suivant | `⏯` | `X` |
| Valider | `Entrée` | Toucher | `OK` | `A` |
| Fermer | `Échap` | Glisser vers le bas | `Retour` | `B` |

Dans le test de grille de glissement, les gestes ne changent pas de test et ne ferment pas la visionneuse, et toucher ne masque pas le panneau, pour pouvoir peindre librement. Utilisez le bouton Fermer, `Échap` ou `H` dans ce test.

Sur la page d'accueil, les télécommandes et les manettes se déplacent entre les boutons, les filtres et les vignettes avec les flèches (navigation spatiale). Sur les TV avec Tizen, webOS, Android TV, Fire TV et similaires, le site démarre avec les indications de télécommande. Les manettes sont détectées dès qu'on appuie sur un bouton.

## Compatibilité

Navigateurs actuels sur Android, iPhone, Windows, macOS et Linux, et navigateurs de téléviseurs connectés avec une prise en charge moderne de CSS et JavaScript.

## Contribuer

Voir [AGENTS.fr.md](AGENTS.fr.md) pour la structure, les conventions et la manière d'ajouter un nouvel outil.

## Licence

GNU GPL v3. Voir [LICENSE](LICENSE).
