# 📅 Workflow n8n : RECAP_RDV_AXIORNET

![n8n](https://img.shields.io/badge/n8n-v1.1-red?style=flat-square&logo=n8n)
![Author](https://img.shields.io/badge/Author-Axiornet-blue?style=flat-square)
![Status](https://img.shields.io/badge/Status-Active-green?style=flat-square)

## 📝 Présentation
Ce workflow automatise la gestion et la diffusion des agendas et des statistiques de messagerie pour **Axiornet**. Chaque soir à **20h00**, il centralise les informations cruciales pour la semaine à venir et génère des rapports visuels distribués via **Telegram** et **Email**.

Le workflow est structuré en deux pipelines distincts :
1. **Recap Calendrier** : Extraction des événements Google Calendar, filtrage et mise en forme (HTML/Telegram).
2. **Recap Day** : Génération d'un rapport de performance sur les flux d'emails reçus (Total vs Importants).

---

## ✨ Fonctionnalités clés
* **Trigger Planifié** : Exécution automatique chaque jour à 20h00.
* **Gestion Dynamique des Labels** : Vérification et création automatique du label "Axiornet" dans Gmail si absent.
* **Analyse Google Calendar** : Récupération exhaustive des événements sur 7 jours glissants (Titre, Lieu, Description, Liens).
* **Formatage Multi-Support** :
    * **Telegram** : Message structuré avec emojis pour une lecture rapide sur mobile.
    * **Email HTML** : Design moderne style "Card" responsive avec badges d'état (Heure vs Toute la journée).
* **Diffusion Multi-Destinataires** : Envoi synchronisé vers Ethan Franqueville et l'adresse générique Axiornet.

---

## 🏗️ Architecture du Workflow

### Branche 1 : Agenda (7 jours)
* **Nodes Gmail/Code** : Identifie l'ID du label "Axiornet".
* **Google Calendar API** : Récupère les données brutes de `your-email`.
* **Logic (JS)** : Le nœud `Format Recap` trie les événements par date, gère le fuseau horaire `Europe/Paris` et génère les templates HTML et Markdown.

### Branche 2 : Statistiques Quotidiennes
* **Static Data Management** : Utilise `$getWorkflowStaticData` pour compiler les compteurs d'emails reçus durant la journée.
* **Daily Recap Builder** : Produit un tableau de bord HTML résumant l'activité.

---

## ⚙️ Configuration

### Prérequis
Vous aurez besoin des identifiants (Credentials) suivants dans votre instance n8n :
* **Google Calendar OAuth2**.
* **Gmail OAuth2**.
* **Telegram API**.

### Variables de temps
Le workflow est configuré pour le fuseau horaire : `Europe/Paris`.

---

## 🚀 Installation
1.  Téléchargez le fichier `ManagerCalendarGoogle.json`.
2.  Dans n8n, cliquez sur **Import from File**.
3.  Associez vos propres **Credentials** aux nœuds Gmail, Calendar et Telegram.
4.  Activez le workflow pour lancer la planification.

---

## 👤 Auteur
Workflow maintenu par **Axiornet**. 
*Simple, propre, et toujours à jour.*
