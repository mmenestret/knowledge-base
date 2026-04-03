# Knowledge Base

Vault Obsidian maintenu par Claude Code. Deposer des sources brutes, le LLM les compile en articles wiki structures.

## Prerequis

- [Claude Code](https://claude.com/claude-code)
- [Obsidian](https://obsidian.md/)

## Installation

```bash
git clone <repo-url>
cd kownledge-base
```

Ouvrir le dossier dans Claude Code :

```bash
claude
```

Les commandes `/compiler`, `/indexer`, `/demander`, `/verifier` sont disponibles immediatement.

## Configuration Obsidian

1. **Ouvrir le coffre** : dans Obsidian, choisir "Open folder as vault" et pointer sur la racine du projet (`kownledge-base/`). Les articles wiki sont dans `wiki/`.

2. **Wikilinks** : laisser le reglage par defaut (`Use [[Wikilinks]]` → ON). C'est le format utilise par le systeme.

3. **Web Clipper** (optionnel) : installer l'extension [Obsidian Web Clipper](https://obsidian.md/clipper) et configurer le dossier de destination sur `raw/pending/`. Ca permet de clipper des pages web directement dans la KB depuis le navigateur.

## Commandes

| Commande | Description |
|----------|-------------|
| `/compiler [fichier]` | Compile les sources dans `raw/pending/` en articles wiki |
| `/indexer <url>` | Fetch une URL, la sauve en source, puis compile |
| `/demander <question>` | Repond en cherchant dans le wiki |
| `/verifier` | Audit de coherence, qualite, et suggestions d'amelioration |

Les commandes fonctionnent aussi en langage naturel (ex: "compile cette source", "c'est quoi le prompt engineering ?").

## Workflow

```
Source brute          →  /compiler  →  Articles wiki
(raw/pending/)                         (wiki/*.md)

URL                   →  /indexer   →  Source + compilation auto

Question              →  /demander  →  Reponse avec citations

Maintenance           →  /verifier  →  Rapport dans outputs/
```
