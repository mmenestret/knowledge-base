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
5. Cite les articles utilises avec des wikilinks : `[[fichier]]`.
6. Si la reponse est longue ou structuree (tableau, rapport, comparatif), genere aussi un fichier dans `outputs/pending/` (meme si l'etape 7 s'applique).
7. **Feedback loop** : evalue si ta reponse contient des connexions, syntheses ou insights qui n'existent pas tels quels dans le wiki. Si oui, genere un fichier dans `outputs/pending/` avec le format suivant :
   - Nom : `YYYY-MM-DD-<slug>.md`
   - Frontmatter :
     ```yaml
     ---
     title: Sujet de la reponse
     type: output
     question: "La question posee"
     created: YYYY-MM-DD
     ---
     ```
   - Corps : la reponse telle que formulee.
   - Si la reponse est purement factuelle et n'apporte rien de nouveau par rapport au wiki, ne pas generer de fichier.

## Regles

- Toujours citer les sources wiki utilisees.
- Si l'information n'est pas dans la KB, le dire explicitement — ne pas inventer.
- Ne pas modifier le wiki ni les sources lors d'une question.
