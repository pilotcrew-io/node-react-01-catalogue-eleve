# Prérequis et reprise avant la séance

- Day 0 terminé : Node 22 compatible, Git et deux projets squelettes préparés.
- Fonctions, tableaux, promises, HTML et CSS déjà pratiqués.
- Savoir lancer une commande dans le bon répertoire et lire une réponse JSON.

Lire [Day 0](../DAY0.md). La préparation, les installations et l’import des acquis se font **avant** les 270 minutes. Le formateur vérifie que chacun dispose d’un point de départ utilisable.

## Premier fork

Cloner le dépôt élève réellement proposé par PilotCrew. Préparer uniquement les squelettes techniques Node/TypeScript et React/TypeScript/Vite pendant le Day 0. Le catalogue, les composants et les règles du laboratoire seront écrits pendant la séance. Aucun téléchargement d’une solution privée n’est un prérequis.

## Contrat commun du magasin fictif

**PilotCrew Retail** est un laboratoire local : 30 produits inventés, `retail-001` à `retail-030`, dix dans chacune des catégories `maison`, `bureau`, `plein-air`. Chaque produit commence avec un stock de 20. Aucun paiement, compte client, prestataire de paiement, livraison ou achat réel n’est réalisé. Tous les montants sont des entiers en centimes EUR ; `priceCents: 2500` signifie 25,00 € fictifs. Les images externes sont absentes du socle pour garder une mesure reproductible.

| Objet | Champs du contrat |
|---|---|
| Produit | `id`, `name`, `description`, `category`, `priceCents`, `stock` |
| Page de produits | `items`, `total`, `page`, `pageSize` |
| Intention de réservation | `items`, tableau de lignes `{productId, quantity}` |
| Réservation | `id`, `status: CONFIRMED`, `items`, `totalCents`, `currency: EUR`, `createdAt` |
| Ligne confirmée | `productId`, `name`, `quantity`, `unitPriceCents`, `lineTotalCents` |

| Route | Résultat attendu |
|---|---|
| `GET /api/products` | 200, page ; défauts : page 1, 12 éléments, tri name-asc |
| `GET /api/products/{id}` | 200, produit actuel ; 404 PRODUCT_NOT_FOUND |
| `POST /api/reservations` | Dès l’atelier 03 : 201 et Location ; clé Idempotency-Key obligatoire |
| `GET /api/reservations/{id}` | Dès l’atelier 03 : 200, réservation ; 404 RESERVATION_NOT_FOUND |

La recherche `q` contient au plus 80 caractères après retrait des espaces en bordure et ignore casse et accents dans le nom et la description. `category` accepte uniquement les trois valeurs ci-dessus ; omettre le paramètre pour toutes les catégories. `page` est un entier de 1 à 10000 et `pageSize` de 1 à 24, écrits en chiffres ASCII sans zéro initial. `sort` accepte `name-asc`, `price-asc`, `price-desc` ; l’ID départage les égalités. Paramètres inconnus, répétés, structurés et valeurs invalides produisent 400 INVALID_QUERY. Une page au-delà des résultats reste une page valide, avec `items: []`.

Une réservation accepte **1 à 10 produits distincts, quantité entière de 1 à 5 par produit**, sans champ de prix, remise, devise ou statut envoyé par le client. La clé comprend 8 à 80 caractères ASCII alphanumériques ou tirets ; un UUID convient. L’ordre des lignes ne change pas l’intention. Même clé et mêmes couples produit/quantité : même réponse 201, même ID, aucun retrait supplémentaire. Même clé et intention différente : 409 IDEMPOTENCY_CONFLICT. Stock insuffisant : 409 INSUFFICIENT_STOCK, sans aucune écriture ni consommation de la clé. Toutes les lignes sont contrôlées avant de diminuer le moindre stock.

Le format d’erreur est `{error: {code, message}}`. Le backend normalise 400 INVALID_REQUEST/INVALID_JSON, 404, 405 METHOD_NOT_ALLOWED avec Allow, 413 PAYLOAD_TOO_LARGE au-delà de 16 KiB, 415 UNSUPPORTED_MEDIA_TYPE, 409 et 503 CAPACITY_REACHED à 500 réservations uniques. Le code peut expliquer l’erreur sans exposer une trace technique. Le plafond laisse rejouer les intentions déjà enregistrées.

Le serveur écoute `127.0.0.1:8080`. Vite écoute `127.0.0.1:5173` et relaie `/api`. Réservations et stocks restent en mémoire dans **un seul processus Node**. L’opération métier demeure synchrone, sans await entre vérification et écriture. Elle n’est ni une transaction durable, ni un verrou entre plusieurs processus. Le redémarrage perd les réservations et réinitialise les stocks ; aucune expiration ni annulation de réservation n’est implémentée.
