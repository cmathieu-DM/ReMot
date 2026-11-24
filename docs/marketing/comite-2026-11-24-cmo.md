# [CMO] Contribution au comité de direction du 2026-11-24

Statut : **brouillon interne**. Rien n'est publié ni envoyé. Toute publication externe exige l'accord écrit de Christophe (CLAUDE.md §4). Toute allégation ci-dessous doit être validée par `raqa` avant usage externe.

Rappel du cadre (decisions.md, 2026-11-24) : le MVP est une **preuve de concept** testée **uniquement avec des patients fictifs**. Les orthophonistes testeurs jouent eux-mêmes (ou font jouer à un testeur) le rôle du patient avec des profils inventés.

---

## 1. Vérification préliminaire du nom « ReMot »

> **Avertissement** : ceci n'est **pas** une recherche d'antériorité INPI/EUIPO officielle ni un avis juridique. Ce sont des recherches web générales faites le 2026-11-24. La recherche officielle (INPI, EUIPO, OMPI, classes 9, 10, 41, 42, 44 à confirmer) revient au `juridique-dpo`.

### 1.1 Usages existants repérés

| Constat | Source | Risque estimé |
|---|---|---|
| Une société « REMOT » est active, APE 43.21A (installation électrique), à Pont-Scorff (56), active depuis 2010. | Avis de situation SIRENE : https://api-avis-situation-sirene.insee.fr/identification/pdf/51951258600016 | Faible a priori (secteur sans rapport), mais à confirmer : dépôt de marque éventuel inconnu. |
| Proximité visuelle et phonétique forte avec « Remote » : Remote (RH internationale, remote.com, site en français) et Remote.It (app). | https://remote.com/fr-fr/conditions-utilisation ; https://apps.apple.com/app/id1437569166 | **Moyen** : confusion de lecture (« faute de frappe de remote »), moteurs de recherche qui corrigent « remot » en « remote », SEO difficile sur le nom seul. |
| Aucun usage « ReMot » repéré en orthophonie, aphasie ou santé dans les résultats consultés. | Recherches web « ReMot orthophonie aphasie », « ReMot application rééducation » | Absence de résultat ≠ disponibilité. |
| Concurrent proche dans l'espace (nom différent) : **Rééduc&Moi** (Interlude Santé), app d'aide au suivi à domicile de programmes de rééducation conçus par les soignants. | https://apps.apple.com/us/app/id6471974514 | Pas un risque de nom, mais un concurrent à intégrer au positionnement (veille à faire). |

### 1.2 Domaines

| Domaine | Statut | Commentaire |
|---|---|---|
| remot.fr | **à vérifier chez un registrar** (WHOIS AFNIC) | Non confirmé par mes recherches. |
| remot.com | **à vérifier chez un registrar** | Hypothèse non vérifiée : un .com de 5 lettres est rarement libre. |
| remot.app | **à vérifier chez un registrar** | Non confirmé. |
| getremot.fr | **à vérifier chez un registrar** | Non confirmé. |

Aucune réservation ne doit être faite sans accord de Christophe (dépense).

### 1.3 Analyse marketing du nom

- **Pour** : court, prononçable, évoque « re-mot » (retrouver le mot), cohérent avec l'anomie ; lisible pour un public aphasique.
- **Contre** : confusion avec « remote », SEO faible sur le nom seul, la casse « ReMot » se perd souvent (« Remot »). Le nom évoque surtout le langage alors que le produit couvre aussi mémoire et attention.
- **Recommandation CMO** : garder « ReMot » comme **nom de code interne** ; ne pas investir dans l'identité visuelle ni réserver de domaine avant le retour du `juridique-dpo`. Préparer 3 noms alternatifs à soumettre à la même vérification (pistes non vérifiées, à faire en sprint suivant).

---

## 2. Positionnement et messages clés (brouillon, à valider par `raqa`)

**Positionnement (1 phrase)** :
ReMot permet à l'orthophoniste d'assigner à ses patients aphasiques des exercices d'entraînement à faire à domicile entre les séances, en français, sur une interface conçue pour les personnes aphasiques, avec un historique d'activité consultable.

**Message 1 — L'entraînement continue entre les séances.**
Vous choisissez les exercices (langage, anomie, mémoire, attention), votre patient s'entraîne chez lui, à son rythme.

