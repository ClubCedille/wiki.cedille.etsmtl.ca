---
title: Document de vision
description: Présentation générale de notre infrastructure
weight: 1
---

# Plateforme CEDILLE -  _Document de vision_

**Organization:** Cedille, École de Technologie Supérieure

Voici une vue d'ensemble sur notre nouvelle plateforme CEDILLE. Cette section est conçue pour vous donner une vue d'ensemble claire du 'pourquoi' et du 'quoi' de notre projet. Ici, nous plongeons dans la raison d'être de notre plateforme basée sur Kubernetes, exploitée par le SaaS Omni de SideroLabs, décrivant en détail pourquoi nous avons entrepris ce voyage et comment nous pensons que cela va transformer la façon dont on gère nos services d'hébergement sur nos serveurs bare-metal. 

## Table des matières

- [1. Survol](#1-survol)
  * [1.1 Objectif](#11-objectif)
  * [1.2 Porté](#12-porté)
  * [1.3 Définitions et acronymes](#13-définitions-et-acronymes)
- [2. Position du produit](#2-position-du-produit)
  * [2.1 Énoncé du problème](#21-énoncé-du-problème)
  * [2.2 Énoncé du produit](#22-énoncé-du-produit)
- [3. Utilisateur et parties prenantes](#3-utilisateur-et-parties-prenantes)
  * [3.1 Sommaire des parties prenantes](#31-sommaire-des-parties-prenantes)
  * [3.2 Sommaire des utilisateurs](#32-sommaire-des-utilisateurs)
  * [3.3 Environnement utilisateur](#33-environnement-utilisateur)
- [4. Besoins des principaux utilisateurs et parties prenantes](#4-besoins-des-principaux-utilisateurs-et-parties-prenantes)
- [4. Présentation du produit](#4-présentation-du-produit)
  * [4.1 Contexte du produit](#41-contexte-du-produit)
  * [4.2 Principaux avantages](#42-principaux-avantages)
  * [4.3 Hypothèses et dépendances](#43-hypothèses-et-dépendances)
  * [4.4 Licence](#44-licence)
  * [4.5 Caractéristiques du produit](#45-caractéristiques-du-produit)
  * [5. Contraintes](#5-contraintes)
  * [6. Attributs de qualité](#6-attributs-de-qualité)
- [7. Autres exigences](#7-autres-exigences)
  * [7.1 Normes et standards](#71-normes-et-standards)
  * [7.2 Configuration requise](#72-configuration-requise)
  * [7.3 Exigences en matière de documentation](#73-exigences-en-matière-de-documentation)

## 1. Survol

### 1.1 Problématique

Le club Cédille est responsable de l’hébergement et de l’aide au développement d’un nombre important de sites web et services web pour les clubs étudiants de l’ÉTS. De plus, le club cherche à donner à ses membres une occasion d’apprentissage des technologies DevOps, Kubernetes et de gestion de serveur.

En ce moment, les services sont déployés sur un Kubernetes hébergé par Google Cloud (GKE). Toutefois, cette plateforme engendre des coûts importants et l’augmentation de clubs hébergés rend le maintien d’utilisation de cette plateforme une difficulté financière. De plus, la structure des opérations de maintenances et de déploiement est en ce moment trop complexe pour assurer une courbe d’apprentissage intéressante pour les membres du club. 

Aussi, la solution actuelle n’offre pas assez de flexibilité et de contrôle pour permettre aux membres d’expérimenter les technologies utilisées. Enfin, l’ÉTS est en processus de révision de ses pratiques de sécurité suite aux nouvelles directives gouvernementales, ainsi CÉDILLE doit retravailler son infrastructure pour répondre aux nouvelles exigences.


### 1.2 Objectif

À cause des problèmes mentionnées et des nouveaux requis, le club CÉDILLE a récemment acheté des serveurs physiques et y a installé Kubernetes. La décision a été prise d’en profiter pour revoir l’ensemble de l’infrastructure et des systèmes DevOps afin de mieux répondre aux besoins du club, de ses clients et de l’ÉTS.

Pour ce faire, nous déploieront plusieurs systèmes d'automatisation, d'observabilité et de redondance. La volonté sera ici de rendre l'expérience des clients de CÉDILLE plus fluide et plus consistante. De plus, nous viseront à rendre plus clair le processus de développement et maintenance pour les membres du club CÉDILLE eux-mêmes. Lorsque possible, les logiciels libres et cloud-native seront à favoriser afin de respecter la philosophie du club étudiant CÉDILLE. 

### 1.3 Porté

Cette solution devra être exhaustive afin de couvrir les différents cas d'utilisation tout en respectant les requis de sécurité demandé par l'ÉTS. Toutefois, il est important de délimiter ce qui fait partie du projet et ce qui n'en fera pas parti à ce stage-ci:

**Inclus**
- Toutes les définitions de l'infrastructure et de la typologie réseau
- Les systèmes de redondance
- Les systèmes d'observabilité
- La gestion d'environnements (pré-production, productions, etc.)
- La gestion des déploiements, notamment progressifs (bleu-vert, canary...)
- Les systèmes de sécurité
- Pipelines de tests et déploiement (CI/CD)

**Exclus**
- Configuration d'environnement de développements pour les développeurs
- Programmation des sites web qui seront sur l'infrastructure
- Effectuer la migration complète de services (certains services en preuve de concept d'ici la fin de ce projet, les autres après la fin de ce projet)

### 1.3 Définitions et acronymes

**Table 1.3.1: Définitions et acronymes**

| **Acronyme** | Définition |
| --- | --- |
| **ÉTS** | École de Technologie Supérieure |
| **Docker** | Un conteneur est une unité logicielle standard qui regroupe le code et toutes ses dépendances afin que l'application s'exécute rapidement et de manière fiable d'un environnement informatique à un autre. Une image de conteneur Docker est un package logiciel léger, autonome et exécutable qui comprend tout ce dont vous avez besoin pour exécuter une application : code, runtime, outils système, bibliothèques système et paramètres. |
| **Kubernetes** |  Système open source pour automatiser le déploiement, la mise à l'échelle et la gestion des applications conteneurisées. |
| **Cluster** | Dans un système informatique, un cluster est un groupe de serveurs et d'autres ressources qui agissent comme un système unique et permettent une haute disponibilité, un équilibrage de charge et un traitement parallèle. Ces systèmes peuvent aller d'un système à deux nœuds de deux ordinateurs personnels (PC) à un superordinateur doté d'une architecture en cluster. |
| **Namespace** | Dans Kubernetes, les espaces de noms fournissent un mécanisme permettant d'isoler des groupes de ressources au sein d'un seul cluster. Les noms de ressources doivent être uniques au sein d’un espace de noms, mais pas entre les espaces de noms. La portée basée sur l'espace de noms s'applique uniquement aux objets avec espace de noms (par exemple, déploiements, services, etc.) et non aux objets à l'échelle du cluster. |
| **vCluster** | Clusters Kubernetes virtuels qui s'exécutent dans des espaces de noms (namespace) standards |
| **Load balancer** | L'équilibrage de charge fait référence à la répartition efficace du trafic réseau entrant sur un groupe de serveurs back-end, également appelé batterie de serveurs ou pool de serveurs. |
| **MetalLB** | MetalLB est une implémentation d'équilibrage de charge pour les clusters Kubernetes sur place (on-prem), utilisant des protocoles de routage standard. |
| **KubeVirt** | Extension pour Kubernetes qui permet de gérer et exécuter des machines virtuelles à côté de conteneurs. |
| **Mikrotik** | Mikrotik est un fournisseur d'équipements réseaux Enterprise a prix raisonable. |
| **Clickhouse** | Clickhouse est une base de données a haute performance pour des données a grande échelle. |
| **Logs** | Les logs sont des information purement textuels provenants d'un service logiciel. |
| **Traces** | Les traces sont des informations détaillés des opération internes d'un service logiciel comme le temps de réponse d'une requête SQL. |
| **Metriques** | Les metriques sont des informations usuellement formatés en séries chronologiques qui mesurent des statistiques. |
| **OTEL (OpenTelemetry)** | OpenTelemetry est un projet open source qui definit des protocoles et methodes standards pour la collection et transfert des Logs, Traces et Metriques. |
| **BGP** | Border Gateway Protocol (BGP) fait référence à un protocole de passerelle qui permet à Internet d'échanger des informations de routage entre des systèmes autonomes (AS). |
| **Talos Linux** | Distribution Kubernetes offerte par Sidero Labs |
| **Contour** | Contour est un contrôleur d'entrée Kubernetes open source fournissant le plan de contrôle pour Envoy Edge et le proxy de service. Contour prend en charge les mises à jour de configuration dynamiques et la délégation d'entrée multi-équipes prêtes à l'emploi tout en conservant un profil léger. |
| **Ingress** | Dans Kubernetes, un Ingress est un objet qui permet de gérer l'accès externe aux services dans un cluster, généralement via HTTP. |
| **Egress** | Le trafic sortant d'un réseau ou d'un pod dans un contexte Kubernetes. |
| **Linkerd** | Un service mesh léger et sécurisé pour Kubernetes qui offre des fonctionnalités telles que le routage du trafic, la télémétrie et la sécurité mTLS. |
| **Service mesh** | Une couche d'infrastructure dédiée pour faciliter les communications orientées services, offrant des fonctionnalités telles que la découverte, la charge, la télémétrie et l'authentification des services. |
| **Terraform** | Terraform est un outil qui permet de faire de l'insfrastructure en tant que code (IaC). |
| **Rook/Ceph** | Rook est une orchestration de stockage pour Kubernetes, et Ceph est un système de stockage distribué que Rook peut orchestrer. |
| **Kube-score** | Kube-score est un outil pour Kubernetes qui recommande des changements pour améliorer la sécurité et la fiabilité. |
| **CI** | Intégration continue |
| **CD** | Déploiement continue |
| **Github Action** | Github action est l'outil qui permet de faire du CI/CD pour la plateforme Github. |
| **Gitops** | Une méthode pour gérer et mettre à jour les infrastructures et les applications en utilisant des outils Git. Avec GitOps, Git sert de source unique de vérité pour le code et l'infrastructure. |
| **ArgoCD** | Un outil déclaratif, GitOps-continu pour Kubernetes. |
| **Déploiment Canaray**| Une stratégie de déploiement qui consiste à déployer une nouvelle version d'une application côte à côte avec la version existante, mais à diriger seulement une petite partie du trafic vers la nouvelle version. Si tout va bien, le trafic est progressivement augmenté jusqu'à ce que la nouvelle version prenne la totalité du trafic. |
| **Déploiement Blue-Green** | Une stratégie de déploiement où deux versions de l'application sont maintenues côte à côte (bleue pour l'actuelle, verte pour la nouvelle). Une fois que la nouvelle version (verte) est prête et testée, le routage du trafic est basculé de la version bleue à la version verte. Cela permet des mises à jour sans temps d'arrêt. |
| **Argo Rollouts** | Extension d'Argo qui fournit des fonctionnalités avancées de déploiement telles que Canary et Blue-Green. |
| **Kustomize** | Outil de personnalisation pour les manifests Kubernetes, permettant de définir des variantes d'une base de configuration. |
| **Odo** | Odo est un outil de développement rapide pour les applications Kubernetes et OpenShift, simplifiant le cycle DevOps. |
| **Github registry** | Un service d'hébergement de packages logiciels lié à GitHub. |
| **Graphana** | 	Une plateforme open source pour la surveillance et l'alerte. Typiquement utilisé en tandem avec Prometheus pour la surveillance des clusters Kubernetes. |
| **Pixie** | Outil d'observabilité natif pour Kubernetes, permettant de diagnostiquer les applications sans code d'instrumentation. |
| **Oneuptime** | OneUptime est une solution complète de suivi et de gestion de vos services en ligne. Que vous ayez besoin de vérifier la disponibilité de votre site Web, de votre tableau de bord, de votre API ou de toute autre ressource en ligne, OneUptime peut alerter votre équipe en cas de temps d'arrêt et tenir vos clients informés avec une page d'état. OneUptime vous aide également à gérer les incidents, à configurer des rotations d'astreinte, à exécuter des tests, à sécuriser vos services, à analyser les journaux, à suivre les performances et à déboguer les erreurs. |
| **Trivy** | Un scanner de vulnérabilité de conteneurs simple et complet. |
| **Cosign** | 	Un outil pour signer et vérifier les signatures des images de conteneurs. |
| **CodeQL** | Une plateforme d'analyse de code source pour trouver les vulnérabilités dans le code. Propriété de GitHub. |
| **Hashicorp Vault** | Outil pour gérer les secrets et protéger les données sensibles. |
| **Kubescape** | Outil d'analyse pour vérifier la conformité et la sécurité d'un cluster Kubernetes. |
| **SonarQube** | Plateforme d'analyse continue de la qualité du code qui inspecte le code pour détecter les bugs, les odeurs de code et les vulnérabilités de sécurité. |


## 2. Position du produit

### 2.1 Énoncé du problème

Le club Cédille assume la tâche d'héberger et de soutenir le développement d'une multitude de sites web et services en ligne pour les associations étudiantes de l'ÉTS. En outre, le club vise à offrir à ses membres des opportunités d'acquisition de compétences dans les domaines du DevOps, de Kubernetes et de la gestion des serveurs.

À l'heure actuelle, notre infrastructure repose sur un cluster Kubernetes géré par Google Cloud (GKE). Cependant, les frais associés à cette plateforme sont élevés, et avec l'augmentation du nombre de clubs que nous soutenons, les coûts deviennent financièrement problématiques. De surcroît, la gestion majoritairement automatisée par Google Cloud limite notre flexibilité pour personnaliser nos solutions d'hébergement et restreint les occasions d'apprentissage pour nos membres.

**Table 2.1.1: Énoncé du problème**

|Déclaration||
| --- | --- |
| Le problème | 1. Contrainte Financière : Le coût de maintien des services sur Google Cloud est significativement élevé et devient de plus en plus difficile à gérer à mesure que le nombre de clubs étudiants hébergés augmente. <br /> 2. Apprentissage et Personnalisation Limités : La gestion de la plupart des opérations par Google Cloud résulte en un environnement restreint qui offre peu d'opportunités pour apprendre et personnaliser les solutions d'hébergement, en particulier dans les domaines du DevOps, de Kubernetes et de la gestion de serveur. |
| affecte | 1. Durabilité Financière : Le club fait face à un fardeau financier croissant qui pourrait menacer sa capacité à continuer d'offrir des services d'hébergement aux clubs étudiants. <br /> 2. Valeur Éducative : La configuration actuelle limite les expériences d'apprentissage des membres du club, particulièrement dans des domaines pertinents à leur croissance technique comme le DevOps, Kubernetes et la gestion de serveur. |
| et cela se traduit par l'impact de | 1. Tension Financière : Si la situation reste inchangée, le club Cédille risque de devenir financièrement insoutenable, ce qui pourrait entraîner l'arrêt des services d'hébergement pour de nombreux clubs étudiants, affectant ainsi leur présence en ligne et leurs opérations. <br /> 2. Développement de Compétences Techniques Réduit : Les membres du club passent à côté d'expériences pratiques et de développement de compétences précieuses, ce qui est l'un des objectifs clés du club pour améliorer l'employabilité et l'expertise technique de ses membres. |

### 2.2 Énoncé du produit

Le club a décidé de migrer les serveurs vers des serveurs physiques, qui seront déployés à l’ÉTS.
 Le produit nommé **Plateforme CEDILLE** est une infrastructure d'hébergement basée sur des serveurs physiques, déployée à l'ÉTS, et gérée via une licence Omni de Sidero Labs. Cette plateforme vise à offrir une solution durable et évolutive pour héberger les sites web et les autres services des clubs étudiants. La plateforme utilise une architecture GitOps, intégrant divers outils d'automatisation, de surveillance et de sécurité pour simplifier la gestion tout en maintenant un haut niveau de performance et de sécurité.



**Tableau 2.2.1: Énoncé du produit**

|Déclaration||
|--|--|
| Plateforme CEDILLE est | Une infrastructure d'hébergement locale sur des serveurs physiques, conçue pour réduire les coûts tout en fournissant un environnement flexible et éducatif pour les membres du club Cédille. |
| ce qui | Permet une meilleure maîtrise des coûts et offre des opportunités plus riches pour l'apprentissage et le développement des compétences en DevOps, Kubernetes et gestion de serveur. Elle facilite également la surveillance, la sécurité et l'automatisation, tout en étant suffisamment flexible pour répondre aux besoins spécifiques de divers clubs étudiants. |
| Au contraire de | L'ancienne infrastructure basée sur Google Cloud (GKE), qui entraînait des coûts élevés et offrait moins de possibilités d'apprentissage et de personnalisation en raison de la gestion centralisée par Google Cloud. |
| Ce produit | Réduit significativement le fardeau financier du club tout en améliorant la valeur éducative et l'expérience pratique pour les membres. Il offre une solution plus durable et personnalisable pour les besoins d'hébergement des clubs étudiants de l'ÉTS. |

## 3. Utilisateur et parties prenantes

### 3.1 Sommaire des parties prenantes

Les parties prenantes sont toutes les personnes ou entités ayant un intérêt dans la réalisation du projet.

**Table 3.1.1: Résumé des parties prenantes**

| **Nom** | **Description** | **Responsabilités** |
| --- | --- | --- |
| **S1** Le club CEDILLE et ses membres | Club étudiant Open-Source de l'École de Technologie Supérieure | Conception, mise en place et maintenance de la plateforme CEDILLE. |
| **S2** Régie des clubs de l'ÉTS | Organisation au seins de l'ÉTS qui s'occupe de l'administration des clubs étudiants | S'assurer que tous les services mis en place servent les clubs étudiants et respectent la réglementation. |
| **S3** Département informatique (TI) de l'ÉTS | Organisation au seins de l'ÉTS qui s'occupe de l'informatique | S'assurer que tous nos services sont sécuritaire et n'enfreint aucune règle. |
| **S4** Les clubs étudiants de l'ÉTS | Club étudiant de l'École de Technologie Supérieure | Les clubs doivent communiquer clairement leurs besoins et exigences, ainsi que fournir des retours sur les services et les fonctionnalités offertes par la nouvelle plateforme. |

### 3.2 Sommaire des utilisateurs

Les utilisateurs sont toutes les personnes ou entités qui utiliseront ce produit.

**Table 3.2.1 : Sommaire des utilisateurs**

| **Name** | **Description** | **Responsabilités** |
| --- | --- | --- |
| **U1** Administrateur de la plateforme | Administrateur de la plateforme designé par le club CEDILLE | Maintenance de la plateforme et approbation d'un nouveau déploiement. |
| **U2** Les clubs étudiants et ses membres (Utilisateur) | Club étudiant de l'École de Technologie Supérieure | Interagir avec la plateforme pour obtenir diverses informations sur leurs différents services. |
| **U3** Personnel de l'ETS | Régie des clubs étudiants et services TI de l'ÉTS | Vérifier la comformité des applications et de l'infrastructure |

### 3.3 Environnement utilisateur

Les administrateurs de la plateforme **(U1)** peuvent se connecter à la Plateforme CEDILLE via une interface web ou des outils en ligne de commande pour gérer les différents services. Le Département informatique de l'ÉTS **(S3)** veille à ce que la connectivité et la sécurité des services soient maintenues, tout en respectant les réglementations et les normes en vigueur.

Les clubs étudiants et leurs membres **(U2)** interagissent avec la Plateforme CEDILLE via des portails web et des applications pour accéder à des informations, des services et des ressources diverses. Ils doivent également communiquer leurs besoins et exigences via le serveur Discord.

La réglementation des clubs est supervisée par la Régie des clubs de l'ÉTS **(S2)**, qui s'assure que la Plateforme CEDILLE sert les intérêts des clubs étudiants et est en conformité avec la réglementation institutionnelle.

Les clubs étudiants de l'ÉTS **(S4)** jouent un rôle actif en tant que fournisseurs d'exigences et de commentaires. Ils sont les utilisateurs finaux des services et ont donc un rôle clé à jouer pour s'assurer que la Plateforme CEDILLE répond à leurs besoins et attentes.

L'ensemble de la Plateforme CEDILLE et des services connexes doit être conforme aux normes et aux bonnes pratiques en matière de DevOps telle que défini à la section [Normes et standards](#71-normes-et-standards).

Toutes les parties doivent respecter les normes et les protocoles mis en place pour assurer la sécurité, la performance et la disponibilité de la Plateforme CEDILLE. Ces normes sont définies et maintenues par le club CEDILLE **(S1)** et le Département informatique de l'ÉTS **(S3)**.

## 3.4 Besoins des principaux utilisateurs et parties prenantes

Les besoins sont déterminés à partir d'une série d'entrevues et rencontre avec les parties prenantes. 
Des rapports de ces entrevues et rencontres se trouvent à l'annexe 1 de ce document.

De plus, les besoins d'administrations sont largement déterminés par les auteurs de ce document, puisqu'ils seront aussi responsable de l'administration de
la plateforme qui sera mise en place.

**Tableau 3.4.1: Définition des priorité**
| **Priorité** | **Définition** |
| ------------ | -------------- |
| Critique     | Ce besoin est essentiel à la réussite du projet. S'il n'est pas comblé le projet serait non-fonctionnel |
| Important    | Répondre à ce besoin apporte une valeure substentielle au projet; s'il n'est pas comblé il y aura un impact négatif sur l'expérience |
| Facultatif   | Si ce besoin n'est pas comblé, l'expérience demeurera postive même si réduite |

**Table 3.4.1: Besoins des principaux utilisateurs et parties prenantes**

| **ID** | **Priorité** | **Besoin** |
| --- | --- | --- |
| **B01** | Critique | Les sites webs des clubs étudiants (U2) doivent être publiquement accessibles sur internet |
| **B02** | Critique | Tous les services publics des clubs (U2) doivent utiliser HTTPS |
| **B03** | Important | Les clubs (U2) devraient pouvoir effectuer des changements mineurs aux sites webs par eux-même |
| **B04** | Critique | L'automatisation des processus doit permettre d'effectuer des changements aux applications des clubs (U2) en moins de 3 jours, incluant le processus de révision et approbation |
| **B05** | Critique | Des processus d'observabilité doivent permettre aux administrateurs (U1) d'être notifié de tout problème avec une application d'un club (U2) |
| **B06** | Critique | Des processus d'observabilité doivent permettre aux capitaines des clubs étudiants (U2) d'être notifié en cas d'incident |
| **B07** | Facultatif | Les clubs (U2) devraient avoir accès à des tableaux de bord d'observabilité pour leurs applications |
| **B08** | Critique | Les systèmes doivent être hautement disponible, de sorte que les mises à jours et les problèmes de serveurs de causent pas d'indisponibilité |
| **B09** | Important | Avoir en place des processus de communication de rapports post-incidents pour les clubs (U2) lors d'incidents de disponibilité et pour l'ÉTS (U3) lors d'incidents de sécurité |
| **B10** | Critique | Les bases de données des clubs (U2) et d'administration (U1) doivent pouvoir être restorés en cas de corruption de données ou d'évènements critiques |

## 4. Présentation du produit

This product will allow users to connect to voicerooms with a client using this product SDK and with a homeserver serving this product App Server. The product will respect the Matrix protocol philosophy by enabling distributed, E2EE and private voice communications.

### 4.1 Contexte du produit

![](./vision-context-view.drawio.svg)

**Figure 4.1.1:** Contexte du produit


### 4.2 Principaux avantages

**Table 4.2.1: Caractéristiques correspondantes pour chaque besoin de l'utilisateur**

| **Besoin de l'utilisateur** | **Caractéristiques correspondantes** |
| --- | --- |
| **N01** – Being able to join/quit a voice room | CAR2 |
| **N02** – Talking to multiple persons in a voice room | CAR2 |
| **N03** – Seeing a room state | CAR3 |
| **N04** – Implementing the voice room in current solution with ease | CAR1, CAR4, AQ3, AQ6 |
| **N05** – Voice needs to be only transmitted when active | CAR3 |
| **N06** – User wants to be able to mute himself | CAR9 |
| **N07** – User wants to be adjust volume or mute other individually or as a whole|CAR6, CAR7, CAR9|
| **N08** – Integration with current and future Matrix specifications |CU01, CU02, AQ1|
| **N09** – Users privacy and security must be protected |CAR10, CAR11, AQ4, AQ5|
| **N10** – Users want to share their screen |CAR12, CAR13|
| **N11** – Users want to show their camera feed |CAR12, CAR13|
| **N12** – Users want to suppress background noise |CAR14|
| **N13** – Users wants to experience a responsive environment |AQ2, AQ7|
| **N14** – Room owners wants to change some settings of the room |CAR4|
| **N15** – Users want to be able to control their input sound intensity |CAR15|


### 4.3 Hypothèses et dépendances

Cette section énumère les hypothèses et dépendances qui sont essentielles pour le développement et le déploiement de la Plateforme CEDILLE.

#### Hypothèses
- Disponibilité du Matériel: Nous supposons que tous les serveurs et équipements matériels nécessaires seront disponibles en temps opportun et répondront aux spécifications de configuration requises.
- Expertise Technique: L'hypothèse est faite que les membres du club ont ou acquerront les compétences nécessaires en technologies DevOps, Kubernetes et gestion de serveur.
- Soutien Institutionnel: Nous supposons que l'ÉTS fournira un soutien continu pour le projet, notamment en termes d'espaces pour les serveurs et d'accès à des ressources en réseau.

#### Dépendances
-Système d'Exploitation: Notre plateforme dépend du système d'exploitation Talos linux compatibles avec Kubernetes.
- Kubernetes: Le bon fonctionnement de la plateforme repose sur la dernière version stable de Kubernetes.
- Outils de Surveillance: La plateforme dépend de solutions de surveillance comme Pixie, OpenTelemetry, ClickHouse et Grafana pour le suivi des performances et de l'état du système.

### 4.4 Licence

Étant donné que le club CEDILLE a une dimension éducative et vise à enseigner les technologies DevOps, Kubernetes, et la gestion de serveur, le choix d'une licence qui favorise la flexibilité, l'accessibilité et la collaboration est crucial. C'est pourquoi nous avons opté pour la licence [Apache 2.0](../../../../.LICENSE) pour notre infrastructure.



### 4.5 Caractéristiques du produit

**Tableau 5.1 : Caractéristiques du produit**

| **ID** | **Description** | **Priorité** |
| --- | --- | --- |
| CAR1  | The product is a client library implementable by a developer and a app server ||
| CAR2  | The product allows users to connect to voice rooms and discuss with other users connected ||
| CAR3  | The product shows the room and users status : who is there, who is talking, who is streaming content etc. ||
| CAR4 | The product offers room-level settings tor the room owner ||
| CAR5  | The client library detects when the noise is under a certain level and stops transmitting sound | |
| CAR6  | The App Server API is open and documented so anyone can use it and extend functionalities ||
| CAR7  | The client library allows the end user to adjust other user's volume and mute them||
| CAR8  | The App Server allows Administrators to mute users for all users server-wide ||
| CAR9  | The client library allows users to mute or deafen themselves ||
| CAR10 | The product uses E2EE for signaling ||
| CAR11 | The product hides IP adresses of users ||
| CAR12 | The App server supports video streams for screen and camera sharing ||
| CAR13 | The client library supports device (web or OS) API for screen and camera video streams ||
| CAR14 | The product offer the user the option to enable a filter layer to suppress background noise (e.g. RNNoise) ||
| CAR15 | The client library allows the users to change its input sound intensity ||



### 5. Contraintes

**Table 5.1 :Contraintes**

| **ID** | **Contraintes** | **Description** |
| --- | --- | --- |
| C01 |Matrix protocol adherence| Product must adhere to the matrix protocol as much as possible |
| C02 |Matrix group VoIP proposition adherence| Product should try to follow the existing protocol extension proposition so when (and if) it is accepted in the feature, there is as few conflicts to resolve as possible[^4] |

### 6. Attributs de qualité

**Interopérabilité**

AQ1 - The solution MUST be compatible with the Matrix ecosystem

**Performance**

AQ2 – Voice data must be encoded-decoded fast enough to be unnoticeable

**Modifiabilité**

AQ3 – The system must be easily modified for different languages/platforms/OS

**Securité**

AQ4 – Confidential data must be protected

AQ5 – Voice signaling integrity must be protected

**Usabilité**

AQ6 – Developers should be able to use the APIs and libraries of this product with ease

**Évolutivité**

AQ7 – Product server application must be scalable to accommodate different loads

## 7. Autres exigences

### 7.1 Normes et standards

- On vise à utilisé la norme [ISO 32675:2022](https://www.iso.org/standard/83670.html) comme ligne directrice pour notre infrastructure.

### 7.2 Configuration requise

- TODO


### 7.3 Exigences en matière de documentation

- Architecture Technique : Schémas et explications détaillées de l'architecture des serveurs, du réseau et de la pile technologique.
- Documentation de la Configuration : Instructions pour la mise en place et la configuration de l'environnement, y compris les serveurs physiques, Kubernetes, et tous les autres outils utilisés.
- Manuel Utilisateur : Documentation destinée aux membres du club et autres utilisateurs de la plateforme, expliquant comment déployer et gérer leurs services.
- Procédures de Secours et de Restauration : Protocoles à suivre en cas de défaillance du système ou d'autres types d'urgences.


[^1]: École de Technologie Supérieure, Universités du Québec. [https://www.etsmtl.ca/](https://www.etsmtl.ca/)
