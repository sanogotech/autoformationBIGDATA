# Les **cas pratiques Big Data**

 Les **cas pratiques Big Data**, classés par niveau (1 à 6), avec **user stories**, **objectifs pédagogiques**, **livrables**, et **technos/outils utilisés**. Ce backlog peut servir de base pour un projet de formation, un bootcamp, ou une autoformation intensive.



### 📦 Contenu détaillé :

| Niveau      | Dossier                      | Fichiers inclus                                                   |
| ----------- | ---------------------------- | ----------------------------------------------------------------- |
| Niveau 1    | `niveau_1_fondamentaux/`     | `linux_basics.sh`, `python_intro.ipynb`, `java_hello_world.java`  |
| Niveau 1bis | `niveau_1bis_bi_end_to_end/` | `etl_process.sql`, `powerbi_dashboard.pbix`, `airflow_dag_etl.py` |
| Niveau 2    | `niveau_2_architecture/`     | `mapreduce_wordcount.py`, `hdfs_io.py`                            |
| Niveau 3    | `niveau_3_streaming/`        | `kafka_producer.py`, `spark_streaming_twitter.py`                 |
| Niveau 4    | `niveau_4_visualisation/`    | `hive_query.sql`, `superset_dashboard_setup.md`                   |
| Niveau 5    | `niveau_5_ml/`               | `spark_mllib_churn_prediction.py`, `mlflow_tracking_demo.py`      |
| Niveau 6    | `niveau_6_devops/`           | `docker_compose_spark.yml`, `grafana_dashboard.json`              |



---

## 🔹 **Niveau 0 : Fondamentaux**

### 🎯 Objectif : Acquérir les bases en Linux, Python et Java pour manipuler des outils Big Data.

| ID   | User Story                                                                                                    | Description                                                                     | Livrables               | Outils                  |
| ---- | ------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- | ----------------------- | ----------------------- |
| N1-1 | En tant qu'apprenant, je veux manipuler les commandes Linux de base pour préparer mon environnement Big Data. | Script d'automatisation de setup, manipulation de fichiers, users, droits, SSH. | `linux_basics.sh`       | Bash, Linux             |
| N1-2 | En tant qu’apprenant, je veux écrire un script Python simple pour lire et analyser un fichier CSV.            | Notions de variables, boucles, fonctions, pandas.                               | `python_intro.ipynb`    | Python, Jupyter, pandas |
| N1-3 | En tant qu’apprenant, je veux compiler et exécuter mon premier programme Java.                                | Hello World, gestion de classes, compilation manuelle.                          | `java_hello_world.java` | Java JDK                |


-----------
Voici une **extension complète du Niveau 1 : Fondamentaux des Données** à intégrer dans la **feuille de route Big Data** sous forme de **backlog détaillé**, avec **compétences à acquérir**, **ressources**, **cas pratiques** et **user stories**. Ce niveau est conçu pour durer **3 à 4 semaines**, idéal pour bâtir une base solide avant d’aborder l’architecture Big Data.

---

## 🔹 **Niveau 1 – Fondamentaux des données (3–4 semaines)**

🎯 **Objectif global** : Comprendre les structures de données, les formats, les bases relationnelles et NoSQL, ainsi que les modèles de données.

---

### 🗄️ **1. Bases de données relationnelles (SQL)**

#### ✅ Compétences à acquérir :

* Maîtriser les requêtes SQL de base : `SELECT`, `INSERT`, `UPDATE`, `DELETE`
* Effectuer des **jointures**, des **agrégations**, des **sous-requêtes**
* Appliquer les **principes de normalisation**

#### 📚 Ressources recommandées :

