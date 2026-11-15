# Agents de codage vus par les architectes — sources sociales et web (2025-2026)

> Périmètre : pratiques d'architectes solution / d'entreprise (intégration, cloud, avant-vente technique, modernisation legacy) avec les agents de codage (Claude Code, Codex, Copilot, Cursor, Gemini CLI, opencode, Kiro, etc.).
> Fenêtre : 2025-2026, avec une exception fondatrice (METR, juillet 2025).
> Méthode : chaque fiche a été ouverte et lue. Les citations sont en VO courte, suivies d'une traduction. Tout ce qui n'a pas pu être lu directement est marqué **[non vérifié]**.

**Note d'outillage (transparence)** : l'outil de recherche web natif a renvoyé une erreur HTTP 402 pendant toute la session. La découverte d'URL a donc été faite via l'endpoint HTML de DuckDuckGo lu au travers d'un proxy de lecture (r.jina.ai), puis chaque page a été récupérée et vérifiée individuellement. X/Twitter et LinkedIn ne sont lisibles que via ce même proxy (pages rendues côté serveur ou *authwall* contournée en lecture seule). Voir la section 5.

---

## 1. Synthèse

- **Le centre de gravité a changé de place : du modèle vers le *harness*.** Le consensus 2026 chez les praticiens (Thoughtworks, GitHub, AWS, Tech Mahindra) est que la valeur différentielle n'est plus le choix du modèle mais la couche qui l'entoure : instructions, outils, connecteurs, garde-fous, boucles de feedback.
- **L'architecture s'industrialise en « contraintes exécutables »**, pas en documents. Le mot d'ordre : une règle d'architecture qu'un agent peut ignorer n'existe pas ; il faut qu'elle casse le build *dans la boucle de l'agent*.
- **Nuance importante** : imposer une architecture dans le prompt peut *dégrader* les résultats (« Constraint Decay »), alors que fournir des squelettes (types, signatures, contrats) les améliore. « Requiring structure isn't the same as providing it. »
- **Le spec-driven development (SDD) est passé du gadget au dispositif d'entreprise** : GitHub Spec Kit + couches d'extension (presets, extensions, bundles, workflows) + catalogues gouvernés, pour éviter le fork par équipe.
- **Les ADR redeviennent stratégiques** — non comme documentation, mais comme contexte machine et comme garde-fou : génération par l'agent, puis application via hooks et *fitness functions*.
- **Gestion du contexte = discipline de coût** : divulgation progressive, AGENTS.md maigre, liens plutôt que monolithes, raisonnement ancré sur graphe de code, MCP chargé à la demande.
- **Le garde-fou mature est *gradué par risque*** : sandboxing par défaut, revue humaine réservée aux changements difficiles à inverser, auto-merge des changements à faible risque après CI.
- **Le vrai risque de gouvernance est le « human-in-the-loop theater »** : un humain qui approuve ce qu'il ne peut pas évaluer ne gouverne rien — il absorbe la responsabilité.
- **La revue de code devient le goulot d'étranglement** : les agents produisent plus vite que la capacité humaine de lecture ; les architectes basculent du contrôle unitaire au pilotage par tests, propriétés et modèles formels.
- **Sécurité MCP : la confusion identité d'agent / authentification MCP** est identifiée comme le piège d'architecture n°1 des déploiements d'entreprise.
- **Les chiffres de ROI se contredisent** : GitHub revendique +400 % de commits, METR mesure 19 % de *ralentissement* chez des devs expérimentés, et Thoughtworks classe « le débit de code comme mesure de productivité » en *Caution*.
- **Le legacy est le vrai terrain de test** : les architectes constatent qu'appliquer des agents sans cadre sur du brownfield produit du code qui « marche » avec la mauvaise conception — et qu'on est en train de fabriquer une nouvelle génération de legacy (couche `.md`/skills/rules/hooks).
- **Signal fort sur les rôles** : la valeur de l'architecte se déplace vers la décision, l'arbitrage et la communication ; de nouveaux intitulés apparaissent (« Agentic Solutions Architect »), mais la revendication reste à confirmer.

---

## 2. Fiches sources

### 1. Technology Radar Vol. 35 — thème « Harness engineering at scale »
- **URL** : https://www.thoughtworks.com/radar
- **Plateforme / auteur** : Thoughtworks — Technology Advisory Board (Rachel Laycock CTO et al.)
- **Date** : 2026-11 (volume daté « November 2026 »)
- **Engagement** : n.d. (publication)
- **Citations** :
  > “harness engineering (everything we do to construct the environment around an AI agent, from memory and context to feedback loops and guardrails) is maturing into a more cohesive discipline.” — *« L'ingénierie du harnais — tout ce que nous construisons autour d'un agent : mémoire, contexte, boucles de feedback, garde-fous — devient une discipline à part entière. »*
  > “the harness is a living asset that requires ongoing ownership and maintenance.” — *« Le harnais est un actif vivant qui exige un propriétaire et de la maintenance. »*
