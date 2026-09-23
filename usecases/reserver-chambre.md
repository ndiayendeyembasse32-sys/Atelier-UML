# Réserver une chambre

## Objectif

Réserver une chambre disponible pour une période et un nombre d’occupants compatibles avec sa capacité.

## Acteurs

- **Acteur principal :** client ou agent de voyage.
- **Acteur secondaire :** service de paiement externe.
- **Déclencheur :** le demandeur souhaite réserver un séjour.

## Préconditions

- Les hôtels, chambres, capacités et tarifs sont renseignés.
- Le service de réservation est accessible.
- L’agent de voyage, s’il intervient, est reconnu comme partenaire.

## Scénario nominal

Ce scénario concerne une réservation faite **plus de 8 jours avant l’arrivée**, avec versement immédiat des arrhes.

1. Le demandeur indique l’hôtel, les dates du séjour et le nombre d’occupants.
2. Le système affiche les chambres disponibles de capacité suffisante et leurs tarifs.
3. Le demandeur choisit une chambre et renseigne les coordonnées du client.
4. Le système vérifie de nouveau la disponibilité et la capacité, puis enregistre une réservation en attente en empêchant toute double réservation.
5. Le système présente le récapitulatif et le montant des arrhes exigées, d’au moins **10 %**.
6. Le demandeur valide le paiement auprès du service de paiement externe.
7. Le service de paiement confirme le succès. Le système enregistre les arrhes et confirme la réservation.
8. Le système fournit la référence et le récapitulatif de la réservation.

## Alternatives et exceptions

### 2a — Dates ou nombre d’occupants invalides

Le système explique l’erreur et demande une correction. Le scénario reprend à l’étape 1.

### 2b — Aucune chambre disponible

Le demandeur modifie ses critères ou abandonne. Aucune réservation n’est créée.

### 4a — Chambre devenue indisponible

Le système refuse l’enregistrement et propose un autre choix. Le scénario reprend à l’étape 2. Aucun paiement n’est demandé.

### 5a — Arrivée dans 8 jours ou moins

Selon l’hypothèse retenue, le système confirme la réservation sans exiger d’arrhes au titre de la règle des réservations anticipées. Le scénario reprend à l’étape 8.

### 6a — Versement différé

La réservation reste en attente. Le système communique sa référence et l’échéance de confirmation. Sans confirmation à J-8, elle est automatiquement annulée et la chambre est libérée.

### 7a — Paiement refusé

Le système informe le demandeur. La réservation reste en attente et une nouvelle tentative est possible avant l’échéance.

### 7b — Résultat du paiement inconnu

Le système vérifie la transaction auprès du service de paiement avant toute nouvelle tentative pour éviter un double encaissement.

## Postconditions

- **Succès :** la réservation est confirmée et les arrhes reçues sont enregistrées.
- **Attente :** la réservation anticipée reste non confirmée jusqu’au versement requis ou à son annulation à J-8.
- **Échec avant enregistrement :** aucune réservation n’est créée.
- **Dans tous les cas :** aucune double réservation d’une chambre pour une même nuit n’est autorisée.

## Hypothèses à valider

- Une réservation en attente bloque la chambre jusqu’à confirmation ou annulation.
- Les réservations faites à 8 jours ou moins sont confirmées après les contrôles, sans arrhes obligatoires.
- Le minimum de 10 % est calculé sur le montant prévu de l’hébergement ; cette base reste à valider avec le gérant.
