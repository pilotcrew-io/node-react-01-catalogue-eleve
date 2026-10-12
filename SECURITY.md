# Cadre de la simulation

Ce dépôt est un support de formation. Les trente produits, les prix et les réservations sont fictifs. Aucune vente, aucun paiement, aucun PSP et aucune livraison ne sont déclenchés. Ne saisir aucune donnée de carte, identité de client, adresse ou secret externe : rien de cela n’est nécessaire au parcours.

Garder les services sur 127.0.0.1. Le serveur mémoire est conçu pour un seul processus local. Il ne possède ni comptes, ni authentification, ni coordination entre instances, ni persistance durable. Ne pas présenter sa validation d’entrée ou sa clé d’idempotence comme une protection suffisante pour un service public.

Prix et stocks appartiennent au serveur ; les données du navigateur sont des intentions ou des photographies à vérifier. Une confirmation de réservation n’est pas une preuve de paiement. L’annulation d’un fetch n’annule pas une écriture déjà appliquée.

Le redémarrage efface les réservations et réinitialise les stocks. Prévenir avant cette opération pendant une démonstration et distinguer la perte mémoire d’un refus métier. Conserver des preuves minimales : commande, statut, identifiants fictifs et résultat utile. Les captures et rapports ne doivent contenir aucun compte ou secret personnel.

Si un comportement contredit le contrat, l’inscrire dans le journal avec un scénario reproductible et le corriger dans le périmètre du laboratoire. Aucun essai contre un service tiers n’est demandé.