- **Intérêt architecte** : c'est le cadre de référence le plus explicite pour positionner l'architecte comme propriétaire de la couche d'environnement des agents, pas comme utilisateur d'un outil.

### 2. Blip « Agent sandboxing » (Adopt)
- **URL** : https://www.thoughtworks.com/radar/techniques/agent-sandboxing
- **Plateforme / auteur** : Thoughtworks — Technology Radar Vol. 35
- **Date** : 2026-11
- **Engagement** : n.d.
- **Citations** :
  > “We now consider agent sandboxing a sensible default for all agents.” — *« Nous considérons désormais le sandboxing d'agents comme un réglage par défaut raisonnable pour tous les agents. »*
  > “We recommend teams apply a risk-based approach to sandboxing, informed by threat modeling of their agents and systems.” — *« Approche par risque, guidée par la modélisation de menaces des agents et des systèmes. »*
- **Intérêt architecte** : transforme une bonne pratique sécurité en décision d'architecture standard, avec un livrable associé (threat model).

### 3. Blip « Progressive context disclosure » (Adopt)
- **URL** : https://www.thoughtworks.com/radar/techniques/progressive-context-disclosure
- **Plateforme / auteur** : Thoughtworks — Radar Vol. 35
- **Date** : 2026-11
- **Engagement** : n.d.
- **Citations** :
  > “In coding, one example is to keep your AGENTS.md lean and provide links to documentation that the agent can look up when needed.” — *« Garder un AGENTS.md maigre et fournir des liens que l'agent consulte au besoin. »*
  > “can reduce token consumption and costs and help counter context rot.” — *« Réduit la consommation de tokens et les coûts, et contre la pourriture du contexte. »*
- **Intérêt architecte** : donne une règle concrète et chiffrable (tokens, coûts) pour arbitrer entre « tout dire à l'agent » et « dire où chercher ».

### 4. Blip « Risk-tiered human oversight » (Trial)
- **URL** : https://www.thoughtworks.com/radar/techniques/risk-tiered-human-oversight
- **Plateforme / auteur** : Thoughtworks — Radar Vol. 35
- **Date** : 2026-11
- **Engagement** : n.d.
- **Citations** :
  > “Reviewing everything with the same intensity ends in human-in-the-loop theater.” — *« Tout relire avec la même intensité finit en théâtre du contrôle humain. »*
  > “The riskiest or hardest-to-reverse changes are reserved for humans to apply.” — *« Les changements les plus risqués ou irréversibles sont réservés à l'application humaine. »*
- **Intérêt architecte** : fournit la matrice de délégation (risque → niveau de revue) que beaucoup d'architectes cherchent à formaliser en comité.

### 5. Blip « Human-in-the-loop theater » (Caution)
- **URL** : https://www.thoughtworks.com/radar/techniques/human-in-the-loop-theater
- **Plateforme / auteur** : Thoughtworks — Radar Vol. 35
- **Date** : 2026-11
- **Engagement** : n.d.
- **Citations** :
  > “keeping a human in an agent's loop as an empty approval step rather than a real check.” — *« Garder un humain dans la boucle comme étape d'approbation vide, et non comme vrai contrôle. »*
  > “The approval step functions as an accountability sink: no one truly owns the decision.” — *« L'approbation devient un puits de responsabilité : plus personne ne possède vraiment la décision. »*
- **Intérêt architecte** : nomme le risque politique majeur des comités d'architecture « IA » et propose de remplacer la revue unitaire par des tests de mutation, du property-based testing et des modèles formels.

### 6. Blip « Enterprise harness » (Assess)
- **URL** : https://www.thoughtworks.com/radar/techniques/enterprise-harness
- **Plateforme / auteur** : Thoughtworks — Radar Vol. 35
- **Date** : 2026-11
- **Engagement** : n.d.
- **Citations** :
  > “It includes skills, tools, connectors to internal context, approved technologies, architecture decision records, path-to-production guidance, hooks and security policies.” — *« Skills, outils, connecteurs au contexte interne, technologies approuvées, ADR, guide de mise en production, hooks et politiques de sécurité. »*
  > “It's like a developer experience platform, but for agent experience.” — *« Une plateforme d'expérience développeur… mais pour l'expérience des agents. »*
  > “There's no consensus yet on how to do this well, so keep the enterprise harness thin and federated.” — *« Pas encore de consensus : gardez le harnais d'entreprise mince et fédéré. »*
- **Intérêt architecte** : c'est littéralement le cahier des charges d'une « plateforme d'architecture pour agents » — et l'aveu honnête qu'aucun standard ne s'impose.

