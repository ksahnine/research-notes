# research-notes

Notes de recherche personnelles : synthèses de veille technologique et financière, construites à
partir de sources publiques citées et datées.

Ce dépôt n'est pas un blog. C'est un atelier : chaque dossier est une enquête terminée à une date
donnée, conservée telle quelle. Les notes ne sont pas réécrites après coup — une note périmée est
une information en soi.

## Index

| Date | Dossier | Thème | Notes | Résumé |
|---|---|---|---|---|
| 2026-11-14 | [`2026-11-14_pratiques_ia4archi/`](2026-11-14_pratiques_ia4archi/) | Agents de codage & architecture | [`reddit.md`](2026-11-14_pratiques_ia4archi/reddit.md), [`social-web.md`](2026-11-14_pratiques_ia4archi/social-web.md) | Ce que disent Reddit, Hacker News et les sources sociales/web (2025–2026) sur l'usage des agents de codage par les architectes solution : SDD, contraintes exécutables, gouvernance MCP, coûts, dette du harnais. |

## Conventions

### Nommage

Un dossier par enquête : `AAAA-MM-JJ_sujet_court/`. La date est celle de fin de collecte, pas
celle de publication. Les fichiers à l'intérieur sont nommés par source ou par axe
(`reddit.md`, `social-web.md`, …). Au-delà de trois notes dans un dossier, on y ajoute un
`README.md` d'index.

### Contenu d'une note

Chaque note est autoportante et porte, dans cet ordre :

1. **Périmètre** — ce qui est couvert, ce qui ne l'est pas (les trous de couverture sont nommés).
2. **Méthode** — comment les sources ont été collectées, avec les outils et leurs limites.
3. **Synthèse** — les enseignements, en tête de document.
4. **Fiches sources** — une fiche par source, avec URL, auteur, date, citations littérales en VO
   suivies d'une traduction.
5. **Limites** — biais de sélection, chiffres non reproduits, sources invérifiables.

Règles de fond : rien n'est reconstitué de mémoire ; les citations sont reproduites telles quelles,
fautes incluses ; les conflits d'intérêts déclarés par les sources sont signalés ; les chiffres
repris d'un tiers sont présentés comme des affirmations d'auteur, pas comme des mesures validées.

### Ajouter une note

1. Créer `AAAA-MM-JJ_sujet_court/`.
2. Y écrire la ou les notes selon la structure ci-dessus.
3. Ajouter une ligne dans le tableau d'index, à la date correspondante.
4. Committer : `docs: ajout note <sujet> (<AAAA-MM-JJ>)`.
