# Knowledge Base — LLM Contract

Ne jamais modifier le contenu d'un fichier dans `raw/`. Seulement deplacer de `pending/` vers `indexed/`.

## Commandes

- `/wiki:compiler [fichier]` — Compile les sources pending et les outputs en articles wiki. Sans argument, traite `raw/pending/` puis `outputs/pending/`.
- `/wiki:indexer <url>` — Fetch une URL, sauve en markdown dans `raw/pending/`, puis compile.
- `/wiki:demander <question>` — Repond en cherchant dans le wiki puis dans les sources. Genere un output dans `outputs/pending/` si la reponse enrichit le wiki.
- `/wiki:verifier` — Audit de coherence : liens, orphelins, index. Rapport dans `outputs/`.

## Template article wiki

~~~yaml
---
title: Nom du concept
type: concept | technique | reference
sources:
  - "[[source]]"
tags:
  - tag1
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

Contenu synthetise par le LLM. Jamais de copier-coller.

## Related

- [[concept-lie]]
~~~

## Format `_index.md`

Liste plate alphabetique. Une entree par article :

```
- [[fichier]] — Resume one-liner
```

## Conventions

- Noms de fichiers : kebab-case (`prompt-engineering.md`)
- Liens : wikilinks (`[[fichier]]`) — format natif Obsidian
- Tags : lowercase, pluriel (`agents`, `embeddings`)
- Dates : `YYYY-MM-DD`
- Structure plate dans `wiki/` (pas de sous-dossiers sauf `_attachments/`)

## Principes de compilation

- Synthetiser les sources, jamais copier-coller
- Granularite a la discretion du LLM (split ou regroup selon la densite d'information)
- Enrichir silencieusement les articles existants (fusion sans demander confirmation)
- Toujours tracer les sources dans le front-matter `sources:`
- Mettre a jour les backlinks `## Related` dans les articles lies
- Mettre a jour `wiki/_index.md` apres chaque compilation

## Outputs et feedback loop

Le wiki s'enrichit via deux canaux :

- **Sources brutes** (`raw/pending/` → `raw/indexed/`) : information externe, synthese complete, tracee dans `sources:`.
- **Outputs** (`outputs/pending/` → `outputs/indexed/`) : reponses generees par `/wiki:demander`, extraction selective uniquement, jamais traces dans `sources:`.

### Frontmatter des outputs

~~~yaml
---
title: Sujet de la reponse
type: output
question: "La question posee"
created: YYYY-MM-DD
---
~~~

### Regle de non-tracabilite

Les outputs ne sont pas des sources primaires. Ne jamais les ajouter dans le champ `sources:` des articles wiki. Cela evite la dilution par re-synthese circulaire.
