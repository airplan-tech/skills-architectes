# 02 · Coupe balayée (Section Sweep)

Démo : https://sam1983aing.github.io/flat-to-3d/02-section-sweep/ · Code et prompt : https://github.com/Sam1983Aing/flat-to-3d/tree/main/02-section-sweep

## Ce qui se passe

Une coupe A-A d'une maison sur un terrain en pente : poché noir, terre hachurée, repères de trames, niveaux, cotes, noms des pièces, et trois lignes pointillées pour les angles du soleil aux 21 décembre, mars et juin. En défilant, l'objectif s'ouvre et les pièces derrière la coupe prennent de la profondeur. Un plan de balayage vertical traverse la maison : d'un côté l'encre, de l'autre la matière éclairée. Quand il passe le vitrage, les pointillés solaires deviennent de vrais rayons au même angle. Puis on entre par la coupe, pièce par pièce, et on ressort vers le dessin.

## Le truc

- La coupe est le modèle coupé en A-A, vu par une caméra perspective à 0,12° à environ 12 km : il se lit comme une coupe au 1/100.
- Un shader plein écran « encre » le rendu à partir des normales et de la profondeur : poché, hachures du terrain, arêtes, épaisseur des traits selon la distance derrière la coupe.
- Le balayage mélange encre et rendu éclairé pixel par pixel selon la position.
- La visite suit une seule courbe à hauteur d'yeux, caméra horizontale (décentrement comme un photographe d'architecture), sans arrêt.

## Pour un architecte

- **Terrain en pente** : montrer comment le bâtiment s'assoit, les terres, les niveaux.
- **Ensoleillement** : les angles des solstices et des équinoxes deviennent de vrais rayons. Argument parlant dans une notice ou une réunion de projet.
- Pour un bâtiment réel, calculer les angles avec la vraie latitude (Liège : 50,64° nord) et l'orientation réelle de la coupe.

## Données nécessaires

La coupe (niveaux, épaisseurs, terrain le long de la coupe, idéalement depuis un MNT), l'orientation de la coupe, la latitude, les pièces traversées.

## Pièges

- C'est une des démos les plus travaillées par l'auteur : le premier essai donne l'objectif, le balayage et les rayons, mais des pièces vides. Il conseille de reprendre son code.
- Des angles solaires faux ruinent la crédibilité devant des architectes : les calculer, ne pas les dessiner « à vue ».

## Prompt de départ (adapté de l'auteur)

```text
Je veux construire une page web qui défile pour [le bureau X, la maison Y sur un terrain
en pente].

L'idée : la page s'ouvre sur une coupe A-A à plat de [la maison]. Poché noir là où la
coupe traverse murs et dalles, terre hachurée, repères de trames, niveaux, cotes et noms
des pièces. Trois lignes pointillées en couleur d'accent montrent les angles du soleil
aux [21 décembre, 21 mars et 21 juin], calculés pour [la latitude du site] et
l'orientation réelle de la coupe. Rien n'a l'air 3D.

Le défilement, dans l'ordre :
1. Le chargement est un petit plan de repérage où la ligne de coupe A-A se trace. Puis la
   coupe se dessine : terre et poché d'abord, puis les traits derrière la coupe d'avant
   en arrière, puis les annotations.
2. L'objectif s'ouvre : la caméra approche pendant que l'angle s'élargit, la coupe garde
   sa taille à l'écran et les pièces derrière s'ouvrent en perspective. Puis la vue
   tourne de trois quarts.
3. Le balayage : un plan vertical traverse la maison de [l'aval à l'amont]. D'un côté
   l'encre, de l'autre la matière éclairée. Quand il passe le vitrage, les pointillés
   s'effacent et de vrais rayons entrent à l'angle de [décembre].
4. La visite : on entre par la coupe à hauteur d'yeux, à travers [les pièces], en
   ralentissant à chaque pièce avec une légende.
5. On ressort par la coupe, le balayage repart en arrière, l'objectif se referme et la
   feuille revient avec [Prendre rendez-vous].

Ce qui compte pour moi :
- Le dessin n'est pas une image. C'est le modèle 3D coupé en A-A, vu par une caméra
  perspective à 0,12 degré à environ 12 km, donc il se lit à plat. Un shader plein écran
  l'encre à partir des normales et de la profondeur, et mélange le rendu éclairé selon la
  position du balayage.
- La caméra ne coupe jamais : l'ouverture de l'objectif est un seul dolly zoom continu.
- [Les niveaux et le terrain viennent des données jointes. N'invente aucune pièce.]
- Aspect écran de CAO : papier #f2efe7, encre #1d1c19, une seule couleur d'accent
  ([ambre #e85d04, ou la couleur du bureau]), Chakra Petch pour les titres, IBM Plex Mono
  pour les légendes, repères de coin, une lecture
  de la focale en mm, un cartouche et une petite coupe qui montre où est la caméra.
- three.js [0.160] depuis un CDN, fichiers simples, sans compilation. Pas d'image : toutes
  les matières sont dessinées en code.

Avant d'écrire du code, propose la maison en coupe avec des dimensions que je peux me
représenter et le chemin de la caméra, arrêt par arrêt, et attends ma réponse. Ensuite,
construis par étapes. Première étape seulement : le chargement, la coupe qui se dessine et
l'ouverture de l'objectif. Enregistre-la (vidéo du parcours ou captures à
plusieurs positions) et montre-la-moi avant d'aller plus loin.
```

Difficulté : élevée (shader d'encre, rayons de soleil). Très forte pour un terrain en pente.
