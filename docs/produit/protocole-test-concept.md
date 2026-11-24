# Protocole de test du concept (PoC)

> [PRODUCT-OWNER] Version 0.1 du 2026-11-24, brouillon. À valider par `raqa` (statut du test), `juridique-dpo` (consentements, avantages accordés aux professionnels de santé) et `cfo` (coûts). Toute dépense, publication externe ou prise de contact avec des tiers exige l'accord écrit de Christophe.

## 1. Objectif et décision visée

Décider **go / itérer / no-go** sur le concept, à partir de deux questions :
1. **Valeur** : un orthophoniste assignerait-il cet outil à ses patients aphasiques post-AVC, et paierait-il pour l'utiliser ?
2. **Utilisabilité** : l'orthophoniste juge-t-il le parcours patient utilisable par au moins une partie de ses patients ?

Le test porte sur l'intérêt et l'usage. Il ne mesure aucun effet sur l'état de santé (impossible sans vrais patients et hors du périmètre de la classe I).

## 2. Testeurs

| Profil | Nombre | Critères |
|---|---|---|
| Orthophonistes | **8** (minimum 6 pour conclure) | Au moins 6 sur 8 suivent actuellement au moins un patient aphasique post-AVC. Au moins 5 sur 8 exercent en libéral (le futur client payeur). Au moins 2 régions différentes. Au moins 2 orthophonistes peu à l'aise avec le numérique (auto-déclaré). Aucun lien avec Escyon ou X-Pressure. |
| « Patients fictifs » | **12 à 16** (1 à 2 par orthophoniste) | Proches ou collègues recrutés par l'orthophoniste, idéalement des personnes de plus de 55 ans peu familières du numérique. Ils jouent une **fiche persona fictive** (voir ci-dessous). |

Repère : environ 5 utilisateurs suffisent à faire ressortir la majorité des problèmes d'utilisabilité d'un parcours (Nielsen Norman Group, « Why You Only Need to Test with 5 Users », 2000 ; à vérifier). Nous en prenons 8 pour absorber les abandons et pour disposer d'un signal sur l'intention d'usage.

**Fiches persona fictives** (rédigées par `expert-clinique`, entièrement inventées) : 3 à 4 profils, par exemple un manque du mot modéré avec une compréhension préservée, ou des troubles de compréhension plus marqués. Chaque fiche indique des contraintes à simuler : utiliser la main non dominante, ne pas lire les consignes écrites longues, faire une séance par jour d'environ 20 min.

**Limite assumée** : un testeur sans aphasie ne reproduit pas les difficultés réelles. Le jugement sur l'utilisabilité par des personnes aphasiques repose donc sur l'**avis expert des orthophonistes**. Un test d'utilisabilité avec de vrais patients sera nécessaire après la migration HDS. Il constitue un prérequis de la V1 commerciale et relève de l'avis de `raqa` (ingénierie de l'aptitude à l'utilisation, IEC 62366-1 ; applicabilité à vérifier).

## 3. Déroulé (environ 5 semaines)

| Semaine | Étape | Responsable |
|---|---|---|
| S-2 à S-1 | Recrutement, signature des conditions de test et du consentement à l'enregistrement | `cmo` et `customer-success` |
| J0 | Démarrage : vidéo de prise en main de 10 min, plus une session collective en visio de 30 min (facultative) | `customer-success` |
| J1 à J14 | Usage libre. Les patients fictifs visent au moins 5 séances. Un message de relance est envoyé par l'équipe à J3 et J8. | Testeurs |
| J15 à J20 | Entretien individuel de 45 min avec chaque orthophoniste, plus un questionnaire en ligne de 10 min pour les patients fictifs | Voir la section 6 |
| J21 à J25 | Synthèse, calcul des critères, recommandation au comité de direction | `product-owner` |

## 4. Scénarios

