# Pipeline de Données Notion → SQLite → Metabase

Pipeline ETL complète pour extraire des données depuis Notion, les stocker dans SQLite et les visualiser avec Metabase. 100% gratuit et local.

**📺 [Voir le tutoriel YouTube](LIEN_YOUTUBE)**
**📋 [Template Notion à dupliquer](LIEN_NOTION_TEMPLATE)**
**📖 [Documentation API Notion](https://developers.notion.com/)**

---

## 🎯 Ce que tu vas construire

- **Système d'ingestion** : Extraction de données via l'API Notion avec Python
- **Système de stockage** : Base de données SQLite locale
- **Dashboard Metabase** : Visualisation dans un container Docker
- **Automatisation** : Rafraîchissement automatique avec cron jobs

---

## ⚙️ Prérequis

- Python 3.8+
- Docker
- Compte Notion avec accès API
- Git

---

## 🚀 Installation

### 1. Cloner le projet
```bash
git clone https://github.com/TON_USERNAME/notionLearnings.git
cd notionLearnings
```

### 2. Créer l'environnement virtuel
```bash
python3 -m venv venv
source venv/bin/activate  # Sur Windows: venv\Scripts\activate
```

### 3. Installer les dépendances
```bash
pip install -r requirements.txt
```

### 4. Configurer les variables d'environnement
```bash
cp .env.example .env
```

Édite `.env` avec tes identifiants :
- **NOTION_TOKEN** : Crée une intégration sur [Notion Developers](https://www.notion.so/my-integrations)
- **DATA_SOURCE_ID** : ID de ta base de données Notion (voir vidéo YouTube)

---

## 📊 Utilisation

### Extraction manuelle
```bash
python extraction.py
```

Les données sont sauvegardées dans `notion.db`.

### Lancer Metabase avec Docker
```bash
docker run -d -p 3000:3000 \
  -v $(pwd)/notion.db:/metabase-data/notion.db \
  --name metabase \
  metabase/metabase
```

Accède à Metabase : [http://localhost:3000](http://localhost:3000)

**Configuration Metabase :**
1. Créer un compte admin
2. Ajouter une base de données SQLite
3. Chemin : `/metabase-data/notion.db`
4. Créer ton dashboard

---

## 🔄 Automatisation (Cron)

Pour rafraîchir les données automatiquement :

```bash
crontab -e
```

Ajoute cette ligne (exécution toutes les heures) :
```bash
0 * * * * /chemin/vers/notionLearnings/run_extraction.sh
```

Les logs sont dans `cron.log`.

---

## 📁 Structure du projet

```
notionLearnings/
├── extraction.py              # Script ETL principal
├── run_extraction.sh          # Wrapper pour cron
├── requirements.txt           # Dépendances Python
├── .env.example              # Template configuration
├── notion.db                 # Base de données (généré)
├── cron.log                  # Logs d'exécution
└── Notebooks/
    ├── Exploration.ipynb              # Exploration des données
    └── datasourceExploration.ipynb    # Découverte API
```

---

## 🛠️ Schéma des données

La table `learnings` contient :
- `date_started` : Date de début
- `subject` : Sujet (Business, Tech, Musique, etc.)
- `priority` : Priorité (High, Medium, Low)
- `source` : Source (Book, YouTube, Udemy)
- `scope` : Ampleur (Quick Win, Medium, Long, Epic)
- `status` : Statut (In Progress, Completed, Not Started)
- `url` : Lien vers la ressource
- `topic` : Thème général
- `title` : Nom de la ressource

---

## 📝 Notes importantes

⚠️ **Windows/Linux** : Certaines commandes diffèrent. Utilise ChatGPT pour adapter les commandes terminal à ton système.

💡 **Notebooks** : Les fichiers Jupyter dans `Notebooks/` montrent comment explorer l'API Notion et transformer les données.

---

## 🔗 Ressources

- [Documentation Notion API](https://developers.notion.com/)
- [Documentation Metabase](https://www.metabase.com/docs/)
- [Tutoriel vidéo complet](LIEN_YOUTUBE)

---

## 📄 Licence

MIT - Utilise et modifie librement ce projet.