### 7. Blip « Blanket frontier model usage » (Caution)
- **URL** : https://www.thoughtworks.com/radar/techniques/blanket-frontier-model-usage
- **Plateforme / auteur** : Thoughtworks — Radar Vol. 35
- **Date** : 2026-11
- **Engagement** : n.d.
- **Citations** :
  > “We've sometimes caught ourselves defaulting every task that requires an LLM to the most capable model available, paying no attention to cost, latency or required capability.” — *« Nous nous sommes surpris à tout envoyer au modèle le plus capable, sans regarder coût, latence ni capacité requise. »*
  > “Each model has its own prompt cache, so you can also switch at natural boundaries, a new session, a subagent or the handoff from planning to implementation.” — *« Chaque modèle a son cache de prompt : basculez aux frontières naturelles (session, sous-agent, passage planification → implémentation). »*
- **Intérêt architecte** : introduit le *model routing* et le *context profiling* comme décisions d'architecture de coût, avec un piège contre-intuitif (un gros modèle peut consommer moins de tokens).

### 8. Blip « Coding throughput as a measure of productivity » (Caution)
- **URL** : https://www.thoughtworks.com/radar/techniques/coding-throughput-as-a-measure-of-productivity
- **Plateforme / auteur** : Thoughtworks — Radar Vol. 35
- **Date** : 2026-11
- **Engagement** : n.d.
- **Citations** :
  > “activity-based metrics such as the percentage of code generated by AI or tokens consumed treated as badges of honor.” — *« Le % de code généré par IA ou les tokens consommés érigés en trophées. »*
  > “Treating activity metrics as targets rather than signals risks falling prey to Goodhart's law. We've seen developers generating AI busywork simply to hit these targets.” — *« Traiter des métriques d'activité comme des objectifs, c'est tomber dans la loi de Goodhart : nous avons vu des développeurs produire du travail IA inutile pour atteindre les cibles. »*
- **Intérêt architecte** : arme directement l'architecte qui doit refuser un KPI « % de code IA » en comité de direction.

### 9. « The harness is a product »
- **URL** : https://www.thoughtworks.com/insights/blog/generative-ai/harness-is-a-product
- **Plateforme / auteur** : Thoughtworks Insights — Cecilia Geraldo (membre du Technology Advisory Board)
- **Date** : 2026-11-04
- **Engagement** : n.d.
- **Citations** :
  > “Ask what wraps the model though, from the instructions it loads, the tools it can call, what it's allowed to touch, how its context is assembled, and the answer is likely to be a tour of half-owned artifacts.” — *« Demandez ce qui entoure le modèle… la réponse ressemble à une visite d'artefacts à moitié sans propriétaire. »*
  > “few have a harness strategy. Fewer still will have a named person accountable for it.” — *« Peu ont une stratégie de harnais ; encore moins une personne nommée responsable. »*
- **Intérêt architecte** : transforme le harnais en objet de gouvernance avec propriétaire, budget et roadmap — le pendant « architecture » du platform engineering.

### 10. « Brownfield Agentic Engineering »
- **URL** : https://addyosmani.com/blog/brownfield-agentic-engineering/
- **Plateforme / auteur** : Blog d'Addy Osmani (Google, auteur *Learning JavaScript Design Patterns*)
- **Date** : 2026-09-14
- **Engagement** : n.d.
- **Citations** :
  > “throw them at an older brownfield codebase unsupervised and you may end up with something that 'works' but with the wrong system design and brittle tests.” — *« Lâchés sans supervision sur du brownfield, vous obtenez quelque chose qui 'marche' mais avec la mauvaise conception et des tests fragiles. »*
  > “the repository is no longer a complete description of how the thing actually behaves.” — *« Le dépôt ne décrit plus complètement le comportement réel du système. »*
- **Intérêt architecte** : c'est le cœur du sujet modernisation legacy : rendre visibles les contraintes implicites avant de laisser un agent écrire.

### 11. « Agentic Code Review »
- **URL** : https://addyosmani.com/blog/agentic-code-review/
- **Plateforme / auteur** : Addy Osmani
- **Date** : 2026-06-15
- **Engagement** : n.d.
- **Citations** :
  > “the hard part of engineering moved from writing code to deciding whether to trust it, which makes review the most leveraged skill in software right now.” — *« Le plus dur n'est plus d'écrire le code mais de décider s'il est digne de confiance : la revue devient la compétence à plus fort levier du logiciel aujourd'hui. »*
- **Intérêt architecte** : justifie que l'architecte réinvestisse la revue comme activité de conception, pas comme contrôle qualité.

### 12. Interview « When Good-Looking Diagrams Aren't Good Enough » (Simon Brown)
- **URL** : https://www.software-architecture-gathering.com/when-good-looking-diagrams-arent-good-enough-simon-brown-on-c4-ai-and-software-architecture/
- **Plateforme / auteur** : Blog iSAQB Software Architecture Gathering — Simon Brown (créateur du modèle C4, indépendant)
- **Date** : 2026-10-23
- **Engagement** : n.d.
- **Citations** :
  > “These tools do tend to create very plausible looking diagrams, but the majority of them are terrible.” — *« Ces outils produisent des diagrammes très plausibles, mais la majorité sont mauvais. »*
  > “Those without that knowledge won't though, and are, of course, unable to usefully review or critique them either.” — *« Ceux qui n'ont pas cette connaissance ne le verront pas, et seront incapables de les relire ou de les critiquer utilement. »*
