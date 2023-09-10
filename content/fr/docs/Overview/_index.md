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

-- SURVOL --

### 1.1 Objectif

-- OBJECTIF --

### 1.2 Porté

The scope of this project is to

1. Create a solution multiplexing audio for Matrix users in the same room
2. Create a pluggable solution for the client-side so it can be easily used by any Matrix client

This document does not cover the actual implementation in a client, but it will cover how a client can implement this solution. This project will also not propose any modifications to the Matrix standard; there is already a proposal in progress that will be discussed later in the document so there is no need to propose something new.

### 1.3 Définitions et acronymes

**Table 1.3.1: Définitions et acronymes**

| **ÉTS** | École de Technologie Supérieure |
| --- | --- |
| **Matrix** | Open standard and communication protocol for real-time communication with end-to-end encryption support |
| **E2EE** | End-to-End Encryption |


## 2. Position du produit

### 2.1 Énoncé du problème

The problem of only communicating with calls instead of rooms affects users and potential users of the Matrix protocol as means of communications. The proposed solution will allow them to communicate in a more natural way with voice rooms.

**Table 2.1.1: Problem statement**

|Statement||
| --- | --- |
| The problem of | Communicating only with calls is less natural than rooms in a lot of cases. All the Matrix implementations only support 1:1 calls or Jitsi calls. And even with Jitsi calls, it is not as natural as using a room. |
| affects | Users and potential users of Matrix protocol and clients |
| and this results with the impact of | As seen with the popularity of Discord, being able to organize a space with rooms and to being able to hop in and out of a voice channel can attract a lot of users. There is clearly a market of people using proprietary solutions like discord instead of open source solutions since there is none that really work. It also affects the privacy of these users since Discord have incentives to market the data, which is not E2EE. |

### 2.2 Énoncé du produit

The **Matrix Voicerooms** product aims to solve this problems by creating a pluggable solution that will follow the Matrix protocol, but as a seperate service outside the homeserver, as an application service/server[^3]

**Tableau 2.2.1: Product statement**

|Statement||
|--|--|
| Matrix Voicerooms is | A pluggable application following the Matrix protocol as an application service/server. |
| That | Allows clients and homeserver to add it to their service in a minimum amount of time. |
| In contrary to | The current solution only allowing 1:1 connections. |
| This product | Will be a complete voice room solution available to Matrix users. It will be decentralized and encrypted as the other Matrix events are. |

## 3. Utilisateur et parties prenantes

### 3.1 Sommaire des parties prenantes

Stakeholders are every person or entity with an interest in the project realization.

**Table 3.1.1: Stakeholders summary**

| **Name** | **Description** | **Responsibilities** |
| --- | --- | --- |
| **S1** CEDILLE | Open-Source student club at École de Technologie Supérieure University | Coordination, conceptualization and programming of this product |
| **S2** Open-Source community | Any person outside CEDILLE participating in the project realization | Proposing changes and programming the product |
| **S3** Matrix.org Fondation | Governance organization of the Matrix standard | Managing the Matrix standard and the specifications modification process |

### 3.2 Sommaire des utilisateurs

Users are every person or entity that will be using this product.

**Table 3.2.1 : Users summary**

| **Name** | **Description** | **Responsibilities** |
| --- | --- | --- |
| **U1** Users | Users are every person using the Matrix protocol through a client implementing this product | Using the product through the Matrix protocol to communicate in voice rooms |
| **U2** Matrix Homeservers | Homeservers as defined in the Matrix standard architecture | Coordinate the rooms and room calls |
| **U3** Matrix Clients | Matrix Clients are user interfaces used to access the Matrix network through homeservers | Implements this product in their own |
| **U4** Room owner | Room owners are users owning a voiceroom | Manage the voicerooms settings and members |

### 3.3 Environnement utilisateur

Users ( **U1** ) can connect to voice room through a Matrix Client ( **U3** ) implementing the product described in this document. The voice rooms are managed by its owner ( **U4** ). Each user is also connected to a Matrix homeserver ( **U2** ) that will handle the events so ths product can handle the VoIP signaling.

Every pieces must follow the Matrix standard as defined by the Matrix.org Fondation ( **S3** ).

## 4. Besoins des principaux utilisateurs et parties prenantes

**Table 3.4.1: Main users and stakeholders needs**

