---
name: dessin-en-relief
description: Transforme un dessin d'architecte (plan, coupe, façade, axonométrie éclatée, planche de chantier, planning, maquette blanche) en page web qui défile, où le dessin devient le bâtiment en 3D (three.js), d'après la méthode « Flat to 3D » de Samnang Aing. À utiliser quand un architecte veut « faire sortir son plan du papier », animer une coupe ou une façade, présenter un projet à un client, un jury ou une commune avec une page 3D, ou reproduire une des 7 techniques Flat to 3D (page qui défile, scrollytelling, animation au défilement). Choisit la technique, rassemble les données du bâtiment, rédige le prompt de départ en cinq blocs, fait proposer avant de coder et construit par étapes validées.
---

# Dessin en relief

Une page web s'ouvre sur un dessin d'architecte qui a l'air plat. En la faisant défiler, le dessin devient le bâtiment en 3D et la caméra entre dedans.

Le principe qui rend presque tout possible : **le dessin n'est pas une image. C'est le vrai modèle 3D vu à travers un objectif très long** (de 0,12° à 2°, la caméra à 1 km ou plus, 12 km pour 0,12°), ce qui écrase la perspective. Ouvrir l'objectif en rapprochant la caméra (dolly zoom : on élargit l'angle en avançant, le cadre reste le même) fait revenir la perspective sans coupure. Le dessin et le bâtiment sont le même objet. C'est le cas dans cinq des sept démos et dans le plan d'origine ; 05 repose sur un tableau de phases, 06 sur un changement d'échelle.

Méthode reprise du dépôt public de Samnang Aing (licence MIT) : https://github.com/Sam1983Aing/flat-to-3d. Si on reprend son code, garder sa notice de licence MIT (Copyright (c) 2026 Samnang Aing) ; reprendre seulement l'idée n'impose rien, mais le citer reste correct.

## Règles

1. **Ce n'est pas une pièce de permis.** C'est de la communication (client, jury, réunion de projet, site du bureau). Ne jamais présenter la page comme un relevé ou un plan coté.
2. **Un bâtiment réel se dessine depuis ses données.** Si l'architecte a une maquette (Pascal, Archicad, Revit, SketchUp, IFC) ou des données (cadastre, PICC, LiDAR), utiliser la skill `relief-depuis-maquette`. N'inventer une maison que si l'architecte le demande explicitement, et le dire dans la page.
3. **Faire proposer avant de coder.** Toujours. Sans cette étape, on livre une page que l'architecte n'a pas choisie.
4. **Construire par étapes.** La première étape ne contient que 2 ou 3 choses (par exemple : le dessin qui se trace, l'ouverture de l'objectif, le balayage). Montrer, attendre la validation, continuer.
5. **Pas d'intérieur inventé sur un projet réel.** Si l'intérieur n'est pas connu, la caméra reste dehors ou s'arrête au seuil.
6. **Afficher les limites dans la page** : ce qui est mesuré, ce qui est estimé, ce qui est absent (voir `relief-depuis-maquette`).
7. **Confidentialité.** Ne pas coller les plans d'un client dans une session d'IA sans son accord (secret professionnel, RGPD). Pour une formation ou un atelier, travailler sur une maison fictive ou un bâtiment public.

## Déroulé

### 1. Comprendre la demande (une question à la fois si besoin)

- Quel dessin l'architecte veut-il « faire sortir du papier » ? Si ce n'est pas clair, proposer les techniques de la table ci-dessous selon ce qu'il veut montrer.
- Pour qui ? Client particulier, jury de concours, commune, site du bureau. Ça règle le ton et le niveau de finition.
- Sur quel bâtiment ? Réel (avec quelles données) ou fictif (pour une démo).
- Où la page doit-elle vivre ? Un artefact Claude (un seul fichier HTML, idéal pour une démo ou une formation, faisable sur claude.ai), un dossier local avec Claude Code (plusieurs fichiers, petit serveur local), le site du bureau.

### 2. Choisir la technique

