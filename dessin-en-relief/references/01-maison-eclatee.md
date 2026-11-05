# 01 · Maison éclatée (Exploded House)

Démo : https://sam1983aing.github.io/flat-to-3d/01-exploded-house/?dir=a · Code et prompt : https://github.com/Sam1983Aing/flat-to-3d/tree/main/01-exploded-house

## Ce qui se passe

Une axonométrie éclatée tracée à l'encre : la maison suspendue en six couches au-dessus de son plan (dalle, murs, vitrages, bardage, chevrons, toiture). En défilant, les couches se posent une à une dans l'ordre du chantier. Puis l'objectif s'élargit, le dessin devient une pièce, la porte vitrée s'ouvre et on monte jusqu'à la mezzanine.

Trois variantes dans le même code : la maison bois (`?dir=a`), une cuisine dont les élévations se replient en pièce (`?dir=b`), un immeuble bois de cinq niveaux qui s'empile autour de son noyau (`?dir=c`).

## Le truc

- L'axonométrie est le vrai modèle vu à travers un objectif de 1,5° à environ 1,26 km. Le dolly zoom la fait passer en perspective.
- Les couches horizontales montent et descendent par niveau ; vitrages et bardage glissent le long de leur mur.
- Un « front de traceur » révèle les traits : rien n'est dessiné au-delà du front, les traits proches sont en couleur d'accent.
- À l'intérieur, ça reste un dessin : arêtes en trois épaisseurs, aplats pâles avec un grain dessiné en code, pas d'ombres.

## Pour un architecte

- Expliquer une composition (planche de concours).
- Très parlant pour une **rénovation énergétique** : mur existant, isolant, nouvelle peau, châssis, toiture isolée, chaque couche avec sa légende. Bon outil pédagogique pour un client Reno+.
- Montrer un système constructif (ossature bois, préfabrication).

## Données nécessaires

Les couches dans l'ordre de pose, leurs épaisseurs et leurs matériaux, le plan du rez, l'arrêt d'entrée de la caméra.

## Pièges

- Le style « dessin » à l'intérieur dispense de meubler finement : c'est un avantage pour une démo rapide.
- Le premier essai de l'auteur garde toute l'idée mais manque de finition.

## Prompt de départ (adapté de l'auteur)

```text
Je veux construire une page web qui défile pour [le bureau X, un constructeur bois,
la rénovation de la maison Y].

L'idée : la page s'ouvre sur une axonométrie éclatée, comme sur une planche de concours.
[La maison] est suspendue en couches au-dessus de son propre plan du rez :
[dalle, murs, vitrages, bardage, chevrons, toiture]. Encre sur papier pâle, légendes
numérotées dans une colonne à droite, et des pointillés de chaque couche jusqu'à sa place.

Le défilement, dans l'ordre :
1. Le chargement est un traceur : un front de plume monte du sol au toit, les traits
   d'abord en couleur d'accent, puis à l'encre, puis les aplats. Le titre glisse.
2. Les couches se posent une à une, dans l'ordre du chantier. Tout ce qui est au-dessus
   descend avec elle. La couche qui se pose passe en couleur d'accent et sa légende
   s'allume.
3. La caméra descend vers [l'entrée]. L'objectif s'élargit jusqu'à ce que le dessin
   devienne une pièce à hauteur d'yeux, et la porte vitrée coulisse.
4. La visite : [la table, le poêle, l'escalier vers la mezzanine], avec une légende à
   chaque arrêt, et une dernière vue à travers la maison.

Ce qui compte pour moi :
- L'axonométrie n'est pas une image. C'est le vrai modèle 3D vu à travers un objectif de
  1,5 degré à environ un kilomètre. Élargir l'objectif pendant que la caméra approche
  (dolly zoom) la transforme en perspective à hauteur d'yeux.
- Dalle, murs et toiture flottent vers le haut. Vitrages et bardage glissent sur le côté,
  depuis leur mur.
- À l'intérieur, ça reste un dessin : arêtes en trois épaisseurs, aplats pâles avec un
  grain dessiné en code. La caméra reste horizontale, et un petit plan en coin montre où
  on se trouve.
- [Les épaisseurs et matériaux viennent du détail joint. N'invente aucune couche.]
- Aspect écran de CAO : papier #f2efe7, encre #1d1c19, une seule couleur d'accent
  ([ambre #e85d04, ou la couleur du bureau]), Chakra Petch pour les titres, IBM Plex Mono
  pour les légendes,
  cadre fin avec repères de coin.
- three.js [0.169] depuis un CDN, fichiers simples, sans compilation. Une seule valeur de
  défilement de 0 à 1 pilote tout. Pas d'image.

Avant d'écrire du code, propose la maison avec des dimensions que je peux me représenter
et le chemin de la caméra, arrêt par arrêt, et attends ma réponse. Ensuite, construis par
étapes. Première étape seulement : le chargement en traceur, les couches qui se posent et
le dolly zoom jusqu'à [l'entrée]. Enregistre-la (vidéo du parcours ou captures à
plusieurs positions) et montre-la-moi avant d'aller plus loin.
```

Difficulté : moyenne. Excellent rapport effet sur effort pour une rénovation.