* [SQLZoo](https://sqlzoo.net/)
* [W3Schools SQL Tutorial](https://www.w3schools.com/sql/)

#### 🧪 Cas pratique :

**Créer une base de données pour une boutique en ligne**

* Tables : Clients, Produits, Commandes
* Ajouter des données fictives
* Requêtes : ventes mensuelles, top produits, clients inactifs, panier moyen

#### 🧾 User Stories :

| ID       | User Story                                                                                                      | Livrables                           | Outils              |
| -------- | --------------------------------------------------------------------------------------------------------------- | ----------------------------------- | ------------------- |
| N1-SQL-1 | En tant qu'utilisateur, je veux interroger les ventes mensuelles pour suivre l’évolution du chiffre d’affaires. | `boutique.sql`, rapport de requêtes | SQLite / PostgreSQL |
| N1-SQL-2 | En tant qu’analyste, je veux trouver les produits les plus vendus par catégorie.                                | `requetes_top_ventes.sql`           | SQL                 |
| N1-SQL-3 | En tant qu’admin, je veux structurer ma base selon la 3NF.                                                      | `schema_normalise.pdf`              | dbdiagram.io        |

---

### 🗃️ **2. Bases de données NoSQL**

#### ✅ Compétences à acquérir :

* Différences entre relationnel et NoSQL
* Manipulation de documents **JSON** avec **MongoDB**
* Introduction au stockage en mémoire avec **Redis**

#### 📚 Ressources recommandées :

* [MongoDB University](https://university.mongodb.com/)
* [Redis Tutorials](https://redis.io/docs/)

#### 🧪 Cas pratique :

**Implémenter un catalogue de produits NoSQL et un système de cache**

* Base MongoDB : Produits (nom, prix, stock, catégories)
* Ajout de recherche filtrée
* Mise en cache des produits populaires avec Redis

#### 🧾 User Stories :

| ID         | User Story                                                                                      | Livrables                  | Outils        |
| ---------- | ----------------------------------------------------------------------------------------------- | -------------------------- | ------------- |
| N1-NOSQL-1 | En tant que développeur, je veux stocker mes produits dans une collection MongoDB.              | `mongo_insert_products.js` | MongoDB       |
| N1-NOSQL-2 | En tant qu’analyste, je veux rechercher les produits disponibles dans une catégorie spécifique. | `mongo_query_products.js`  | MongoDB       |
| N1-NOSQL-3 | En tant que devOps, je veux mettre en cache les produits populaires avec Redis.                 | `redis_cache.py`           | Redis, Python |

---

### 📄 **3. Formats de données (CSV, JSON, Parquet, Avro)**

#### ✅ Compétences à acquérir :

* Comprendre les différences : **CSV (simple)**, **JSON (hiérarchique)**, **Avro/Parquet (optimisés Big Data)**
* Convertir les formats en Python

#### 📚 Ressources recommandées :

* [DataFlair – Big Data File Formats](https://data-flair.training/blogs/file-formats-in-hadoop/)

#### 🧪 Cas pratique :

**Convertir un fichier CSV des ventes en format Parquet et Avro**

* Lecture/écriture avec pandas, pyarrow, fastavro
* Comparaison de la taille et de la vitesse de lecture

#### 🧾 User Stories :

| ID          | User Story                                                                                                | Livrables              | Outils               |
| ----------- | --------------------------------------------------------------------------------------------------------- | ---------------------- | -------------------- |
| N1-FORMAT-1 | En tant que data engineer, je veux convertir mes fichiers CSV en Parquet pour l’optimisation du stockage. | `csv_to_parquet.py`    | Python, pyarrow      |
| N1-FORMAT-2 | En tant que développeur, je veux comparer la taille de fichiers JSON et Avro.                             | `format_comparator.py` | fastavro, JSON, Avro |

---

### 🧠 **4. Modélisation de données**

#### ✅ Compétences à acquérir :

* Créer des **modèles conceptuels**, **logiques** et **physiques**
* Utiliser des outils de modélisation : **dbdiagram.io**, **Lucidchart**
* Notions d’**entrepôt de données** et schéma en **étoile** et **flocon**

#### 📚 Ressources recommandées :

* [dbdiagram.io](https://dbdiagram.io/)
* [Lucidchart](https://www.lucidchart.com/pages/)

#### 🧪 Cas pratique :

**Modéliser un entrepôt de données pour une entreprise e-commerce**

* Faits : Commandes
* Dimensions : Clients, Produits, Dates
* Modèle étoile vs flocon

#### 🧾 User Stories :

| ID         | User Story                                                                                            | Livrables               | Outils       |
| ---------- | ----------------------------------------------------------------------------------------------------- | ----------------------- | ------------ |
| N1-MODEL-1 | En tant qu’analyste, je veux modéliser un entrepôt de données e-commerce avec des dimensions claires. | `modele_entrepot.png`   | dbdiagram.io |
| N1-MODEL-2 | En tant que concepteur, je veux comparer les modèles en étoile et en flocon.                          | `comparatif_modeles.md` | Lucidchart   |

---

## 📁 Contenu à ajouter dans le pack `.zip` :

| Dossier                  | Fichiers suggérés                                                 |
| ------------------------ | ----------------------------------------------------------------- |
| `niveau_1_sql/`          | `boutique.sql`, `requetes_top_ventes.sql`, `schema_normalise.pdf` |
| `niveau_1_nosql/`        | `mongo_insert_products.js`, `redis_cache.py`                      |
| `niveau_1_formats/`      | `csv_to_parquet.py`, `format_comparator.py`                       |
| `niveau_1_modelisation/` | `modele_entrepot.png`, `comparatif_modeles.md`                    |



---

## 🔹 **Niveau 1bis : BI end-to-end**

### 🎯 Objectif : Créer une chaîne de Business Intelligence complète (ETL + visualisation).

| ID    | User Story                                                                                        | Description                                  | Livrables                | Outils                  |
| ----- | ------------------------------------------------------------------------------------------------- | -------------------------------------------- | ------------------------ | ----------------------- |
| N1B-1 | En tant qu’analyste, je veux construire un script SQL d’ETL pour transformer des données clients. | Nettoyage, transformation, agrégation.       | `etl_process.sql`        | SQL (PostgreSQL, MySQL) |
| N1B-2 | En tant qu’analyste, je veux créer un dashboard Power BI à partir des données nettoyées.          | KPI, graphiques dynamiques, filtres.         | `powerbi_dashboard.pbix` | Power BI                |
| N1B-3 | En tant qu’admin data, je veux automatiser l’ETL avec Airflow.                                    | Création d’un DAG d’orchestration quotidien. | `airflow_dag_etl.py`     | Apache Airflow          |

---

## 🔹 **Niveau 2 : Architecture Big Data**

### 🎯 Objectif : Comprendre les composants et pipelines de traitement Big Data.

| ID   | User Story                                                                                   | Description                         | Livrables                | Outils         |
| ---- | -------------------------------------------------------------------------------------------- | ----------------------------------- | ------------------------ | -------------- |
| N2-1 | En tant qu’apprenant, je veux développer un MapReduce pour compter les mots dans un fichier. | Logique de map, reduce, test local. | `mapreduce_wordcount.py` | Python, Hadoop |
| N2-2 | En tant que développeur, je veux lire et écrire des fichiers dans HDFS.                      | Opérations HDFS API et CLI.         | `hdfs_io.py`             | Hadoop HDFS    |

---

## 🔹 **Niveau 3 : Streaming & Temps Réel**

### 🎯 Objectif : Collecter, traiter et analyser des données en temps réel.

| ID   | User Story                                                                                     | Description                            | Livrables                    | Outils                    |
| ---- | ---------------------------------------------------------------------------------------------- | -------------------------------------- | ---------------------------- | ------------------------- |
| N3-1 | En tant que développeur, je veux produire des messages Kafka à partir d’une source de données. | Simulation de logs ou événements JSON. | `kafka_producer.py`          | Apache Kafka              |
| N3-2 | En tant que data engineer, je veux consommer ces données avec Spark Streaming.                 | Traitement temps réel avec analyse.    | `spark_streaming_twitter.py` | Apache Spark, Twitter API |

---

## 🔹 **Niveau 4 : Stockage, Requêtage, Visualisation**

### 🎯 Objectif : Stocker, interroger et visualiser efficacement les données.

| ID   | User Story                                                                   | Description                           | Livrables                     | Outils          |
| ---- | ---------------------------------------------------------------------------- | ------------------------------------- | ----------------------------- | --------------- |
| N4-1 | En tant que data analyst, je veux écrire des requêtes Hive sur un data lake. | Table EXTERNAL, GROUP BY, JOINs.      | `hive_query.sql`              | Apache Hive     |
| N4-2 | En tant qu’utilisateur métier, je veux visualiser les KPIs via Superset.     | Création de dashboards, KPI, graphes. | `superset_dashboard_setup.md` | Apache Superset |

---

## 🔹 **Niveau 5 : Machine Learning sur Big Data**

### 🎯 Objectif : Appliquer du Machine Learning distribué avec Spark et suivre les modèles.

| ID   | User Story                                                                        | Description                                    | Livrables                         | Outils        |
| ---- | --------------------------------------------------------------------------------- | ---------------------------------------------- | --------------------------------- | ------------- |
| N5-1 | En tant que data scientist, je veux prédire les départs clients avec Spark MLlib. | Pipeline ML avec features, modèle, évaluation. | `spark_mllib_churn_prediction.py` | Spark MLlib   |
| N5-2 | En tant que MLOps, je veux tracer les expériences ML avec MLFlow.                 | Tracking des modèles, metrics, versionning.    | `mlflow_tracking_demo.py`         | MLFlow, Spark |

---

## 🔹 **Niveau 6 : DevOps & Sécurité**

### 🎯 Objectif : Déployer, monitorer et sécuriser une architecture Big Data.

| ID   | User Story                                                                      | Description                           | Livrables                  | Outils              |
| ---- | ------------------------------------------------------------------------------- | ------------------------------------- | -------------------------- | ------------------- |
| N6-1 | En tant qu’admin, je veux déployer un cluster Spark local avec Docker Compose.  | Services Spark, Master/Worker.        | `docker_compose_spark.yml` | Docker Compose      |
| N6-2 | En tant qu’ops, je veux créer un dashboard Grafana pour surveiller Kafka/Spark. | Intégration avec Prometheus, metrics. | `grafana_dashboard.json`   | Grafana, Prometheus |

---

## 📚 Ressources pour accompagner chaque niveau :

* **Docs officielles** : Apache (Kafka, Spark, Hive, Airflow), Docker, Superset.
* **Cours** : Data Engineering on GCP (Coursera), Datacamp - Big Data Fundamentals.
* **Livres** :

  * *Designing Data-Intensive Applications* – Martin Kleppmann
  * *Streaming Systems* – Tyler Akidau

---

