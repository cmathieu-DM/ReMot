# [CFO] Comité de direction du 2026-11-24 : grille tarifaire et budget MVP

> Document de travail. Le choix de prix et toute dépense relèvent de Christophe (CLAUDE.md, section 4).
> Je ne suis pas expert-comptable : TVA, assurances et traitement comptable sont à valider par le comptable d'Escyon.
> Prix relevés le 2026-11-24 sur les pages publiques citées. Tous les montants Escyon sont HT sauf mention.

## 1. Concurrence : prix publics relevés

| Offre | Modèle | Prix public relevé | Essai | Source |
|---|---|---|---|---|
| HappyNeuron Pro – Starter | Abonnement praticien, 5 comptes patients simultanés | 59 $/mois en annuel (708 $/an) ; 77 $/mois en trimestriel (231 $/trimestre) | 14 jours | https://www.happyneuronpro.com/en/pricing/ |
| HappyNeuron Pro – Professional | Abonnement praticien, patients illimités | 1 praticien : 119 $/mois en annuel (1 428 $/an), 155 $/mois en trimestriel ; 2-3 praticiens : 179 $/mois annuel ; 4-5 : 239 $/mois annuel ; 6+ sur devis | 14 jours | idem |
| HappyNeuron Pro – remises | — | -50 % jeunes diplômés ; offre chercheurs non détaillée | — | idem |
| Constant Therapy (patient) | Abonnement payé par le patient (B2C) | 29,99 $/mois ; pas d'annuel affiché ; remboursement possible sous 30 jours | 2 semaines | https://constanttherapyhealth.com/constant-therapy/for-patients/pricing/ |
| Constant Therapy (clinicien) | Compte clinicien gratuit ; offres « Partner / Enterprise » sans prix publié | Gratuit / sur devis | — | https://constanttherapyhealth.com/constant-therapy/for-clinicians-adult-speech-therapy/pricing/ |
| Tactus Therapy – Advanced Language Therapy | Achat unique d'app iOS, « no subscriptions » | 89,99 $ (App Store US) | Version Lite | https://apps.apple.com/app/id1428254496 |