- **Intérêt architecte** : contrepoint frontal à l'« architecture-as-code générée » : la génération abaisse le coût de production, pas le coût du jugement.

### 13. Dossier « Gregor Hohpe on the Architect's Role in the AI Era »
- **URL** : https://www.thekb.eu/en/fiches/hohpe-decision-options-ia-2026-07-15/
- **Plateforme / auteur** : thekb.eu — synthèse de sources primaires (architectelevator.com, conférences, LinkedIn) sur Gregor Hohpe (auteur *Enterprise Integration Patterns*, *The Software Architect Elevator* ; ex-Chief Architect Allianz, ex-stratège AWS/Google Cloud)
- **Date** : 2026-07-15
- **Engagement** : n.d.
- **Citations** (reprises, **[non vérifiées à la source primaire]**) :
  > “developers mainly interact with machines (compilers, interpreters, GenAI); architects, meanwhile, communicate with humans — sponsors, stakeholders, regulators.” — *« Les développeurs parlent aux machines ; les architectes parlent aux humains : sponsors, parties prenantes, régulateurs. »* (attribué à Craft Conference 2026)
  > “AI does not devalue the architect, it shifts their value from code to what AI does not do.” — *« L'IA ne dévalue pas l'architecte : elle déplace sa valeur du code vers ce que l'IA ne fait pas. »*
- **Intérêt architecte** : la formulation la plus citée du moment pour défendre le rôle en comité exécutif ; à utiliser comme reprise, pas comme source primaire.

### 14. « From Spec-First to Enterprise-Ready: Extending GitHub Spec Kit »
- **URL** : https://developer.microsoft.com/blog/from-spec-first-to-enterprise-ready-extending-github-spec-kit/
- **Plateforme / auteur** : Microsoft for Developers (blog) — Apoorv Gupta
- **Date** : 2026-10-07
- **Engagement** : n.d.
- **Citations** :
  > “Forking the toolkit for every team would fragment the experience and make upgrades costly. The better model is a stable core with explicit extension points.” — *« Forker la boîte à outils par équipe fragmente l'expérience et renchérit les mises à jour : mieux vaut un noyau stable avec des points d'extension explicites. »*
  > “presets change existing behavior, extensions add capabilities, bundles package reusable stacks, and workflows automate repeatable processes.” — *« Presets, extensions, bundles, workflows : quatre couches pour adapter le SDD à l'échelle. »*
- **Intérêt architecte** : montre comment le spec-driven devient un dispositif de plateforme gouvernée (catalogues, standards) plutôt qu'une méthode par projet.

### 15. « Architecture Decision Records with Codex CLI »
- **URL** : https://codex.danielvaughan.com/2026/04/28/codex-cli-architecture-decision-records-adr-automated-governance/
- **Plateforme / auteur** : Blog « Codex Knowledge Base » — Daniel Vaughan (auteur technique, profil architecte .NET **[rôle non vérifié]**)
- **Date** : 2026-04-28
- **Engagement** : n.d.
- **Citations** :
  > “when an AI agent scaffolds your system in minutes, the architectural decisions it makes are buried in generated code with no recorded rationale.” — *« Quand un agent échafaude un système en minutes, ses décisions d'architecture sont enfouies dans le code généré, sans rationale consigné. »*
  > “Agents scaffold systems in minutes; teams need hours or days to audit them.” — *« Les agents échafaudent en minutes ; les équipes mettent des heures ou des jours à auditer. »* (citation d'une étude, reprise par l'auteur — étude non lue)
- **Intérêt architecte** : propose le geste concret « ADR généré puis appliqué par hooks/fitness functions », et nomme le « vibe architecting ».

### 16. « Inside an enterprise AI agent: A governed, observable loop architecture »
- **URL** : https://aws.amazon.com/blogs/architecture/inside-an-enterprise-ai-agent-a-governed-observable-loop-architecture/
- **Plateforme / auteur** : AWS Architecture Blog — Paul Tamburello
- **Date** : 2026-11-12
- **Engagement** : n.d.
- **Citations** :
  > “An enterprise AI agent isn't a bigger chatbot.” — *« Un agent IA d'entreprise n'est pas un chatbot plus gros. »*
  > “Every one of those steps touches real systems and real data, so governance, observability, and trust controls must live at each step.” — *« Chaque étape touche des systèmes et des données réels : gouvernance, observabilité et contrôles de confiance doivent vivre à chaque étape. »*
- **Intérêt architecte** : référence cloud-native à opposer aux architectures « agent = LLM + prompt » ; five layers (gateway identité/politique, runtime 5 phases, connaissance/état, services plateforme, trust & control).

