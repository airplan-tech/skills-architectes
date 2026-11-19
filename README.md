# Skills Claude pour architectes

Cinq skills pour Claude, préparées par [Airplan](https://airplan.be) pour la formation « IA pour architectes » du 6 novembre 2026.

Trois mots reviennent dans cette page :

- **Skill** : un fichier d'instructions que Claude suit quand la tâche s'y prête. Elle cadre le travail, fixe les garde-fous et dit quoi rendre.
- **Connecteur** (ou MCP) : le lien entre Claude et un de vos outils, par exemple votre compte Airplan.
- **Agent** : Claude quand il enchaîne plusieurs étapes dans vos outils au lieu de seulement répondre.

| Skill | Ce qu'elle fait |
|---|---|
| [`releve-surfaces-2d`](releve-surfaces-2d/SKILL.md) | Lit vos plans PDF (AutoCAD, BricsCAD, Vectorworks, scans), propose chaque pièce avec sa catégorie, sa surface et sa hauteur, puis vous la faites valider pièce par pièce dans une page de relevé. Les sommes du formulaire statistique sont calculées par le code et, si le connecteur Airplan est branché, écrites dans le projet après votre accord. |
| [`relecture-avant-depot`](relecture-avant-depot/SKILL.md) | Confronte votre formulaire de demande (annexe 4, annexe 6 ou autre) au texte des règlements que vous lui donnez. Rend un tableau, une ligne par règle : article, texte cité mot pour mot, ce que dit le dossier, statut (« respecté d'après les pièces », « à examiner », « non évaluable ») et question pour vous. Liste les écarts et dérogations non déclarés. Sert aussi à préparer la réponse à un courrier d'incomplétude. N'écrit jamais « conforme ». |
| [`dessin-en-relief`](dessin-en-relief/SKILL.md) | Fait d'un plan, d'une coupe ou d'une façade une page web qui défile, où le dessin devient le bâtiment en 3D. Huit techniques, un prompt de départ en cinq blocs, une construction par étapes validées. |
| [`relief-depuis-maquette`](relief-depuis-maquette/SKILL.md) | La même page, construite depuis un bâtiment réel : votre maquette (Pascal, Archicad, Revit, SketchUp, IFC) ou les données publiques (cadastre, PICC, LiDAR). Chaque donnée porte son statut : mesuré, estimé ou inconnu. |
| [`polir-scene-3d`](polir-scene-3d/SKILL.md) | Fait passer la page d'une première version à une page publiable, zone par zone, et la vérifie avant de la mettre en ligne. |

## Installer une skill

- **Claude Desktop ou claude.ai** : téléchargez le zip de la skill dans la [dernière version](https://github.com/airplan-tech/skills-architectes/releases/latest), puis ajoutez-le dans les réglages, rubrique des skills.
- **Claude Code** : copiez le dossier de la skill dans `~/.claude/skills/` (pour toutes vos sessions) ou dans `.claude/skills/` d'un projet.

Claude déclenche une skill d'après sa description. Vous pouvez aussi l'appeler par son nom : « utilise la skill relecture-avant-depot ».

## Exemples publiés

- [Cour des Mineurs 5A, Liège](https://airplan.be/exemples/cour-des-mineurs-liege) : une maison existante reconstituée depuis les données publiques, en relief.
- [Une extension à Namur, en relief](https://airplan.be/exemples/extension-arriere-namur) : un projet d'extension en zone protégée, depuis une maquette Pascal ; page écrite et mise en ligne depuis Claude.

## Avant de vous en servir

- Ces skills ne remplacent pas votre jugement. Elles repèrent, citent et calculent ; vous décidez.
- Ne collez pas les plans ou les données d'un client dans une session d'IA sans son accord (secret professionnel, RGPD).

## Le connecteur Airplan

Deux skills, `relecture-avant-depot` et `releve-surfaces-2d`, lisent votre projet si le connecteur Airplan est branché. Elles fonctionnent aussi sans lui, à partir de vos PDF.

- Pour le brancher : [le tuto pas à pas](https://airplan.be/aide/connecter-agent-ia-mcp), pour Claude et pour ChatGPT.
- Au départ, l'agent est en lecture seule. Pour qu'il écrive dans un formulaire, choisissez l'accès complet dans votre profil Airplan, rubrique « Accès MCP ».
- Ce qu'il permet et ce qu'il ne fait pas : [airplan.be/ia/mcp/ce-que-le-mcp-permet](https://airplan.be/ia/mcp/ce-que-le-mcp-permet).

## Versions

- **1.1, novembre 2026.** Mise à niveau sur le connecteur Airplan en production : lecture seule au départ, formulaire à créer avant lecture, champs à régler dans Airplan. `relecture-avant-depot` lit le bon formulaire (annexe 4, 6 ou autre), les compléments déjà réclamés par la commune et traite le courrier d'incomplétude. `releve-surfaces-2d` refuse de lire des cotes sur un scan trop peu net.
- **1.0, 5 novembre 2026.** Première version, pour la formation du 6 novembre.

Les prochaines skills et nos tests d'IA sur des cas d'architecte : [la newsletter IA pour architectes](https://airplan.be/ia/newsletter).

## Licence

© 2026 Airplan. Ces skills sont publiées sous licence [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/deed.fr) : vous pouvez les utiliser, les modifier et les partager, y compris pour un usage commercial, à condition de citer Airplan ([airplan.be](https://airplan.be)) et d'indiquer si vous les avez modifiées. Texte complet dans [LICENSE](LICENSE).

Les parties reprises de Flat to 3D (en particulier [`dessin-en-relief/references/prompt-type.md`](dessin-en-relief/references/prompt-type.md)) restent aussi sous la licence MIT de leur auteur, dont la notice est jointe dans [`dessin-en-relief/LICENSE-flat-to-3d`](dessin-en-relief/LICENSE-flat-to-3d).

## Crédits

Les skills « dessin en relief » reprennent la méthode « Flat to 3D » de Samnang Aing ([github.com/Sam1983Aing/flat-to-3d](https://github.com/Sam1983Aing/flat-to-3d), licence MIT), adaptée à des architectes et à des bâtiments réels. Données publiques citées : © SPW, CC-BY 4.0 (CADMAP, PICC, LiDAR 2021-2022).
