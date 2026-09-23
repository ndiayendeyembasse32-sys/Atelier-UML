Fiche de cas d'utilisation : Facturer le départ

Objectif

Établir la facture du séjour : hébergement selon le nombre d'occupants, prestations consommées et taxe de séjour, avec indication des sommes déjà versées et du solde.

Acteurs

Acteur principal : Réceptionniste.

Bénéficiaire : Client.

Déclencheur : le client se présente pour son départ.

Le service de paiement intervient dans le cas associé « Solder le séjour », après la facturation ; il n'est pas nécessaire au seul calcul et à l'émission de la facture.

Préconditions

L'arrivée du client a été enregistrée et le séjour est identifiable.

La chambre, les dates, les occupants, les tarifs et les règles de taxe applicables sont accessibles.

Les consommations enregistrées et les paiements déjà reçus sont consultables.

Le relevé téléphonique d'arrivée a été conservé.

Scénario nominal

Le réceptionniste recherche le séjour du client et demande sa facturation.

Le système affiche les dates, la chambre, le nombre d'occupants, les consommations et les paiements déjà enregistrés.

Le réceptionniste vérifie les informations, complète les dernières consommations et saisit le relevé téléphonique final.

Le système calcule le montant de l'hébergement selon les nuits et le nombre d'occupants, ajoute les prestations et la taxe de séjour. La consommation téléphonique est calculée à partir des relevés et du tarif applicable, sans double comptage.

Le système présente le détail, le total du séjour, les arrhes et autres paiements déjà encaissés, puis le solde restant à payer.

Le réceptionniste vérifie le récapitulatif et valide l'émission.

Le système attribue une référence à la facture, l'enregistre et la rend disponible pour remise au client. La facture indique le solde et son état de règlement.

Alternatives et exceptions

1a - Séjour introuvable ou arrivée non enregistrée

Le système signale le problème. Le réceptionniste vérifie la référence ou régularise le dossier avant de reprendre à l'étape 1. Aucune facture n'est émise.

3a - Consommation oubliée ou erronée

Le réceptionniste ajoute ou corrige la consommation avant validation. Le système conserve la traçabilité de la correction et reprend le calcul à l'étape 4.

3b - Relevé téléphonique final absent ou incohérent

Le système signale l'anomalie. Le réceptionniste vérifie les relevés. La facture définitive n'est pas émise tant que ce montant n'est pas établi ; reprise à l'étape 3 après correction.

4a - Tarif ou règle de taxe manquant

Le système ne remplace pas le montant manquant par zéro. Le dossier est mis en attente de correction des paramètres par une personne autorisée, puis le calcul reprend à l'étape 4.

5a - Solde nul

Le système indique que les sommes encaissées couvrent la facture. Après validation, la facture est enregistrée comme acquittée ; aucun paiement supplémentaire n'est demandé.

5b - Solde négatif

Le système signale un trop-perçu. Son traitement est soumis à une règle à valider avec le gérant ; aucun remboursement automatique non prévu par l'énoncé n'est inventé.

6a - Le réceptionniste détecte une erreur

Il revient aux données à corriger, puis le système recalcule à partir de l'étape 4. Aucune facture définitive n'est émise avant validation.

Postconditions

Succès : une facture détaillée et référencée est enregistrée ; les versements antérieurs sont pris en compte et le solde est connu.

Échec ou interruption : aucune facture définitive incorrecte n'est émise ; le séjour et les paiements précédents restent conservés.

La facturation seule ne prouve pas le paiement. Une facture avec un solde positif reste à régler.

Suite associée : Solder le séjour

Le réceptionniste déclenche le règlement du solde positif.

Le système demande l'encaissement au service de paiement externe.

Si le paiement réussit, le système enregistre la transaction et marque la facture acquittée.

Si le paiement échoue, la facture reste émise et non soldée ; le réceptionniste peut proposer une nouvelle tentative.

Si le résultat est inconnu, le système vérifie la transaction avant de relancer un paiement, afin d'éviter un double encaissement.

Cette séparation permet de réutiliser la fiche pour un diagramme de séquence de facturation, puis d'y associer la séquence de paiement.
