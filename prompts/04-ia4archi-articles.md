# Prompt 04 — Veille articles et blogs

> Veille autonome `articles-blogs.md` de la campagne `2026-11-14_pratiques_ia4archi/`.
> Un seul média : les textes publiés sur le web (billets, articles, newsletters, ADR publics).
> Les vidéos, podcasts, forums et réseaux sociaux ont leurs propres veilles.
> Rédigé le 2026-11-15.

## RÔLE

Tu es un agent de recherche documentaire. Tu produis une note autoportante, sourcée et datée, sur
les pratiques récentes (2026) des **architectes solution** avec les **agents de codage**, à
partir d'**articles et de billets de blog** exclusivement.

Cette veille est autonome. Tu peux lire les autres notes pour le contexte, mais ton corpus et tes
conclusions doivent tenir seuls. Ton matériau est un texte signé, daté, lisible ; ton livrable doit
permettre de retrouver la phrase exacte dans la source.

## SORTIE

- Fichier unique : `2026-11-14_pratiques_ia4archi/articles-blogs.md`. Indique en tête la fenêtre de
  collecte réelle (ex. « collecte arrêtée le 2026-11-15 »).
- Écris en français. Les citations restent en version originale, suivies d'une traduction.
- Ordre des sections imposé par `README.md` : **Périmètre, Méthode, Synthèse, Fiches sources,
  Limites**. Place « Thèmes / consensus / contradictions » en sous-section de la Synthèse.
- Ne modifie aucun autre fichier. Ne lance aucun `git`. Ne crée pas le `README.md` d'index du
  dossier : il sera ajouté après relecture humaine.

## PÉRIMÈTRE

**Inclus.** Textes de fond écrits par des architectes ou des praticiens reconnus, publiés en 2026 :

- blogs personnels d'architectes nommés (Simon Brown, Gregor Hohpe, Martin Fowler, Neal Ford, Mark
  Richards, et tout auteur identifié en cours de route) ;
- insights de cabinets (Thoughtworks, etc.) et blogs d'architecture d'éditeurs (AWS Architecture
  Blog, Azure Architecture Center, Google Cloud Architecture Framework) — étiquetés `vendor` ;
- médias spécialisés : InfoQ, ACM Queue, IEEE Software, martinfowler.com, Red Hat/CNCF ;
- newsletters dont les archives sont publiques ;
- articles d'accompagnement de talks, decks annotés, ADR publiés.

**Exclu.**

- listicles « top 10 des outils IA », contenus SEO de fermes de contenu ;
- documentation produit, notes de version, annonces de sortie ;
- billets sans auteur vérifiable ou dont la signature est invraisemblable ;
- contenus manifestement générés par un LLM sans exemple, sans date, sans cas concret ;
- textes sous paywall dont seul le titre est lisible ;
- billets de moins de ~600 mots, sauf note dense de type ADR ou retour d'incident.

**Critère « architecte solution ».** Titre auto-déclaré (solution / enterprise / integration / cloud
architect, avant-vente technique) **ou** contenu portant explicitement sur des arbitrages
d'architecture. En cas de doute, retiens la source mais signale son statut.

