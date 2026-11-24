# ADR-001 — Hébergement et stack du MVP

- **Statut** : Proposé
- **Date** : 2026-11-24
- **Auteur** : cto
- **Relecteurs attendus** : secops, devops, lead-dev, raqa, cfo
- **Décision liée** : `docs/decisions.md`, 2026-11-24 — MVP hors HDS, patients fictifs uniquement, HDS obligatoire avant le premier vrai patient.

## 1. Contexte

Christophe a décidé que le MVP serait hébergé hors HDS, dans l'UE, avec des patients fictifs, pour valider le concept vite et à moindre coût. Le passage en HDS doit pouvoir se faire **sans refonte** avant le premier vrai patient.

Contraintes à respecter :

- CLAUDE.md §2 : aucune donnée patient réelle hors production HDS, aucune donnée de santé vers un service non HDS (LLM, analytics, e-mail).
- Le modèle de données doit permettre le suivi longitudinal de la V2 (classe IIa), mais la V1 n'affiche qu'un historique d'activité.
- Tous les comptes sont au nom d'Escyon. Leur création et tout abonnement payant exigent l'accord écrit de Christophe (CLAUDE.md §4).

Les prix ci-dessous ont été relevés le 2026-11-24 sur les sites des fournisseurs. Ils sont HT. Toute valeur marquée « à vérifier » doit être confirmée par devops avant engagement.

## 2. Options d'hébergement

### Option A — Scalingo (région standard osc-fr1), recommandée

| Élément MVP | Offre | Prix public / mois HT |
|---|---|---|
| Application Next.js | 1 conteneur M (512 Mo) | 14,40 € |
| PostgreSQL | Starter 512 Mo, 10 Go, sauvegardes quotidiennes et PITR | 7,20 € |
| **Total par environnement** | | **≈ 21,60 €** |

Essai gratuit de 30 jours annoncé sur la page tarifs.
Source : https://scalingo.com/pricing

