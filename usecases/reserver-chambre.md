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
