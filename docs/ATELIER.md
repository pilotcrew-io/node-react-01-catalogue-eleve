# Tutoriel 01 — Retail · Un catalogue React accessible

Le temps indiqué suppose [les prérequis](PREREQUIS.md) terminés. Le [contrat commun](PREREQUIS.md) est la référence pour les champs, routes et limites. Consigner les résultats au fil de l’eau dans [le journal](../travail/REPONSES.md).

## 1. Cadrer le premier incrément — 20 min

Ouvrez le journal et dessinez quatre écrans simples : attente, résultats, aucun résultat et erreur. Inscrivez pour chacun le titre de page, le texte annoncé, le contrôle utilisable et la donnée qui provoque cet état. Une page blanche n’est pas un état acceptable. L’écran ne doit pas présenter trente produits comme une vente réelle : placez la mention « Magasin fictif — exercice sans achat » à proximité du titre.

Séparez le modèle de lecture de son affichage. L’API possède noms, catégories, prix et stocks ; React possède l’état de la requête et les choix d’interface. Indiquez dans le journal pourquoi le stock affiché n’est encore qu’une photographie. Définissez ce qui compte comme terminé : douze produits sur la page initiale, total de trente, montant lisible en EUR, navigation cohérente au clavier et deux erreurs reproduites. Le nombre de produits visibles n’est pas le total du catalogue.

Lisez le contrat commun plus bas, puis reformulez-le à un binôme. Faites identifier le premier cas invalide que votre serveur devra refuser. Réservez dans backend/ une zone pour le domaine, une pour les routes et une pour le démarrage ; dans frontend/, prévoyez un client API, des composants et leurs tests. Les noms de fichiers sont libres si leur rôle est clair.

## 2. Construire le catalogue côté Node — 55 min

Dans le squelette backend préparé au Day 0, ajoutez un jeu déterministe de trente produits. Les identifiants vont de retail-001 à retail-030, les trois catégories contiennent dix produits chacune, les stocks initiaux valent vingt et les prix sont des entiers positifs. Inventez des libellés descriptifs ; n’utilisez aucune fiche commerciale réelle. Une même exécution propre doit fournir le même catalogue.

Écrivez une fonction de lecture qui retourne de nouveaux objets publics, sans exposer directement une collection interne mutable. Séparez la sélection des produits et la fabrication de la réponse HTTP. Ajoutez GET /api/products, puis GET /api/products/{id}. Commencez par vérifier la première page, le nombre total et une référence absente. L’ID de la route désigne un produit ; une ligne hors catalogue doit produire PRODUCT_NOT_FOUND, sans trace d’exception.

Configurez un lancement local après compilation. Une fois les scripts définis, utilisez ces commandes dans le projet backend :

```bash
npm run build
npm start
```

Dans un deuxième terminal, observez les en-têtes et le corps, pas seulement le texte de l’interface :

```bash
curl -i 'http://127.0.0.1:8080/api/products?page=1&pageSize=12'
curl -i 'http://127.0.0.1:8080/api/products/retail-001'
curl -i 'http://127.0.0.1:8080/api/products/reference-absente'
```

Notez le statut de chaque requête et une explication de total/page/pageSize. Ne copiez pas une réponse attendue dans la colonne des observations. Le serveur n’a pas encore à créer de réservation dans cet atelier.

## 3. Valider la frontière HTTP — 55 min

Traitez la query comme une donnée inconnue. Énumérez les paramètres autorisés, refusez les paramètres supplémentaires ou répétés, puis validez chaque valeur avant de l’utiliser. Une conversion permissive ne suffit pas : page=1.5, page=01, page=-1 et page=bonjour sont tous invalides. Le paramètre category vide est invalide ; son absence signifie toutes les catégories. Aucun client ne doit pouvoir contourner pageSize=24 comme limite haute.

Construisez ensuite recherche, sélection de catégorie et tri stable dans cet ordre : filtrer, compter, trier, paginer. Le total précède la pagination. Normalisez la recherche pour ignorer casse et accents, sans changer les noms affichés. Pour deux prix identiques, départagez par l’ID. Décrivez pourquoi trier seulement la page déjà découpée donnerait un résultat trompeur.

