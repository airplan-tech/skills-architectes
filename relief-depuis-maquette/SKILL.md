---
name: relief-depuis-maquette
description: Construit une page « dessin en relief » (Flat to 3D) à partir d'un bâtiment réel plutôt que d'une maison inventée, en partant de la maquette de l'architecte (Pascal, Archicad, Revit, SketchUp, export IFC, glTF ou OBJ) ou de données publiques (cadastre, PICC, LiDAR du SPW, latitude pour le soleil). À utiliser quand un architecte veut animer le plan, la coupe ou la façade de son propre projet ou d'un bâtiment existant, quand la page doit rester fidèle aux mesures, ou quand il faut afficher ce qui est mesuré, estimé ou inconnu. Complète la skill `dessin-en-relief`.
---

# Relief depuis une maquette réelle

Les démos de Samnang Aing montrent des maisons inventées. Sur un projet d'architecte, l'effet n'a de valeur que si le bâtiment est le bon. Cette skill fait passer la page d'un exercice de style à un outil de présentation honnête.

Exemple de référence : la page « Cour des Mineurs en relief » (https://airplan.be/exemples/cour-des-mineurs-liege), construite depuis une maquette reconstituée avec le cadastre, le PICC et le LiDAR du SPW, puis la page méthode (https://airplan.be/exemples/cour-des-mineurs-liege/methode). Sources : dossier interne Airplan (données, scripts d'assemblage, gabarit de page), non diffusé.

Deuxième exemple, un projet : « Une extension à Namur, en relief » (https://airplan.be/exemples/extension-arriere-namur), construite depuis l'export JSON d'une maquette Pascal. La façade arrière, jamais vue, y est déduite de la façade à rue et annoncée comme supposée ; le lieu est anonymisé.

## Règles

1. **Le fichier de la maquette est la source unique.** La page lit ses dimensions dans les données, jamais dans la conversation. Une nouvelle version de la maquette, on relance le script qui assemble la page.
2. **Chaque donnée a un statut** : mesuré (avec sa source), estimé (avec sa marge), ou inconnu.
3. **Rien d'inventé en silence.** Une façade jamais vue est modélisée sans baie et annoncée comme telle. Un intérieur inconnu n'est pas visité.
4. **La page dit ses limites.** Elle se termine par un bloc « Mesuré, estimé, inconnu » et une ligne de sources. Elle ne se présente jamais comme un relevé.
5. **Les données publiques se citent** : « Données © SPW, CC-BY 4.0 (CADMAP, PICC, LiDAR) ». Une photo d'un tiers ne se publie qu'avec son crédit, et seulement si on y est autorisé.

## Déroulé

### 1. Identifier la source du bâtiment

| Source | Ce qu'on en tire | Comment |
|---|---|---|
| Maquette Pascal | Murs, baies, toitures, niveaux en JSON | Export de la scène, ou le fichier de description envoyé à Pascal ; c'est ce qu'on a fait pour la Cour des Mineurs |
| Archicad, Revit, SketchUp | Le volume complet | Un export 3D lisible par three.js (glTF/GLB de préférence, sinon OBJ ; IFC avec la bibliothèque web-ifc). Les formats proposés dépendent du logiciel et de sa version : vérifier avant la séance |
| Plans 2D seulement | Emprises, niveaux, baies | Saisir les cotes dans un fichier de données (JSON ou tableau), puis générer les volumes en code |
| Données publiques (Wallonie) | Parcelle, emprise, hauteurs de corniche, relief, toiture | Cadastre (CADMAP), PICC, LiDAR MNT/MNS 2021-2022 du SPW ; via le MCP Airplan quand il sera disponible |
| Photos | Baies, matériaux, saillies | Lecture sur image : statut « estimé », avec marge |

Un modèle importé (glTF) va à l'encontre du « pas de modèle » des démos d'origine. Pour un projet réel, la fidélité passe avant : garder la géométrie importée, mais dessiner les matières en code pour rester léger.

### 2. Construire la fiche des données

Une ligne par donnée, chacune avec son statut (mesuré, estimé, inconnu) :

| Donnée | Valeur | Statut et source |
|---|---|---|
| Emprise (longueur × largeur) | | |
| Niveaux et hauteurs (rez, étage, combles) | | |
| Forme de la toiture, pentes, faîte, corniches | | |
| Baies par façade (position, taille, forme) | | |
| Matériaux par façade | | |
| Terrain : pente, niveaux autour du bâtiment | | |
| Orientation (nord), latitude pour le soleil | | |
| Intérieur | | |

Exemple tiré de la Cour des Mineurs :

| Donnée | Valeur | Statut |
|---|---|---|
| Emprise de la maison | 9,83 × 6,29 m | Mesuré (PICC) |
| Corniches | 115,21 m (SE), 116,93 m (NO) | Mesuré (PICC) |
| Toiture | Comble brisé, dessus à 117,36 m | Mesuré (MNS LiDAR) |
| Baies de la façade sud-est | ± 0,3 à 0,5 m | Estimé (photo) |
| Façades nord-ouest et sud-ouest | Sans baie | Inconnu (jamais vues) |
| Intérieur | Non modélisé | Inconnu |

### 3. Préparer les données pour la page

- Écrire un petit script qui lit la maquette (ou l'export) et produit un seul objet de données injecté dans le gabarit HTML (comme `build_page.py`). Garder le gabarit et les données séparés.
- Ramener le bâtiment dans un repère simple : origine au centre du bâtiment, 1 unité = 1 m, axe vertical = altitude moins une altitude de référence. Noter la rotation par rapport au nord.
- Terrain : une grille d'altitudes (MNT à 1 m) suffit, aplanie sous le bâtiment.
- Soleil : calculer la position réelle (latitude, longitude, dates et heures choisies) avec une bibliothèque à version figée (SunCalc, par exemple) plutôt que de la dessiner à vue. Valeurs de contrôle à Liège (50,64° nord), hauteur du soleil à midi solaire : environ 16° le 21 décembre, 39° le 21 mars, 63° le 21 juin. Pour une élévation, commencer par le soleil de convention (45°, en haut à gauche), puis passer au vrai soleil.

### 4. Choisir la technique et écrire le prompt

Suivre la skill `dessin-en-relief` si elle est installée (sinon, décrire le dessin, la séquence, les règles, et demander une proposition avant le code). Ajouter au bloc « ce qui compte » du prompt :

> Les dimensions viennent uniquement du fichier de données joint. N'invente aucune pièce, aucune baie, aucun élément. Ce qui manque reste simple et sera signalé dans la page.

Pour un bâtiment existant mal connu, préférer 07 (façade) : c'est la vue qu'on connaît le mieux depuis l'extérieur. Une coupe (02, 03) seulement si les niveaux sont mesurés, et sans visite intérieure.

### 5. Écrire le bloc final de la page

Dernière carte de la page :
- **Mesuré** : la liste, avec les sources ;
- **Estimé** : la liste, avec les marges et ce qui a servi à estimer ;
- **Inconnu** : la liste, et ce qu'il faudrait pour savoir (visite, relevé, photos) ;
- une ligne de sources et de crédits (données, technique Flat to 3D de Samnang Aing, licence MIT si du code est repris).

### 6. Contrôler contre la réalité

- Comparer un rendu de la page à une photo prise du même point de vue : même nombre de baies, même pente de toit, même rapport hauteur/largeur.
- Tracer l'élévation depuis les données et y reporter les altitudes cibles (corniches, faîte) : un écart visible doit être expliqué ou corrigé.
- Faire relire la page par l'architecte avant toute diffusion.

## Ce qu'on livre

- Le script d'assemblage, le gabarit et le fichier de données, dans un dossier à part.
- La page générée.
- Une note (LISEZMOI) : sources, statut de chaque donnée, comment régénérer la page.