| # | Acteur | Scénario | Mesure |
|---|---|---|---|
| S1 | Orthophoniste | Se connecter, créer un patient fictif, assigner un programme de 2 exercices, 5 jours par semaine, 20 min | Réussite sans aide (oui/non), durée |
| S2 | Orthophoniste | Transmettre l'accès (lien ou QR code) au patient fictif | Réussite sans aide |
| S3 | Patient fictif | Ouvrir le lien, faire une séance complète en respectant sa fiche persona | Séance terminée sans aide, nombre d'appels à l'aide |
| S4 | Patient fictif | Faire au moins 5 séances sur 14 jours | Séances faites (journal d'usage) |
| S5 | Orthophoniste | Consulter l'historique d'activité et modifier le programme (niveau, durée) | Réussite, commentaire spontané |
| S6 (si US-10 livrée) | Orthophoniste | Ajouter 10 images fictives avec leur mot et les intégrer à l'anomie | Réussite, durée |

## 5. Questions à poser à l'orthophoniste (entretien de 45 min)

Questions ouvertes d'abord, échelles ensuite. Aucune démonstration ni défense du produit par l'intervieweur.

1. Racontez la dernière fois que vous avez donné des exercices à faire à la maison à un patient aphasique. Avec quel support, et que s'est-il passé ?
2. Qu'avez-vous fait avec l'outil pendant ces deux semaines ? Qu'est-ce qui vous a surpris ?
3. À quel moment avez-vous été bloqué ou hésitant ?
4. Les exercices et la hiérarchie d'indices correspondent-ils à votre pratique ? Que changeriez-vous ? (échelle de 1 à 5)
5. À quels patients, réels, de votre file active le proposeriez-vous ? À lesquels non, et pourquoi ?
6. L'espace patient serait-il utilisable seul par ces patients ? Avec un aidant ? (échelle de 1 à 5)
7. Que vous apporte l'historique d'activité ? Que vous manque-t-il ? (Noter toute demande de graphique ou de suivi de l'évolution comme une demande V2, sans rien promettre.)
8. Question principale : « Si l'outil était disponible demain, l'assigneriez-vous à au moins un patient ? » (certainement / probablement / je ne sais pas / probablement pas / certainement pas)
9. Intention de payer : questions de sensibilité au prix de type Van Westendorp (trop cher, cher, bonne affaire, trop bon marché). Aucun prix n'est annoncé, sauf une fourchette validée au préalable par Christophe (`cfo`).
10. Qu'est-ce qui vous empêcherait de l'utiliser (temps, coût, confiance, réglementation, matériel des patients) ?
11. Qu'utilisez-vous aujourd'hui à la place (logiciels, papier, applications) ?
12. Questionnaire SUS (System Usability Scale, 10 items, Brooke 1996), à remplir en fin d'entretien.

**Patients fictifs** (questionnaire de 10 min) : SUS ; « Avez-vous su quoi faire sur chaque écran ? » (1 à 5) ; « Qu'est-ce qui vous a gêné ? » ; durée ressentie d'une séance.

## 6. Recrutement et conduite des entretiens sans Christophe

**Canaux de recrutement** (pilotés par `cmo`, toute publication externe soumise à l'accord de Christophe) : groupes professionnels d'orthophonistes en ligne (LinkedIn, groupes Facebook spécialisés en neurologie et aphasie, à identifier), contacts des centres de formation en orthophonie, associations de patients aphasiques (à identifier, pour relayer auprès des orthophonistes), bouche-à-oreille entre testeurs. Un formulaire de pré-sélection reprend les critères de la section 2.

**Contrepartie** : une compensation pour environ 3 h de temps (montant à proposer par `cfo`, accord de Christophe requis). Point de vigilance pour `juridique-dpo` : l'encadrement des avantages consentis aux professionnels de santé par les entreprises de produits de santé (Code de la santé publique, art. L.1453-3 et suivants, dispositif dit « anti-cadeaux » ; applicabilité à Escyon et forme de la convention à vérifier).

**Conduite des entretiens** : deux options, à arbitrer par Christophe (décision A/B) :
- **Option A, entretien asynchrone** : questionnaire guidé en ligne avec questions ouvertes et échelles, plus une courte vidéo d'écran commentée par l'orthophoniste (S1 et S5). `customer-success` et `product-owner` analysent. Coût faible, mais moins de profondeur et pas de relance possible.
- **Option B, intervieweur humain externe** : un chercheur UX freelance ou un orthophoniste consultant mène les 8 entretiens en visio en suivant la grille de la section 5, enregistre avec consentement et transmet les notes. Coût à chiffrer par `cfo`, avec une meilleure qualité de signal.

Recommandation du PO : **option B**, la qualité du signal étant l'objet même du test. Repli sur A si le budget est refusé.

**Données des testeurs** : noms, e-mails et enregistrements des orthophonistes sont des données personnelles, pas des données de santé. Ils nécessitent un consentement écrit, une durée de conservation définie et un stockage chez Escyon (`juridique-dpo`). Aucune donnée réelle de patient ne doit apparaître dans les enregistrements : consigne à rappeler en début d'entretien.

## 7. Critères de décision (go / itérer / no-go)

| # | Critère | Go si | No-go si |
|---|---|---|---|
| C1 (principal) | Orthophonistes répondant « certainement » ou « probablement » à la question 8 | ≥ 5 sur 8 (≥ 60 %) | ≤ 2 sur 8 (≤ 25 %) |
| C2 | Orthophonistes déclarant une intention de payer dans la fourchette jugée viable par `cfo` | ≥ 4 sur 8 (≥ 50 %) | ≤ 1 sur 8 |
| C3 | S1 réussi sans aide en 10 min ou moins | ≥ 80 % des orthophonistes | < 50 % |
| C4 | Note moyenne de pertinence des exercices (question 4) | ≥ 4 sur 5 | < 3 sur 5 |
| C5 | Utilisabilité de l'espace patient jugée par les orthophonistes (question 6) | ≥ 6 sur 8 donnent 4 ou plus | ≤ 3 sur 8 |
| C6 | SUS moyen des orthophonistes | ≥ 68 (moyenne de référence du SUS selon J. Sauro, à vérifier) | < 50 |
| C7 (comportemental) | Orthophonistes s'étant connectés au moins 3 fois en 14 jours | ≥ 6 sur 8 | ≤ 3 sur 8 |

**Règle de décision** :
- **Go** : C1 et C2 sont atteints, et au moins 3 des critères C3 à C7 sont atteints.
- **No-go** : C1 est en no-go, ou au moins 3 orthophonistes citent le même frein rédhibitoire qui ne peut pas être levé par le produit (par exemple « mes patients n'ont pas d'équipement »).
- **Itérer** : tous les autres cas. Un cycle correctif de 2 à 4 semaines au maximum, puis un nouveau test avec au moins 4 nouveaux orthophonistes.

Ces seuils sont des **hypothèses de travail du PO**, sans référence externe. Ils sont à valider par le comité de direction avant le lancement, et ne doivent pas être modifiés après le recueil des résultats.

## 8. Livrable

Une synthèse en 2 pages au comité de direction : résultats C1 à C7, les 5 principaux freins, les verbatims clés, les demandes classées en `mvp` ou `v2`, et une recommandation go / itérer / no-go pour décision de Christophe.
