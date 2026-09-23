# Partie 1 : Les Acteurs

## Liste des acteurs
* **Client** (Humain) : Consulte les disponibilités, réserve et annule ses réservations.
* **Agent de voyage** (Humain / Système externe) : Réserve des chambres pour le compte de ses clients.
* **Réceptionniste** (Humain) : Enregistre les arrivées, saisit les consommations et effectue la facturation au départ.
* **Gérant** (Humain) : Gère le paramétrage (hôtels, chambres, tarifs) et consulte les statistiques.
* **Service de paiement externe** (Système externe) : Encaisse les paiements.
* **Horloge Système** (Temps) : Déclenche l'annulation automatique à J-8 et l'édition des arrivées du jour.

## Question sur l'Agent de voyage
L'Agent de voyage est un **acteur distinct** du Client. Même s'il effectue des réservations, il agit pour le compte de tiers et peut disposer de conditions d'accès ou de règles de gestion spécifiques liées à son partenariat.

---

# Partie 2 : Diagramme de Cas d'Utilisation

```plantuml
@startuml
left to right direction
skinparam packageStyle rectangle

actor "Client" as client
actor "Agent de Voyage" as agent
actor "Réceptionniste" as recep
actor "Gérant" as gerant
actor "Service de Paiement" as paiement << System >>
actor "Horloge Système" as temps << Time >>

rectangle "Système de Gestion Hôtelière" {
    usecase "Consulter les disponibilités" as UC_Consulter
    usecase "Réserver une chambre" as UC_Reserver
    usecase "Annuler une réservation" as UC_Annuler
    usecase "Payer des arrhes / solde" as UC_Payer
    usecase "Enregistrer l'arrivée" as UC_Arrivee
    usecase "Saisir les consommations" as UC_Conso
    usecase "Facturer le départ" as UC_Depart
    usecase "Editer les arrivées du jour" as UC_EditerArrivees
    usecase "Consulter le taux d'occupation" as UC_Taux
    usecase "Administrer l'hôtel (chambres, tarifs)" as UC_Admin
    usecase "Annuler automatiquement (J-8)" as UC_AnnulAuto
}

client --> UC_Consulter
client --> UC_Reserver
client --> UC_Annuler

agent --> UC_Consulter
agent --> UC_Reserver

recep --> UC_Arrivee
recep --> UC_Conso
recep --> UC_Depart

gerant --> UC_Taux
gerant --> UC_Admin

UC_Reserver .> UC_Payer : <<include>>
UC_Annuler .> UC_Payer : <<extend>>
UC_Depart .> UC_Payer : <<include>>

UC_Payer -- paiement

temps --> UC_AnnulAuto
temps --> UC_EditerArrivees

@enduml
