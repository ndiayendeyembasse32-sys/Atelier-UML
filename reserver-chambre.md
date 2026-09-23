
1fa40abd-9633-4b4b-9dcc-aa7d9f72593f.png

94c690a5-e0c0-44f1-a4a0-c84239f6709f.png

aujourd’hui 16:38

atelier-hotel-usecase-2_260923_163500.pdf
PDF

861ce46f-2a6f-4d95-9c1c-863a817fb930.png
ca correspond ou pas

Voici ton code usecase-beta avec les suppressions, ajouts et modifications intégrés :

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
J’ai adapté tes modifications à la syntaxe usecase-beta, car les écritures -.->|...| et (["..."]) appartiennent au format flowchart.


81ac5f3d-caf4-49d9-8f56-26e695f3b94c.png
cest bon?

Oui, ton diagramme correspond maintenant aux corrections demandées. ✅

Le client est relié à l’annulation.

La réservation inclut la vérification de disponibilité et de capacité.

L’annulation automatique précise J-8, sans remboursement systématique.

Le remboursement et l’encaissement sont conditionnels.

Le taux d’occupation précise la catégorie et la période.

Les acteurs sont à l’extérieur de la frontière du logiciel.

Pense à harmoniser ton explication écrite avec le diagramme : Client et Agent de voyage sont deux acteurs distincts qui héritent ici d’un acteur commun abstrait, Demandeur.

Pour le rendu complet, il reste à joindre la liste des acteurs et les deux fiches textuelles : « Réserver une chambre » et « Facturer le départ ».


renvoie les 2 fichiers

Voici les deux fichiers :






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

Ce code est en PlantUML, autorisé par l’énoncé. Il faut cependant corriger les paiements : les arrhes sont conditionnelles, et annuler peut entraîner un remboursement, pas un paiement.

Voici la version corrigée :

@startuml
left to right direction
skinparam packageStyle rectangle

actor "Client" as client
actor "Agent de voyage" as agent
actor "Réceptionniste" as recep
actor "Personnel restaurant / bar" as personnel
actor "Gérant" as gerant
actor "Service de paiement" as paiement <<externe>>
actor "Horloge système" as temps <<temps>>

rectangle "Système de gestion hôtelière" {
    usecase "Consulter les disponibilités" as UC_Consulter
    usecase "Réserver une chambre" as UC_Reserver
    usecase "Vérifier disponibilité\net capacité" as UC_Verifier
    usecase "Verser des arrhes" as UC_Arrhes
    usecase "Annuler sa réservation" as UC_Annuler
    usecase "Rembourser selon le délai" as UC_Rembourser

    usecase "Enregistrer l'arrivée" as UC_Arrivee
    usecase "Saisir les consommations" as UC_Conso
    usecase "Facturer le départ" as UC_Depart
    usecase "Encaisser un paiement" as UC_Encaisser

    usecase "Éditer les arrivées prévues" as UC_EditerArrivees
    usecase "Consulter le taux d'occupation\npar catégorie et période" as UC_Taux
    usecase "Administrer hôtels, catégories,\nchambres et tarifs" as UC_Admin
    usecase "Annuler les réservations\nnon confirmées à J-8" as UC_AnnulAuto
}

client -- UC_Consulter
client -- UC_Reserver
client -- UC_Annuler
client -- UC_Arrhes

agent -- UC_Consulter
agent -- UC_Reserver
agent -- UC_Arrhes

recep -- UC_Arrivee
recep -- UC_Conso
recep -- UC_Depart
recep -- UC_EditerArrivees

personnel -- UC_Conso

gerant -- UC_Taux
gerant -- UC_Admin

paiement -- UC_Encaisser
paiement -- UC_Rembourser

temps -- UC_AnnulAuto
temps -- UC_EditerArrivees

UC_Reserver ..> UC_Verifier : <<include>>
UC_Arrhes ..> UC_Encaisser : <<include>>

UC_Rembourser ..> UC_Annuler : <<extend>>\n[montant remboursable > 0]
UC_Encaisser ..> UC_Depart : <<extend>>\n[solde à payer > 0]

note bottom of UC_Arrhes
  Réservation faite plus de 8 jours avant l'arrivée :
  arrhes de 10 % minimum pour la confirmation.
  Versement immédiat ou ultérieur avant l'échéance.
end note

note bottom of UC_EditerArrivees
  Déclenchement chaque matin.
end note

@enduml
Ici, « Verser des arrhes » reste une action distincte, ce qui permet au client ou à l’agent de payer après avoir créé la réservation, avant l’échéance de confirmation.