**Trajectoire HDS** (même fournisseur, même buildpack, même `Procfile`, mêmes variables d'environnement) :

- HDS exige un plan Business ou Enterprise avec au moins 2 conteneurs (https://scalingo.com/pricing).
- Scalingo déclare ne pas facturer de surcoût pour la certification HDS elle-même (FAQ de https://scalingo.com/pricing).
- **Point clé** : l'option HDS se choisit à la création de la ressource. Une ressource existante ne peut pas être convertie (https://doc.scalingo.com/platform/hds). La bascule consiste donc à créer une **nouvelle** application et une nouvelle base HDS, puis à y redéployer le même code. C'est souhaitable ici : les données fictives du MVP ne doivent de toute façon pas être reprises.
- Coût HDS minimal estimé, par environnement : 2 conteneurs M (28,80 €) + PostgreSQL Business 512 Mo (20 €) = **≈ 48,80 €/mois HT**, hors stockage additionnel et support. À confirmer avec Scalingo.
- Un avenant HDS aux CGV existe (https://scalingo.com/gtc-appendix-health-data-hosting). Son contenu et la signature relèvent de juridique-dpo et de Christophe.
- Le certificat HDS de Scalingo a été renouvelé selon le référentiel HDS 2.0 (https://doc.scalingo.com/compliance/hds).

**Avantages** : prix publics et prévisibles, chemin HDS documenté en libre-service, aucune modification de code prévue.
**Limites** : conteneur M pour Next.js (consommation mémoire à mesurer, prévoir L à 28,80 € si nécessaire) ; pas de stockage objet natif (sans objet pour le MVP, voir §4).

### Option B — Clever Cloud (zone Paris)

| Élément MVP | Offre | Prix calculé / mois HT (30 j) |
|---|---|---|
| Application Node.js | instance nano (512 Mio) ou XS (1 Gio) | 6 € ou 16 € |
| PostgreSQL | plan XXS (XXS_SML) | ≈ 5,25 € (taille et stockage : à vérifier) |
| **Total par environnement** | | **≈ 11 à 21 €** |

Les montants proviennent de l'API publique de tarification de Clever Cloud (`https://api.clever-cloud.com/v4/billing/price-system?zone_id=par&currency=EUR`, prix horaires × 720). La page tarifs ne publie qu'un estimateur interactif (https://www.clever.cloud/pricing). Des crédits gratuits sont offerts à l'inscription sans carte bancaire, pour un montant non publié.

**Trajectoire HDS** :

- Certification HDS obtenue en janvier 2025 (https://www.clever.cloud/blog/press/2025/01/15/clever-cloud-obtains-hds-certification/).
- Zones HDS en France : Paris, Gravelines et Roubaix. PostgreSQL est dans le périmètre. Node.js n'est pas cité nommément (« JavaScript » l'est) : à confirmer (https://www.clever.cloud/health-data-hosting/).
- Un **contrat spécifique** négocié avec un account manager est requis. Aucun prix HDS n'est publié.

**Avantages** : MVP le moins cher, facturation à la seconde.
**Limites** : coût et conditions HDS inconnus avant négociation, ce qui fait peser un risque budgétaire et de calendrier sur la bascule ; Node.js à confirmer dans le périmètre HDS.

### Alternative grand public C — Vercel + Neon (PostgreSQL serverless)

- Vercel : le plan Hobby est gratuit. Son usage commercial est à vérifier dans les CGU Vercel ; à notre connaissance, il est réservé à un usage personnel. Le plan Pro coûte 20 $ par développeur et par mois (https://vercel.com/docs/plans/hobby).
- Neon : plan gratuit (1 Go par projet, 100 CU-heures par projet et par mois), puis facturation à l'usage sans minimum (https://neon.com/pricing). La disponibilité d'une région UE est à vérifier.
- **Coût de migration vers HDS : élevé.** Il faudra quitter les primitives propres à Vercel (fonctions serverless, middleware edge, optimisation d'images, cron, logs, previews), réécrire le pipeline CI/CD, conteneuriser l'application et changer de driver de base. Estimation : 1,5 à 3 semaines de travail devops et dev-backend, plus une campagne de non-régression. Il y a aussi deux sous-traitants supplémentaires (sociétés de droit américain) à couvrir dans le registre RGPD, même pour les comptes de test des orthophonistes.
- **Conclusion** : c'est l'option la plus rapide au premier jour, mais elle contredit l'objectif « migration sans refonte ». Écartée.

### Synthèse

| | A — Scalingo | B — Clever Cloud | C — Vercel + Neon |
|---|---|---|---|
| Coût MVP par environnement | ≈ 22 € | ≈ 11 à 21 € | 0 € (Hobby, usage commercial à vérifier) à 20 $ et plus |
| Coût HDS public | oui, ≈ 49 € minimum | non (sur contrat) | sans objet |
| Bascule HDS | nouvelle application et nouvelle base, même code | même code, contrat à négocier | refonte du déploiement |
| Risque de verrouillage | faible (buildpacks, Postgres standard) | faible | moyen à fort |

## 3. Décision proposée

**Option A, Scalingo**, en région standard, avec deux environnements :

- `staging` : déploiement continu depuis `main` ;
- `demo` : environnement de démonstration (patients fictifs), créé à la demande pour la présentation aux orthophonistes.

L'environnement `production` sera créé **directement en HDS** (plan Business, au moins 2 conteneurs), le jour où Christophe autorisera le premier vrai patient. Aucune donnée ne sera migrée depuis `staging` ou `demo`.

Option B en repli si Scalingo ne convient pas (conditions de l'avenant HDS, support). Dans ce cas, il faudra demander dès maintenant à Clever Cloud un devis HDS pour lever l'inconnue.

Pour rester portable entre A et B :

- Next.js en `output: 'standalone'`, démarré par `node server.js` ;
- configuration exclusivement par variables d'environnement (12-factor) ;
- aucun service propriétaire de l'hébergeur dans le code ;
- migrations SQL versionnées.

## 4. Stack confirmée ou ajustée

| Couche | Choix | Justification |
|---|---|---|
| Front et back | **Next.js** (App Router) + **TypeScript** strict, en PWA (manifest et service worker). Version : dernière version stable maintenue, à figer par lead-dev | Stack de référence confirmée. Un seul déploiement pour l'espace orthophoniste, l'espace patient et l'API. |
| Base de données | **PostgreSQL** (version majeure supportée par l'hébergeur, à vérifier) | Confirmé. Même moteur en MVP et en HDS. |
| Accès aux données | ORM avec migrations versionnées (Prisma ou Drizzle, choix de lead-dev à justifier dans la liste SOUP) | Traçabilité des évolutions de schéma, ce qui est utile pour l'IEC 62304. |
| Authentification orthophoniste | Bibliothèque auto-hébergée, données en base Escyon, **MFA TOTP obligatoire** (Better Auth avec son plugin 2FA ou Auth.js + otplib : arbitrage par secops) | Pas d'IdP SaaS tiers qui verrait l'identité des patients ou des soignants. |
| Accès patient | Code d'appairage à usage unique, généré par l'orthophoniste et **remis en séance** (code ou QR), puis session longue liée à l'appareil, révocable par l'orthophoniste ; code PIN facultatif | Adapté à l'aphasie (pas de mot de passe ni d'e-mail obligatoire). Évite d'envoyer par e-mail une invitation qui révélerait un suivi orthophonique, donc une donnée de santé. |
| Paiement | **Stripe en mode test** uniquement (Checkout + webhooks d'abonnement) | Aucune donnée de santé ne transite par Stripe (identité de l'orthophoniste payeur uniquement). Compte Stripe au nom d'Escyon : accord de Christophe requis. |
| E-mails | MVP : e-mails transactionnels **destinés aux orthophonistes uniquement** (vérification, réinitialisation), via Brevo (offre gratuite à vérifier). En `staging`, un collecteur local (Mailpit) peut suffire. | Aucune donnée patient dans un e-mail : règle à tester automatiquement. |
| Audio des consignes | Fichiers pré-générés, versionnés et servis comme ressources statiques de l'application | Ce ne sont pas des données patient. Aucun appel à un service vocal à l'exécution. La licence de la voix de synthèse utilisée pour la génération est à vérifier (juridique-dpo). |
| Erreurs | Sentry, région UE, `sendDefaultPii: false`, filtrage `beforeSend` (offre gratuite à vérifier) | Conforme à la stack de référence. |
| Analytics | Aucun en MVP | CLAUDE.md §2. |

### Modèle de données compatible avec la V2 (principe)

- `practitioner`, `patient` (pseudonyme en MVP, aucune identité réelle), `practitioner_patient` (lien et droits).
- `exercise_definition` versionnée : type, paramètres, version du contenu et des stimuli.
- `assignment` : exercice, niveau et fréquence attribués par l'orthophoniste.
- `session` : début, fin, durée active, appareil.
- `trial` : **un enregistrement par essai**, horodaté. Il contient le stimulus, la réponse brute, la justesse, la latence, le niveau d'indice utilisé et la version de l'exercice.
- Aucune colonne de score agrégé ni aucune vue d'agrégation en V1. L'interface V1 lit `session` et `trial` pour produire le tableau d'historique d'activité.

### Garde-fous propres au MVP hors HDS

- Bandeau permanent « Démonstration — données fictives uniquement ».
- Champs d'identité du patient limités à un pseudonyme, sans date de naissance ni texte libre clinique.
- CGU de test signées par les orthophonistes testeurs, interdisant toute donnée réelle (juridique-dpo).
- Comptes de démonstration créés par Escyon et non en libre inscription : à valider par product-owner.

## 5. Conséquences

**Positives** : coût mensuel de l'ordre de 20 à 45 € HT pour un ou deux environnements, chemin HDS chez le même fournisseur, code identique entre MVP et production.

**Négatives et risques** :

- La bascule HDS demande de recréer les ressources : application, base, variables, domaine, sauvegardes. devops doit écrire la procédure (runbook) et la tester avant le Go/No-Go.
- Le coût passe à ≈ 49 € HT minimum par environnement HDS (staging HDS non obligatoire, puisqu'aucune donnée réelle n'y est stockée : à confirmer par secops).
- Le code du MVP sera réutilisé en production. Le **cycle de vie IEC 62304 s'applique donc dès maintenant** : plan de développement, liste des SOUP, revues. Sinon il faudra le rétro-documenter. Classe de sécurité logicielle proposée : **A**, à justifier avec raqa à partir de l'analyse de risques ISO 14971.

**Actions dépendantes** (aucune n'est engagée par cet ADR) :

1. Accord de Christophe pour créer les comptes Scalingo, Stripe (mode test), Brevo et Sentry au nom d'Escyon.
2. devops : prototype de déploiement Next.js standalone sur un conteneur M (mesure de la mémoire).
3. juridique-dpo : lecture de l'avenant HDS de Scalingo.
4. secops : arbitrage de la bibliothèque d'authentification et du mécanisme d'accès patient.

## 6. Annexe — Estimation de charge du MVP démontrable (ordre de grandeur)

Le périmètre comprend : espace orthophoniste, 3 ou 4 exercices, espace patient PWA et historique d'activité. L'unité est la semaine-équivalent développeur ; ce sont des ordres de grandeur à affiner en sprint planning avec lead-dev.

| Lot | Charge |
|---|---|
| Socle : dépôt, CI, Next.js, schéma de base, déploiement `staging` | 1,5 à 2 |
| Authentification orthophoniste avec MFA et accès patient par code d'appairage | 1,5 à 2 |
| Espace orthophoniste : patients fictifs, assignation, réglage du niveau | 1,5 à 2 |
| Moteur d'exercice générique (essais, indices, audio, enregistrement `trial`) | 2 |
| 3 ou 4 exercices (par exemple dénomination avec indices, mémoire, attention) | 2 à 3 |
| Espace patient PWA adapté à l'aphasie | 1,5 à 2 |
| Historique d'activité (tableau par séance) | 1 |
| Stripe en mode test (Checkout et webhooks) | 1 |
| Tests, revues, livrables IEC 62304 classe A minimaux | 1,5 à 2 |
| **Total** | **≈ 13,5 à 17 semaines-équivalent**, soit environ **7 à 9 semaines calendaires** avec dev-frontend et dev-backend en parallèle |

**Risques principaux** :

1. **Contenus cliniques** (stimuli, images et sons sous licence commerciale, hiérarchies d'indices). C'est le chemin critique : sans eux, les exercices restent des coquilles vides.
2. Les itérations UX propres à l'aphasie peuvent allonger le lot de l'espace patient.
3. Dérive du périmètre vers des fonctions interdites en V1 (score, courbe). Une revue raqa est nécessaire sur les écrans de l'historique.
4. Le choix de la bibliothèque d'authentification et du mécanisme d'accès patient (secops) bloque le lot d'authentification.
5. Charge de revue du code produit par les agents : la capacité de lead-dev et de qa-test est le goulot d'étranglement.
6. La consommation mémoire de Next.js sur un conteneur de 512 Mo peut imposer un conteneur L (surcoût de 14,40 € par mois).
