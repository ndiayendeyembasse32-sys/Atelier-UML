sequenceDiagram
    autonumber
    actor Client as Client / Agent
    participant Systeme as Système Hôtelier
    participant Paiement as Service de Paiement

    Client->>Systeme: Saisir dates de séjour et nombre d'occupants
    activate Systeme
    Systeme->>Systeme: Vérifier disponibilités et capacité
    Systeme-->>Client: Afficher catégories et tarifs
    deactivate Systeme

    Client->>Systeme: Sélectionner une catégorie
    activate Systeme
    Systeme->>Systeme: Calculer les arrhes (10% min.)
    Systeme-->>Client: Demander le paiement des arrhes
    deactivate Systeme

    Client->>Systeme: Saisir les données de paiement
    activate Systeme
    Systeme->>Paiement: Demander le prélèvement des arrhes
    activate Paiement

    alt Paiement accepté
        Paiement-->>Systeme: Confirmation du paiement
        Systeme->>Systeme: Enregistrer la réservation
        Systeme-->>Client: Confirmation et récapitulatif
    else Alternative 6a : Échec du paiement
        Paiement-->>Systeme: Refus du paiement
        Systeme-->>Client: Message d'erreur (remise en attente)
    end

    deactivate Paiement
    deactivate Systeme