comment tester

Ton dernier code est en PlantUML. Pour le tester :

Ouvre l’éditeur PlantUML.

Efface le code d’exemple.

Colle tout ton code, de @startuml jusqu’à @enduml.

Clique sur Submit pour générer le diagramme.

Si le diagramme apparaît, la syntaxe est acceptée. Si un message d’erreur apparaît, envoie-moi une capture pour que je t’aide à le corriger.

Ne colle pas ce code dans un bloc Mermaid : ce sont deux formats différents.


Bibliothèque
/
reserver-chambre.md



Fiche de cas d'utilisation : Réserver une chambre
Objectif
Réserver une chambre disponible pour une période et un nombre d'occupants compatibles avec sa capacité.

Acteurs
Acteur principal : Client ou Agent de voyage partenaire agissant pour un client.

Acteur secondaire : Service de paiement, si des arrhes sont versées.

Déclencheur : l'acteur souhaite réserver un séjour.

Préconditions
Les hôtels, chambres, capacités et tarifs sont renseignés.

L'acteur peut accéder au service de réservation ; l'agent est reconnu comme partenaire.

Une disponibilité affichée ne constitue pas une garantie : elle sera contrôlée au moment de l'enregistrement.

Scénario nominal
Ce scénario décrit une réservation à plus de 8 jours de l'arrivée, avec versement immédiat des arrhes.

L'acteur indique l'hôtel souhaité, les dates d'arrivée et de départ et le nombre d'occupants.

Le système vérifie la cohérence des dates et du nombre d'occupants, puis présente les chambres disponibles de capacité suffisante et leurs prix.

L'acteur choisit une chambre, renseigne les coordonnées du client et valide le récapitulatif.

Le système revérifie la disponibilité et la capacité, puis enregistre atomiquement une réservation en attente. La chambre est bloquée pour les nuits concernées, sans double réservation.

Le système constate que l'arrivée est à plus de 8 jours et indique le minimum d'arrhes, d'au moins 10 %, ainsi que l'échéance de confirmation à J-8.

L'acteur choisit de verser les arrhes ; le système transmet la demande au service de paiement.

Le service de paiement confirme le succès. Le système enregistre la transaction et le montant reçu, puis confirme la réservation si le minimum requis est atteint.

Le système fournit la référence de réservation et un récapitulatif : hôtel, chambre, période, occupants, montant et arrhes versées.

Alternatives et exceptions
2a - Dates ou nombre d'occupants invalides
Le système explique l'erreur. L'acteur corrige sa demande ; reprise à l'étape 1.

2b - Aucune chambre compatible disponible
Le système signale l'absence de résultat. L'acteur modifie ses critères ou abandonne. Aucune réservation n'est créée.

4a - Chambre devenue indisponible
Une autre demande a réservé la chambre depuis l'affichage. Le système refuse l'enregistrement et propose de choisir une autre chambre ; reprise à l'étape 2. Aucun paiement n'est demandé.

5a - Réservation à 8 jours ou moins de l'arrivée
Selon l'hypothèse retenue, le système confirme la réservation sans exiger d'arrhes au titre de la règle des réservations anticipées. Reprise à l'étape 8.

6a - Versement différé
La réservation reste en attente. Le système communique la référence et l'échéance. L'acteur pourra déclencher « Verser les arrhes » ultérieurement. Si la réservation n'est pas confirmée à J-8, le traitement automatique l'annule et libère la chambre.

7a - Paiement refusé ou montant insuffisant
Le système ne confirme pas la réservation et indique le problème. L'acteur peut réessayer ou compléter le versement. Tout montant réellement encaissé est conservé dans le suivi des paiements. L'échéance à J-8 reste applicable.

7b - Résultat de paiement inconnu
Le système indique que la vérification est en cours. Il vérifie le résultat auprès du service de paiement avant une nouvelle tentative afin d'éviter un double encaissement. La réservation n'est pas confirmée sans preuve du versement requis.

Postconditions
Succès nominal : une réservation confirmée existe, liée à une chambre, une période et un nombre d'occupants valide ; les arrhes et la référence de paiement sont enregistrées.

Attente : une réservation non confirmée existe avec une échéance à J-8.

Échec avant enregistrement : aucune réservation ni aucun paiement n'est créé.

Invariant : aucune chambre ne possède deux réservations actives sur une même nuit.

Points à valider
Assiette de calcul des 10 %, politique applicable aux réservations proches de l'arrivée, et heure exacte du traitement à J-8. Les choix provisoires sont indiqués dans l'index.

