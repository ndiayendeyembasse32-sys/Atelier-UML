sequenceDiagram
    autonumber
    actor Recep as Réceptionniste
    participant Systeme as Système Hôtelier
    participant Paiement as Service de Paiement

    Recep->>Systeme: Rechercher la réservation
    activate Systeme
    Systeme->>Systeme: Calculer total (chambre + prestations + taxe + tél)
    Systeme->>Systeme: Déduire les arrhes
    Systeme-->>Recep: Afficher le montant net
    deactivate Systeme

    opt Alternative 2a : Prestation oubliée
        Recep->>Systeme: Saisir la prestation manquante
        activate Systeme
        Systeme->>Systeme: Recalculer le montant
        Systeme-->>Recep: Mettre à jour le montant net
        deactivate Systeme
    end

    Recep->>Systeme: Valider le montant final
    activate Systeme
    Systeme->>Paiement: Demander le règlement du solde
    activate Paiement

    alt Paiement validé
        Paiement-->>Systeme: Confirmation du règlement
        Systeme->>Systeme: Éditer la facture finale
        Systeme->>Systeme: Libérer la chambre (statut "À nettoyer")
        Systeme-->>Recep: Afficher la facture validée
    else Alternative 5a : Refus de paiement
        Paiement-->>Systeme: Échec de la transaction
        Systeme->>Systeme: Marquer la facture "En souffrance"
        Systeme-->>Recep: Alerter (litige gérant)
    end

    deactivate Paiement
    deactivate Systeme
