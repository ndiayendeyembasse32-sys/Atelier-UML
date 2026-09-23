# Facturer le départ

## Objectif

Établir la facture du séjour et déterminer le solde à payer en tenant compte de l’hébergement, des consommations, de la taxe de séjour et des versements déjà reçus.

## Acteurs

- **Acteur principal :** réceptionniste.
- **Acteur secondaire :** service de paiement externe, si un encaissement est nécessaire.
- **Bénéficiaire :** client.
- **Déclencheur :** le client se présente pour son départ.

## Préconditions

- L’arrivée du client a été enregistrée.
- Le séjour, la chambre et le nombre d’occupants sont connus.
- Les tarifs et les règles de taxe sont accessibles.
- Les consommations et les versements déjà reçus sont consultables.
- Le relevé téléphonique d’arrivée est enregistré.

## Scénario nominal

1. Le réceptionniste recherche le séjour du client.
2. Le système affiche les dates, la chambre, les occupants, les consommations et les versements déjà reçus.
3. Le réceptionniste vérifie les informations, ajoute les dernières consommations et saisit le relevé téléphonique final.
4. Le système calcule le prix de l’hébergement selon les nuits et le nombre d’occupants, puis ajoute les prestations et la taxe de séjour.
5. Le système présente le total, déduit les arrhes et autres paiements déjà reçus, puis affiche le solde.
6. Le réceptionniste vérifie le détail et valide l’émission de la facture.
7. Le système enregistre la facture avec une référence et la rend disponible pour remise au client.

## Extension — Encaisser un paiement

**Condition :** le solde à payer est positif.

Après l’étape 7 :

1. Le réceptionniste déclenche le règlement du solde.
2. Le système transmet la demande au service de paiement externe.
3. Le service de paiement confirme le succès.
4. Le système enregistre la transaction et marque la facture comme acquittée.

## Alternatives et exceptions

### 1a — Séjour introuvable

Le réceptionniste vérifie la référence et relance la recherche. Aucune facture n’est émise.

### 3a — Consommation oubliée ou erronée

Le réceptionniste corrige les données avant le calcul. Le scénario reprend à l’étape 4.

### 3b — Relevé téléphonique incohérent

Le système signale l’anomalie. Le réceptionniste vérifie et corrige les relevés avant de poursuivre.

### 4a — Tarif ou règle de taxe manquant

Le système suspend le calcul jusqu’à correction des paramètres par une personne autorisée.

### 5a — Solde nul

Aucun paiement supplémentaire n’est demandé. La facture est enregistrée comme acquittée après validation.

### 5b — Solde négatif

Le système signale un trop-perçu. Son traitement suit une règle à définir avec le gérant.

### 6a — Erreur détectée avant validation

Le réceptionniste corrige les données. Le système reprend le calcul à l’étape 4.

### Extension, étape 3a — Paiement refusé

La facture reste émise et non soldée. Le réceptionniste peut proposer une nouvelle tentative de paiement.

### Extension, étape 3b — Résultat du paiement inconnu

Le système vérifie la transaction avant toute nouvelle tentative pour éviter un double encaissement.

## Postconditions

- Une facture détaillée et référencée est enregistrée après validation.
- Les versements antérieurs sont pris en compte.
- Le solde restant à payer est connu.
- Si le règlement réussit ou si le solde est nul, la facture est acquittée.
- Si le paiement échoue, la facture reste non soldée.

## Règle de calcul

**Total du séjour = hébergement + prestations + taxe de séjour**

**Solde = total du séjour − arrhes − autres paiements déjà reçus**

La consommation téléphonique est calculée à partir des relevés et du tarif applicable, sans compter deux fois les montants déjà enregistrés.
