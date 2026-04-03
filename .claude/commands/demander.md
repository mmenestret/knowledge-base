---
name: demander
description: Repond a une question en cherchant dans la knowledge base
---

Repond a une question en cherchant dans le wiki puis dans les sources brutes.

Question : $ARGUMENTS

## Instructions

1. Lis `wiki/_index.md` pour identifier les articles potentiellement pertinents.
2. Lis les articles wiki qui semblent repondre a la question.
3. Si les articles wiki ne suffisent pas, cherche dans `raw/indexed/` avec Grep ou en lisant les fichiers pertinents.
4. Reponds en markdown dans la conversation.
5. Cite les articles utilises avec des liens relatifs : `[Titre](wiki/fichier.md)`.
6. Si la reponse est longue ou structuree (tableau, rapport, comparatif), genere un fichier dans `outputs/` en plus de la reponse conversationnelle.

## Regles

- Toujours citer les sources wiki utilisees.
- Si l'information n'est pas dans la KB, le dire explicitement — ne pas inventer.
- Ne pas modifier le wiki ni les sources lors d'une question.