Limites :
- HappyNeuron Pro n'affiche que des prix en dollars ; aucun prix en euros n'est publié sur la page consultée. **Prix France (happyneuron.com) à vérifier** (demande de devis possible, sans engagement).
- Je n'ai pas trouvé de prix publics pour d'autres logiciels d'orthophonie adulte français (recherche à poursuivre avec le `cmo` : éditeurs de matériel orthophonique, apps FR). **À vérifier.**
- Lecture : le marché de référence pour un praticien libéral est d'environ **60 à 155 $/mois** (HappyNeuron), contre un abonnement patient à **30 $/mois** chez Constant Therapy. La V1 d'Escyon est plus étroite (aphasie / anomie post-AVC, historique d'activité seulement, pas de fonctionnalités de classe IIa) : elle doit se positionner **nettement en dessous** de HappyNeuron Pro Professional.

## 2. Marché adressable

| Donnée | Valeur | Source / statut |
|---|---|---|
| Orthophonistes en France hexagonale | 28 398 | ADELI au 1er octobre 2024, repris par l'ARS Centre-Val de Loire : https://www.centre-val-de-loire.ars.sante.fr/system/files/2025-02/Orthophoniste_ProfSante2024.pdf |
| dont libéraux | 22 143 (78,0 %) ; salariés 6 166 (21,7 %) ; mixtes 89 | même source |
| Densité nationale | environ 43,4 pour 100 000 habitants | même source (lecture du graphique, à vérifier) |
| AVC par an en France | environ 150 000 nouveaux cas | La Revue du Praticien : https://www.larevuedupraticien.fr/article/post-avc-reeduquer-laphasie |
| Patients AVC aphasiques en phase initiale | « un tiers », soit 30 000 nouveaux cas par an | Le Quotidien du Médecin (titre d'article) : https://www.lequotidiendumedecin.fr/specialites/medecine-physique-et-de-readaptation/un-tiers — **incohérence à vérifier** : un tiers de 150 000 = 50 000 ; les deux sources n'ont sans doute pas la même base |
| Orthophonistes ayant suivi au moins une personne atteinte d'Alzheimer | 73 % des répondants (N ≈ 2 361, enquête 2024) | Fondation Médéric Alzheimer : https://fondation-mederic-alzheimer.org/wp-content/uploads/2025/03/synthese-lo-orthophonistes-58.pdf — indicateur indirect : beaucoup d'orthophonistes voient des adultes en neurologie |
| Part des orthophonistes libéraux suivant au moins un patient aphasique adulte post-AVC | **25 % (fourchette 15-35 %)** | **Hypothèse à valider** (aucune source trouvée ; à demander au `cmo` via sondage ou à la FNO) |

Marché adressable (libéraux, hypothèse centrale) : 22 143 × 25 % ≈ **5 500 orthophonistes**. Fourchette : 3 300 à 7 750.
Les salariés (hôpitaux, SMR) sont un second segment (achat institutionnel, cycle plus long) non compté ici.

## 3. Deux options de grille pour Christophe

Contrainte de calendrier : pendant le MVP, il n'y a **aucun vrai patient** (décision du 2026-11-24). Aucune facturation n'est donc possible avant : hébergement HDS, marquage CE classe I (déclaration de conformité, `raqa`) et CGV (`juridique-dpo`). La « bêta » ci-dessous est gratuite par construction.

### Option A : prix unique, simple

| Élément | Proposition |
|---|---|
| Mensuel | **29 € HT / praticien / mois**, patients illimités |
| Annuel | **290 € HT / an** (2 mois offerts) |
| Essai gratuit | 30 jours, sans carte bancaire |
| Cabinet | -20 % par praticien dès 2 praticiens sur une même facture (23,20 € HT / praticien / mois) ; 6+ sur devis |
| Lancement | Testeurs bêta du MVP : gratuit pendant le MVP, puis **tarif fondateur 19 € HT / mois garanti 12 mois** pour les 50 premiers abonnés payants |

Arguments : lisible, 4 fois moins cher que HappyNeuron Pro Professional en annuel, facile à paramétrer dans Stripe Billing (2 prix, 1 coupon). Risque : prix bas difficile à remonter quand la V2 (classe IIa) arrivera ; il faudra une offre V2 distincte.

### Option B : paliers selon le nombre de patients actifs

| Élément | Proposition |
|---|---|
| Essentiel | **19 € HT / mois**, jusqu'à 5 patients actifs |
| Illimité | **39 € HT / mois**, patients illimités |
| Annuel | 2 mois offerts (190 € et 390 € HT / an) |
| Essai gratuit | 30 jours sur l'offre Illimité, sans carte bancaire |
| Cabinet | 2 à 5 praticiens : **99 € HT / mois** pour le cabinet ; 6+ sur devis |
| Lancement | Testeurs bêta : gratuit pendant le MVP, puis 6 mois à -50 % |

Arguments : calqué sur la structure HappyNeuron (Starter / Professional), capte les orthophonistes qui n'ont que 1 à 3 patients aphasiques. Risque : plus complexe (comptage des patients actifs à coder, cas limites de facturation), revenu moyen incertain.

### Recommandation CFO

**Option A**, pour un lancement plus simple et plus rapide, avec revue du prix après 6 mois de données réelles (conversion, churn). Les montants restent des **hypothèses à tester** en entretien avec les orthophonistes bêta (`cmo`) avant la décision de Christophe.

## 4. Budget mensuel

### 4.1 Phase MVP (hors HDS, UE, patients fictifs)

Proposition : héberger le MVP chez **Scalingo, région standard**, pour passer en HDS chez le même hébergeur sans changer d'architecture (à confirmer par le `cto`).

| Poste | Coût mensuel HT | Source / statut |
|---|---|---|
| Conteneur applicatif Scalingo S (256 Mo) | 7,20 € | https://scalingo.com/pricing (estimation 30 jours) |
| PostgreSQL Scalingo Starter (512 Mo, 10 Go) | 7,20 € | idem |
| Nom de domaine (.fr ou .com) | environ 1 € (lissé sur 12 mois) | **à vérifier** auprès du registrar choisi |
| E-mail professionnel (1 boîte) | 0 à 7 € | **à vérifier** (offres gratuites possibles au départ) |
| GitHub (dépôt existant), CI GitHub Actions dans le quota gratuit | 0 € | **à vérifier** selon le volume de CI |
| Maquettes, documentation, suivi | 0 € (offres gratuites) | **à vérifier** avec le `coo` |
| **Total MVP** | **environ 15 à 25 € HT / mois** | Scalingo propose aussi un essai gratuit de 30 jours (page pricing) |

### 4.2 Passage HDS (avant le premier vrai patient)

| Poste | Coût mensuel HT | Source / statut |
|---|---|---|
| 2 conteneurs Scalingo M (512 Mo) | 28,80 € (2 × 14,40 €) | https://scalingo.com/pricing ; HDS sans surcoût mais exige une offre Business ou Enterprise et au moins 2 conteneurs |
| PostgreSQL Scalingo Business (512 Mo, 10 Go) | 20,00 € | idem |
| Variante région SecNumCloud | environ +20 % (34,56 € + 24,00 €) | idem ; non requise pour HDS, à trancher par `cto` / `secops` |
| Clever Cloud HDS (alternative) | **sur devis** : contrat HDS spécifique défini avec un account manager | https://www.clever.cloud/health-data-hosting/ |
| E-mail transactionnel (sans aucune donnée de santé) | 0 à 20 € | **à vérifier** |
| Stripe Billing (frais par transaction et frais Billing) | variable | **à vérifier** sur la page tarifs Stripe France |
| Assurance RC professionnelle et RC produit (fabricant de DM) | **à vérifier** (devis) | point majeur, à voir avec le `juridique-dpo` |
| Expert-comptable | **à vérifier** (devis) | — |
| Banque professionnelle | **à vérifier** | — |
| PRRC (personne chargée du respect de la réglementation, MDR art. 15) | **à vérifier** avec le `raqa` (externe possible pour une petite entreprise) | — |

Scalingo HDS : certification HDS 2.0 n° 38436, valable jusqu'au 11 septembre 2028 (https://doc.scalingo.com/compliance/hds).

## 5. Seuil d'abonnés

Les coûts fixes hors hébergement n'ont pas de prix public. J'utilise donc deux scénarios, à remplacer par des devis.

| Scénario de coûts fixes mensuels HT | Hypothèses | Seuil Option A (29 €) | Seuil Option A tarif fondateur (19 €) |
|---|---|---|---|
| Minimal : environ 350 € | Hébergement HDS 49 €, outils 30 €, comptable 150 €, assurances 100 €, banque 20 € (**hypothèses à valider**) | **13 abonnés** | 19 abonnés |
| Élargi : environ 1 000 € | Idem, plus PRRC externe, veille réglementaire, marketing minimal (**hypothèses à valider**) | **36 abonnés** | 55 abonnés |

Calcul : coûts fixes / (prix HT moins frais de paiement estimés à environ 3 %, **à vérifier**). Pas de rémunération de Christophe dans ces seuils ; avec un salaire, le seuil change d'ordre de grandeur (à chiffrer dans le business plan sur 3 ans).
Pour l'Option B, avec un revenu moyen supposé de 30 € HT par praticien (**hypothèse**), les seuils sont proches de ceux de l'Option A.

Lecture : 36 abonnés représentent environ 0,7 % du marché adressable central (5 500). Le seuil des coûts fixes paraît donc atteignable ; le vrai risque est le **délai** avant la première facture (HDS, CE, CGV).

## 6. Questions aux autres agents

- `pour:cto` : confirmes-tu Scalingo standard pour le MVP puis Scalingo HDS (2 conteneurs, PostgreSQL Business), ou une autre cible ? SecNumCloud nécessaire ?
- `pour:cmo` : peux-tu valider en entretien avec les orthophonistes bêta la part qui suit des patients aphasiques adultes et leur sensibilité au prix (19 / 29 / 39 €) ? Prix des concurrents FR à compléter.
- `pour:raqa` : quel calendrier et quel coût pour la déclaration de conformité classe I, le SMQ et la PRRC ? Sans CE, pas de première facture.
- `pour:product-owner` : l'Option B exige le comptage des « patients actifs » : est-ce acceptable dans le backlog V1 ? Un essai sans carte bancaire te convient-il ?
- `pour:juridique-dpo` : assurance RC produit et CGV : qui obtient les devis ?
- Comptable d'Escyon : TVA applicable aux abonnements (taux normal a priori pour un logiciel, **à confirmer**) et mentions de facture.
