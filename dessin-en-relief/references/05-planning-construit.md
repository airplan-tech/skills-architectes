# 05 · Planning qui construit (Schedule Build)

Démo : https://sam1983aing.github.io/flat-to-3d/05-schedule-build/?dir=a · Code et prompt : https://github.com/Sam1983Aing/flat-to-3d/tree/main/05-schedule-build

## Ce qui se passe

Un diagramme de Gantt occupe une bande en bas de l'écran, le chantier est au-dessus. La molette fait avancer le trait « aujourd'hui » : une clôture se monte, la fouille se creuse, une grue pose chaque cadre, mur et panneau de toiture pendant que sa barre se remplit. À la remise des clés, la porte s'ouvre et on entre. En remontant, la maison se démonte.

Trois variantes : le planning (`?dir=a`), le plan de fondations imprimé à l'échelle 1 sur le sol (`?dir=b`), la caméra de chantier du constructeur (`?dir=c`).

La démo s'ouvre à la semaine 7, en plein chantier. `?dir=a&wk=0&open` part de la feuille de planning complète à la semaine 0. On peut aussi glisser sur le planning ou appuyer sur ▶ BUILD.

## Le truc

- Un seul tableau (`PHASES` : nom, semaine de début, semaine de fin) dessine les barres et décide quand chaque élément existe. Le défilement est une date ; le planning et le modèle lisent le même nombre.
- Chaque élément connaît sa phase et son ordre dans la phase, et arrive par la grue, monte, pousse ou apparaît. L'état est une fonction pure de la semaine : c'est pour ça que le retour en arrière marche.
- La phase en cours est en couleur d'accent dans le planning et sur l'élément en vol.
- Les dates comptent les jours ouvrables.

## Pour un architecte

- **Échéancier** : rendre lisible un planning de travaux, pour un client ou un jury qui note l'échéancier.
- Préfabrication et ossature bois : la pose par la grue est spectaculaire et vraie.
- Contrairement au 04, la caméra reste haute pendant la construction : c'est le bâtiment qui bouge.

## Données nécessaires

Le planning (phases, semaines), les éléments du bâtiment rangés par phase, le mode d'arrivée de chaque élément, le parcours intérieur final.

## Pièges

- Pas de mise en page mobile dans la démo d'origine.
- Éviter l'aspect dessin animé : demander des matières crédibles, des ombres douces, un soleil qui monte avec les semaines.

## Prompt de départ (adapté de l'auteur)

```text
Je veux construire une page web pour [une entreprise de construction, le projet Y] qui
promet « Votre maison en [14 semaines] ».

L'idée : un planning de travaux, le diagramme de Gantt des entrepreneurs, occupe une bande
en bas de l'écran : barres hachurées, semaines en haut, un trait « aujourd'hui » en
couleur d'accent. Au-dessus, le chantier, encore vide. La molette fait avancer le trait
« aujourd'hui » et la maison se construit dans l'ordre : [clôture et baraque, fouille,
fondations, ossature, planchers, murs, toiture, châssis, bardage et finitions, mobilier].
En remontant, elle se démonte.

Ce que le visiteur voit, dans l'ordre :
1. L'installation de chantier et la fouille.
2. Une grue pose chaque cadre, mur et panneau de toiture, avec un léger balancement et
   un atterrissage en douceur.
3. Le bardage se pose, la pelouse pousse, les lumières s'allument à l'intérieur.
4. À la remise des clés, le matériel de chantier part, la porte s'ouvre et la caméra
   entre : [l'entrée, le séjour, la cuisine, l'escalier vers la mezzanine], pour finir sur
   [la galerie au-dessus de la double hauteur].

Ce qui compte pour moi :
- Le planning n'est pas une image. Un seul tableau de phases (nom, semaine de début,
  semaine de fin) dessine les barres et décide quand chaque élément existe. Chaque élément
  connaît sa phase et son ordre. [Les phases viennent du planning joint.]
- La phase en cours est en couleur d'accent aux deux endroits : sa barre se remplit et
  l'élément posé a des arêtes en couleur d'accent.
- La caméra garde une vue haute de trois quarts pendant la construction. Glisser sur le
  planning fait défiler aussi, et un bouton lance la construction.
- Pas d'aspect dessin animé : béton, lamellé-collé, OSB, bois brûlé, zinc, chêne,
  dessinés en code, ombres douces, un soleil qui monte avec les semaines, de légères arêtes
  à l'encre. Les dates
  comptent les jours ouvrables.
- Aspect écran de CAO : papier #f2efe7, encre #1d1c19, une seule couleur d'accent
  ([ambre #e85d04, ou la couleur du bureau]), Chakra Petch pour les titres, IBM Plex Mono
  pour les légendes, repères de coin, un
  affichage sombre avec la semaine, la date et la phase.
- three.js [0.169] depuis un CDN, fichiers simples, sans compilation. Pas d'image.

Avant d'écrire du code, propose la maison avec des dimensions, les phases avec leurs
semaines et la caméra pour la construction et pour la visite, et attends ma réponse.
Ensuite, construis par étapes. Première étape seulement : la bande du planning, le
chantier et la construction jusqu'à l'ossature. Enregistre-la (vidéo du parcours ou captures à
plusieurs positions) et montre-la-moi avant d'aller plus loin.
```

Difficulté : moyenne à élevée. La partie difficile (le planning qui pilote) marche souvent du premier coup selon l'auteur.
