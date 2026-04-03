---
name: verifier
description: Audit de coherence (auto-fix), qualite du contenu, et amelioration du systeme
---

Verifie la coherence du wiki, evalue la qualite du contenu, et propose des ameliorations au systeme. Execute les 3 phases dans l'ordre et produit un rapport unique.

## Phase 1 : Coherence (auto-fix)

Applique automatiquement les corrections mecaniques, puis liste ce qui a ete corrige dans le rapport.

1. Lis tous les fichiers `wiki/*.md` et `wiki/_index.md`.
2. **Liens casses** : pour chaque wikilink (`[[fichier]]`) dans le corps ou `## Related`, verifie que le fichier cible existe dans `wiki/`. Si non : retire le lien et note la correction.
3. **Sources manquantes** : pour chaque chemin dans `sources:` du front-matter, verifie que le fichier existe dans `raw/indexed/`. Si non : signale dans le rapport (pas de fix possible).
4. **Backlinks manquants** : si A reference B dans `## Related`, ouvre B et verifie que B reference A. Si non : ajoute le backlink dans B.
5. **Index desynchronise** :
   - Fichiers `wiki/*.md` (sauf `_index.md`) absents de `_index.md` → ajoute l'entree (titre depuis front-matter, resume one-liner genere).
   - Entrees dans `_index.md` sans fichier correspondant → retire l'entree.
   - Maintiens l'ordre alphabetique.
6. **Articles orphelins** : articles qui ne sont references par aucun autre article (ni `## Related`, ni corps). Signale dans le rapport.
7. Commit les corrections avec le message : `fix: verifier auto-fix coherence`.

## Phase 2 : Qualite du contenu (suggestions)

Pas d'auto-fix. Analyse chaque article et signale dans le rapport :

1. **Articles pauvres** : pour chaque article, lis les sources listees dans `sources:` (dans `raw/indexed/`). Si l'article est significativement plus court ou superficiel que ses sources, signale-le avec la comparaison (nb lignes article vs nb lignes sources).
2. **Granularite suspecte** :
   - Article couvrant 3+ concepts distincts → candidat au split.
   - Plusieurs articles de moins de 5 lignes de contenu sur des sujets proches → candidats a la fusion.
3. **Connexions manquantes** : articles partageant des tags identiques ou des concepts communs dans le corps mais non lies dans `## Related`.
4. **Tags incoherents** :
   - Tags utilises une seule fois dans tout le wiki → signaler (possible typo ou tag trop specifique).
   - Articles sans tags → signaler.

## Phase 3 : Amelioration du systeme (suggestions)

Examine les patterns dans les problemes detectes en phases 1 et 2, et dans l'historique git recent (`git log --oneline -20`). Propose des ameliorations concretes :

1. Pour chaque type de probleme recurrent (ex: backlinks manquants dans 50%+ des articles), propose une modification precise du fichier responsable.
2. Chaque suggestion doit contenir :
   - Le fichier cible (`AGENTS.md`, `compiler.md`, etc.)
   - Le probleme observe (avec chiffres)
   - Le changement propose (texte exact a ajouter/modifier)
3. Types de suggestions possibles :
   - Instruction manquante ou trop vague dans un skill → proposition de reformulation.
   - Convention absente dans AGENTS.md → proposition d'ajout.
   - Pattern d'erreur recurrent malgre une regle existante → proposition de renforcement.

## Generation du rapport

Genere `outputs/lint-YYYY-MM-DD.md` avec ce format exact :

~~~markdown
# Lint — YYYY-MM-DD

## Corrections appliquees

- [x] Description de chaque correction automatique
- (ou "Aucune correction necessaire." si tout est propre)

## Qualite du contenu

- [ ] `fichier.md` — Description du probleme
- (ou "Aucun probleme detecte." si tout est bon)

## Ameliorations systeme

- [ ] `fichier-cible.md` — Probleme observe. Suggestion : changement propose.
- (ou "Aucune amelioration suggeree." si tout est bon)
~~~

## Regles

- Phase 1 modifie les fichiers wiki et commit. Phases 2 et 3 sont en lecture seule.
- Ne jamais modifier les fichiers dans `raw/`.
- Ne jamais modifier AGENTS.md ou les skills automatiquement — seulement suggerer.
- Ne pas detecter d'incoherences factuelles entre articles.