### 17. « Beyond code generation: A developer's guide to agentic engineering »
- **URL** : https://github.blog/ai-and-ml/github-copilot/beyond-code-generation-a-developers-guide-to-agentic-engineering/
- **Plateforme / auteur** : The GitHub Blog — Nick Liffen, Philip Holleran
- **Date** : 2026-11-06
- **Engagement** : n.d.
- **Citations** :
  > “This October, GitHub saw more than 1.2 billion commits in one week—over 400% more than a year earlier.” — *« En octobre, GitHub a vu plus de 1,2 milliard de commits en une semaine, +400 % sur un an. »*
  > “But ask yourself: do you feel 400% more productive than you were last year?” — *« Mais demandez-vous : vous sentez-vous 400 % plus productif qu'il y a un an ? »*
- **Intérêt architecte** : la meilleure formulation « hype vs réalité » côté éditeur : le volume monte, la contrainte se déplace vers la planification et la revue.

### 18. « Agentic AI Architecture: Current Challenges and Future Opportunities » (InfoQ)
- **URL** : https://www.infoq.com/articles/agentic-ai-architecture-challenges-opportunities
- **Plateforme / auteur** : InfoQ (article) — auteur non affiché dans l'extrait accessible
- **Date** : **non affichée sur la page lue [non vérifié]**
- **Engagement** : n.d.
- **Citations** (résumé éditorial présent sur la page ; corps de l'article inaccessible sans compte) :
  > “Agentic AI architecture extends microservices and cloud-native architectures with AI agents that work with context, memory, and protocols such as MCP and A2A.” — *« L'architecture agentique prolonge les architectures microservices/cloud-native avec des agents dotés de contexte, mémoire et protocoles (MCP, A2A). »*
  > “It expects gradual adoption alongside existing architectures, with platforms absorbing common components.” — *« Adoption graduelle aux côtés des architectures existantes, les plateformes absorbant les composants communs. »*
- **Intérêt architecte** : confirme la thèse « agents = nouveau style d'architecture d'intégration », avec intégration par contexte borné (bounded context).

### 19. « AI Coding Assistants Through the Lens of a Solution Architect: GitHub Copilot vs Amazon Q vs Cursor AI »
- **URL** : https://www.linkedin.com/pulse/ai-coding-assistants-through-lens-solution-architect-github-gupta-fdxdc
- **Plateforme / auteur** : LinkedIn (article Pulse) — Ankit Gupta (angle revendiqué « solution architect » ; intitulé de poste non vérifiable, profil sous authwall **[non vérifié]**)
- **Date** : 2026-07-05
- **Engagement** : non visible en lecture invite
- **Citations** :
  > “As architects, the question is different: Which AI tool helps teams design better systems, reduce technical debt, accelerate delivery, and improve engineering quality?” — *« Pour un architecte la question est autre : quel outil aide les équipes à mieux concevoir, réduire la dette, accélérer et améliorer la qualité ? »*
  > “While Copilot improves developer velocity, it has limited awareness of the broader solution architecture. It doesn't inherently understand organizational standards, domain boundaries, or long-term architectural decisions unless they're explicitly provided in context.” — *« Copilot accélère, mais ne comprend pas les standards, frontières de domaine ni décisions durables sauf si on les fournit explicitement au contexte. »*
- **Intérêt architecte** : grille d'évaluation d'outils par impact architectural (et non par vitesse de frappe) — utilisable telle quelle en avant-vente technique.

### 20. « The Agentic Solution Architect: The Missing Layer Every Role in IT Needs Now »
- **URL** : https://www.linkedin.com/pulse/agentic-solution-architect-missing-layer-every-role-needs-rashid-bxyce
- **Plateforme / auteur** : LinkedIn (article Pulse) — Dr. Humayun (Hugh) Rashid
- **Date** : 2026-07-13
- **Engagement** : non visible en lecture invite
- **Citations** :
  > “Companies including Cisco, NVIDIA, and Cognizant are now hiring for 'Agentic Solutions Architect,' 'Agentic AI Architect,' and similar roles.” — *« Cisco, NVIDIA, Cognizant recrutent des 'Agentic Solutions Architect'. »* **[non vérifié indépendamment]**
  > “Most IT professionals think the path to architecture runs through mastering more technology. It doesn't.” — *« Beaucoup croient que la voie vers l'architecture passe par plus de technologie. C'est faux. »*
- **Intérêt architecte** : documente l'émergence d'un intitulé de poste hybride EA/IA ; à traiter comme signal de marché, pas comme preuve.

### 21. Post LinkedIn de Nick Tune (architecture appliquée par la build)
- **URL** : https://www.linkedin.com/posts/nick-tune_enforced-application-architecture-for-agents-activity-7494123210037346304-1qSi
- **Plateforme / auteur** : LinkedIn — Nick Tune (Principal Engineer & consultant, auteur *Architecture Modernization*)
- **Date** : 2026-08-14
- **Engagement** : non visible en lecture invite
- **Citations** :
  > “An architecture doc is advice an agent can talk itself out of. A check that fails the build is feedback it cannot.” — *« Un document d'architecture est un conseil dont un agent peut se persuader de s'affranchir. Un contrôle qui casse le build est un feedback auquel il ne peut pas échapper. »*
  > “It also has to fire inside the agent's own loop rather than in CI afterwards. A violation caught after the run is a bug report for a human to triage. Caught during the run, it is the agent's next iteration.” — *« Le contrôle doit se déclencher dans la boucle de l'agent, pas en CI après coup : détectée après, la violation est un ticket ; détectée pendant, c'est l'itération suivante. »*
- **Intérêt architecte** : la formulation la plus opérationnelle de l'« architecture-as-code pour agents » (frontières de domaine, couches, permissions fines).

### 22. « Agent = Model + Harness: Engineering the Enterprise Control Layer »
- **URL** : https://www.linkedin.com/pulse/agent-model-harness-engineering-enterprise-control-layer-zm5rc
- **Plateforme / auteur** : LinkedIn — compte Tech Mahindra (publication d'entreprise, pas un architecte nommé)
- **Date** : 2026-11-05
- **Engagement** : non visible en lecture invite
- **Citations** :
  > “Agent = Model + Harness.” — *« Agent = Modèle + Harnais. »*
  > “With every enterprise having access to the same frontier models, the advantage is shifting to the layer around models.” — *« Toutes les entreprises accédant aux mêmes modèles de pointe, l'avantage se déplace vers la couche qui entoure les modèles. »*
- **Intérêt architecte** : formule mémorisable pour vendre un programme « control layer » (données, outils, contexte, gouvernance) en avant-vente.

### 23. Post X de Leo Gorodinski — « Constraint Decay »
- **URL** : https://x.com/eulerfx/status/2119495926083625106
- **Plateforme / auteur** : X — Leo Gorodinski (@eulerfx), praticien logiciel (Del Mar, CA) ; rôle exact **[non vérifié]**
- **Date** : 2026-11-08
- **Engagement** : 8 réponses, 6 reposts, 77 likes, 87 bookmarks, 5 817 vues (au moment de la lecture)
- **Citations** :
  > “Coding agents don't like being told how to architect their code. In Constraint Decay, requiring Clean Architecture, a specific database, and an ORM cut assertion pass rates by ~27 points. The database requirement hurt most. Agents often introduced functional bugs while trying to comply.” — *« Les agents n'aiment pas qu'on leur dicte l'architecture : imposer Clean Architecture + base + ORM fait chuter le taux de réussite d'environ 27 points ; les agents introduisent des bugs fonctionnels en essayant de se conformer. »*
  > “requiring structure isn't the same as providing it.” — *« Exiger une structure n'est pas la fournir. »*
  > “Lower pass rates don't establish that the architecture is worse, but we should revisit what we consider good architecture in the agentic era.” — *« Un taux plus bas ne prouve pas que l'architecture est mauvaise, mais il faut revisiter ce qu'est une bonne architecture à l'ère agentique. »*
- **Intérêt architecte** : la contradiction la plus utile au discours « il suffit de mettre les règles d'archi dans le prompt » ; à lire avec les caveats de l'auteur (comparaison non contrôlée).

### 24. Post X de Merill Fernando — identité d'agent vs auth MCP
- **URL** : https://x.com/merill/status/2034059156584550881
- **Plateforme / auteur** : X — Merill Fernando (@merill), « Ex-Microsoft Entra PM », blogueur identité (Melbourne)
- **Date** : 2026-03-18
- **Engagement** : 5 réponses, 26 reposts, 154 likes, 158 bookmarks, 10 629 vues
- **Citations** :
  > “MCP auth for enterprise is confusing and most of the confusion comes down to one thing: mixing up agent identity and MCP authentication.” — *« L'auth MCP en entreprise est confuse, et tout vient d'une chose : confondre identité de l'agent et authentification MCP. »*
  > “It's incredibly easy to blur the lines between agent identity and MCP authentication, which is exactly where things can get messy for an architecture team.” — *« La frontière est très facile à brouiller — c'est précisément là que ça devient ingérable pour une équipe d'architecture. »*
- **Intérêt architecte** : nomme le point de conception (App ID distinct, scopes auditables, hosting APIM/Logic Apps/EasyAuth) qui fera échouer un programme MCP d'entreprise.

### 25. Post X de Dan Patrascu-Baba — la nouvelle couche legacy
- **URL** : https://x.com/danpdc/status/2076195435580965248
- **Plateforme / auteur** : X — Dan Patrascu-Baba (@danpdc), développeur/fondateur (Atherio, d'après ses posts) **[rôle non vérifié]**
- **Date** : 2026-07-12
- **Engagement** : non visible sur la page rendue (compteurs non exposés)
- **Citations** :
  > “We may be creating the next generation of legacy systems before AI-assisted engineering has even properly started.” — *« Nous sommes peut-être en train de créer la prochaine génération de systèmes legacy avant même que l'ingénierie assistée par IA ait vraiment commencé. »*
  > “Most teams experimenting with coding agents are gradually building an additional execution layer around them: .md files, skills, rules, hooks, MCP configurations, permission policies, prompt templates and model-specific workarounds.” — *« La plupart des équipes se construisent une couche d'exécution autour des agents : fichiers .md, skills, règles, hooks, configs MCP, politiques de permission, templates de prompt et contournements propres à chaque modèle. »*
- **Intérêt architecte** : formule le risque de dette « de second ordre » (le harnais lui-même devient legacy) que peu de roadmaps anticipent.

### 26. METR — « Measuring the Impact of Early-2025 AI on Experienced Open-Source Developer Productivity »
- **URL** : https://metr.org/blog/2025-07-10-early-2025-ai-experienced-os-dev-study/
- **Plateforme / auteur** : METR (organisme de recherche) — Joel Becker, Nate Rush, Beth Barnes, David Rein
- **Date** : 2025-07-10 (étude fondatrice ; la page signale une mise à jour de février 2026 non lue ici)
- **Engagement** : n.d.
- **Citations** :
  > “when developers use AI tools, they take 19% longer than without—AI makes them slower.” — *« Avec les outils IA, les développeurs mettent 19 % plus de temps : l'IA les ralentit. »*
  > “We view this result as a snapshot of early-2025 AI capabilities in one relevant setting.” — *« Un instantané des capacités début 2025 dans un contexte donné. »*
- **Intérêt architecte** : la référence méthodologique (RCT) à opposer aux ROI déclaratifs ; à citer avec sa date, pas comme verdict sur 2026.

---

## 3. Thèmes émergents et consensus

**a) Le harnais comme produit d'architecture.** Thoughtworks en fait un thème de volume (« harness engineering at scale »), Cecilia Geraldo en fait un produit avec propriétaire, Tech Mahindra en fait une formule commerciale (« Agent = Model + Harness »). Consensus : la couche instructions/outils/contexte/garde-fous est le facteur différenciant principal, et elle n'a souvent ni propriétaire ni stratégie.

**b) L'architecture doit être exécutable, pas déclarative.** Nick Tune (build-breaking checks dans la boucle), Daniel Vaughan (hooks + fitness functions + ADR), Thoughtworks (ADR et politique de sécurité *dans* le harnais d'entreprise). Le document d'architecture survit comme **contexte machine**, pas comme livrable de conformité.

