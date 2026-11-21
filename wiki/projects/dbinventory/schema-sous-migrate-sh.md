---
type: project
created: 2026-11-21
tags: [dbinventory, migrate, oracle]
related: ["[[_index]]", "[[prerequis-application-110]]"]
---

# Importer un schéma sous migrate.sh

Voir aussi [[_index]] et [[prerequis-application-110]].

## Code en R__, tables en V__
Why : un `V__` ne se modifie plus une fois appliqué (checksum refusé), alors qu'un package
corrigé dans un `R__` se rejoue. Les vues, packages et triggers sont donc en `R__`, un objet
par fichier, listés dans `R__order.txt` dans l'ordre des dépendances.
Ce découpage n'était permis que parce que rien n'avait encore été appliqué nulle part :
sur un schéma déjà migré, on n'aurait pas pu réécrire les anciens `V__`.

Piège : un `comment on table` visant une vue doit suivre la vue dans son `R__`. Dans un
`V__` il échoue, la vue n'existant qu'après le rejeu des `R__`.

## T__ : indépendants des données
DEV ne reçoit jamais les fixtures et `migrate.sh` lance les `T__` sur un schéma vide : ils
ne doivent rien supposer des données. Les contrôles qui ont besoin du jeu de démonstration
sont dans `fixtures/checks/`, à lancer en DEMO après `fixtures/load_fixtures.sh`.

Piège : `migrate.sh` ne prend que `T__*.sql` (deux tirets bas). Un `T_001` est ignoré
sans aucun avertissement ; c'est pourquoi `fixtures/checks/` garde ce nom à un tiret bas,
hors du périmètre de `migrate.sh`.
