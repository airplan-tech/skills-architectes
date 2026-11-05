# 04 · Chantier en accéléré (Build Time-Lapse)

Démo : https://sam1983aing.github.io/flat-to-3d/04-build-time-lapse/ · Code et prompt : https://github.com/Sam1983Aing/flat-to-3d/tree/main/04-build-time-lapse

## Ce qui se passe

Une planche de six axonométries de la même maison, de la fouille à la remise des clés, chacune avec ses semaines. On plonge dans la première vignette et le vrai chantier apparaît derrière l'encre. Ensuite, le défilement devient le calendrier : on marche dans le chantier pendant que la maison monte semaine après semaine. À la semaine 18, on traverse une forêt d'étançons sous la toiture fraîchement posée. Le dernier jour, on ressort dans la dernière vignette.

## Le truc

- Chaque pièce de la maison (et le terrain, les ouvrages provisoires, les meubles) connaît sa semaine d'arrivée et de départ. Une seule variable décide ce qui existe.
- Les six vignettes sont le même modèle vivant, chacune à sa semaine, rendue dans son propre rectangle d'écran au téléobjectif (2°).
- La plongée est un dolly zoom inversé de 2° à 50° jusqu'à hauteur d'yeux.
- La lumière suit les semaines : matin sur la fouille, soleil bas entre les étançons, fin d'après-midi à la remise des clés.

Paramètres utiles en démo : `?v=12.5` saute à une position (en hauteurs d'écran), `?still` saute le chargement.

## Pour un architecte

- **Phasage** : montrer à un client ou à une commune l'ordre des travaux.
- **Chantier-école, chantier participatif** : raconter les étapes et ce qu'on y apprend.
- Pédagogie client : pourquoi le gros œuvre prend du temps, pourquoi on attend avant les finitions.

## Données nécessaires

La liste des phases avec leurs semaines (un seul tableau qui pilote tout), le bâtiment par éléments, le chemin de la caméra dans le chantier.

## Pièges

- C'est la plus complexe des sept selon l'auteur. Le premier essai reproduit bien la planche et la fin, mais un vrai accéléré demande beaucoup de polissage.
- Un planning faux décrédibilise : partir du vrai planning ou annoncer qu'il est indicatif.

## Prompt de départ (adapté de l'auteur)

```text
Je veux construire une page web qui défile pour [une entreprise générale, un chantier-école,
le projet Y], autour d'une [maison en béton sur un terrain en pente].

L'idée : la page s'ouvre sur une planche de phasage. Six petites axonométries au trait
de la même maison, une par étape : [fouille et fondations, niveau inférieur, dalle du rez,
murs, toiture, vitrages et finitions], chacune avec ses semaines. À côté du titre, le
planning, une barre par phase.

Le défilement, dans l'ordre :
1. Le chargement : le planning trace ses barres. Puis les six dessins se tracent ensemble,
   traits frais en couleur d'accent qui refroidissent au noir.
2. Le papier zoome dans le dessin 01 jusqu'à remplir l'écran. Derrière l'encre, le vrai
   chantier apparaît dans l'ordre de construction, avec une bande en couleur d'accent à la
   frontière.
3. L'objectif s'ouvre de 2 à 50 degrés pendant que le cadre tient, jusqu'à hauteur d'yeux
   au bord de la fouille.
4. Le défilement devient le calendrier. La maison monte semaine après semaine pendant que
   la caméra marche [vers le jardin, sur un escalier d'échafaudage, sur la terrasse].
   Le remblai monte du fond de la fouille.
5. À [la semaine 18], la caméra traverse une forêt d'étançons sous la toiture fraîchement posée, le
   soleil passant entre eux.
6. Les finitions et les meubles arrivent autour de la caméra : [la mezzanine, la cuisine,
   le séjour], jusqu'à la remise des clés.
7. Le jour de la remise, la caméra recule dans le dessin 06, la maison redevient dessin
   dans l'ordre inverse, et la planche revient avec toutes les barres pleines et
   [Visiter le chantier].

Ce qui compte pour moi :
- Les dessins sont le modèle 3D lui-même, tracés en direct par un shader d'arêtes à
  travers un objectif de 2 degrés, chaque vignette à sa semaine. Chaque pièce porte la
  semaine où elle est construite, donc un seul nombre décide de ce qui existe.
- Un seul tableau de phases pilote le planning, les dessins et le chantier.
  [Les phases et leurs semaines viennent du planning joint.]
- Aspect écran de CAO : papier #f2efe7, encre #1d1c19, une seule couleur d'accent
  ([ambre #e85d04, ou la couleur du bureau]), Chakra Petch pour les titres, IBM Plex Mono
  pour les légendes, repères de coin, une
  pastille de semaine et le planning ancré en bas à gauche avec une ligne « aujourd'hui ».
- three.js [0.160] depuis un CDN, fichiers simples, sans compilation. Pas d'image.

Avant d'écrire du code, propose la maison avec des dimensions que je peux me représenter,
la semaine de chaque phase et le chemin de la caméra, arrêt par arrêt, et attends ma
réponse. Ensuite, construis par étapes. Première étape seulement : le chargement, la
planche qui se dessine et la plongée dans le dessin 01 jusqu'à hauteur d'yeux.
Enregistre-la (vidéo du parcours ou captures à
plusieurs positions) et montre-la-moi avant d'aller plus loin.
```

Difficulté : très élevée. À réserver à un projet où le phasage est l'argument principal.