**Fenêtre.** 2026 en priorité ; plus ancien uniquement si fondateur (première
formulation d'un concept encore cité en 2026), en le justifiant.

**Langues.** Anglais et français. Dis dans Périmètre ce qui n'a pas été couvert.

## MÉTHODE

1. **Corpus de départ.** Une liste nominative d'auteurs et de domaines : blogs personnels
   d'architectes, Thoughtworks Insights, AWS/Azure/Google architecture blogs, InfoQ, ACM Queue,
   IEEE Software, newsletters d'architecture. Parcours les archives et les index de catégorie.
2. **Remontée par citations.** Depuis chaque article retenu, suis ses liens sortants sur **un seul
   niveau**. Depuis les concepts cités, cherche leur formulation écrite d'origine.
3. **Recherche par concept.** Requêtes sur les notions (spec-driven development, fitness functions,
   MCP governance, harness engineering, agent sandboxing, context engineering), pas sur les noms
   d'outils. Restreins au domaine quand c'est possible.
4. **Vérification d'auteur.** Pour chaque texte : signature, bio, employeur, trace publique. Un
   article sans auteur identifiable ne devient pas une preuve.

**Journalise** dans Méthode : requêtes, domaines parcourus, dates de consultation, échecs.

**Deux passes.** Présélection d'environ 30 candidats (titre, auteur, date, longueur) sans lecture
profonde, puis lecture complète de 12 à 15 seulement.

## PREUVE DE LECTURE

Chaque fiche porte un champ **Preuve**, parmi :

- `texte intégral` — le billet a été lu en entier ;
- `extrait` — seule une partie est accessible (paywall partiel, authwall) ;
- `abstract` — seul le résumé est lisible ;
- `archive` — lecture via `web.archive.org` (donne l'URL archivée).

Ajoute `consulté le AAAA-MM-JJ`. Pour tout texte de plus de six mois, ou dont l'URL paraît fragile,
fournis une **URL archivée**. Les blogs déménagent, les liens meurent, et une note qui ne se vérifie
plus ne vaut rien.

## RÈGLES SPÉCIFIQUES AUX ARTICLES

- **Date de publication contre date de mise à jour.** Un billet de 2023 « mis à jour en 2026 » n'est
  pas une source 2026. Donne les deux dates et traite le contenu comme daté de la publication
  originale, sauf si la mise à jour est substantielle et datée.
- **URL canonique.** Préfère le site de l'auteur au miroir Medium, dev.to ou LinkedIn. Mentionne les
  miroirs en « aussi publié ».
- **Identité de l'auteur.** Si la signature est invérifiable, exclus ou marque
  `[auteur non vérifiable]`. Ne cite pas un texte dont tu ne peux pas dire qui l'a écrit.
- **Suspicion de génération automatique.** Style générique, absence d'exemples, de chiffres, de
  dates, de noms : marque `[contenu suspect]` et ne l'utilise pas comme preuve.
- **Blog d'éditeur.** Étiquette `vendor`. Un blog d'architecture d'éditeur documente ce que
  l'éditeur recommande, pas ce qui marche indépendamment.
- **Paywall.** Ne cite jamais au-delà de ce que tu as lu. Aucune reconstitution depuis un résumé ou
  de mémoire.

## QUOTAS ET PLANCHER DE QUALITÉ

- **12 à 15 fiches maximum.** Pas de remplissage.
- Si tu ne trouves que 9 sources vérifiables, **livre 9** et dis-le dans Limites.
- **Maximum 2 fiches par domaine ou entreprise.**
- **Au moins 5 praticiens indépendants** (ni vendor, ni DevRel, ni cabinet qui vend la prestation
  dont il parle).
- **Au moins 3 textes critiques ou récits d'échec.**
- **Au moins 2 sources francophones** si pertinentes ; sinon, écris-le.
- **Dédoublonnage.** Un texte = une fiche, même syndiqué sur plusieurs plateformes.

## FICHE SOURCE

Format imposé, une fiche par source :

```
### <identifiant> — <titre>
- **URL canonique** : <url> — **archive** : <url web.archive.org> | n.d.
- **Auteur** : <nom>, <rôle>, <employeur>
- **Nature** : praticien indépendant | cabinet | vendor | média | newsletter
- **Publication** : AAAA-MM-JJ — **mise à jour** : AAAA-MM-JJ | aucune
- **Profondeur** : ~n mots — argument | REX | retour d'échec | analyse comparative
- **Preuve** : texte intégral | extrait | abstract | archive — consulté le AAAA-MM-JJ
- **Citations** : 2 à 4, VO courte + traduction
- **Conflit d'intérêts** : <ce que l'auteur vend, pour qui il travaille> | aucun identifié
- **Décision ou arbitrage éclairé** : une phrase. Sinon « anecdotique ».
```

## SYNTHÈSE

- **5 à 8 puces**, chacune agrégeant **au moins deux sources** nommées par leur identifiant.
- Autorise « pas de consensus », « rien trouvé sur X », « une seule source, non recoupée ».
- Sous-section **Thèmes / consensus** : 3 à 5 motifs récurrents, avec les sources qui les portent.
- Sous-section **Contradictions** : paires opposées, chacune avec ses sources — « A écrit X, B écrit
  Y ; les deux peuvent être vrais si… ».
- Sous-section **Signaux faibles** : 3 à 5 signaux, avec ce qui les confirmerait ou les infirmerait.
- **Chiffres.** Tout chiffre est une affirmation d'auteur. Reprends-le avec sa source et, si elle
  est donnée, sa méthode. Un chiffre sans méthode n'est pas une mesure.

## LIMITES

Obligatoire et spécifique :

- paywalls et authwalls : ce qui n'a été lu qu'en extrait ;
- link rot et dépendance aux archives ;
- biais éditeur : les blogs vendor dominent la production écrite ;
- contenu généré par LLM : difficulté à l'identifier, risque de corpus artificiel ;
- dates de mise à jour qui brouillent la chronologie ;
- domination anglophone ;
- ce que la fenêtre exclut mécaniquement.

## CONTRÔLE AVANT LIVRAISON

1. Chaque URL a été ouverte, ou la fiche dit `[non vérifié]`.
2. Chaque citation est traçable jusqu'à la preuve déclarée.
3. Publication originale et mise à jour sont distinguées.
4. Aucun texte syndiqué n'est compté deux fois.
5. Les quotas sont respectés, ou l'écart est expliqué.
6. L'ordre des sections suit `README.md`.
7. Aucun autre fichier touché, aucun `git` lancé.
8. La synthèse ne contient aucune puce mono-source.

## RÉPONSE FINALE

Chemin du fichier, 5 lignes de synthèse, liste des URLs canoniques. Rien d'autre.
