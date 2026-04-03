---
name: compiler
description: Compile les sources pending et les outputs en articles wiki
---

Compile les sources de `raw/pending/` et les outputs de `outputs/pending/` en articles wiki.

Argument optionnel : chemin d'un fichier specifique. Si absent, traite tous les fichiers pending (raw puis outputs).

$ARGUMENTS

## Instructions

1. Lis `AGENTS.md` pour les conventions et le template article.
2. Lis `wiki/_index.md` pour connaitre les articles existants.

### Etape A : Sources brutes (`raw/pending/`)

3. Liste les fichiers dans `raw/pending/` (ou le fichier specifie en argument s'il est dans `raw/`).
4. Pour chaque source :
   a. Lis le contenu de la source.
   b. Identifie les concepts a creer ou enrichir dans le wiki.
   c. Pour chaque concept :
      - Si l'article existe : lis-le, fusionne les nouvelles informations, ajoute la source dans `sources:`, mets a jour `updated:`.
      - Si l'article n'existe pas : cree-le avec le template defini dans AGENTS.md.
   d. Mets a jour la section `## Related` des articles lies (backlinks bidirectionnels).
   e. Mets a jour `wiki/_index.md` (ajout ou mise a jour des entrees, maintenir l'ordre alphabetique).
   f. Deplace la source de `raw/pending/` vers `raw/indexed/`.

### Etape B : Outputs (`outputs/pending/`)

5. Liste les fichiers dans `outputs/pending/` (ou le fichier specifie en argument s'il est dans `outputs/`).
6. Pour chaque output :
   a. Lis le contenu de l'output.
   b. Lis les articles wiki existants qui couvrent le meme sujet.
   c. **Integration legere** : les outputs sont deja synthetises par `/demander`. Si le contenu est pertinent, l'integrer dans les articles wiki sans re-resumer ni re-compresser — le texte a deja ete digere une fois, le re-machonner dilue l'information. Privilegier l'insertion directe des passages pertinents plutot que la re-synthese.
   d. Si de nouveaux concepts emergent : cree un article (sans ajouter l'output dans `sources:` — les outputs ne sont pas des sources primaires).
   e. Mets a jour la section `## Related` des articles lies si de nouvelles connexions sont identifiees.
   f. Mets a jour `wiki/_index.md` si necessaire.
   g. Deplace l'output de `outputs/pending/` vers `outputs/indexed/`.

## Regles

- Synthetiser, jamais copier-coller.
- La granularite (un article par concept vs un article par sujet) est a ta discretion selon la densite.
- Enrichir silencieusement les articles existants — pas de confirmation.
- Toujours tracer les sources brutes dans le front-matter `sources:`.
- Ne jamais tracer les outputs dans `sources:` — ce sont des derives, pas des sources primaires. Cela evite les chaines circulaires.
- Le champ `type` est un de : `concept`, `technique`, `reference`.
- Ne jamais `git add` ou commiter les fichiers personnels (`raw/`, `wiki/`, `outputs/`). Git sert au projet (skills, config, AGENTS.md), pas au contenu de la knowledge base.
