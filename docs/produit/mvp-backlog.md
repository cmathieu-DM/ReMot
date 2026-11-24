# Backlog MVP « preuve de concept » (PoC)

> [PRODUCT-OWNER] Version 0.1 du 2026-11-24, brouillon soumis au comité de direction. Rien n'est encore créé dans GitHub Issues : ce sera fait après validation, avec les labels `mvp` ou `v2`, `reglementaire` si l'impact réglementaire est « oui », et `pour:<agent>`.

## 1. Cadre

- **Décision du 2026-11-24** : le MVP sert à valider le concept avec des **patients fictifs** (orthophonistes et testeurs qui jouent le rôle du patient). Hébergement standard en UE, hors HDS. Aucun vrai patient, aucune donnée de santé réelle.
- **Objectif du PoC** : qu'un orthophoniste puisse, en moins de 2 semaines, juger s'il assignerait ce produit à ses patients et s'il paierait pour l'utiliser. Rien de plus.
- **Question à trancher** : « Un orthophoniste trouve-t-il utile d'assigner des exercices d'entraînement à domicile via cet outil, et le parcours patient lui paraît-il utilisable par une personne aphasique ? »
- **Règles transverses (critères d'acceptation communs à toutes les stories)** :
  - CA-T1 : aucun terme interdit (section 2 de `CLAUDE.md`) dans l'UI ni dans les textes. Une recherche automatique dans le code et les libellés ne renvoie aucune occurrence.
  - CA-T2 : l'interface n'affiche ni courbe, ni score agrégé, ni comparaison avant/après, ni interprétation, ni alerte, ni recommandation.
  - CA-T3 : un bandeau permanent « Version de test : n'utilisez que des données fictives » est visible sur tous les écrans orthophoniste.
  - CA-T4 : aucun outil tiers d'analytics, de LLM ou d'e-mail marketing ne reçoit de données saisies dans l'application.
  - CA-T5 : le modèle de données conserve les résultats bruts par essai (horodatage, item, réponse, indices utilisés, niveau). Cela permet le module V2 (classe IIa) sans migration lourde. Rien de tout cela n'est affiché au-delà de l'historique d'activité.

## 2. User stories

Légende : **M** = Must, **S** = Should, **C** = Could, **W** = Won't (pas dans le PoC). « Régl. » = impact réglementaire.

### Must : sans ces stories, l'orthophoniste ne peut pas juger le concept

| ID | User story | Critères d'acceptation (testables) | Régl. |
|---|---|---|---|
| US-01 | En tant qu'orthophoniste testeur, je veux me connecter avec l'accès qu'Escyon m'a envoyé, pour tester sans rien payer. | 1. Seules les adresses de la liste blanche des testeurs peuvent créer un compte. 2. Connexion par e-mail et mot de passe (ou lien magique), en moins de 2 min. 3. Aucune étape de paiement. 4. L'acceptation des conditions de test (rédigées par `juridique-dpo`) est obligatoire au premier accès et horodatée. | Oui (conditions de test, statut du PoC) |
| US-02 | En tant qu'orthophoniste, je veux créer un patient fictif, pour simuler mon usage réel. | 1. Champs autorisés : pseudonyme (obligatoire), et c'est tout. Pas de date de naissance, de nom réel, de champ médical ni de champ texte libre. 2. Le formulaire rappelle « Profil fictif uniquement ». 3. Création en moins de 1 min. 4. Un orthophoniste ne voit que ses propres patients fictifs (test d'accès croisé négatif). | Oui (minimisation des données) |
| US-03 | En tant qu'orthophoniste, je veux donner un accès au patient fictif sans qu'il ait à saisir d'identifiant, pour reproduire un usage par une personne aphasique. | 1. Un lien unique et un QR code sont générés par patient. 2. Le lien ouvre directement l'espace patient sur mobile, tablette et ordinateur (Chrome, Safari, Firefox dans leurs versions courantes). 3. L'orthophoniste peut révoquer le lien et en générer un nouveau. 4. Aucun e-mail n'est envoyé au patient par l'application. | Non |
| US-04 | En tant qu'orthophoniste, je veux assigner un programme (exercices, fréquence, durée cible), pour cadrer l'entraînement à domicile. | 1. Choix d'un ou plusieurs exercices dans le catalogue. 2. Fréquence : jours de la semaine cochables. 3. Durée cible par séance, réglable de 5 à 30 min (20 min par défaut). 4. Niveau de départ par exercice. 5. La modification est visible côté patient à la séance suivante. | Oui (paramétrage par le professionnel, lien avec l'intended use) |
| US-05 | En tant que patient, je veux un exercice de dénomination d'images avec des indices progressifs, pour m'entraîner sur l'anomie. | 1. Une image est affichée et le patient choisit ou tape le mot (réponse vocale exclue, voir V2). 2. Hiérarchie d'indices définie par `expert-clinique` dans `docs/clinique/` (par exemple : sémantique, puis première syllabe, puis mot entendu). 3. Un indice s'affiche sur demande ou après un délai réglable. 4. Chaque essai enregistre l'item, la réponse, les indices utilisés et la durée. 5. Au moins 60 items validés par `expert-clinique` (à confirmer par lui). | Oui (contenu clinique) |
| US-06 | En tant que patient, je veux un exercice de compréhension orale (j'entends un mot et je désigne l'image), pour m'entraîner. | 1. Le mot est lu par un fichier audio préenregistré et peut être réécouté. 2. Choix entre 2 et 4 images selon le niveau. 3. Retour immédiat juste ou faux, sans score cumulé. 4. Au moins 60 items validés par `expert-clinique`. | Oui (contenu clinique) |
| US-07 | En tant que patient aphasique, je veux lancer ma séance du jour en un seul geste et être guidé sans lire de longs textes, pour m'entraîner seul. | 1. L'écran d'accueil comporte un seul bouton principal « Commencer ». 2. Toutes les consignes sont disponibles en audio. 3. Cibles tactiles d'au moins 44 × 44 px (repère WCAG 2.2, critère 2.5.5 ; à confirmer par `ux-designer`). 4. Pas plus d'une action par écran. 5. Fin de séance signalée quand la durée cible est atteinte. 6. Lors du test, au moins 4 testeurs sur 5 terminent une séance sans aide (voir le protocole). | Non |
| US-08 | En tant qu'orthophoniste, je veux consulter l'historique d'activité d'un patient fictif, pour savoir ce qu'il a fait. | 1. Tableau par séance : date, exercices faits, temps passé, niveau en cours, nombre d'items, réponses justes et fausses, indices utilisés. 2. Assiduité exprimée en séances faites sur séances prévues pour la semaine. 3. Pas de graphique, de score agrégé, de couleur d'alerte ni de commentaire automatique. 4. Revue par `raqa` avant fusion. | Oui (frontière classe I / IIa) |
| US-09 | En tant qu'équipe Escyon, je veux recueillir l'avis des testeurs dans l'application, pour mesurer les critères de go/no-go. | 1. Bouton « Donner mon avis » sur chaque écran orthophoniste. 2. Formulaire interne, hébergé avec l'application (pas d'outil tiers sans accord). 3. Export CSV des retours et des journaux d'usage (connexions, séances, durées) pour l'équipe. | Non |

### Should : renforcent nettement le jugement de l'orthophoniste

| ID | User story | Critères d'acceptation | Régl. |
|---|---|---|---|
| US-10 | En tant qu'orthophoniste, je veux ajouter des photos et des mots propres au patient, pour personnaliser l'anomie. | 1. Import d'au moins 20 images (JPG ou PNG, 5 Mo max) avec le mot cible. 2. Les items personnalisés apparaissent dans l'exercice US-05. 3. Avertissement : « Images fictives ou libres de droits uniquement, pas de photo de personne réelle. » 4. Métadonnées EXIF supprimées à l'import. | Oui (données personnelles potentielles) |
| US-11 | En tant que patient, je veux que la difficulté s'ajuste pendant l'exercice, pour ne pas être en échec ni m'ennuyer. | 1. Règle simple et documentée, fixée par `expert-clinique` (par exemple : N réussites d'affilée, niveau +1 ; M échecs, niveau −1). 2. La règle est déterministe et testée unitairement. 3. Le niveau en cours est visible dans l'historique (US-08). 4. L'orthophoniste peut bloquer le niveau. | Oui (logique logicielle qui agit sur l'entraînement) |
| US-12 | En tant que patient, je veux un exercice de compréhension écrite (associer un mot écrit à une image). | Mêmes critères qu'US-06, avec un mot écrit en gros caractères au lieu de l'audio. | Oui (contenu clinique) |

### Could : seulement s'il reste de la capacité

| ID | User story | Critères d'acceptation | Régl. |
|---|---|---|---|
| US-13 | En tant que patient, je veux un exercice d'attention et de mémoire (par exemple un empan de séquences d'images). | 1. Un seul type d'exercice. 2. 5 niveaux. 3. Contenu validé par `expert-clinique`. | Oui (contenu clinique) |
| US-14 | En tant que patient, je veux installer l'application sur mon écran d'accueil (PWA). | Installable sur Android (Chrome) et iOS (Safari, ajout à l'écran d'accueil). | Non |

## 3. Ce qu'on NE fait PAS dans le PoC (Won't, label `v2` ou « après PoC »)

| Élément | Justification |
|---|---|
| Abonnement Stripe | Les testeurs ne paient pas. On mesure l'intention de payer par entretien, pas par transaction. La mise en place se fera après le go. |
| Rappels (notifications push ou e-mail) | Ils ne sont pas nécessaires pour juger le concept sur 2 semaines. Les testeurs reçoivent leurs rappels hors application, envoyés par l'équipe de test. |
| Hébergement HDS, comptes de vrais patients, données réelles | Exclus par la décision du 2026-11-24. Ils sont obligatoires avant le premier vrai patient. |
| Reconnaissance vocale | Prévue en V2. Elle impliquerait d'envoyer la voix (donnée de santé) à un service tiers, et le risque réglementaire est à instruire. |
| Espace aidant, communication fonctionnelle | Prévus en V2, hors périmètre. |
| Module de suivi de l'évolution, graphiques, scores, comparaisons | Classe IIa, interdit en V1. Seules les données brutes sont stockées (CA-T5). |
| Gestion de cabinet (plusieurs orthophonistes, partage de patients) | Inutile pour le jugement individuel d'un orthophoniste. |
| Catalogue complet d'exercices | Deux exercices Must suffisent à juger le concept. Les autres sont en Should ou Could. |
| Éditeur d'exercices par l'orthophoniste (au-delà des photos et mots) | Coût élevé, sans effet sur la décision de go/no-go. |
| Mode hors ligne, application native, multilingue | La PWA en ligne et en français suffit. |
| Marquage CE, dossier technique complet, EUDAMED | Le PoC n'est pas mis sur le marché. Le statut exact du PoC est à confirmer par `raqa`. |
| SSO, MFA avancée, RBAC fin | Compte simple sur liste blanche. Le niveau de sécurité minimal est à valider par `secops`. |

## 4. Points ouverts

1. `raqa` : un PoC gratuit, réservé à des orthophonistes testeurs et utilisé avec des profils fictifs, constitue-t-il une « mise à disposition » au sens du MDR ? Quelles mentions faut-il imposer ? Quels documents IEC 62304 faut-il produire dès maintenant (SRS minimal) ?
2. `expert-clinique` : hiérarchie d'indices, règles adaptatives et listes d'items (sources de stimuli libres de droits, à vérifier).
3. `ux-designer` : maquettes de l'espace patient (US-07) avant le sprint 1.
4. `cto` : estimation des Must. Cible PoC : 2 sprints de 2 semaines (hypothèse à confirmer).
