---
type: project
created: 2026-11-21
tags: [dbinventory, apex, grants]
related: ["[[_index]]", "[[schema-sous-migrate-sh]]"]
---

# Prérequis : DBMS_CRYPTO et id 110

Voir aussi [[_index]] et [[schema-sous-migrate-sh]].

## EXECUTE ON SYS.DBMS_CRYPTO
Les packages (`pkg_dbinv_application`, `pkg_dbinv_exception`) l'appellent en SQL dynamique :
ils compilent donc sans ce droit, et `T__000` (aucun objet invalide) ne le détecte pas.
L'envoi de fichiers (pages 71 et 85) échoue à l'exécution. Seul un DBA l'accorde ; fait en
DEV et DEMO le 2026-11-20. Sur une base recréée, vérifier ce droit en premier.

## Id 110
L'id 100 d'origine est celui de la Core Library dans la factory. L'application est en 110
en DEV et DEMO (`workspace.yml`). Le `.apx` ne portait aucun id en dur : seuls
`deployments/default.json` et les tests en avaient un.
