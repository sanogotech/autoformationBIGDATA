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

## 🔹 **Niveau 1 : Fondamentaux**

### 🎯 Objectif : Acquérir les bases en Linux, Python et Java pour manipuler des outils Big Data.

| ID   | User Story                                                                                                    | Description                                                                     | Livrables               | Outils                  |
| ---- | ------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- | ----------------------- | ----------------------- |
| N1-1 | En tant qu'apprenant, je veux manipuler les commandes Linux de base pour préparer mon environnement Big Data. | Script d'automatisation de setup, manipulation de fichiers, users, droits, SSH. | `linux_basics.sh`       | Bash, Linux             |
| N1-2 | En tant qu’apprenant, je veux écrire un script Python simple pour lire et analyser un fichier CSV.            | Notions de variables, boucles, fonctions, pandas.                               | `python_intro.ipynb`    | Python, Jupyter, pandas |
| N1-3 | En tant qu’apprenant, je veux compiler et exécuter mon premier programme Java.                                | Hello World, gestion de classes, compilation manuelle.                          | `java_hello_world.java` | Java JDK                |

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

