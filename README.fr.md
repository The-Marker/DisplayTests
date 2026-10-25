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
| Échelle de gris | Couleur | Voir si les tons sombres et clairs se distinguent |
| Noirs foncés | Couleur | Barres de 0 à 8 % sur noir pour voir si la TV écrase les ombres ou relève le noir (pièce sombre) |
| Échelle RVB et CMJN | Couleur | Six échelles de dix paliers, une par couleur (rouge, vert, bleu, cyan, magenta et jaune). Choisissez dans Échelle pour toutes les afficher ou une seule |
| Luminosité crête | Couleur | Fenêtre blanche de 10 à 100 % de la surface sur noir, pour mesurer la luminosité crête ; plage SDR ou HDR (HDR seulement si le navigateur et l'écran le prennent en charge) |
| Contraste | Couleur | Blocs de 5 % à 95 % avec niveau réglable |
| Uniformité grise | Uniformité | Gris de 0 à 100 % avec raccourcis vers le noir et le blanc : taches, vignetage, fuites de lumière, nuages et bandes |
| Uniformité RVB et CMJN | Uniformité | Une couleur en plein écran à la fois (rouge, vert, bleu, cyan, magenta, jaune, blanc et noir), choisie à la main. Sert aussi à trouver les pixels morts |
| Compteur de touchers | Tactile | Un cercle coloré par point de contact ; ils restent après le relâchement et sont effacés quand on touche à nouveau l'écran. Compte les touchers simultanés et le maximum |
| Grille de glissement | Tactile | Grille réglable qui peint les carrés traversés par le doigt ou la souris, avec le pourcentage couvert |
| Débloqueur de pixels | Pixels | Grille carrée adaptative dont les carrés changent au hasard entre RVB, CMJN, blanc et noir, chacun à son rythme ; taille (4–25 % de la largeur) et vitesse (1–16, de toutes les 10 s à toutes les 0,1 s) réglables |
| Gradation locale | Mouvement | Étoiles de plusieurs tailles qui se déplacent sur noir pour détecter les halos et la gradation locale (local dimming) ; vitesse et densité réglables |
| Smearing (VA) | Mouvement | Une barre blanche se déplace sur des fonds sombres pour montrer la traînée sombre ou claire des dalles VA ; vitesse et fond réglables, avec pause |
| Rémanence | Mouvement | Traînées dues à un temps de réponse lent ; passage de 2 à 6 s |
| Overscan et marges | Netteté | Cadres à 0, 2, 5 et 10 % des bords pour voir si l'image est rognée (surtout sur les TV) |
| Lignes fines | Netteté | Lignes d'un pixel réel pour détecter la mise à l'échelle, le flou et le moiré |
| Géométrie | Netteté | Grille, cercle et diagonales pour les proportions et la mise au point |
| Géométrie et calibrage | Netteté | La même chose, avec un cadre central dans le cercle qui réunit barres SMPTE, échelle de gris, échelle RVB et CMJN et contraste, et affiche la résolution, la densité et l'échelle de l'écran ; avec la diagonale indiquée, il calcule les ppp |

**Site**

- **Adaptatif :** 2 colonnes sur mobile, 3 sur tablette, 4 sur ordinateur avec filtres dans une barre latérale et 5 sur TV avec un texte plus grand.
- **Visionneuse plein écran :** chaque test s'adapte au format réel de l'écran. Les commandes se masquent avec `H` ou en touchant l'écran, pour ne pas polluer les tests d'uniformité.
- **Plusieurs entrées :** clavier, souris, écrans tactiles, télécommandes de TV, manettes et joysticks. Les indications de commande de la visionneuse s'adaptent à l'entrée détectée, et les touches s'affichent dans une case pour bien ressortir. Voir la section Commandes.
- **Thème automatique :** suit le mode clair ou sombre du système sur Android, iPhone, Windows, macOS et Linux. Avec le système en sombre, il utilise le noir pur, idéal pour les écrans OLED. Si l'appareil ne le signale pas, il utilise le thème clair.
- **Menu de thème :** une seule icône dans l'en-tête ouvre un menu Automatique, Clair, Sombre et Noir pur, et l'icône reflète l'état. Clair, Sombre et Noir pur fixent le thème et désactivent le suivi du système. La préférence est mémorisée dans le navigateur.
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
| Afficher ou masquer le panneau | `H` | Toucher l'écran | `OK` ou `Info` | `Start` |
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
