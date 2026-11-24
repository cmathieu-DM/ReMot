# Destination (intended use) — ReMot — v0.1

| Champ | Valeur |
|---|---|
| Fabricant | Escyon, 30 avenue de la Libération, 33320 Eysines |
| Rédacteur | raqa |
| Statut | **Brouillon v0.1, non approuvé.** Toute modification de la destination ou de la classe exige l'accord écrit de Christophe (CLAUDE.md §4) |
| Date | 2026-11-24 |
| Références | Règlement (UE) 2017/745 (MDR) ; MDCG 2019-11 rév. 1 (juin 2025) |

> Note de vocabulaire : ce document est réglementaire. Les termes de la liste interdite (CLAUDE.md §2) n'y figurent que dans les citations littérales du MDR ou du MDCG (ex. « fins diagnostiques ou thérapeutiques », « clinical evaluation »), jamais pour décrire le produit.

---

## 1. Destination (MDR art. 2, point 12)

ReMot est un logiciel autonome (application web progressive) destiné à **mettre à disposition de patients adultes ayant eu un accident vasculaire cérébral des exercices d'entraînement cognitif et langagier (mémoire, attention, langage, anomie), choisis et assignés par leur orthophoniste, et à réaliser à domicile entre les séances**, ainsi qu'à **restituer à l'orthophoniste un historique d'activité** (exercices faits, temps passé, assiduité, niveau en cours, résultats bruts par séance sous forme de tableau).

Finalité médicale revendiquée (MDR art. 2, point 1, 2e tiret) : soutien à la compensation d'un handicap (troubles cognitifs et du langage acquis après AVC), **en complément** d'une prise en charge orthophonique et **sous sa responsabilité**.

> Point ouvert (à trancher avec avis externe) : la qualification même de dispositif médical. Un outil de simple « mise à disposition d'exercices » pourrait être argumenté hors DM. La décision projet est de **qualifier DM** (CLAUDE.md §2), ce qui est la position prudente compte tenu de la population et de la finalité de rééducation. Cette qualification est retenue ici.

## 2. Population de patients

- Adultes (18 ans et plus) ayant présenté un AVC (ischémique ou hémorragique), en phase subaiguë ou chronique, présentant des troubles cognitifs et/ou du langage (dont aphasie, anomie), **suivis par un orthophoniste** qui les a inclus.
- Capables, seuls ou avec l'aide d'un aidant, d'utiliser une tablette ou un ordinateur et d'en voir et entendre les contenus.
- Critères d'inclusion fins (sévérité, type d'aphasie) : **à définir par l'`expert-clinique`** avec références. À vérifier.

## 3. Utilisateurs prévus

| Utilisateur | Rôle | Hypothèses |
|---|---|---|
| Orthophoniste (utilisateur professionnel) | Crée le compte patient, choisit et assigne les exercices et niveaux, consulte l'historique d'activité, interprète **seul** l'activité dans son raisonnement clinique | Professionnel de santé diplômé, exerçant en France (V1) |
| Patient (utilisateur profane) | Réalise les exercices à domicile | Troubles cognitifs/langagiers possibles : l'interface doit être conçue selon l'IEC 62366-1 pour ce profil (entrées `ux-designer`) |
| Aidant (proposé, à confirmer) | Aide le patient à se connecter, lancer une séance, gérer l'appareil. Ne modifie pas le programme | Profane. **Décision produit à prendre** : pas de compte séparé en V1 recommandé (utilisation sur la session du patient) |

## 4. Environnement d'utilisation

- Domicile du patient (environnement non contrôlé), navigateur web récent sur tablette ou ordinateur ; smartphone à confirmer (lisibilité).
- Cabinet de l'orthophoniste ou télé-soin pour le paramétrage et la consultation.
- Connexion internet requise. Hébergement HDS obligatoire dès le premier vrai patient (CLAUDE.md §2).
- Pas d'usage en situation d'urgence ni en milieu hospitalier aigu.

## 5. Contre-indications et précautions (projet, à valider par l'`expert-clinique`)

Contre-indications envisagées :
- Patient non suivi par un orthophoniste.
- Phase aiguë de l'AVC.
- Troubles visuels, auditifs ou moteurs empêchant l'utilisation de l'interface sans aide adaptée.

