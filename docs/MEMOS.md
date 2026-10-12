# Mémos — Retail · Un catalogue React accessible

À relire pour expliquer les décisions ; les mémos ne remplacent pas les preuves de [l’évaluation](EVALUATION.md).

## Source de vérité et photographie

Un catalogue HTTP est une photographie de l’état au moment de la lecture. Un stock de vingt ne promet pas que vingt unités seront encore disponibles au moment de réserver. Cette distinction prépare les ateliers suivants : l’interface informe, le serveur tranche lors de l’opération métier. Le prix affiché vient de priceCents ; les centimes évitent d’utiliser un nombre décimal approximatif comme unité de calcul.

## Une page n’est pas un catalogue entier

Le serveur filtre d’abord les trente produits, compte les résultats, les trie puis extrait la page. total renseigne l’ensemble filtré ; items décrit seulement la page courante. Une page vide peut être valide, tout comme une recherche sans résultat. Mélanger ces cas avec une panne empêcherait l’utilisateur de savoir quelle action est utile.

## Trois frontières de validation

La query HTTP, le JSON de réponse et l’état de l’interface sont trois sujets différents. Une query valide permet au serveur de travailler. Une réponse validée à l’exécution protège React contre une forme inattendue. Une union d’états évite d’afficher simultanément réussite et erreur. TypeScript contribue au raisonnement dans le code ; il ne transforme pas une donnée reçue en donnée sûre par une simple annotation.

## Composants et responsabilités

Un composant utile correspond à une partie de l’expérience ou à une logique réutilisable. Découper chaque ligne en un composant n’améliore pas automatiquement la compréhension. La liste gère l’ensemble, une fiche décrit un produit, le client HTTP gère les réponses. Les contrôles natifs apportent un comportement clavier cohérent ; leur nom accessible indique l’action, pas seulement leur forme visuelle.

## Effet et action

La lecture du catalogue synchronise l’interface avec une ressource externe. Un effet convient si ses dépendances et son nettoyage sont explicites. Le clic sur Réessayer représente une intention ; il demande une nouvelle lecture. Créer une nouvelle requête à chaque rendu ou oublier les anciennes réponses produit des boucles et des écrans incohérents. Le nettoyage existe pour gérer ces changements, y compris les cycles supplémentaires du mode de développement.

## Ce qu’une preuve démontre

Une capture prouve un état vu dans un contexte donné ; un test HTTP prouve une règle contrôlée ; un build prouve la compilation. Aucune de ces preuves ne couvre seule tout le parcours. Associer les observations au commit permet de retrouver ce qui a réellement été vérifié. La revue cherche une explication reproductible, pas une série de cases cochées par défaut.
