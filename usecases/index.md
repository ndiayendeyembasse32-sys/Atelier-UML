```mermaid

usecase-beta
direction LR

actor Demandeur("Demandeur") <<abstrait>>
actor Client("Client")
actor Agent("Agent de voyage")
actor Recep("Réceptionniste")
actor Serveur("Serveur restaurant/bar")
actor Gerant("Gérant")
actor Temps("Temps") <<temps>>
actor Paiement("Service de paiement externe") <<système externe>>

systemBoundary SYS["Logiciel de gestion hôtelière"]
  UC_Dispo("Consulter les disponibilités")
  UC_Res("Réserver une chambre")
  UC_Verif("Vérifier disponibilité et capacité")
  UC_Arrhes("Verser des arrhes")
  UC_Annul("Annuler une réservation")
  UC_Remb("Rembourser selon le délai")
  UC_AutoAnnul("Annuler automatiquement à J-8 les réservations non confirmées")
  UC_Arrivee("Enregistrer l'arrivée")
  UC_Conso("Enregistrer une consommation")
  UC_Fact("Facturer le départ")
  UC_Enc("Encaisser un paiement")
  UC_ListeArr("Éditer les arrivées prévues")
  UC_Taux("Consulter le taux d'occupation par catégorie et période")
  UC_AdmHotel("Administrer hôtels et catégories")
  UC_AdmCh("Administrer chambres")
  UC_AdmTarif("Administrer tarifs")
end

Client --|> Demandeur
Agent --|> Demandeur

Demandeur -- UC_Dispo
Demandeur -- UC_Res
Client -- UC_Annul

Recep -- UC_Arrivee
Recep -- UC_Conso
Recep -- UC_Fact
Recep -- UC_ListeArr
Serveur -- UC_Conso

Gerant -- UC_Taux
Gerant -- UC_AdmHotel
Gerant -- UC_AdmCh
Gerant -- UC_AdmTarif

Temps -- UC_AutoAnnul
Temps -- UC_ListeArr

UC_Enc -- Paiement
UC_Remb -- Paiement

UC_Res ..> : include UC_Verif
UC_Arrhes ..> : extend UC_Res
UC_Arrhes ..> : include UC_Enc
UC_Enc ..> : extend UC_Fact
UC_Remb ..> : extend UC_Annul

note for UC_Arrhes "Réservation faite plus de 8 jours avant l'arrivée : arrhes de 10 % minimum."
note for UC_Enc "Extension de Facturer le départ uniquement si le solde à payer est positif."
note for UC_Remb "Extension uniquement si un montant est remboursable selon le délai et les sommes versées."

```