Précautions :
- Épilepsie photosensible : pas de stimuli clignotants ; information dans la notice. À vérifier par l'`expert-clinique` pour la population post-AVC.
- Fatigabilité : durée de séance recommandée fixée par l'orthophoniste ; pauses.
- Risque de mise en échec et de découragement : niveaux paramétrés par l'orthophoniste.
- Le produit ne remplace pas les séances avec l'orthophoniste.
- Tout signe neurologique nouveau (récidive d'AVC) relève de l'urgence (15) : mention dans la notice, le produit n'a aucun rôle d'alerte.

## 6. Ce que le produit ne fait pas (limites de destination)

ReMot V1 :
- ne pose, n'aide à poser ni ne suggère aucun diagnostic ;
- ne calcule aucun score agrégé, n'affiche aucune courbe ni comparaison avant/après présentée comme une mesure de l'état du patient ;
- n'interprète pas les résultats, n'émet aucune alerte et aucune recommandation thérapeutique ;
- **ne choisit pas** les exercices ni ne modifie le niveau de lui-même : l'orthophoniste décide (voir fragilité F2) ;
- ne surveille aucun processus physiologique ;
- n'est pas un dispositif de télésurveillance médicale ;
- n'est pas destiné aux enfants, ni aux troubles d'origine non vasculaire (V1) ;
- n'est pas utilisable sans orthophoniste prescripteur.

## 7. Argumentaire de classe I

### 7.1 Qualification comme logiciel dispositif médical (MDSW)
Selon l'arbre de décision de MDCG 2019-11 rév. 1 (section 3) : le produit est un logiciel ; il n'est pas un accessoire ni ne pilote un matériel ; il réalise une action sur des données au-delà du simple stockage (sélection et présentation d'exercices paramétrés, enregistrement des réponses) ; cette action est au bénéfice de patients individuels ; finalité de l'art. 2, point 1 (compensation d'un handicap). → MDSW autonome, classé en propre (MDR annexe VIII, chapitre II, point 3.3).

### 7.2 Application de la règle 11 (MDR annexe VIII, chapitre III, point 6.3)
- **1er alinéa** (« logiciel destiné à fournir des informations utilisées pour prendre des décisions à des fins diagnostiques ou thérapeutiques » → IIa au moins) : **non applicable** en V1. L'historique d'activité restitue des données brutes d'usage (fait/pas fait, durée, réponses brutes) sans calcul ni interprétation ; il n'est pas présenté comme information destinée à fonder une décision thérapeutique. Position défendable mais **fragile** (F1).
- **2e alinéa** (surveillance de processus physiologiques → IIa/IIb) : non applicable.
- **3e alinéa** (« tous les autres logiciels sont classés dans la classe I ») : **applicable**.
- Autres règles (règles 9, 10, 12, 22) : non applicables, logiciel sans énergie délivrée au patient ni pilotage de matériel. À confirmer dans le dossier de classification.

Conséquence : auto-déclaration de conformité (MDR art. 52, paragraphe 7 ; annexes II et III), sans organisme notifié, sous réserve que la classe I « simple » ne soit ni stérile, ni à fonction de mesurage, ni réutilisable chirurgical (non concerné).

### 7.3 Points de fragilité (à surveiller, veto raqa)
| # | Fragilité | Risque | Maîtrise |
|---|---|---|---|
| F1 | L'orthophoniste utilise *de fait* l'historique (résultats bruts par séance) pour adapter la thérapie. Une autorité peut y voir une « information utilisée pour prendre des décisions thérapeutiques » | Requalification IIa | Données brutes uniquement, aucune mise en forme comparative, aucun indicateur calculé ; notice : « historique d'usage, ne constitue pas une mesure de l'état du patient » ; **avis externe recommandé** (consultant MDSW ou ON) |
| F2 | Ajustement **automatique** de la difficulté (niveau suivant débloqué selon le taux de réussite) | Logiciel qui prend une décision à visée thérapeutique → IIa | V1 : changement de niveau uniquement par l'orthophoniste (ou règle fixée et validée par lui, à examiner) |
| F3 | « Taux de réussite » par séance affiché en pourcentage | Glisse vers un score | Afficher le nombre brut de réponses ; pas de pourcentage agrégé multi-séances |
| F4 | Allégations marketing (`cmo`) : « améliore le langage », « mesure les progrès » | La destination est aussi déterminée par la publicité (art. 2, point 12 ; art. 7) → requalification et pratique trompeuse | Revue raqa obligatoire de tout contenu externe |
| F5 | Modèle de données prêt pour la V2 (suivi longitudinal) | Fonction cachée activée trop tôt | Feature flag désactivé et non exposé ; revue raqa des releases |
| F6 | Exercices « hiérarchie d'indices » qui adaptent l'indice selon l'erreur | Peut être vu comme décision thérapeutique automatisée | Analyse au cas par cas avec `expert-clinique` ; hiérarchie fixe et paramétrée par l'orthophoniste |

## 8. Historique
| Version | Date | Auteur | Modification |
|---|---|---|---|
| 0.1 | 2026-11-24 | raqa | Création, pour revue en comité de direction |
