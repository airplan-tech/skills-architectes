# 03 · Coupe ouverte (Open Section)

Démo : https://sam1983aing.github.io/flat-to-3d/03-open-section/ · Code et prompt : https://github.com/Sam1983Aing/flat-to-3d/tree/main/03-open-section

## Ce qui se passe

Deux variantes : `?dir=a` ouvre l'objectif et visite pièce par pièce (par défaut), `?dir=c` plonge dans la cuisine et descend l'escalier.

Une coupe au 1/100 d'une maison sur trois niveaux se trace d'elle-même. En défilant, l'objectif s'ouvre mais la coupe garde exactement sa taille à l'écran : tout ce qui est derrière recule en profondeur. Un balayage change l'encre en matière et en lumière, puis la caméra visite la maison étage par étage, toujours face à la coupe, comme une maison de poupée. Elle termine sur la coupe en couleur.

## Le truc

- Un seul plan de coupe vertical, et un « couvercle » noir sur chaque solide qu'il traverse : vu de face au téléobjectif (1,6° à environ 1 km), c'est la coupe.
- La coupe garde sa taille parce que la distance suit l'angle : distance = (hauteur du cadre / 2) / tan(angle / 2). Le README de l'auteur écrit « frame height / tan(lens / 2) » parce que son code appelle « frame height » la demi-hauteur : c'est la même formule. L'objectif peut passer de 1,6° à 64° sans que le cadre bouge. La caméra ne tourne jamais.
- Les annotations (trames, niveaux, noms de pièces) sont dessinées sur un calque 2D au-dessus de la scène.
- Une petite vue 3D en coin montre ce que la caméra regarde.

## Pour un architecte

- Maisons à demi-niveaux, escaliers, doubles hauteurs : la lecture des niveaux devient évidente.
- Expliquer une division en logements ou un programme sur plusieurs étages.

## Données nécessaires

Coupe avec niveaux et hauteurs, position de l'escalier, pièces de chaque niveau, mobilier principal.

## Pièges

- Le premier essai de l'auteur a l'air plus « dessin animé » : prévoir un tour de polissage des matières.
- Il faut de la profondeur derrière la coupe (plusieurs pièces, un escalier, une cour), sinon l'effet tombe à plat.

## Prompt de départ (adapté de l'auteur)

```text
Je veux construire une page web qui défile pour [le bureau X, la maison Y sur trois
niveaux].

L'idée : la page s'ouvre sur une coupe à plat au 1/100. Murs et dalles coupés en noir
plein, terre hachurée, repères de trames, niveaux, noms des pièces, petits personnages et
arbres. Rien n'a l'air 3D. Au chargement, des traits de plume en couleur d'accent
balaient de gauche à droite et la coupe se trace.

Le défilement, dans l'ordre :
1. L'objectif s'ouvre. Les pièces derrière la coupe reculent en profondeur pendant que la
   coupe garde exactement sa taille à l'écran.
2. Une ligne de balayage en couleur d'accent traverse la maison et change l'encre en matière, lumière et
   ombre.
3. La caméra visite la maison étage par étage à hauteur d'yeux, toujours face à la coupe :
   [l'escalier, la cuisine, la chambre, le séjour], avec une carte pour chaque arrêt.
4. Elle recule jusqu'à la coupe à plat, maintenant en couleur.
5. Une section de fin sur papier : les faits du projet et [Prendre rendez-vous].

Ce qui compte pour moi :
- La coupe n'est pas une image. C'est le vrai modèle 3D coupé par un plan, avec un
  couvercle noir sur chaque solide traversé, vu de face à travers un objectif de 1,6 degré
  à environ 1 km.
- Ouvrir l'objectif rapproche la caméra pour que le cadre sur la coupe ne change jamais :
  distance = (hauteur du cadre / 2) / tan(angle / 2). La caméra ne tourne jamais.
- Donner de la profondeur à montrer : [les niveaux, l'escalier, la cour derrière la coupe], avec du vrai mobilier.
- [Les niveaux viennent des données jointes. N'invente aucune pièce.]
- Aspect écran de CAO : papier #f2efe7, encre #1d1c19, une seule couleur d'accent
  ([ambre #e85d04, ou la couleur du bureau]), Chakra Petch pour les titres, IBM Plex Mono
  pour les légendes, repères de coin, cartouche,
  échelle graphique, lecture de l'angle en direct, petite vue 3D de repérage.
- three.js [0.160] depuis un CDN, fichiers simples, sans compilation. Pas d'image.

Avant d'écrire du code, propose la maison en coupe avec des dimensions que je peux me
représenter et les arrêts de la caméra dans l'ordre, et attends ma réponse. Ensuite,
construis par étapes. Première étape seulement : le chargement, la coupe qui se trace,
l'ouverture de l'objectif et le balayage de couleur. Enregistre-la (vidéo du parcours ou captures à
plusieurs positions) et montre-la-moi avant d'aller plus loin.
```

Difficulté : moyenne.
