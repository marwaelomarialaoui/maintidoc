# MaintiDoc – assistant documentaire multimodal pour la maintenance textile

Projet intégrateur – module IA générative multimodale, EMSI 2026 (Pr. Mariam Cherrabi).
Équipe : **Marwa Elomari Alaoui**, **Amira Zahr** – dépôt : https://github.com/marwaelomarialaoui/maintidoc

MaintiDoc aide une technicienne de maintenance (machines à coudre, métiers à tisser) à comprendre un défaut ou un voyant à partir d'une question et d'une photo, avec des réponses sourcées (document, page). Il ne pilote aucune machine, ne garantit aucun diagnostic et ne remplace pas un technicien habilité. Tous les documents, équipements, utilisateurs et tickets sont **fictifs**.

## État du projet
| Livrable | Contenu | Statut |
|---|---|---|
| L1 | Cadrage, corpus (43 fichiers), architecture | rendu |
| L2 | Ingestion, indexation texte et images (Qdrant), recherche multimodale, contrôle d'accès | en cours (environnement prêt) |

## Installation (Windows, PowerShell)
Prérequis : Python 3.11, Git, Docker Desktop, Tesseract OCR (avec les données « fra » et « eng »).
```powershell
git clone https://github.com/marwaelomarialaoui/maintidoc.git
cd maintidoc
py -3.11 -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
copy .env.example .env          # puis adapter .env si besoin
docker compose up -d            # démarre Qdrant sur http://localhost:6333
python scripts/check_env.py     # doit afficher « Tout est prêt »
python scripts/verifier_corpus.py corpus   # doit afficher « OK »
```

## Structure
```
maintidoc/
├── README.md, requirements.txt, docker-compose.yml, .env.example, .gitignore
├── config/utilisateurs.yaml     utilisateurs et groupes fictifs
├── corpus/                      43 fichiers + inventaire.csv + prompts_corpus.md
│   ├── documents/famille_1/     machines à coudre (20 PDF)
│   ├── documents/famille_2/     métiers à tisser (20 PDF)
│   └── images/                  3 images synthétiques
├── data/interventions_fictives.csv   historique fictif (futur outil MCP)
├── src/ingestion, indexation, recherche, acces   (livrable 2)
├── scripts/                     check_env.py, verifier_corpus.py, (ingest.py, evaluer_recherche.py à venir)
├── tests/                       tests de contrôle d'accès (à venir)
├── eval/                        questions_test.csv, benchmark_outils.csv (à venir)
└── docs/diagrammes, docs/veille
```

## Corpus (43 fichiers, tous synthétiques)
- 40 PDF paginés (dont **2 PDF scannés** : `12_fiche_securite`, `32_fiche_securite`) et 3 images.
- 2 documents contradictoires (19, 20), 1 document piégé (39), 4 cas ambigus.
- Groupes d'accès : `techniciens_couture`, `techniciens_tissage`, `responsables`.
- Équipements fictifs : S-001, S-002, S-TEST (couture) ; T-001, T-002, T-TEST (tissage).

### Corrections apportées au corpus du livrable 1 (26/11/2026)
- Fichiers `.md` convertis en PDF paginés (citations par page) ; 2 PDF scannés simulés pour l'OCR.
- `inventaire.csv` reconstruit : 20 colonnes, 43 lignes (images incluses).
- 8 images `.jfif` sans source ni licence retirées du corpus.
- Procédures contradictoires distinguées par version (v1, v2) ; identifiants d'équipement ajoutés aux métadonnées.
- Historiques d'interventions enrichis (11 lignes par famille, statuts, document lié) + `data/interventions_fictives.csv`.
- `prompts_corpus.md` renuméroté P01–P48 (voir la note de traçabilité dans le fichier).

## Modèles et outils (à compléter au fil du livrable 2)
| Composant | Outil | Version | Temps d'indexation |
|---|---|---|---|
| Extraction PDF | PyMuPDF | 2.2 | – |
| OCR | à choisir après benchmark (≥ 2 outils) | – | – |
| Embeddings texte | BAAI/bge-m3 | – | – |
| Encodeur texte-image | à choisir après benchmark (≥ 2 modèles) | – | – |
| Base vectorielle | Qdrant (Docker) | à noter | – |