Centralisez les erreurs sous error.code et error.message. Vérifiez une route inconnue et une méthode non autorisée sur une route connue ; différenciez 404 et 405. Pour 405, annoncez Allow. N’exposez pas de chemin local ou de pile technique. Une erreur publique doit expliquer quoi corriger sans prétendre que le serveur n’a jamais de panne.

```bash
curl -i 'http://127.0.0.1:8080/api/products?page=01'
curl -i 'http://127.0.0.1:8080/api/products?pageSize=25'
curl -i 'http://127.0.0.1:8080/api/products?q=introuvable-fictif'
curl -i 'http://127.0.0.1:8080/api/products?page=100'
```

Les deux dernières réponses peuvent être 200 avec une liste vide : ce ne sont pas des erreurs de protocole. Ajoutez un test HTTP ciblé pour chaque frontière, avec une nouvelle instance du magasin par test.

## 4. Construire la page React — 65 min

Créez des composants qui ont chacun une responsabilité observable : structure de page, liste, fiche de produit et message de chargement ou d’erreur. Utilisez de vrais titres, une liste sémantique et des boutons natifs. Un bouton d’ajout peut être reporté à l’atelier suivant ; ne laissez pas de contrôle cliquable sans action utile. Affichez les prix avec Intl.NumberFormat après conversion des centimes, sans modifier la donnée serveur.

Le client API appelle /api via le proxy Vite. Vérifiez response.ok avant de traiter une réponse comme un succès. Le JSON entre sous le type unknown ; contrôlez items, total, page, pageSize et les champs de chaque produit. Exigez des entiers sûrs pour prix et stock. Un simple cast TypeScript ne valide pas les octets reçus. Si la réponse est incohérente, affichez une erreur maîtrisée au lieu d’un montant NaN.

Représentez chargement, succès et erreur avec des variantes cohérentes. Une réussite avec items vide a son propre message. L’effet de lecture dépend de la demande courante et possède un nettoyage ; une réponse qui appartient à un ancien rendu ne doit pas réécrire l’écran. Le traitement détaillé de plusieurs recherches concurrentes sera approfondi dans l’atelier 04.

Branchez « Réessayer » sur une nouvelle lecture explicite. Cette action garde le contexte visible et ne multiplie pas les requêtes à chaque rendu. Utilisez une zone de statut sobre pour annoncer l’attente ou le nombre de résultats ; gardez l’erreur lisible et proche du bouton qui permet d’agir. Vérifiez qu’un zoom à 200 % ne masque ni titre ni prix.

## 5. Vérifier le parcours — 50 min

Rédigez trois tests comportementaux frontend : résultats chargés, erreur suivie d’un réessai réussi, réponse contractuelle invalide. Interrogez l’interface par rôle et nom accessible. Le test doit reconnaître ce que peut faire une personne ; il n’a pas à connaître les noms des variables internes. Ajoutez le cas vide si les trois premiers passent.

Parcourez ensuite la page avec Tab, Maj+Tab et Entrée. Le focus reste visible ; l’ordre doit suivre la lecture. Pour simuler une panne, arrêtez uniquement le serveur de votre exercice puis relancez-le. Contrôlez que Réessayer remet des résultats sans rechargement forcé de tout le navigateur. Gardez une capture de l’erreur et une capture du retour aux produits.

```bash
npm test
npm run build
```

Exécutez ces commandes dans backend/ puis frontend/. Conservez leurs résultats séparément, avec les versions et le commit. Introduisez brièvement une erreur de contrat, par exemple total calculé après pagination, et faites observer quel test échoue. Retirez la régression avant la remise. Un build réussi ne remplace pas une assertion sur le total.

## 6. Faire relire et remettre — 25 min

Faites expliquer à votre binôme le trajet depuis la requête jusqu’au titre d’une fiche. Demandez-lui de reproduire une query invalide et le réessai frontend à partir de vos instructions seules. Corrigez d’abord un manque de preuve ou une erreur visible, avant un détail de présentation.

Renseignez le journal, les sources réellement utilisées et les limites connues. Remettez le code écrit, les tests ciblés et les preuves sans dépendances générées. Le prochain fork importera ce travail : notez donc un commit identifiable. L’extension facultative consiste à préciser un état de catégorie vide, sans développer le panier à la place de terminer la validation actuelle.
