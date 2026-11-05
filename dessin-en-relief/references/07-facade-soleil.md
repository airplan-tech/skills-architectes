# 07 · Façade au soleil (Sunlit Elevation)

Démo : https://sam1983aing.github.io/flat-to-3d/07-sunlit-elevation/a-one-door/ · Code et prompt : https://github.com/Sam1983Aing/flat-to-3d/tree/main/07-sunlit-elevation

Technique déjà appliquée par Airplan à un bâtiment réel : https://airplan.be/exemples/cour-des-mineurs-liege (sources dans un dossier interne Airplan, non diffusé).

## Ce qui se passe

L'élévation de la façade avant, à l'encre, avec des hachures à 45° dans chaque ombre. En défilant, la façade prend du relief, puis un balayage change le papier en brique, pierre, zinc et verre, et aucune ombre ne bouge : les hachures étaient les vraies ombres depuis le début. Ensuite le soleil tourne, les ombres glissent sur la brique, la porte s'ouvre et on traverse la maison jusqu'à la cour.

Trois variantes : une maison (`a-one-door/`), une rue de six maisons (`b-the-row/`), un détail de brique au 1/20 où le soleil rase le relief (`c-the-face/`).

## Le truc

- L'élévation est le modèle vu de face à travers un objectif de 2° : il se lit comme un dessin orthogonal.
- Les hachures sont calculées : le soleil part de la convention de dessin (lumière en haut à gauche, à 45°, direction (-1, 1, 1) normalisée). Chaque pixel que la carte d'ombres met à l'ombre reçoit une hachure, donc les ombres dessinées et les vraies ont la même forme.
- Une seule matière par surface, papier ou réelle, choisie pixel par pixel par le balayage.
- Chaque position de caméra est un cadrage (cible, hauteur de cadre, angle) ; la distance suit, et l'angle est interpolé en échelle logarithmique, ce qui permet de passer de 2° à 55° sans saut.

Paramètres utiles en démo : `?skip` saute l'introduction, `?at=300` saute à une position.

## Pour un architecte

- **Façade, intégration à la rue** : l'élévation est le dessin le plus familier des clients et des communes.
- **Ombres** : partir de la convention à 45°, puis montrer le vrai soleil du site (latitude, dates) : c'est ce que nous avons fait pour Liège aux 21 décembre, mars et juin.
- Rénovation de façade : avant et après sur la même élévation.

## Données nécessaires

La façade (baies, saillies, corniche, matériaux), le plan pour la profondeur, l'orientation et la latitude si on fait tourner le vrai soleil.

## Pièges

- Pas de mise en page mobile dans la démo d'origine.
- Sur un bâtiment réel dont on ne connaît pas l'intérieur, arrêter la caméra au seuil (c'est notre choix pour la Cour des Mineurs).
- Les saillies (marquise, balcon, appuis) font tout l'effet des ombres : les modéliser même grossièrement.

## Prompt de départ (adapté de l'auteur)

```text
Je veux construire une page web qui défile pour [une maison à vendre, la rénovation de la
façade de Y].

L'idée : la page s'ouvre sur une élévation de la façade avant, dessinée de face. Encre sur
papier crème, niveaux, cartouche, un personnage pour l'échelle, et des hachures à 45 degrés
dans chaque ombre. Après le chargement, le dessin se trace depuis le sol, puis les hachures
coulent le long de la lumière.

Le défilement, dans l'ordre :
1. Le relief : l'objectif s'ouvre un peu et la caméra tourne, le porche recule et le balcon
   avance.
2. Le soleil : une fine ligne d'accent balaie la façade à 45 degrés et change le papier en
   brique, pierre, zinc et verre. Aucune ombre ne bouge.
3. Puis le soleil passe à [la fin d'après-midi, ou le vrai soleil du site aux 21 décembre,
   mars et juin à la latitude X] et les ombres glissent sur la brique.
4. [Si l'intérieur est connu :] la caméra monte les marches, la porte s'ouvre et elle
   traverse [le hall, le séjour, la cuisine] à hauteur d'yeux jusqu'à [la cour].
   [Sinon :] la caméra recule et la page se referme sur une coupe.
5. Une dernière carte avec les faits et [Prendre rendez-vous].

Ce qui compte pour moi :
- L'élévation est le vrai modèle 3D vu de face à travers un objectif de 2 degrés. Chaque
  position de caméra est un cadrage (cible, hauteur de cadre, angle) et la distance suit,
  pour que l'objectif s'ouvre jusqu'à 55 degrés sans saut.
- Les hachures sont calculées, pas dessinées. Le soleil part de la convention de dessin,
  lumière en haut à gauche à 45 degrés, direction (-1, 1, 1) normalisée. Chaque pixel que
  la carte d'ombres met à l'ombre est hachuré, donc ombres dessinées et vraies ombres ont
  la même forme.
- Une matière par surface, papier ou réelle, choisie pixel par pixel par le balayage.
- [La façade et le volume viennent des données jointes. N'invente aucune baie.]
- Aspect écran de CAO : papier #f2efe7, encre #1d1c19, une seule couleur d'accent
  ([ambre #e85d04, ou la couleur du bureau]), Chakra Petch pour les titres, IBM Plex Mono
  pour les légendes, cadre avec repères de coin,
  lecture du soleil et de l'angle, petit plan qui montre où est la caméra.
- three.js [0.160] et Lenis (défilement doux) depuis un CDN, fichiers simples, sans
  compilation. Pas d'image.

Avant d'écrire du code, propose la façade et le plan avec des dimensions que je peux me
représenter et le chemin de la caméra, arrêt par arrêt, et attends ma réponse. Ensuite,
construis par étapes. Première étape seulement : le dessin qui se trace, le relief et le
balayage. Enregistre-la (vidéo du parcours ou captures à
plusieurs positions) et montre-la-moi avant d'aller plus loin.
```

Difficulté : moyenne. Le meilleur choix pour une première démo sur un bâtiment réel.