| Ce que l'architecte veut montrer | Technique | Fiche |
|---|---|---|
| Un aménagement intérieur, un programme | 00 Plan qui se lève | `references/00-plan.md` |
| La composition, une rénovation par couches (existant, isolant, nouvelle peau) | 01 Maison éclatée | `references/01-maison-eclatee.md` |
| Un terrain en pente, l'ensoleillement | 02 Coupe balayée | `references/02-coupe-balayee.md` |
| Des niveaux, des demi-niveaux, un escalier | 03 Coupe ouverte | `references/03-coupe-ouverte.md` |
| Le phasage, un chantier-école, la pédagogie client | 04 Chantier en accéléré | `references/04-chantier-accelere.md` |
| L'échéancier, la préfabrication | 05 Planning qui construit | `references/05-planning-construit.md` |
| L'effet « concours », une maquette blanche | 06 Maquette en carton | `references/06-maquette-carton.md` |
| Une façade, ses ombres, son intégration | 07 Façade au soleil | `references/07-facade-soleil.md` |

Lire la fiche choisie avant d'écrire le prompt : elle donne le truc technique, les pièges et un prompt de départ en français.

Pour une première démo, recommander 07 (façade) ou 01 (maison éclatée) : ce sont les plus lisibles et ils ne demandent pas d'intérieur meublé, que les premiers essais rendent vide. 00 (plan) seulement si l'intérieur est connu et qu'on a du temps pour le polir.

### 3. Rassembler les données

Remplir la fiche « Données du bâtiment » (`references/prompt-type.md`, section 2). Pour un bâtiment réel, chaque cote doit venir d'une source nommée. Ce qui manque est marqué « à estimer » ou « absent », jamais inventé en silence.

### 4. Écrire le prompt de départ en cinq blocs

Partir du prompt de la fiche de la technique et remplacer les crochets. La structure est toujours la même (détail dans `references/prompt-type.md`) :

1. le sujet ;
2. l'idée : le dessin décrit comme un architecte le décrirait (échelle, poché, hachures, cotes, noms des pièces, cartouche) ;
3. le défilement, en 4 à 7 étapes numérotées ;
4. ce qui compte : le principe du téléobjectif, la caméra qui ne coupe jamais, la charte, les bibliothèques et versions, « pas d'image » ;
5. proposer avant de coder, puis la première étape seulement.

Si on construit soi-même (Claude Code), on suit ce prompt comme un cahier des charges. Si un participant le colle dans une session neuve, il doit garder le bloc 5 intact.

### 5. Proposer, puis attendre

Avant tout code, présenter à l'architecte :
- le bâtiment avec des dimensions qu'il peut se représenter (et leur source) ;
- le chemin de la caméra, arrêt par arrêt ;
- deux ou trois directions si le sujet s'y prête ;
- ce qui sera estimé ou laissé vide.

Attendre sa réponse.

### 6. Construire par étapes

- Socle technique : three.js chargé depuis un CDN (un serveur public de bibliothèques), version figée (0.160 ou 0.169 comme l'auteur), HTML, CSS et JavaScript simples, sans compilation. Notre recommandation : une seule valeur de défilement de 0 à 1 pilote tout (chez l'auteur, c'est parfois une semaine de chantier ou une position en pixels). Matières dessinées en code, pas de texture photo (voir `polir-scene-3d`).
- Pour un artefact Claude : tout dans un seul fichier, scripts depuis cdnjs ou jsdelivr avec une version exacte.
- Ajouter un moyen de placer la page à une position donnée (par exemple `?p=0.6` comme dans la démo 01, ou une fonction du type `window.__page.go(p)` ; notre page Cour des Mineurs utilise `window.__relief.go(p)`) : indispensable pour tester et faire des captures.
- Après chaque étape : vérifier dans un vrai navigateur avec écran (WebGL, la 3D du navigateur), enregistrer le parcours ou faire des captures à plusieurs positions, les montrer, attendre.

### 7. Polir, vérifier, publier

Passer à la skill `polir-scene-3d` pour la boucle de polissage et la liste de contrôle avant publication.

## Ce qu'on livre

- La page (fichier HTML ou dossier), lisible sur un ordinateur portable, avec une mise en page mobile si possible.
- Une ligne de sources en bas de page : données utilisées, ce qui est estimé, crédit de la technique.
- Le prompt de départ utilisé, enregistré à côté de la page, pour pouvoir refaire.

## Ce qu'il faut dire à l'architecte

- Une première version prend environ une heure. Une page publiable demande des dizaines de tours de polissage.
- Deux essais du même prompt ne donnent jamais la même page.
- L'IA peut inventer des pièces, mettre un meuble devant une fenêtre, ajouter du décor. Il est le seul à juger.
