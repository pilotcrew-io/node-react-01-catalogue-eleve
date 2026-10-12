# Day 0 — Préparer le cursus Node.js / React

**À réaliser avant la première séance ; ces préparatifs ne sont pas compris dans les six séances de 4 h 30.** Le cursus représente 27 heures d’ateliers. Il s’adresse à une personne qui sait déjà écrire des fonctions JavaScript, lire du JSON, utiliser promises/async-await, construire une page HTML/CSS simple et effectuer un commit Git. Il développe une pratique vérifiable ; il ne remplace pas les sept années ou plus d’expérience visées par l’offre d’inspiration.

## 1. Vérifier les acquis et les outils

Prévoir un poste sur lequel vous pouvez installer des dépendances, un éditeur, Git, deux terminaux et un navigateur Chromium récent avec outils de développement. Employer Node.js 22 **au moins 22.12**, ainsi qu’une version npm compatible ; consigner les versions exactes. La référence pédagogique verrouille ses dépendances dans package-lock.json. Les versions choisies pour l’enseignement ne sont pas annoncées comme des exigences de l’offre.

```bash
node --version
npm --version
git --version
```

Expliquez sans assistance la différence entre un tableau et une promesse de tableau ; écrivez une fonction qui refuse une quantité non entière ; retrouvez un bouton par son nom dans une page. Si ces points bloquent, prévoir une mise à niveau avant l’atelier. Télécharger avant la séance les dépendances du socle technique validé par le formateur et le navigateur de test Playwright. Une création initiale de projet n’a pas encore de lockfile : npm install le crée ; npm ci sert ensuite à restaurer un lockfile existant et cohérent.

## 2. Préparer son premier espace de travail

Ouvrir le dépôt élève réellement lié dans PilotCrew, créer son fork personnel puis le cloner. Le dépôt contient les tutoriels, mémos et espaces à compléter. Il ne contient ni solution finale, ni application métier terminée. Préparer uniquement les squelettes techniques backend/ et frontend/, avec leurs manifests, configurations et lockfiles, lors du Day 0. Les routes, composants, transitions et tests métier seront construits pendant les séances. Les commandes npm test et npm run build ne sont utilisables qu’après avoir défini leurs scripts.

Le backend utilisera TypeScript et Express 5, avec compilation avant exécution. Le frontend utilisera React, TypeScript et Vite. Enregistrer les versions exactes du socle validé par le formateur ; éviter toute mise à jour opportuniste le matin de l’atelier. Le contrat local est /api sur 127.0.0.1:8080, proxifié par Vite depuis 127.0.0.1:5173. Vérifier que ces ports sont libres. Garder les services liés à l’interface de boucle locale.

## 3. Reprendre les acquis avant les séances 02 à 06

Chaque séance possède **un nouveau dépôt élève et un nouveau fork**. Avant l’horloge de 4 h 30, enregistrer le commit du travail précédent, cloner le nouveau fork, puis copier uniquement ses propres backend/, frontend/, scripts/ et configurations utiles. Copier aussi les package-lock.json et la configuration CI déjà construite. Ne pas copier l’ancien .git, node_modules, dist, rapports de test, fichiers temporaires, secrets, ni les anciens tutoriels : les documents du nouveau dépôt font autorité pour la nouvelle séance. Ne pas écraser le README ou le journal du nouveau module.

Dans le nouveau journal, noter le dépôt et le commit d’origine ainsi que les répertoires importés. Relancer npm ci, npm test et npm run build dans chacun des projets construits. Faire un commit de reprise distinct. Un échec de transfert se résout avant le début de l’atelier. Si le formateur fournit un acquis de rattrapage, le mentionner explicitement : l’évaluation distinguera ce point de départ du code que vous avez produit.

## 4. Préparer la qualité et la mesure

Avant l’atelier 04, apprendre à enregistrer une trace Performance dans le navigateur, choisir le même profil réseau/CPU pour les comparaisons et vérifier que les outils fonctionnent hors de tout compte analytique. Avant l’atelier 05, installer le navigateur Playwright depuis le package du projet, et préparer un runner GitLab si une exécution distante est prévue. Le socle peut être distribué sur GitHub : les concepts et le fichier .gitlab-ci.yml seront réellement ceux de GitLab CI. Une exécution GitHub ne devient pas une pipeline GitLab.

Une pipeline distante nécessite un projet GitLab et un runner accessibles au participant. Si ce prérequis manque, le préciser avant la séance : la production locale des commandes et la revue de configuration restent possibles, mais le critère « pipeline GitLab distante exécutée » demeure non validé. Aucun succès ne doit être déduit d’un simple fichier YAML ou d’un lint.

## 5. Préparer les preuves sans données réelles

Utiliser uniquement les trente produits inventés. Aucune adresse, aucun nom de client, aucun moyen de paiement et aucun secret de service ne sont nécessaires. Les preuves montreront le commit, la commande, l’environnement, le résultat réel et son interprétation. Les journaux sont des espaces à compléter, pas des attestations préremplies. Un test absent, bloqué ou non exécuté est signalé comme tel.

Sources : [Vite](https://vite.dev/guide/), [npm ci](https://docs.npmjs.com/cli/v11/commands/npm-ci/), [Playwright CI](https://playwright.dev/docs/ci), [GitLab CI](https://docs.gitlab.com/ci/yaml/).
