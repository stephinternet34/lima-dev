# Lima — dev

Ce repo est un **Lima** : l'instance de [lima](https://github.com/stephinternet34/lima) pour le projet **dev**. Il porte le **ledger** du projet (décisions, plan, connaissance, messages entre acteurs) et sa composition de greffons.

## Démarrer

Tout passe d'abord par un **agent LLM** (par exemple Claude Code), ouvert dans ce dossier : il lit `CLAUDE.md`, vous pose quelques questions sur le projet, déclare vos repos de code et propose une composition sur mesure.

Sans agent, suivez le guide `getting-started.md` du catalogue lima (https://github.com/stephinternet34/lima) : composer (§3), relier un repo de code (§4), le cycle d'un travail (§5), la webapp (§7).

## Commandes utiles

```bash
python -m lima status
```
```bash
python -m lima ledger status
```
```bash
python -m lima sync
```

- `lima status` : ce que contient ce Lima (composition, catalogue, ledgers, acteurs, repos).
- `lima ledger …` : la CLI du ledger (`status`, `blockers`, `inbox`, `add`…).
- `lima sync` : récupère le travail des autres, pousse le vôtre, rejoue ce qui a bougé.
- `lima help` : toutes les commandes, dont celles des greffons composés ; `lima web` : la page dans le navigateur.

## Fichiers

| Fichier | Rôle |
|---|---|
| `lima.yaml` | la composition et la version du catalogue épinglée |
| `ledger.yaml` | la configuration de la CLI ledger (greffons désignés par leur nom) |
| `repos.yaml` | les repos de code du projet (alias → URL) |
| `CLAUDE.md` | les consignes de l'agent |

Le ledger vit sur les branches `ledger/actor/<nom>` (une par acteur). Ne jamais les rebaser : leurs hashes sont des ids.
