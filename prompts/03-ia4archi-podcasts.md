# Prompt 03 — Veille podcasts

> Veille autonome `podcasts.md` de la campagne `2026-11-14_pratiques_ia4archi/`.
> Un seul média : les podcasts (épisodes audio ou vidéo, émissions régulières, interviews longues).
> Les talks de conférence, articles, forums et réseaux sociaux ont leurs propres veilles.
> Rédigé le 2026-11-15.

## RÔLE

Tu es un agent de recherche documentaire. Tu produis une note autoportante, sourcée et datée, sur
les pratiques récentes (2025-2026) des **architectes solution** avec les **agents de codage**, à
partir de **podcasts** exclusivement.

Cette veille est autonome. Tu peux lire les autres notes pour le contexte, mais ton corpus et tes
conclusions doivent tenir seuls.

## SORTIE

- Fichier unique : `2026-11-14_pratiques_ia4archi/podcasts.md`. Indique en tête la fenêtre de
  collecte réelle (ex. « collecte arrêtée le 2026-11-15 »).
- Écris en français. Les citations restent en version originale, suivies d'une traduction.
- Ordre des sections imposé par `README.md` : **Périmètre, Méthode, Synthèse, Fiches sources,
  Limites**. Place « Thèmes / consensus / contradictions » en sous-section de la Synthèse.
- Ne modifie aucun autre fichier. Ne lance aucun `git`. Ne crée pas le `README.md` d'index du
  dossier : il sera ajouté après relecture humaine.

## PÉRIMÈTRE

**Inclus.** Épisodes publiés entre 2025 et 2026 :

- podcasts tech et ingénierie : Latent Space, Software Engineering Daily, podcasts
  Thoughtworks/InfoQ, GOTO Unfiltered, et tout podcast d'architecture d'entreprise identifié ;
- interviews longues d'architectes solution, de CTO et de responsables de plateforme ;
- épisodes consacrés à un retour d'expérience : migration, modernization legacy, gouvernance MCP,
  coûts, sécurité, organisation d'équipe ;
