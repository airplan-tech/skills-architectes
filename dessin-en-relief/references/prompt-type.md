# Le prompt de départ en cinq blocs, et la fiche des données

Structure commune aux sept prompts de Samnang Aing du dépôt flat-to-3d (licence MIT), traduite et adaptée pour des architectes. Le prompt d'origine du plan (Casa Serra) est plus court : il décrit le défilement dans l'idée, sans liste numérotée.

## 1. Les cinq blocs

### Bloc 1. Le sujet

> Je veux construire une page web qui défile pour [un bureau d'architecture, la maison X, le projet de rénovation de Y].

Une phrase. Elle règle le ton et l'appel à l'action de la fin (« Prendre rendez-vous », « Découvrir le projet »).

### Bloc 2. L'idée : le dessin de départ

Décrire le dessin comme on le décrirait à un dessinateur :
- type et échelle (plan au 1/100, coupe A-A, élévation de la façade avant, axonométrie éclatée) ;
- conventions : poché noir dans la coupe, hachures du terrain, hachures d'ombre à 45°, cotes, niveaux, noms des pièces, cartouche, flèche du nord, échelle graphique ;
- papier et encre ;
- et toujours : « Rien n'a l'air 3D. »

### Bloc 3. Le défilement, dans l'ordre

Une liste numérotée de 4 à 7 étapes. Le squelette type :
1. le chargement (un traceur qui dessine, un plan de repérage) ;
2. le dessin qui se trace ;
3. l'ouverture de l'objectif (le dessin prend de la profondeur) ;
4. le balayage qui change l'encre en matières ;
5. la visite à hauteur d'yeux, arrêt par arrêt, avec une légende à chaque arrêt ;
6. le retour au dessin ;
7. la carte de fin (les faits du projet, un bouton).

### Bloc 4. Ce qui compte pour moi

Les règles qui font que ça marche. Les reprendre presque telles quelles :
- (Pour 00, 01, 02, 03, 04 et 07. Les techniques 05 et 06 reposent sur un tableau de phases et sur un changement d'échelle.) « Le dessin n'est pas une image. C'est le vrai modèle 3D vu à travers un objectif de [1,5 à 2]° placé à [environ 1 km] (0,12° à 12 km pour une coupe très plate), ce qui le fait lire comme un dessin. Ouvrir l'objectif en rapprochant la caméra (dolly zoom) le transforme en perspective à hauteur d'yeux. »
- « La caméra ne coupe jamais. »
- La charte, qui fait beaucoup de l'effet professionnel : aspect écran de CAO, papier #f2efe7, encre #1d1c19, une seule couleur d'accent (ambre #e85d04 chez l'auteur), Chakra Petch pour les titres, IBM Plex Mono pour les légendes, repères de coin, cartouche, une petite vue de repérage qui montre où est la caméra.
- Le socle : « three.js [0.160] depuis un CDN, fichiers simples, sans compilation. Une seule valeur de défilement de 0 à 1 pilote tout (notre recommandation). Pas d'image : toutes les matières sont dessinées en code. »
- Pour un bâtiment réel : « Les dimensions viennent de [la maquette, les données jointes]. N'invente aucune pièce, aucune baie. Ce qui manque reste simple et sera signalé dans la page. »

### Bloc 5. Proposer, puis la première étape seulement

À recopier sans le raccourcir :

> Avant d'écrire du code, propose [le bâtiment] avec des dimensions que je peux me représenter et le chemin de la caméra, arrêt par arrêt, et attends ma réponse. Ensuite, construis par étapes. Première étape seulement : [deux ou trois choses]. Enregistre-la (vidéo du parcours ou captures à plusieurs positions) et montre-la-moi avant d'aller plus loin.

L'auteur le dit lui-même : ce dernier bloc compte autant que l'idée. Sans lui, on reçoit une page finie qu'on n'a pas choisie.

## 2. Fiche « Données du bâtiment »

À remplir avant le prompt. Chaque ligne porte sa source, ou la mention « estimé » ou « absent ».

| Donnée | Valeur | Source ou statut |
|---|---|---|
| Emprise (longueur × largeur) | | |
| Niveaux et hauteurs (rez, étage, combles) | | |
| Forme de la toiture, pentes, faîte, corniches | | |
| Baies par façade (position, taille, forme) | | |
| Matériaux par façade | | |
| Terrain : pente, niveaux autour du bâtiment | | |
| Orientation (nord), latitude pour le soleil | | |
| Pièces visitées par la caméra (si intérieur connu) | | |
| Ce qui est inconnu | | |

## 3. Variantes utiles

- **Session neuve pour un participant** : coller le prompt dans Claude (claude.ai ou Claude Desktop) et demander un artefact. Remplacer alors « fichiers simples » par « un seul fichier HTML, three.js chargé depuis jsdelivr ou cdnjs avec une version exacte ». Prévoir une heure.
- **Repartir du code de l'auteur** : pour les démos qu'il a le plus travaillées (02, 04, 06), il conseille de reprendre son code plutôt que de partir du prompt. Garder la notice de licence MIT (Copyright (c) 2026 Samnang Aing) dans le code repris.
- **Projet réel** : joindre les données (fichier de la maquette, export, tableau ci-dessus) et ajouter au bloc 4 la phrase « N'invente aucune pièce, aucune baie ».