**c) Spécifier avant de générer, mais avec des points d'extension.** Microsoft/Spec Kit décrit une chaîne d'artefacts traçable (principes → spec → plan → tâches → code → tests) et une personnalisation en quatre couches pour éviter le fork par équipe. Le SDD devient une affaire de **catalogue gouverné**.

**d) Contexte : divulguer progressivement, mesurer en tokens.** AGENTS.md maigre + liens, MCP et skills chargés à la demande, raisonnement ancré sur graphe de code, *context profiling*. Le contexte est traité comme une ressource budgétée (tokens, cache par modèle).

**e) Revue graduée par le risque.** Sandboxing par défaut, humain sur l'irréversible, auto-merge du faible risque après CI. Le vocabulaire « human-in-the-loop theater » devient un lieu commun : la qualité de la revue, pas sa présence, est le critère.

**f) Le goulot est en aval du code.** Thoughtworks (path-to-production mapping), GitHub (« do you feel 400% more productive? »), Addy Osmani (review). Les architectes déplacent l'investissement vers tests, pipelines, observabilité de production.

**g) Sécurité = identité + périmètre.** Sandboxing (Thoughtworks), threat modeling, identité d'agent distincte de l'auth MCP (Merill Fernando), contrôles de confiance à chaque étape (AWS). Le sujet n'est plus « le prompt », c'est le **plan de contrôle**.

