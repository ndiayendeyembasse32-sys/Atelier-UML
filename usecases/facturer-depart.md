Acteur principal : Réceptionniste 
Précondition : Le client est présent pour son départ (check-out). 
Scénario nominal :Le réceptionniste recherche la réservation du client. 
Le système calcule le total : chambre + prestations (bar/restaurant) + taxe de séjour + relève téléphonique. 
Le système déduit les arrhes déjà versées lors de la réservation. 
Le réceptionniste valide le montant final à payer.  
Le client règle via le service de paiement externe. 
Le système édite la facture finale et libère la chambre dans le système. 
Exceptions / Alternatives :
2a. Saisie de consommations oubliées : Le réceptionniste ajoute manuellement une prestation avant de relancer le calcul.
5a. Refus de paiement : La facture reste marquée comme "En souffrance" et le litige est transmis au gérant.
Postcondition : Le solde est réglé et la chambre passe au statut "À nettoyer/Libre".
