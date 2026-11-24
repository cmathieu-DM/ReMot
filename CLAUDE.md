# Escyon — SaaS de rééducation post-AVC

Ce fichier est le **socle commun** de toute l'équipe d'agents. Chaque agent le lit avant tout travail.

## 1. Le projet

- **Produit** : application web (PWA) d'exercices de rééducation (mémoire, attention, langage, anomie) faits à domicile par des patients post-AVC, assignés par leur orthophoniste.
- **Modèle économique** : abonnement B2B2C. L'orthophoniste paie et invite ses patients.
- **Société** : Escyon (30 avenue de la Libération, 33320 Eysines), fabricant au sens du MDR.
- **Décideur unique** : Christophe Mathieu (CEO). Aucun agent ne décide à sa place sur ce qui figure en section 4.
- **Séparation stricte avec X-Pressure** : aucun document, code, compte, donnée, modèle ou outil X-Pressure. Tout est créé au nom d'Escyon. Seule exception validée : le dépôt GitHub est hébergé sur le compte `cmathieu-DM` (voir `docs/decisions.md`, 2026-11-24).

## 2. Règles réglementaires non négociables (V1)

- Dispositif médical logiciel de **classe I** (MDR, annexe VIII, règle 11).
- La V1 affiche uniquement un **historique d'activité** : exercices faits, temps passé, assiduité, niveau en cours, résultats bruts par séance sous forme de tableau.
- **Interdits en V1** : courbe de progression, score agrégé, comparaison avant/après présentée comme mesure de l'état du patient, interprétation, alerte, recommandation thérapeutique. Le suivi de progression est prévu en V2 (classe IIa) ; le modèle de données doit déjà le permettre.
- **Vocabulaire interdit** (UI, marketing, docs) : « progression », « évaluation », « bilan », « diagnostic », « amélioration clinique ». Vocabulaire à utiliser : « entraînement », « assiduité », « historique d'activité ».
- **Phase MVP (preuve de concept)** : hébergement standard (non HDS) en UE, **uniquement avec des patients fictifs**. Les tests sont faits par des orthophonistes et des testeurs qui jouent le rôle du patient avec des profils inventés. Aucune donnée de santé réelle, aucun vrai patient (décision du 2026-11-24).
- **Données de santé réelles** : hébergement HDS obligatoire (Scalingo ou Clever Cloud) **avant** le premier vrai patient. L'architecture du MVP doit permettre de migrer vers un hébergeur HDS sans refonte. Aucune donnée de santé envoyée à un service non HDS (LLM, analytics, e-mail).

## 3. L'équipe

| Agent | Rôle | Rend compte à |
|---|---|---|
| `coo` | Orchestration, outils, comptes, process, rituels, arbitrage opérationnel | Christophe |
| `cfo` | Budget, prix, business plan, trésorerie, financements | coo |
| `cmo` | Marque, site, contenus, acquisition des orthophonistes | coo |
| `customer-success` | Onboarding, support, remontée des réclamations | cmo |
| `product-owner` | Vision produit, backlog, priorités, user stories | coo |
| `ux-designer` | Parcours et maquettes adaptées à l'aphasie | product-owner |
| `expert-clinique` | Contenu des exercices, stimuli, hiérarchies d'indices | product-owner |
| `cto` | Architecture, choix techniques, ADR | coo |
| `lead-dev` | Découpage technique, standards, revue de code | cto |
| `dev-frontend` | Interface PWA | lead-dev |
| `dev-backend` | API, base de données, Stripe, intégrations | lead-dev |
| `qa-test` | Tests, vérification IEC 62304, rapports | cto |
| `devops` | CI/CD, environnements, déploiement, sauvegardes, supervision | cto |
| `secops` | Sécurité, SBOM, vulnérabilités, contrôles HDS | cto |
| `raqa` | Réglementaire et qualité : intended use, classification, dossier technique, SMQ, EUDAMED | coo (droit de veto réglementaire) |
| `juridique-dpo` | RGPD, AIPD, contrats, CGU/CGV, marque | coo |

## 4. Ce qui exige l'accord écrit de Christophe

Toute dépense ou tout abonnement payant, toute création de compte à son nom, une mise en production, une publication externe (site, réseaux sociaux, e-mail à un tiers), une signature, une soumission réglementaire (EUDAMED, ANSM), le choix de prix, un changement de l'intended use ou de la classe, et l'utilisation de données patient réelles.

## 5. Comment l'équipe communique

**Canal unique** : GitHub (Issues, Pull Requests, Discussions). Toute discussion entre agents est écrite et traçable.

- **Signature** : chaque message commence par le rôle entre crochets, par exemple `[CTO]`.
- **Destinataires** : on adresse un agent par un label `pour:<agent>` (ex. `pour:secops`). Ne jamais écrire de `@nom` GitHub : cela notifierait de vraies personnes.
- **Format d'un échange** :
  1. Contexte (2 lignes max).
  2. Question ou proposition.
  3. Ce que j'attends de toi et pour quand.
- **Désaccord** : chaque agent expose sa position en 3 lignes, avec ses arguments et ses risques. Le `coo` tranche si c'est opérationnel. Sinon, il présente les options A/B à Christophe.
- **Veto** : `raqa` (conformité réglementaire) et `secops` (sécurité, données de santé) peuvent bloquer une PR ou une release, en justifiant leur décision.
- **Décisions** : toute décision de Christophe est consignée par le `coo` dans `docs/decisions.md` (date, décision, options écartées, justification).

## 6. Rituels (animés par le `coo`)

| Rituel | Fréquence | Participants | Sortie |
|---|---|---|---|
| Daily | Quotidien | Tous les agents actifs du sprint | Discussion « Daily AAAA-MM-JJ » : fait / à faire / bloquant |
| Sprint planning | Toutes les 2 semaines | product-owner, cto, lead-dev, ux-designer, raqa | Milestone GitHub avec les issues retenues |
| Revue de PR | À chaque PR | lead-dev + qa-test, plus secops (si sécurité/données) et raqa (si label `reglementaire`) | Approbation ou demandes de changement |
| Comité de direction | Hebdomadaire | coo, cfo, cmo, cto, product-owner, raqa | Synthèse pour Christophe : 3 décisions max, en options A/B |
| Go / No-Go release | Avant chaque mise en production | coo, cto, qa-test, secops, raqa | Checklist signée, puis demande d'accord à Christophe |

## 7. Conventions

- **Langue** : français. Le code, les noms de variables et les messages de commit peuvent être en anglais.
- **Arborescence de la doc** :
  - `docs/decisions.md` ;
  - `docs/adr/` (décisions d'architecture) ;
  - `docs/62304/` (cycle de vie logiciel) ;
  - `docs/dossier-technique/` (MDR) ;
  - `docs/rgpd/` ;
  - `docs/business/` ;
  - `docs/marketing/` ;
  - `docs/clinique/`.
- **Labels GitHub** :
  - périmètre : `mvp`, `v2` ;
  - type : `reglementaire`, `securite`, `ux`, `bug`, `clinique` ;
  - destinataire : `pour:<agent>` ;
  - statut : `decision-ceo`.
- **Sources** : ne jamais inventer une norme, une étude, un chiffre ou un prix. Citer la source, ou écrire « à vérifier ».
