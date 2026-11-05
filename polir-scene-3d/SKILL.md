---
name: polir-scene-3d
description: Fait passer une page 3D three.js (dessin en relief, Flat to 3D, visite d'un projet) d'une première version brute à une page publiable, par une boucle de polissage zone par zone, puis la vérifie avant publication (WebGL, mobile, poids, chemins, licences, honnêteté des données). À utiliser après une première version produite avec `dessin-en-relief` ou `relief-depuis-maquette`, quand l'architecte dit que « c'est vide », « ça fait dessin animé », « trop lourd », « pas réaliste », veut ajouter un objet, changer le parcours de la caméra ou mettre la page en ligne.
---

# Polir une scène 3D

Méthode tirée du récit de Samnang Aing (de son plan viral à la version « Lintel ») et de notre propre mise en ligne de la Cour des Mineurs. Il n'y a pas de truc magique : on regarde, on dit ce qu'on veut, on juge, on recommence, zone par zone.

## Règles

1. **Une zone à la fois.** La façade, puis l'entrée, puis le séjour. L'IA se concentre mieux sur une partie précise.
2. **Matières en code, pas en photo.** Les textures scannées (type Poly Haven) se déforment sur les formes courbes, se répètent, se règlent mal et alourdissent la page. L'auteur est passé de près de 38 Mo à moins de 1 Mo en les remplaçant par des matières dessinées en code, et tout est devenu réglable.
3. **Ne polir que ce que la caméra voit de près.** Une pièce jamais visitée reste brute.
4. **Une image de référence pour tout nouvel objet.** Sans référence, l'IA invente, et on finit souvent par jeter.
5. **L'architecte juge.** L'IA met un meuble devant une fenêtre, ajoute des pièces, du décor. Chaque tour se termine par une relecture d'architecte, pas seulement esthétique.
6. **Sur un projet réel, polir ne veut pas dire inventer.** On peut améliorer la lumière, le grain, les matières connues. On n'ajoute ni baie, ni pièce, ni élément absent des données (voir `relief-depuis-maquette`).

## La boucle

Pour chaque zone :

1. **Placer la page à la position voulue** (paramètre `?p=0.6`, ou une fonction du type `window.__page.go(p)` ; `window.__relief.go(p)` sur notre page Cour des Mineurs) et faire une capture.
2. **Dire en langage simple** ce qui plaît et ce qui ne plaît pas. Exemple : « Ajoute de la texture au mur de façade et rends-le plus réaliste ; garde la couleur de la brique. »
3. **Montrer le détail** : joindre la capture de la zone, entourée ou recadrée, avec la demande précise.
4. **Pour un objet nouveau** : joindre une image de référence (photo, catalogue, croquis).
5. **Juger le résultat** sur une nouvelle capture, au même cadrage, ou sur l'enregistrement du parcours. Comparer avant et après. L'auteur note chaque pièce sur 10 à partir des enregistrements : une note écrite évite de tourner en rond.
6. **Recommencer** jusqu'à satisfaction, puis passer à la zone suivante. Compter plusieurs tours par zone.

Entre deux zones, revoir **le chemin de la caméra** : rate-t-il un espace intéressant (l'auteur a découvert une cave à vin que la caméra ignorait) ? S'arrête-t-il assez longtemps là où il y a quelque chose à voir ?

Interaction simple qui ajoute beaucoup : le choix du moment de la journée (matin, midi, heure dorée, nuit), ou des dates d'ensoleillement pour un projet réel.

**Savoir s'arrêter.** Fixer avant de commencer ce qui doit être fini pour publier. Le reste attendra.

## Liste de contrôle avant publication

### Technique

- [ ] La page s'ouvre dans un vrai navigateur avec écran. Un navigateur sans écran n'a souvent pas de WebGL ; un onglet masqué ralentit ou fige le rendu.
- [ ] Captures à au moins cinq positions du défilement (début, ouverture de l'objectif, balayage, visite, fin).
- [ ] Mobile : mesurer la largeur réelle de la page (pas de défilement horizontal) à 320, 375 et 390 px avec une densité d'écran de 2. Une capture ne suffit pas.
- [ ] Une solution de repli si l'appareil ne fait pas tourner la 3D : image fixe et court extrait vidéo du parcours, comme sur la démo Casa Serra.
- [ ] Le mouvement est réduit quand l'utilisateur l'a demandé à son système (`prefers-reduced-motion`), et les légendes restent lisibles sans la 3D.
- [ ] Poids de la page mesuré. Objectif : quelques centaines de Ko hors bibliothèques.
- [ ] Bibliothèques chargées depuis un CDN avec une version exacte (three.js 0.160, par exemple), jamais « la dernière ».
- [ ] Médias en chemins absolus sur un site. Une adresse servie sans barre finale casse les chemins relatifs (vécu sur airplan.be : vidéo introuvable).
- [ ] Aucune erreur dans la console.

### Honnêteté et droits

- [ ] Le bloc « Mesuré, estimé, inconnu » est présent et à jour (projet réel).
- [ ] La ligne de sources cite les données (par exemple « Données © SPW, CC-BY 4.0 »), la technique (Flat to 3D, Samnang Aing) et la licence MIT si du code est repris.
- [ ] Aucune photo ou image de tiers sans crédit et sans droit de l'utiliser. Une image qui ne montre pas le bâtiment n'a rien à faire sur la page (vécu : une carte postale ancienne retirée parce qu'elle ne montrait pas la maison).
- [ ] Les images générées par IA sont annoncées comme telles, avec ce qu'elles peuvent inventer.
- [ ] Pour un projet en cours (concours, appel à intérêts, permis non accordé) : accord du maître d'ouvrage ou de l'autorité avant diffusion, page non indexée si besoin.

### Relecture d'architecte

- [ ] Rien devant une fenêtre, pas de porte qui ouvre dans un mur, des hauteurs d'allège plausibles.
- [ ] Les ombres partent du bon côté pour l'orientation réelle.
- [ ] Les légendes disent ce qu'on voit, sans promesse (« conforme », « validé ») que la page ne peut pas tenir.

## Ce qu'on livre

- La page polie et la liste des zones travaillées.
- Les captures avant et après de chaque zone : utiles pour expliquer la méthode en formation.
- La liste de contrôle cochée.
