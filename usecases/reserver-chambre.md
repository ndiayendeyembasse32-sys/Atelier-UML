# Fiche de cas d'utilisation : Réserver une chambre

* **Acteur principal :** Client (ou Agent de voyage)
* **Précondition :** Des chambres sont disponibles pour la période demandée.

## Scénario nominal
1. Le client saisit les dates de séjour et le nombre d'occupants.
2. Le système affiche les catégories de chambres disponibles et les tarifs.
3. Le client sélectionne une catégorie.
4. Le système calcule le montant des arrhes exigées (10% minimum).
5. Le client saisit ses informations de paiement.
6. Le système valide le paiement auprès du service externe.
7. Le système confirme la réservation et transmet un récapitulatif.

## Exceptions / Alternatives
* **3a. Aucune chambre disponible :** Le système informe le client et propose d'autres dates.
* **6a. Échec du paiement :** Le système affiche une erreur de paiement et remet la réservation en attente.

* **Postcondition :** La chambre est bloquée pour les dates choisies et les arrhes sont encaissées.