**h) Le legacy est le cas d'usage réel.** Brownfield (Osmani), audit gap (Vaughan), couche d'exécution qui devient dette (Patrascu-Baba). Les architectes d'intégration y trouvent leur valeur : cartographier les contraintes invisibles.

---

## 4. Contradictions, hype vs réalité, signaux faibles

**Contradictions assumées**
1. **Débit vs productivité.** GitHub : +400 % de commits sur un an. METR : −19 % de vitesse chez des devs expérimentés (2025). Thoughtworks : le débit de code est une *Caution*. Les trois peuvent être vrais simultanément (volume ↑, cycle ↑, valeur inchangée) — c'est précisément le piège.
2. **Imposer l'architecture vs la fournir.** « Mettez vos règles d'archi dans le prompt » (discours dominant) vs « Constraint Decay » (Gorodinski : −27 points de réussite) vs « fournir des squelettes améliore la correction ». Synthèse praticienne : fournir des structures (types, contrats, scaffolds de référence), pas des interdits en prose.
3. **Spec-driven « default » vs absence de consensus.** Les posts X grand public annoncent le SDD comme « architecture par défaut » ; Thoughtworks écrit noir sur blanc qu'il n'y a « pas encore de consensus » sur le harnais d'entreprise et recommande de le garder mince et fédéré.
4. **Documentation générée = progrès ?** Simon Brown : les diagrammes générés sont « plausibles mais majoritairement mauvais », et invisibles à ceux qui ne savent pas juger. À l'inverse, Thoughtworks classe la « documentation sprawl » en *Caution* — même diagnostic par un autre chemin.
5. **Human-in-the-loop partout, gouvernance nulle part.** Tous revendiquent l'humain dans la boucle ; Thoughtworks montre que l'étape d'approbation peut n'être qu'un « puits de responsabilité ».