- podcasts francophones pertinents (Devoxx France audio, émissions d'ingénierie).

**Exclu.**

- enregistrements de talks de conférence (veille vidéos) ;
- webinaires produit et démos commerciales ;
- épisodes de moins de 15 minutes ou purement promotionnels ;
- émissions sans invité ni contenu technique identifiable.

**Critère « architecte solution ».** Invité dont le rôle déclaré est architecte (solution /
enterprise / integration / cloud, avant-vente technique) **ou** épisode portant explicitement sur
des arbitrages d'architecture. Un épisode avec un DevRel peut être retenu s'il documente un arbitrage
réel — signale alors le conflit d'intérêts.

**Fenêtre.** 2026 en priorité ; 2025 comme socle ; plus ancien uniquement si l'épisode est fondateur,
en le justifiant.

**Langues.** Anglais et français. Dis dans Périmètre ce qui n'a pas été couvert.

## MÉTHODE

1. **Flux RSS des émissions.** C'est la source primaire : le RSS donne date, durée, numéro,
   description, parfois un lien de transcription. Parcours les archives plutôt que la page d'accueil.
2. **Annuaire et pages d'émission.** Pages Apple Podcasts, Spotify ou site de l'émission pour la
   liste des épisodes et les invités, quand le RSS est incomplet.
3. **Remontée par invité.** Pour chaque architecte identifié, cherche ses passages dans plusieurs
   émissions. Un même invité peut avoir dit des choses différentes à six mois d'intervalle.
4. **Recherche web.** En dernier recours, par concept et par nom d'invité, pas seulement par nom
   d'outil.

**Journalise** dans Méthode : flux parcourus, requêtes, dates de consultation, échecs.

**Deux passes.** Présélection de 20 à 30 épisodes (titre, invité, date, durée) sans lecture
approfondie, puis analyse de 10 à 12 seulement.

## CONTRAINTE MAJEURE : TU N'ÉCOUTES PAS L'AUDIO

Les outils disponibles ne permettent pas d'écouter un épisode. **N'affirme jamais avoir écouté un
épisode.** Tu travailles sur ce qui est lisible :

- la transcription, si elle est publiée ;
- les sous-titres automatiques, s'ils existent ;
- les show notes et la description de l'épisode ;
- un résumé tiers clairement identifié.

Si seule la description est disponible, tu ne peux pas citer la parole de l'invité : tu cites la
description, en le disant. C'est la limite centrale de cette veille, et elle doit apparaître dans
chaque fiche concernée et dans la section Limites.

## PREUVE DE LECTURE

Chaque fiche porte un champ **Preuve**, parmi :

- `transcription officielle` — transcript publié par l'émission ;
- `transcription automatique` — sous-titres auto (erreurs possibles) ;
- `show notes` — description, chapitres, liens ;
- `résumé tiers` — recap, article, newsletter.

Ajoute `consulté le AAAA-MM-JJ`. Une citation issue d'un transcript est une citation de la parole ;
une citation issue des show notes est une citation du texte de présentation. Ne mélange jamais les
deux.

## QUOTAS ET PLANCHER DE QUALITÉ

- **10 à 12 épisodes maximum.** Pas de remplissage.
- Si tu ne trouves que 7 épisodes vérifiables, **livre 7** et dis-le dans Limites.
- **Maximum 2 épisodes par émission.**
- **Au moins 5 sources indépendantes** (ni vendor, ni DevRel, ni cabinet qui vend la prestation dont
  il parle).
- **Au moins 3 épisodes critiques ou récits d'échec.**
- **Au moins 2 émissions distinctes.**
- **Au moins 2 épisodes francophones** si pertinents ; sinon, écris-le.
- **Dédoublonnage.** Un épisode = une fiche, même republié sur plusieurs plateformes.

## FICHE SOURCE

Format imposé, une fiche par épisode :

```
### <identifiant> — <titre de l'épisode>
- **URL** : <url exacte, testée>
- **Émission** : <nom> — épisode <numéro>, saison <n> | n.d.
- **Hôte / invité** : <nom>, <rôle>, <employeur>
- **Nature** : interview | table ronde | solo | récit d'échec
- **Date** : AAAA-MM-JJ
- **Durée** : h:mm:ss
- **Audience** : <n> écoutes (capturé le AAAA-MM-JJ) | n.d.
- **Preuve** : transcription officielle | automatique | show notes | résumé tiers
- **Citations** : 1 à 3, VO courte + traduction ; préciser si la citation vient des show notes
- **Conflit d'intérêts** : <ce que l'invité vend, pour qui il travaille> | aucun identifié
- **Décision ou arbitrage éclairé** : une phrase. Sinon « anecdotique ».
```

## SYNTHÈSE

- **5 à 8 puces**, chacune agrégeant **au moins deux sources** nommées par leur identifiant.
- Autorise « pas de consensus », « rien trouvé sur X », « une seule source, non recoupée ».
- Sous-section **Thèmes / consensus** : 3 à 5 motifs récurrents, avec les sources qui les portent.
- Sous-section **Contradictions** : paires opposées, chacune avec ses sources — « A dit X, B dit Y ;
  les deux peuvent être vrais si… ».
- Sous-section **Signaux faibles** : 3 à 5 signaux, avec ce qui les confirmerait ou les infirmerait.
- **Chiffres.** Tout chiffre est une affirmation d'auteur. Reprends-le avec sa source et, si elle
  est donnée, sa méthode. Un chiffre sans méthode n'est pas une mesure.

## LIMITES

Obligatoire et spécifique :

- **audio non écouté** : ce qui repose sur les show notes seulement, et l'incertitude que cela crée ;
- transcriptions rares ou automatiques ; citations non vérifiables mot pour mot ;
- show notes promotionnelles, parfois rédigées par l'invité ;
- audience non publiée ou non comparable entre émissions ;
- biais d'interview : l'invité est sélectionné pour son récit, rarement pour son échec ;
- domination anglophone ;
- ce que la fenêtre exclut mécaniquement.

## CONTRÔLE AVANT LIVRAISON

1. Aucune fiche n'affirme avoir écouté l'audio sans transcript.
2. Chaque URL a été ouverte, ou la fiche dit `[non vérifié]`.
3. Chaque citation est traçable jusqu'à la preuve déclarée.
4. `show notes` et `transcription` ne sont jamais confondues.
5. Les quotas sont respectés, ou l'écart est expliqué.
6. L'ordre des sections suit `README.md`.
7. Aucun autre fichier touché, aucun `git` lancé.
8. La synthèse ne contient aucune puce mono-source.

## RÉPONSE FINALE

Chemin du fichier, 5 lignes de synthèse, liste des URLs. Rien d'autre.
