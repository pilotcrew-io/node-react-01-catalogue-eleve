# Dépannage raisonné

Reproduire le symptôme sur un état connu, lire la réponse ou la trace, formuler une hypothèse puis effectuer un contrôle ciblé. Ne pas effacer tout le projet pour faire disparaître l’erreur.

| Symptôme | Hypothèse à vérifier | Contrôle et correction |
| --- | --- | --- |
| Liste toujours vide | Confusion entre items et la réponse complète | Inspecter le JSON réel et le type Page ; vérifier total séparément. |
| Total égal à douze | Comptage après pagination | Compter l’ensemble filtré avant slice et ajouter une assertion. |
| CORS ou API introuvable | URL absolue ou proxy absent | Appeler /api depuis Vite et vérifier la cible locale 8080. |
| page=01 accepté | Conversion numérique permissive | Valider la forme textuelle avant conversion. |
| Requêtes répétées sans fin | Dépendance instable de l’effet | Identifier la dépendance recréée ; ne pas supprimer arbitrairement la liste de dépendances. |
| Montant NaN | Réponse convertie sans contrôle | Valider le nombre entier au passage unknown vers Product. |
| Réessayer invisible au clavier | Faux bouton ou focus masqué | Employer un bouton natif et une règle focus-visible lisible. |

Si le blocage concerne une installation manquante du Day 0, le noter séparément du résultat métier. Demander une aide ciblée après avoir inscrit la commande, le statut et le message utile dans le journal.
