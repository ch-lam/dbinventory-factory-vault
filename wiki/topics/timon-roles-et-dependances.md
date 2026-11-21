---
type: topic
created: 2026-11-21
tags: [timon, kanban, roles]
related: ["[[_index]]", "[[schema-sous-migrate-sh]]"]
---

# Timon : rôle chore et dépendances de tâches

Exemple de projet : [[_index]] ; méthode de recette liée : [[schema-sous-migrate-sh]].

- Une tâche `chore` confiée à un agent qui tient déjà un autre rôle part chez le titulaire
  du rôle `chore` ; si personne ne le tient, Timon crée un agent `<projet>.ops`.
  Why : éviter cet agent surprise en assignant le rôle `chore` explicitement (ici au merger).
- Une tâche qui doit voir un correctif dépend de la tâche `merge`, pas seulement de la
  tâche `code` : sinon elle part avant l'intégration.