| **Need** | **Priority** | **Current situation**| **Desired situation** |
| --- | --- | --- | --- |
| **N01** – Being able to join/quit a voice room | Critical | All calls (Jitsi or 1:1) must be initiated manually every time | A voice room must act as an always active call, with people joining and quitting them whenever they want |
| **N02** – Talking to multiple persons in a voice room | Critical | Matrix only supports 1:1 calls and Jitsi through an extension, but Jitsi does not act as a voice room | Matrix should support many-to-many audio communication in a voice room |
| **N03** – Seeing a room state | Important | N/A | Some information like connected users and active speaks should be displayed |
| **N04** – Implementing the voice room in current solution with ease | Important | N/A | Through a library or a similar solution, this product should be easy enough to implement so that it can be done in a few hours |
| **N05** – Voice needs to be only transmitted when active | Critical | N/A | Voice activity is detected and data is only transmitted when a person is talking |
| **N06** – User wants to be able to mute himself | Critical | Users can mute themselves in 1:1 calls and Jitsi | Users can mute themselves in all calls including voice rooms |
| **N07** – User wants to be adjust volume or mute other individually | Important | Jitsi supports muting others but adjusting volume individually | Users can mute others in a voice room or adjust their volume  |
| **N08** – Integration with current and future Matrix specifications | Critical | 1:1 calls respect the Matrix protocol and Jitsi is an extension as defined in theMatrix protocol | This product should also fit in the Matrix specification and be open to future changes, notably the proposal for group VoIP[^4] |
| **N09** – Users privacy and security must be protected | Critical | Everything is E2EE by default. | Some version of E2EE must be used in voice rooms. IPs must be protected |
| **N10** – Users want to share their screen | Low | Only through a Jitsi call | Users should be able to share their screen directly in a room |
| **N11** – Users want to show their camera feed | Low | Only through a Jitsi call | Users should be able to share their camera feed directly a room |
| **N12** – Users want to suppress background noise | Low | N/A | Users should be able to activate some background noise suppression on their device |
| **N13** – Users wants to experience a responsive environment | Important | We can currently scale a cluster with ease to accommodate load | The new solution should also be scalable by an admin and the load should be balanced between different app servers |
| **N14** – Room owners wants to change some settings of the room | Low | Room owners can manage users and permissions | The new solution should allow personalization of the voice settings and permissions of a room (mute server, bitrate...) |
| **N15** – Users want to be able to control their output sound intensity | Low | N/A | Should allow users to lower or increase their sound output to accommodate for different microphone sensitivity. |

## 4. Présentation du produit

This product will allow users to connect to voicerooms with a client using this product SDK and with a homeserver serving this product App Server. The product will respect the Matrix protocol philosophy by enabling distributed, E2EE and private voice communications.

### 4.1 Contexte du produit

![](./vision-context-view.drawio.svg)

**Figure 4.1.1:** Product context


### 4.2 Principaux avantages

**Table 4.2.1: Corresponding Characteristics for each User Needs**

| **User Need** | **Corresponding Characteristics** |
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

This project will assume that the external parts (homeserver and clients) respects the Matrix protocol.

### 4.4 Licence

The Matrix.org organisation distributes the protocol and the reference implementations under the *Apache 2.0* license. This permissive license allows anyone to use the software as they please. By doing so, Matrix.org reduces the risk that the licensing is an impediment to the growth of the Matrix standard.

To stay consistant with this, and since the growth of the protocol is also an objective of this project, we should also use the *Apache 2.0* license. See here for reference: https://www.apache.org/licenses/LICENSE-2.0

### 4.5 Caractéristiques du produit

**Tableau 5.1 : Product Characteristics**

| **ID** | **Description** | **Priority** |
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

**Table 5.1 :Constraints**

| **ID** | **Constraint** | **Description** |
| --- | --- | --- |
| C01 |Matrix protocol adherence| Product must adhere to the matrix protocol as much as possible |
| C02 |Matrix group VoIP proposition adherence| Product should try to follow the existing protocol extension proposition so when (and if) it is accepted in the feature, there is as few conflicts to resolve as possible[^4] |

### 6. Attributs de qualité

**Interoperability**

AQ1 - The solution MUST be compatible with the Matrix ecosystem

**Performance**

AQ2 – Voice data must be encoded-decoded fast enough to be unnoticeable

**Modifiability**

AQ3 – The system must be easily modified for different languages/platforms/OS

**Security**

AQ4 – Confidential data must be protected

AQ5 – Voice signaling integrity must be protected

**Usability**

AQ6 – Developers should be able to use the APIs and libraries of this product with ease

**Scalability**

AQ7 – Product server application must be scalable to accommodate different loads

## 7. Autres exigences

### 7.1 Normes et standards

- Matrix Protocol Specification
- Matrix Protocol Extension Proposal for Voice Rooms

### 7.2 Configuration requise

- The deployment must work in a containerized environment. Both docker-compose and Kubernetes should be possible targets. 


### 7.3 Exigences en matière de documentation

- The API of the App Server must be documented in detail
- The public methods of the client libraries must be documented in detail
- The requirements, planning and architecture documentation should be produced as thing progress and should be publicly available
- A user manual should be written, destined mainly to Matrix clients developpers


[^1]: [https://spec.matrix.org/latest/#architecture](https://spec.matrix.org/latest/#architecture)
[^2]: École de Technologie Supérieure, Universités du Québec. [https://www.etsmtl.ca/](https://www.etsmtl.ca/)
[^3]: [https://matrix.org/docs/guides/application-services](https://matrix.org/docs/guides/application-services)
[^4]: Matrix Spec proposal for group VoIP [https://github.com/matrix-org/matrix-spec-proposals/blob/matthew/group-voip/proposals/3401-group-voip.md](https://github.com/matrix-org/matrix-spec-proposals/blob/matthew/group-voip/proposals/3401-group-voip.md) 
  Matrix Spec proposal PR [https://github.com/matrix-org/matrix-spec-proposals/pull/3401](https://github.com/matrix-org/matrix-spec-proposals/pull/3401)


