Acteur principal : Client (ou Agent de voyage)  
Précondition : Des chambres sont disponibles pour la période demandée.   
Scénario nominal :Le client saisit les dates de séjour et le nombre d'occupants. 
Le système affiche les catégories de chambres disponibles et les tarifs. 
Le client sélectionne une catégorie.  
Le système calcule le montant des arrhes exigées (10% minimum).
Le client saisit ses informations de paiement.
Le système valide le paiement auprès du service externe. 
Le système confirme la réservation et transmet un récapitulatif. 
Exceptions / Alternatives :
3a. Aucune chambre disponible : Le système informe le client et propose d'autres dates.
6a. Échec du paiement : Le système affiche une erreur de paiement et remet la réservation en attente.
Postcondition : La chambre est bloquée pour les dates choisies et les arrhes sont encaissées.   
