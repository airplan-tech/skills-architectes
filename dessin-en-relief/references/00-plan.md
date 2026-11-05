# 00 · Plan qui se lève (Casa Serra)

Origine de toute la série. Démo : https://sam1983aing.github.io/casa-serra/ · Version polie : https://sam1983aing.github.io/lintel-live/ · Prompt d'origine : https://github.com/Sam1983Aing/casa-serra/blob/main/starter-prompt.md

## Ce qui se passe

La page s'ouvre sur un plan d'étage imprimé : encre noire, noms des pièces, cotes. En défilant, les murs sortent du dessin, la caméra descend jusqu'à la porte d'entrée et visite les pièces à hauteur d'yeux. Chaque pièce reste un dessin au trait jusqu'à ce que la caméra y arrive, puis les matières la balaient.

## Le truc

Le plan est le modèle 3D coupé à environ 1,20 m, vu d'en haut au téléobjectif. Monter le plan de coupe, c'est faire pousser les murs.

## Pour un architecte

- Présenter un aménagement intérieur ou un programme à un client.
- Montrer l'enchaînement des pièces, les vues traversantes.
- Ne convient que si l'intérieur est connu (projet dessiné, ou relevé intérieur).

## Données nécessaires

Plan avec épaisseurs de murs, baies (allèges et hauteurs), hauteur sous plafond, mobilier principal, ordre de visite.

## Pièges

- La version d'origine utilisait des textures photo (Poly Haven) : environ 39 Mo de textures sur ordinateur et 13 Mo sur téléphone selon le README, « près de 38 Mo » dans la vidéo. L'auteur les a retirées ensuite au profit de matières dessinées en code (moins de 1 Mo). Demander d'emblée des matières en code.
- La caméra doit entrer et circuler, pas tourner autour du bâtiment.
- L'IA a ajouté des pièces quand l'auteur a demandé une maison plus luxueuse : sur un projet réel, l'interdire.
- Le plan d'origine a demandé environ 70 prompts sur deux semaines. Le prompt de départ donne une base en une heure : voir Casa Larga, le résultat d'un seul essai, tel quel (https://sam1983aing.github.io/casa-larga/, code : https://github.com/Sam1983Aing/casa-larga). Vidéo de fabrication de 8 minutes : https://youtu.be/rKv4PrtBkb8.

## Prompt de départ (adapté de l'auteur)

```text
Je veux construire une page web qui défile pour [le bureau X, le projet de la maison Y].

L'idée : la page s'ouvre sur un plan d'étage à plat, comme une feuille imprimée par un
architecte. Encre noire sur papier, noms des pièces, cotes. Rien n'a l'air 3D. Quand on
fait défiler, les murs sortent du dessin, la caméra descend jusqu'à la porte d'entrée et
traverse [les pièces, dans l'ordre] à hauteur d'yeux. Chaque pièce reste un dessin au
trait jusqu'à ce que la caméra y arrive, puis les vraies matières la balaient.

Ce qui compte pour moi :
- Le plan n'est pas une image. C'est le vrai modèle 3D, coupé à environ 1,20 m et vu
  d'en haut à travers un objectif très long. Le dessin et le bâtiment sont la même chose.
- La caméra entre et circule de pièce en pièce. Elle ne tourne pas autour du bâtiment.
- [Les dimensions viennent du plan joint. N'invente aucune pièce ni aucune baie.]
- Lumière de [fin d'après-midi], mobilier réel, matières dessinées en code (pas de
  texture photo).
- three.js [0.160] depuis un CDN, fichiers simples, sans compilation. Une seule valeur
  de défilement de 0 à 1 pilote tout.

Avant d'écrire du code, propose le plan avec des dimensions que je peux me représenter et
le chemin de la caméra, arrêt par arrêt. Donne-moi deux ou trois directions et attends ma
réponse. Ensuite, construis par étapes. Première étape seulement : la feuille du plan,
les murs qui montent et la marche jusqu'à la première pièce. Enregistre-la (vidéo du parcours ou captures à
plusieurs positions) et montre-la-moi avant d'aller plus loin.
```

Écart volontaire avec le prompt d'origine : il demandait three.js, GSAP ScrollTrigger et Lenis avec des textures CC0. Ici, three.js seul et des matières en code, pour un fichier léger et un artefact en un seul fichier. L'auteur a lui-même retiré les textures ensuite.

Difficulté : moyenne. À choisir seulement si l'intérieur est connu : les premiers essais rendent des pièces vides.
