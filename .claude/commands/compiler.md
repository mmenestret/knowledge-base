---
name: compiler
description: Compile les sources pending en articles wiki
---

Compile les sources de `raw/pending/` en articles wiki.

Argument optionnel : chemin d'un fichier specifique dans `raw/pending/`. Si absent, traite tous les fichiers pending.

$ARGUMENTS

## Instructions

1. Lis `AGENTS.md` pour les conventions et le template article.
2. Liste les fichiers dans `raw/pending/` (ou le fichier specifie en argument).
3. Lis `wiki/_index.md` pour connaitre les articles existants.
4. Pour chaque source :
   a. Lis le contenu de la source.
   b. Identifie les concepts a creer ou enrichir dans le wiki.
   c. Pour chaque concept :
      - Si l'article existe : lis-le, fusionne les nouvelles informations, ajoute la source dans `sources:`, mets a jour `updated:`.
      - Si l'article n'existe pas : cree-le avec le template defini dans AGENTS.md.
   d. Mets a jour la section `## Related` des articles lies (backlinks bidirectionnels).
   e. Mets a jour `wiki/_index.md` (ajout ou mise a jour des entrees, maintenir l'ordre alphabetique).
   f. Deplace la source de `raw/pending/` vers `raw/indexed/` avec `git mv`.
5. Commit git avec un message descriptif listant les articles crees/modifies.

## Regles

- Synthetiser, jamais copier-coller.
- La granularite (un article par concept vs un article par sujet) est a ta discretion selon la densite.
- Enrichir silencieusement les articles existants — pas de confirmation.
- Toujours tracer les sources dans le front-matter.
- Le champ `type` est un de : `concept`, `technique`, `reference`.
