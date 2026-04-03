---
name: indexer
description: Fetch une URL et compile le contenu dans le wiki
---

Fetch le contenu d'une URL, le sauve en markdown dans `raw/pending/`, puis lance la compilation.

URL a indexer : $ARGUMENTS

## Instructions

1. Fetch le contenu de l'URL avec WebFetch (prompt: "Extract the full content of this page as clean markdown. Keep all factual content, remove navigation, ads, and boilerplate.").
2. Determine un slug kebab-case a partir du titre de la page.
3. Sauve le contenu en markdown dans `raw/pending/<slug>.md`.
4. Lance la compilation de ce fichier en suivant les instructions de `/compiler` (lis `.claude/commands/compiler.md` et execute le workflow sur le fichier cree).

## Regles

- Si l'URL est inaccessible, signale l'erreur et arrete.
- Le fichier dans `raw/pending/` doit etre du markdown brut — pas de HTML residuel.
- Preserve les images en tant que liens markdown (ne pas telecharger les images en v1).
