# Évaluation et preuves

Le barème porte sur ce qui est **démontré et expliqué**. Une suite non exécutée ou une capture absente n’est pas un succès implicite. Les choix internes peuvent différer du corrigé si le contrat et les critères sont respectés.

| Critère | Points / 20 | Preuve attendue |
| --- | --- | --- |
| Contrat et invariants formulés | 3 | Le journal distingue total, page, photographie et autorité serveur. |
| API cohérente et validation stricte | 4 | Requêtes nominales et frontières invalides observées avec statuts. |
| Composants et états React | 4 | Attente, liste, vide et erreur réellement reproductibles. |
| Validation runtime et erreurs | 3 | Réponse mal formée refusée sans NaN ni écran cassé. |
| Accessibilité et tests ciblés | 3 | Parcours clavier et tests par rôle montrés. |
| Preuves, revue et limites | 3 | Commit, commandes et limites mémoire explicitement rendus. |

## Questions d’explication

1. Pourquoi total peut-il être supérieur à items.length ?
2. Une quantité de stock affichée garantit-elle la future réservation ?
3. Que protège TypeScript, et que faut-il encore vérifier sur le JSON ?
4. Pourquoi une recherche vide peut-elle répondre 200 ?
5. Que doit faire le nettoyage d’un effet de lecture ?

## Format de preuve

Pour chaque contrôle : commit, environnement, commande ou action, résultat attendu, résultat observé, interprétation et lien vers le rapport/capture. Séparer backend, frontend, navigateur et éventuelle CI distante. Pour une mesure : conserver aussi protocole et valeurs brutes.

Un invariant critique non respecté reste non acquis même si les points de présentation sont obtenus. L’évaluation est formative ; elle n’atteste ni une mise en production, ni un niveau senior, ni la sécurité d’un service public.
