# Sprint Backlog
- (Orchestrator) Exposer un point de départ (route)
- (Orchestrator) 3 envois sur les différents endpoints (jobs)
- (Orchestrator) Passer le paramètre reçu de l'api gateway au extract (nom du provider de facture)
- (Orchestrator) Gestion d'erreur simple si job casse
- (Orchestrator) Création du dockerfile

- (Extract) Exposer 1 endpoint
- (Extract) Extraction du pdf depuis le S3
- (Extract) Envoi sur S3 du PDF (pour URL de retour pour le transform plus tard)
- (Extract) Renvoi de l'URL à l'Orchestrator pour la suite
- (Extract) Création de l'image docker

- (Transform) Fetch PDF du S3
- (Transform) Transformer les données
- (Transform) Création de la route 
- (Transform) Envoi des données transformées sur le S3
- (Transform) Retourner l'URL du S3 à l'orchestrator 
- (Transform) Création de l'image docker

- (CICD) Déploiement des images
- (CICD) Faire un package Dépôt
- (CICD) Faire un package organisation

- (load) Création du modèle de facture
- (load) Créer la route
- (load) Générer la Transaction SQL
- (load) Stocker la transaction dans le bucket S3
- (Load) Création de l'image docker

- (OPS) Déploiement du bucket S3 avec les dossiers suivants : extract, transform, load, hm_invoices

## Objectif de Sprint
Dans le dossier load du bucket avoir une transaction SQL pouvant être utilisée plus tard pour la base de données

## Durée du sprint
Jusqu'au 1 Décembre

## DoD
L'orchestrator reçoit et attend bien le retour de chaque job avant d'effectuer le prochain et se termine en fin de processus

L'Extraction retourne bien une URL pointant sur le dossier S3 contenant le/les pdf extraits correspondant à la demande.

Le Transform renvoie un Json formé correctement par rapport aux données ciblées, celles-ci seront stockées dans le dossier relié au transform dans le S3

Le load sera capable en partant des données JSON extraites de retourner une Transaction SQL suivant les bonnes pratiques et syntaxe SQL

Les tests de chaque processus (Orchestrator, Extract, Transform, Load) réussissent

## Détails du sprint

### Orchestrator 
Capable d'appeler les différents jobs dans l'ordre demandé par un ETL et renvoie bien les données dont ils ont chacun besoin

### Extract
Identifie les bons pdf à prendre et les met à disposition dans un bucket S3 pour le transform

### Transform
En partant des données extraites est capable de prendre les informations provenant de la section "VOS INFORMATIONS PERSONNELLES"

### Load
Sera capable à partir d'un objet json récupéré d'en extraire une transaction SQL répondant au modèle de facture
