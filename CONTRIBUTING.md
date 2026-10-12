# Travailler et remettre — atelier 01

Développer dans ce fork, à partir de vos acquis identifiés. Conserver les tutoriels et compléter travail/ au fur et à mesure. Le code métier n’est pas fourni prêt à exécuter. Les commandes npm indiquées dans le tutoriel supposent que vos manifests et scripts existent.

## Organisation attendue

- backend/ : TypeScript Node/Express, domaine, HTTP et tests.
- frontend/ : React/TypeScript, client API, composants et tests.
- scripts/ : outils de contrôle que vous avez écrits, à partir de l’atelier qualité si nécessaire.
- travail/ : journal, preuves référencées et documents de décision.

## Commits et revue

Faire des commits lisibles qui expliquent l’intention du changement. Avant remise, examiner git status, exclure node_modules, dist, caches, secrets et fichiers temporaires. Les manifests, lockfiles, sources et configurations utiles restent versionnés. Utiliser [le modèle de revue](.github/PULL_REQUEST_TEMPLATE.md), puis consigner une remarque réelle et son traitement. La configuration .gitlab-ci.yml se construit pendant l’atelier 05 ; le lieu de distribution GitHub ne vaut pas exécution GitLab.

## Remise

Fournir le commit final, le journal, les réponses, les résultats de tests/build réellement exécutés et les captures ou rapports utiles. Ne pas cocher les tâches à partir du seul code présent. Garder les mesures et rapports volumineux dans les artefacts prévus par le formateur et les référencer. Préparer ensuite le transfert vers le prochain fork avant sa séance, selon [Day 0](DAY0.md).

La version est une simulation locale documentée. Les extensions de production sont discutées comme suites possibles, pas annoncées comme déjà construites.
