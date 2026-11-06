# MaintiDoc – Assistant documentaire multimodal pour la maintenance

## Équipe
- Marwa Elomari Alaoui
- Amira Zahr

> Nom d'équipe proposé pour les fichiers : `ALAOUI-ZAHR`. Vérifiez qu'il correspond bien au nom déclaré dans le fichier partagé de Classroom avant de remettre le ZIP.

## Objectif
MaintiDoc est un assistant documentaire multimodal destiné aux techniciens et responsables de maintenance. Le cas d'usage de l'équipe porte sur deux familles d'équipements textiles :
- Machines à coudre industrielles.
- Métiers à tisser.

L'assistant aide à rechercher des informations dans des documents et des images, à produire des réponses avec références, à demander des précisions lorsque les preuves sont insuffisantes et à préparer un brouillon de ticket. La création d'un ticket nécessite une approbation humaine explicite.

L'assistant ne pilote aucune machine, ne garantit aucun diagnostic et ne remplace pas les procédures de sécurité ni un technicien habilité.

## Dépôt GitHub
https://github.com/marwaelomarialaoui/maintidoc

## Structure du dépôt
```text
maintidoc/
├── README.md
├── .gitignore
├── docs/
│   └── diagrammes/
└── corpus/
    ├── inventaire.csv
    ├── prompts_corpus.md
    ├── documents/
    │   ├── famille_1/
    │   └── famille_2/
    └── images/
```

## Contenu du corpus
Le corpus cible comprend 30 à 50 documents. La proposition de travail est de 39 documents :
- 20 documents sur les machines à coudre industrielles (responsable : Amira Zahr).
- 19 documents sur les métiers à tisser (responsable : Marwa Elomari Alaoui).

Le volume et le statut de vérification doivent être confirmés à partir des fichiers réellement présents. Chaque document doit avoir une ligne dans `corpus/inventaire.csv`. Les prompts réellement utilisés doivent être consignés dans `corpus/prompts_corpus.md`.

Exigences à vérifier :
- Au moins 10 documents avec des éléments visuels exploitables.
- Au moins 2 PDF scannés pour tester l'OCR.
- Au moins 2 documents contradictoires, signalés dans l'inventaire.
- Au moins 1 document de test contenant une tentative d'injection de prompt, signalé dans l'inventaire.
- Provenance et licence/conditions de réutilisation vérifiées pour chaque document public. Les documents synthétiques doivent être identifiés comme tels.
- Aucun document non vérifié ne doit être présenté comme validé.

## Rapport
Le rapport du livrable 1 couvre : cadrage, corpus, architecture cible, flux de données et contrôle d'accès, analyse des risques, planning et répartition des rôles.

## Technologies envisagées
L'architecture de référence mentionne notamment FastAPI, LangChain/LangGraph, Qdrant, un modèle vision-langage, PyMuPDF/OCR, PostgreSQL, MinIO et un serveur MCP de démonstration. Les versions et compatibilités restent à confirmer pendant l'implémentation.

## Sécurité et limites
- Les utilisateurs, équipements, historiques et tickets de démonstration sont fictifs.
- Les documents et résultats d'outils sont traités comme des données non fiables, jamais comme des instructions système.
- Les documents sont filtrés selon les groupes d'accès.
- Les citations sont vérifiées avant affichage.
- Aucun ticket n'est créé sans approbation humaine explicite.
- Aucun secret, mot de passe ou fichier `.env` ne doit être ajouté au dépôt.