**Message 2 — Une interface pensée pour l'aphasie.**
Consignes courtes, gros boutons, peu d'éléments à l'écran, entièrement en français. *(À étayer par les choix de l'`ux-designer` avant toute publication.)*

**Message 3 — Vous gardez la main, avec un historique d'activité clair.**
Exercices faits, temps passé, assiduité et résultats bruts par séance, présentés en tableau. L'interprétation reste la vôtre.

Points de vigilance vocabulaire : aucun des termes interdits (CLAUDE.md §2) n'est utilisé. Aucune promesse de résultat clinique. « Plus d'entraînement » est formulé comme une possibilité d'usage, pas comme un effet démontré.

---

## 3. Plan de recrutement de 5 à 10 orthophonistes testeurs du concept

### 3.1 Principes

- **Pas d'entretien mené par Christophe** : recrutement et suivi asynchrones (formulaire, onboarding guidé, questionnaire de retour). Les échanges éventuels en visio sont menés par `customer-success` (agent) ou se font par écrit ; à arbitrer par le `coo` si un humain doit intervenir.
- **Aucun vrai patient, aucune donnée de santé** : les testeurs créent des profils patients **inventés** et jouent eux-mêmes le rôle du patient. C'est rappelé dans l'invitation et dans l'app.
- **Profil cible** : orthophonistes libéraux suivant des patients aphasiques post-AVC ; 1 à 2 orthophonistes en centre de rééducation (cible secondaire) si possible.
- **Contrepartie** : à décider (voir décision 2). Toute contrepartie à un professionnel de santé par un fabricant de dispositif médical relève a priori de l'encadrement des avantages (dit « anti-cadeaux ») : **à vérifier par `juridique-dpo`** avant toute offre.
- **Données des testeurs** (nom, e-mail, mode d'exercice) : données personnelles, à couvrir par une mention RGPD rédigée par `juridique-dpo`. Le formulaire ne doit poser **aucune question sur des patients réels**.

### 3.2 Canaux concrets (France)

Ordre proposé : local (Bordeaux / Nouvelle-Aquitaine) d'abord, puis national.

| # | Canal | Action proposée | Coût | Responsable |
|---|---|---|---|---|
| 1 | **Centre de formation universitaire en orthophonie de Bordeaux** (Institut universitaire des sciences de la réadaptation, campus Carreire) — https://www.onisep.fr/ressources/structures-enseignement/nouvelle-aquitaine/gironde/institut-universitaire-des-sciences-de-la-readaptation-campus-carreire-universite-de-bordeaux/certificat-de-capacite-d-orthophoniste | Demander la diffusion de l'appel aux maîtres de stage et aux enseignants cliniciens (orthophonistes en exercice). Piste : sujet de mémoire de fin d'études sur l'usage du concept. | 0 € (à vérifier) | cmo |
| 2 | **Association Bordelaise des Futurs Orthophonistes (AFBO)** — https://www.u-bordeaux.fr/campus/animation-des-campus/associations/assos-des-campus-de-bordeaux/formation-filiere/afbo | Recruter des étudiants pour jouer le rôle du patient fictif aux côtés des orthophonistes testeurs ; relais vers leurs maîtres de stage. | 0 € (à vérifier) | cmo |
| 3 | **Syndicat régional FNO** de Gironde / Nouvelle-Aquitaine et **URPS orthophonistes Nouvelle-Aquitaine** (FNO : https://fno.fr) | Demander une diffusion dans leur lettre d'information. Coordonnées exactes **à vérifier**. Un syndicat peut refuser de relayer un acteur commercial : prévoir ce cas. | à vérifier | cmo |
| 4 | **Groupes professionnels en ligne** : groupes Facebook d'orthophonistes (aphasiologie, libéraux), LinkedIn (orthophonistes, neuropsychologie). Noms exacts des groupes **à identifier**. | Publication d'un appel à testeurs, après validation `raqa` et **accord de Christophe** (publication externe). Respecter les règles de chaque groupe (souvent : accord des modérateurs). | 0 € | cmo |
| 5 | **Associations d'aphasiques et de patients AVC** : ex. Groupe des Aphasiques d'Île-de-France (https://www.aphp.fr/associations/groupe-des-aphasiques-dile-de-france-gaif), Aphasiques 44 (https://metropole.nantes.fr/mes-services-mon-quotidien/espace-associations-nantaises/annuaire-des-associations-nantaises/aphasiques-44), France AVC (https://franceavc.com). Association girondine **à identifier**. | **Uniquement comme relais vers les orthophonistes** qui interviennent auprès d'elles. Ne pas recruter de personnes aphasiques comme utilisateurs au stade MVP (cela reviendrait à des vrais patients). Question posée à `raqa`. | 0 € | cmo + customer-success |
| 6 | **Centres de rééducation / SMR** de la métropole bordelaise (liste **à établir**) | Contact écrit du service d'orthophonie ; cible secondaire, 1 à 2 testeurs max. | 0 € | cmo |
| 7 | Congrès et salons d'orthophonie | **Hors calendrier MVP** (dates et coûts à vérifier) ; utile pour la bêta suivante, pas pour ce recrutement. | à vérifier | cmo + cfo |

### 3.3 Parcours du testeur (asynchrone)

1. Candidature via formulaire court (mode d'exercice, nombre approximatif de patients aphasiques suivis — sans aucune donnée sur ces patients —, équipement, disponibilité sur 3 semaines).
2. Sélection par `customer-success` selon critères écrits (mix libéral / centre, matériel varié). Validation finale de la liste par le `coo`.
3. Envoi d'un kit d'accueil : accès au MVP, 3 profils patients fictifs fournis, scénario de test pas à pas (assigner des exercices, jouer le patient, consulter l'historique d'activité).
4. Période de test : 2 à 3 semaines (à caler avec le `product-owner`).
5. Questionnaire de retour en ligne + possibilité de commentaires écrits libres. Outil à choisir avec `secops` / `juridique-dpo` (données personnelles des testeurs uniquement).
6. Synthèse des retours par `customer-success`, transmise au `product-owner`.

**Critère de succès** : 5 testeurs actifs minimum ayant terminé le scénario. Indicateur de canal : nombre de candidatures et de testeurs actifs par canal (premier jalon pour la mesure du CAC par canal).

### 3.4 Brouillon de message d'invitation (NON ENVOYÉ)

> Objet : Appel à orthophonistes testeurs — application d'entraînement à domicile pour patients aphasiques
>
> Bonjour,
>
> Escyon, jeune société basée à Eysines (Gironde), conçoit une application web qui permet à l'orthophoniste d'assigner à ses patients aphasiques des exercices d'entraînement à faire à domicile entre les séances (langage, anomie, mémoire, attention), avec une interface pensée pour les personnes aphasiques et un historique d'activité consultable par l'orthophoniste.
>
> Nous cherchons 5 à 10 orthophonistes, en libéral ou en centre de rééducation, qui suivent des patients aphasiques, pour tester une première version pendant 2 à 3 semaines et nous dire franchement ce qui est utile, inutile ou à revoir.
>
> **Important** : ce test se fait **sans aucun patient réel**. Vous utiliserez des profils patients fictifs que nous fournissons et jouerez vous-même le rôle du patient. Merci de ne saisir aucune information concernant vos patients.
>
> Ce que nous vous demandons : environ [durée à préciser] au total, à votre rythme, puis un questionnaire en ligne.
> Ce que nous proposons : [contrepartie à définir — voir décision du CEO].
>
> Pour participer : [lien du formulaire — à créer].
> Vos données (nom, e-mail, mode d'exercice) sont utilisées uniquement pour organiser ce test. [Mention RGPD à rédiger par le juridique-dpo.]
>
> Merci pour votre temps,
> L'équipe Escyon — 30 avenue de la Libération, 33320 Eysines

Avant tout envoi : relecture `raqa` (allégations, vocabulaire), `juridique-dpo` (RGPD, contrepartie), accord écrit de Christophe.

---

## 4. Décisions proposées à Christophe (options A/B)

1. **Nom**
   - A (recommandé) : « ReMot » reste un nom de code ; `juridique-dpo` fait la recherche INPI/EUIPO et domaines, le CMO propose 3 alternatives vérifiées au même niveau.
   - B : adopter « ReMot » comme marque dès maintenant et lancer dépôt + réservation de domaines (dépense, risque de confusion avec « Remote »).
2. **Contrepartie des testeurs**
   - A (recommandé, sous réserve `juridique-dpo`) : participation bénévole + accès offert pendant une durée limitée au lancement commercial (durée et valeur = décision de prix, avec `cfo`).
   - B : indemnisation forfaitaire (dépense ; encadrement des avantages à vérifier).
3. **Zone de recrutement**
   - A (recommandé) : Bordeaux / Nouvelle-Aquitaine d'abord (CFUO, AFBO, syndicat régional, URPS), national ensuite si moins de 5 testeurs après 3 semaines.
   - B : appel national d'emblée via groupes en ligne (plus rapide, mais publication externe et moins de maîtrise).

## 5. Questions aux autres agents

- **`raqa`** : (a) Les 3 messages et la phrase de positionnement sont-ils couverts par l'intended use actuel ? « Interface pensée pour l'aphasie » est-elle une allégation à étayer ? (b) Le test par des orthophonistes avec patients fictifs doit-il être tracé comme évaluation formative d'aptitude à l'utilisation (IEC 62366-1) ? (c) Confirmer qu'aucune personne aphasique ne peut tester au stade MVP.
- **`product-owner`** : périmètre du MVP disponible pour les testeurs, date de disponibilité, durée du test, temps demandé, et questions prioritaires à poser dans le questionnaire.
- **`cfo`** : budget de recrutement (0 € visé), valeur et durée possibles de l'accès offert aux testeurs, coût des domaines et du dépôt de marque si décision B.
- **`juridique-dpo`** (hors comité) : recherche d'antériorité « ReMot », encadrement des avantages consentis aux orthophonistes, mention RGPD du formulaire.
