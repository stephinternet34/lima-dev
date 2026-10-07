# Lima — dev : consignes pour l'agent

Ce repo est un **Lima** (instance de lima) pour le projet **dev**. Il porte le ledger du projet. Tu es l'agent qui guide son **onboarding**, puis qui y travaille.

## Onboarding (à la première session)

1. **Présente-toi**, puis interroge l'humain, une question à la fois : l'historique du projet, ce que l'équipe fait (développement, spec, recherche…), où se trouvent les repos de code (un dossier racine, ou chaque repo).
2. **Déclare les repos** : `python -m lima repo add <alias> <url> --path <chemin local>` (alias en kebab-case).
3. **Propose une composition sur mesure**, à partir du socle (`ledger0`, `storage-git`, `actor`, `inbox`, `decision`), selon la taille de l'équipe :
   - développement léger (corrections, petit projet) : `workflow::work` ;
   - moyen (besoins utilisateurs, tests) : `workflow::work`, `workflow::story`, `workflow::verification` ;
   - lourd (produit, ensembles fonctionnels) : les précédents et `workflow::feature` ;
   - hors développement : `workflow::plan` (goals, tâches) ; `workflow::idea` pour suivre des réflexions ; `workflow::autonomy` si des agents travaillent seuls ;
   - pour tous : `view::webapp` (la page dans le navigateur : `python -m lima web`).

   Explique chaque proposition, attends l'accord, puis `python -m lima compose add <greffon>`. `python -m lima help` liste ensuite les commandes que la composition apporte.
4. **Consigne chaque choix** dans le ledger (`python -m lima ledger add`), avec le workflow decision : `Question —`, `Option —`, `Chosen —`.
5. **Enregistre-toi** comme acteur : `python -m lima ledger actor add <ton-nom> --nature llm --model <modèle>`.

## Le cycle d'un travail (avec `workflow::work`)

`python -m lima work add "…" --repo <alias>`, puis `python -m lima work start <id>` (branche de code créée), notes en cours de route **depuis le repo de code** (`python -m lima ledger add …`), push et pull request, puis `python -m lima sync` : au merge, le travail est clos. Guide complet : `getting-started.md` du catalogue lima.

## Règles de travail

- **Signe tes écritures** avec ton nom d'acteur : `LEDGER_ACTOR=<ton-nom>`. Sans cela, elles seraient signées au nom de l'humain.
- **Décisions de conception** : propose des options et une recommandation, puis attends l'accord de l'humain avant d'écrire le `Chosen —`.
- **Consigne dans le ledger** les faits, décisions, problèmes et pièges importants, reliés à ce qu'ils touchent.
- **Synchronise** régulièrement : `python -m lima sync`.
- Ne jamais rebaser une branche `ledger/*` (les hashes sont des ids).
