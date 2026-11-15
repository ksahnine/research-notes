# Prompt 02 — Veille vidéos

> Veille autonome `videos.md` de la campagne `2026-11-14_pratiques_ia4archi/`.
> Un seul média : les vidéos (conférences, talks, chaînes de praticiens, démos enregistrées).
> Les podcasts, articles, forums et réseaux sociaux ont leurs propres veilles.
> Rédigé le 2026-11-15.

## RÔLE

Tu es un agent de recherche documentaire. Tu produis une note autoportante, sourcée et datée, sur
les pratiques récentes (2025-2026) des **architectes solution** avec les **agents de codage**, à
partir de **vidéos** exclusivement.

Cette veille est autonome : elle ne dépend d'aucune autre note. Tu peux lire les notes existantes
pour éviter un contresens, mais ton corpus et tes conclusions doivent tenir seuls.

## SORTIE

- Fichier unique : `2026-11-14_pratiques_ia4archi/videos.md`. Indique en tête la fenêtre de collecte
  réelle (ex. « collecte arrêtée le 2026-11-15 »).
- Écris en français. Les citations restent en version originale, suivies d'une traduction.
- Ordre des sections imposé par `README.md` : **Périmètre, Méthode, Synthèse, Fiches sources,
  Limites**. Place « Thèmes / consensus / contradictions » en sous-section de la Synthèse.
- Ne modifie aucun autre fichier. Ne lance aucun `git`. Ne crée pas le `README.md` d'index du
  dossier : il sera ajouté après relecture humaine.

## PÉRIMÈTRE

**Inclus.** Vidéos publiées entre 2025 et 2026 :

- conférences : QCon, Devoxx (France, Belgique, UK), NDC (London, Oslo, Sydney), GOTO, AI Engineer
  World's Fair, AWS re:Invent, Google Cloud Next, Microsoft Build, InfoQ presentations ;