**Hype vs réalité**
- Le ROI est majoritairement raconté par les éditeurs (commits, PR, tokens) ; la seule mesure contrôlée largement citée est un ralentissement de 19 % (2025), avec des caveats explicites.
- Les nouveaux intitulés (« Agentic Solutions Architect ») et les offres d'emploi associées sont rapportés par des articles LinkedIn, non vérifiés indépendamment.
- Les résultats de benchmarks d'agents (« +27 points », « 5,9× de code ») circulent sans protocole reproductible ; leurs auteurs eux-mêmes appellent à la prudence.

**Signaux faibles à surveiller**
- **Le harnais devient un produit** (Thoughtworks) : apparition probable d'un marché « enterprise harness » comparable au platform engineering.
- **Les agents comme contrainte de conception, pas seulement de production** : « revisiter ce qu'est une bonne architecture à l'ère agentique » (Gorodinski), diagrammes non relisibles (Brown).
- **La dette du harnais** : `.md`, skills, hooks, configs MCP et contournements par modèle forment déjà une couche à maintenir (Patrascu-Baba).
- **Le passage du contrôle unitaire au contrôle statistique** : mutation testing, property-based testing, TLA+/Quint, revue sémantique assistée (Thoughtworks).
- **Modèles ouverts et routage** pour la confidentialité et le coût (Thoughtworks : open-weight, local coding models, model routing) — début de découplage entre « meilleur modèle » et « bon choix d'architecture ».
- **Titres de poste hybrides EA/IA** et architectes en avant-vente qui évaluent des outils par « outcomes architecturaux » (Ankit Gupta).

---

## 5. Limites

- **Recherche** : l'outil de recherche natif a échoué (HTTP 402) sur toute la session. La découverte s'est appuyée sur DuckDuckGo HTML via proxy de lecture, avec des résultats parfois pollués par du contenu SEO de fournisseurs (surtout sur « MCP entreprise » et « multi-repo »). Ces contenus ont été écartés faute de vérifiabilité.
- **X/Twitter** : les pages de statut ne sont lisibles que via proxy ; les compteurs (vues, likes, reposts) sont un instantané à la date de lecture et peuvent avoir changé. Aucune recherche native X n'est accessible sans compte : l'échantillon de posts est donc **opportuniste**, pas représentatif.
- **LinkedIn** : les articles Pulse sont lisibles en lecture invite, mais les profils passent par un *authwall* ; les intitulés de poste et l'engagement ne sont pas vérifiables. Deux fiches (#19, #20) reposent sur des articles dont l'auteur se présente comme architecte, sans confirmation indépendante.
- **Bluesky / Mastodon** : la recherche Bluesky est indisponible hors connexion (« Search is currently unavailable when logged out ») et la recherche Mastodon non authentifiée ne renvoie pas de résultats fédérés exploitables. **Aucune source Bluesky ou Mastodon n'a donc pu être vérifiée** — l'absence de ces plateformes dans ce document est un trou de couverture, pas une preuve de moindre activité.
- **InfoQ** : le corps des articles est réservé aux comptes ; seule la synthèse éditoriale est citable (#18), et la date n'est pas affichée.
- **Thoughtworks Radar** : les blips sont datés au volume (novembre 2026), pas au jour ; les auteurs sont le Technology Advisory Board, pas des individus.
- **Biais de sélection** : sources majoritairement anglophones, early adopters, souvent liées à des éditeurs (GitHub, Microsoft, AWS) ou à des cabinets (Thoughtworks, Tech Mahindra). Les retours d'expérience négatifs ou les programmes échoués sont structurellement sous-représentés.
- **Chiffres** : les métriques fortes (5,9× de croissance de code, −27 points, +400 % de commits) sont citées telles que publiées ; je n'ai pas reproduit les protocoles. Elles doivent être lues comme des affirmations d'auteurs, pas comme des mesures validées.
