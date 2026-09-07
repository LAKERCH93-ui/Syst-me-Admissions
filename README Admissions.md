Backend Centralisé des Admissions

Description

Ce projet est une API de routage intelligente pour la gestion des admissions étudiantes. Il est capable de recevoir des candidatures depuis un formulaire frontend, de déterminer le campus de destination et d'appliquer une logique de traitement différente selon que l'étudiant suive un flux national (France) ou international.

Matrice de Routage

Le système dispatche les données vers 8 bases de données (Google Sheets) distinctes :

4 Campus différents.

2 Flux distincts : NATIONAL (France) et INTERNATIONAL (Hors France).

Fonctionnalités principales

Point d'entrée API unique : Réception des données en JSON via une requête HTTP POST (doPost).

Différenciation des flux :

Flux National : Génère un document Google Docs, envoie un code OTP par e-mail, gère une signature manuscrite en ligne et archive le dossier.

Flux International : Génère directement un PDF et l'envoie par e-mail sans passer par un prestataire externe.

Gestion des doublons : Vérification stricte basée sur l'adresse e-mail du candidat pour éviter les inscriptions multiples.

Outils d'administration : Fonctions de test de routage, audit de configuration et simulation d'inscriptions internes.

Formattage de données : Remplacement de variables dynamiques dans les textes (système de templates de type {{variable}}).

Requête Frontend attendue

Pour envoyer des données à ce backend, le frontend doit effectuer une requête HTTP POST avec un corps en JSON et un Content-Type spécifique.

Exemple d'appel :

fetch(URL_APPS_SCRIPT, {
  method: "POST",
  headers: { "Content-Type": "text/plain;charset=utf-8" },
  body: JSON.stringify(donneesCandidat)
});


Déploiement

Déployer ce script en tant qu'Application Web avec les droits d'accès définis sur "N'importe qui" (pour permettre la réception des requêtes POST depuis votre site web).