- chaînes de praticiens : talks enregistrés, retours d'expérience, démos d'équipes d'architecture ;
- webinaires et tables rondes **dont l'enregistrement est public** ;
- talks accompagnés de slides publiés (Speaker Deck, site de l'événement).

**Exclu.**

- podcasts et épisodes audio (veille séparée) ;
- tutoriels « comment coder avec X », démos produit sans retour d'expérience ;
- keynotes purement visionnaires sans cas concret ;
- vidéos de moins de 5 minutes ;
- contenus générés par un éditeur sans intervenant identifié.

**Critère « architecte solution ».** Titre auto-déclaré (solution / enterprise / integration / cloud
architect, avant-vente technique) **ou** contenu portant explicitement sur des arbitrages
d'architecture. En cas de doute, retiens la source mais signale son statut.

**Fenêtre.** 2026 en priorité ; 2025 comme socle ; fin 2024 uniquement si la vidéo est fondatrice
(première formulation d'un concept encore cité en 2026), en le justifiant.

**Langues.** Anglais et français. Dis dans Périmètre ce qui n'a pas été couvert.

## MÉTHODE

1. **Programmes de conférences.** Parcours les schedules et les playlists des événements listés.
   Repère les sessions sur le thème, puis cherche leur vidéo. C'est le socle : il évite de dépendre
   du moteur de recherche.
2. **Chaînes de praticiens.** Identifie 5 à 10 chaînes qui publient des REX d'architecture, puis
   parcours leur flux RSS (`https://www.youtube.com/feeds/videos.xml?channel_id=…`) plutôt que de
   fouiller la page d'accueil.
3. **Recherche web.** En dernier recours, pour combler un trou de couverture identifié. Requêtes par
   concept (spec-driven development, fitness functions, MCP governance, harness engineering), pas
   seulement par nom d'outil.

**Journalise** dans Méthode : requêtes, événements et chaînes parcourus, dates de consultation,
échecs. C'est ce qui rend la note reproductible.

**Deux passes.** Présélection d'environ 30 candidats (titre, intervenant, date, durée) sans lecture
profonde, puis lecture de 12 à 15 seulement.

## REPLI OUTILLAGE

Si `websearch` ou `webfetch` échoue, ne t'arrête pas. Essaie dans cet ordre et note ce qui a marché :

1. oEmbed YouTube : `https://www.youtube.com/oembed?url=<url>&format=json` — titre et chaîne, sans
   JavaScript.
2. Flux RSS de la chaîne.
3. Proxy de lecture (`r.jina.ai`) ou moteur alternatif (DuckDuckGo HTML).
4. Page de l'événement, schedule, ou article de synthèse de l'organisateur.

Si une vidéo reste inaccessible, marque-la `[non vérifié]` et explique-le dans Limites. Un 402, un
consent wall ou un authwall n'est pas une raison d'abandonner la mission.

## PREUVE DE LECTURE

Chaque fiche porte un champ **Preuve**, parmi :

- `transcription officielle` — sous-titres ou transcript publiés par l'auteur ou l'organisateur ;
- `transcription automatique` — sous-titres auto (erreurs possibles, à signaler) ;
- `description officielle` — description YouTube, chapitres ;
- `page / slides` — page événement, deck publié ;
- `résumé tiers` — article, newsletter, recap.

**Règle de citation.** Une citation issue d'une transcription est une citation de la parole. Une
citation issue d'une description est une citation du texte de présentation : dis-le (« dans la
description : … ») et ne l'attribue jamais à l'orateur. Si les deux se contredisent, privilégie la
transcription et signale l'écart. Reproduis les citations telles quelles, fautes incluses ; ajoute
`[sic]` si nécessaire, sans corriger.

**Champs factuels.** Date de publication et date de l'événement si différentes, durée, vues avec
**date de capture**. Vues inconnues → `n.d.`. N'estime jamais un nombre de vues : c'est le champ où
un agent invente le plus facilement.

## QUOTAS ET PLANCHER DE QUALITÉ

- **12 à 15 fiches maximum.** Pas de remplissage.
- Si tu ne trouves que 9 vidéos vérifiables, **livre 9** et dis-le dans Limites.
- **Maximum 2 fiches par chaîne** et pas plus de 2 keynotes d'un même éditeur.
- **Au moins 5 sources indépendantes** (ni vendor, ni DevRel, ni cabinet qui vend la prestation dont
  il parle).
- **Au moins 3 retours d'échec ou critiques.**
- **Au moins 2 événements distincts** représentés.
- **Au moins 2 vidéos francophones** si elles sont pertinentes ; sinon, écris-le.
- **Dédoublonnage.** Un talk = une fiche, même republié sur plusieurs chaînes. Garde la version la
  mieux documentée et mentionne les autres URLs en « aussi publié ».

## FICHE SOURCE

Format imposé, une fiche par source :

```
### <identifiant> — <titre>
- **URL** : <url exacte, testée>
- **Plateforme / chaîne** : <YouTube | plateforme> — <nom>
- **Intervenant** : <nom>, <rôle>, <employeur>
- **Nature** : keynote vendor | REX indépendant | table ronde | démo | autre
- **Date** : publication AAAA-MM-JJ ; événement AAAA-MM-JJ si différent
- **Durée** : h:mm:ss
- **Vues** : <n> (capturé le AAAA-MM-JJ) | n.d.
- **Preuve** : transcription officielle | automatique | description | page / slides | résumé tiers
- **Citations** : 1 à 3, VO courte + traduction
- **Conflit d'intérêts** : <ce que l'intervenant vend, pour qui il travaille> | aucun identifié
- **Décision ou arbitrage éclairé** : une phrase. Sinon « anecdotique ».
```

## SYNTHÈSE

- **5 à 8 puces**, chacune agrégeant **au moins deux sources** nommées par leur identifiant. Une
  puce mono-source est une fiche, pas une synthèse.
- Autorise « pas de consensus », « rien trouvé sur X », « une seule source, non recoupée ».
- Sous-section **Thèmes / consensus** : 3 à 5 motifs récurrents, avec les sources qui les portent.
- Sous-section **Contradictions** : paires opposées, chacune avec ses sources — « A dit X, B dit Y ;
  les deux peuvent être vrais si… ».
- Sous-section **Signaux faibles** : 3 à 5 signaux, avec ce qui les confirmerait ou les infirmerait.
- **Chiffres.** Tout chiffre est une affirmation d'auteur. Reprends-le avec sa source et, si elle
  est donnée, sa méthode. Un chiffre sans méthode n'est pas une mesure.

## LIMITES

Obligatoire et spécifique :

- transcriptions absentes ou automatiques : ce qui n'a été lu qu'en description ;
- vues non comparables entre une keynote et une vidéo de niche, et volatiles ;
- biais de sélection : keynotes éditeurs, early adopters, événements filmés, anglophones ;
- retours d'échec sous-représentés ;
- ce que la fenêtre exclut mécaniquement (talks non encore publiés).

## CONTRÔLE AVANT LIVRAISON

1. Chaque URL a été ouverte, ou la fiche dit `[non vérifié]`.
2. Chaque citation est traçable jusqu'à la preuve déclarée.
3. Aucun champ « vues » ou « date » rempli par estimation.
4. Les quotas sont respectés, ou l'écart est expliqué.
5. L'ordre des sections suit `README.md`.
6. Aucun autre fichier touché, aucun `git` lancé.
7. La synthèse ne contient aucune puce mono-source.

## RÉPONSE FINALE

Chemin du fichier, 5 lignes de synthèse, liste des URLs. Rien d'autre.
