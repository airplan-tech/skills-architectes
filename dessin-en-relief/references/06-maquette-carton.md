# 06 · Maquette en carton (Card Model)

Démo : https://sam1983aing.github.io/flat-to-3d/06-card-model/ · Code et prompt : https://github.com/Sam1983Aing/flat-to-3d/tree/main/06-card-model

## Ce qui se passe

Une maquette d'étude en carton blanc sur un bureau d'architecte, la nuit : murs en carton, fenêtres en acétate, courbes de niveau en carton gris, arbres en carton, un petit personnage. Une lampe de bureau l'éclaire, des dessins de la même maison sont punaisés au mur. En défilant, la caméra descend jusqu'aux yeux du personnage. Une sphère grandit depuis l'ampoule : à l'intérieur, le carton devient béton, chêne, verre et gazon, et la lumière de la lampe devient un soleil bas venant de la même direction. On entre, on monte jusqu'au bureau où la même maquette est posée. Puis on ressort, la maison redevient carton, la lampe s'éteint.

## Le truc

- Une seule liste de pièces, à 1 unité = 1 m. Le bureau, la lampe et l'atelier sont construits 100 fois plus grands autour : la maquette et la vraie maison sont les mêmes volumes aux mêmes coordonnées.
- La descente « paie » le défilement selon l'échelle : chaque division par deux de la hauteur coûte autant de défilement.
- Le passage carton → matière est une sphère centrée sur l'ampoule, avec une ligne d'accent là où elle coupe une surface.
- Deux éclairages dans une scène : la lampe pour le carton, un soleil pour la maison.

Paramètres utiles en démo : `?noao` coupe l'occlusion ambiante, `?dpr=1` règle la résolution (utile sur un ordinateur lent).

## Pour un architecte

- **Concours, jury** : la maquette blanche est le langage commun des architectes, l'effet est immédiat.
- Projet haut de gamme, intérieur soigné.
- Hommage à l'atelier : bon pour la page d'accueil d'un bureau.

## Données nécessaires

Le bâtiment et son terrain (courbes de niveau), l'orientation de la lumière, le parcours intérieur.

## Pièges

- Une des démos les plus polies par l'auteur : le premier essai sort plus sombre et avec des pièces vides. Il conseille de reprendre son code.
- Pas de ciel : l'atelier sombre reste autour de la maison, c'est voulu.

## Prompt de départ (adapté de l'auteur)

```text
Je veux construire une page web qui défile pour [le bureau X, le projet Y].

L'idée : une maquette d'étude en carton blanc de [la maison sur son terrain] est posée sur
un bureau d'architecte, la nuit. Murs en carton, fenêtres en acétate, courbes de niveau en
carton gris, arbres en carton et un petit personnage à l'échelle. Une lampe de bureau
l'éclaire, et des dessins de la même maison sont punaisés au mur sombre derrière.

Le défilement, dans l'ordre :
1. Le chargement : un cutter trace une ligne sur une feuille de carton, qui s'ouvre le
   long de la coupe.
2. La scène se monte : la lampe s'allume, les courbes de niveau tombent en place, la
   maison s'emboîte sur son terrain, les arbres se lèvent.
3. La descente jusqu'à hauteur des yeux du personnage. Chaque division par deux de la
   hauteur coûte autant de défilement. Un affichage donne la hauteur en centimètres sur
   le bureau et en mètres dans la maison.
4. Le passage : une sphère grandit depuis l'ampoule. Dedans, le carton devient béton,
   chêne, verre et gazon, avec une fine ligne d'accent là où elle coupe chaque surface. La
   caméra prend la place du personnage, la lumière de la lampe devient un soleil bas venant
   de la même direction. La sphère s'arrête quand la maison et son terrain sont faits ;
   l'atelier sombre reste autour. Pas de ciel.
5. La visite : par la porte coulissante dans [le séjour], jusqu'à [la pièce de travail], où la même
   maquette est posée sur la table.
6. Le retour : la sphère rétrécit, la maison redevient carton, la lampe s'éteint et
   [Prendre rendez-vous] apparaît.

Ce qui compte pour moi :
- La maquette n'est pas une image. 1 unité = 1 m de maison, le bureau est construit
  100 fois plus grand autour, et une seule liste de pièces se rend soit en carton, soit en
  vraies matières, aux mêmes coordonnées.
- Carton et maison sont éclairés séparément : le carton par la lampe, la maison par le
  soleil.
- [Le bâtiment et le terrain viennent des données jointes.]
- Page presque noire, carton crème #f2efe7, une seule couleur d'accent ([ambre #e85d04,
  ou la couleur du bureau]), Chakra Petch pour les titres, IBM Plex Mono pour les
  légendes, repères de coin.
- three.js [0.160] depuis un CDN, fichiers simples, sans compilation. Pas d'image.

Avant d'écrire du code, propose la maison avec des dimensions que je peux me représenter
et le chemin de la caméra, arrêt par arrêt, et attends ma réponse. Ensuite, construis par
étapes. Première étape seulement : le chargement, la scène qui se monte et la descente
jusqu'au personnage. Enregistre-la (vidéo du parcours ou captures à
plusieurs positions) et montre-la-moi avant d'aller plus loin.
```

Difficulté : élevée. Effet le plus « concours ».
