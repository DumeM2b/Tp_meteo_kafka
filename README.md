# Projet Individuel - Real Time Data Streaming

## Contexte
Ce projet est réalisé dans le cadre de mes études et vise à mettre en œuvre un pipeline de traitement de données en temps réel. Le but est de collecter, traiter et analyser des données météo issues de l'API OpenWeatherMap, en exploitant les outils Kafka et Spark Streaming pour fournir un système fonctionnel et optimisé.



## Objectifs
1. **Collecte des données** : Intégrer l'API OpenWeatherMap pour récupérer des informations météo en temps réel et les envoyer dans un topic Kafka nommé `topic-weather`.
2. **Traitement en temps réel** : Utiliser Spark Streaming pour transformer les données, enrichir leur contenu, et les publier dans un topic Kafka nommé `topic-weather-final`.
3. **Pipeline opérationnel** : Créer un système robuste et documenté qui assure un fonctionnement fiable de bout en bout.



## Installation et Configuration

### Pré-requis
- **Java JDK 11** : Requis pour exécuter Kafka et Spark.
- **Python 3.10** : Pour les scripts du producteur Kafka et du traitement Spark.
- **Kafka 2.6.0** : Pour la gestion des messages entre les systèmes.
- **Spark 3.2.3** : Pour le traitement des données en streaming.
- **Clé API OpenWeatherMap** : Pour accéder aux données météo.

### Étapes d'installation

#### 1. Configuration de l'environnement
1. Mettre à jour les paquets :
   ```bash
   sudo apt-get update
   ```

2. Installer Java JDK 11 :
   ```bash
   sudo apt-get install openjdk-11-jdk-headless
   java --version
   ```

3. Ajouter Java à la variable d'environnement :
   ```bash
   echo 'export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64' >> ~/.bashrc
   echo 'export PATH=$JAVA_HOME/bin:$PATH' >> ~/.bashrc
   source ~/.bashrc
   ```

#### 2. Installation de Kafka
1. Téléchargez et extrayez Kafka :
   ```bash
   wget https://archive.apache.org/dist/kafka/2.6.0/kafka_2.12-2.6.0.tgz
   tar -xzf kafka_2.12-2.6.0.tgz
   ```

2. Lancez Zookeeper et Kafka :
   ```bash
   ./kafka_2.12-2.6.0/bin/zookeeper-server-start.sh ./kafka_2.12-2.6.0/config/zookeeper.properties
   ./kafka_2.12-2.6.0/bin/kafka-server-start.sh ./kafka_2.12-2.6.0/config/server.properties
   ```

3. Créez les topics nécessaires :
   ```bash
   ./kafka_2.12-2.6.0/bin/kafka-topics.sh --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --topic topic-weather
   ./kafka_2.12-2.6.0/bin/kafka-topics.sh --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --topic topic-weather-final
   ```

#### 3. Installation de Spark
1. Téléchargez et extrayez Spark :
   ```bash
   wget https://archive.apache.org/dist/spark/spark-3.2.3/spark-3.2.3-bin-hadoop2.7.tgz
   tar -xvf spark-3.2.3-bin-hadoop2.7.tgz
   ```

2. Configurez Spark :
   ```bash
   export SPARK_HOME=/workspaces/Tp_meteo_kafka/spark-3.2.3-bin-hadoop2.7
   export PATH=$SPARK_HOME/bin:$PATH
   ```

#### 4. Installation de Python et des dépendances
1. Installez Python 3.10 et les bibliothèques nécessaires :
   ```bash
   sudo apt update
   sudo apt install -y python3.10 python3.10-venv python3.10-distutils
   python3.10 -m pip install kafka-python
   ```



## Exécution du Projet

1. **Lancement du producteur Kafka** : Exécutez le script `producer.py` pour collecter les données météo et les envoyer vers `topic-weather`.
   ```bash
   python3.10 producer.py
   ```

2. **Traitement avec Spark Streaming** : Exécutez le script `spark.py` pour traiter les données et les publier dans `topic-weather-final`.
   ```bash
   $SPARK_HOME/bin/spark-submit --packages org.apache.spark:spark-sql-kafka-0-10_2.12:3.2.3 spark.py
   ```


## Fonctionnalités Clés
- **Collecte en temps réel** : Exploitation de l'API OpenWeatherMap pour des données météo actualisées.
- **Traitement avancé** : Enrichissement des données avec des transformations Spark Streaming.
- **Flexibilité** : Résultats disponibles dans un topic Kafka final, prêt pour des analyses ultérieures.

## Ressources
- [Documentation Kafka](https://kafka.apache.org/documentation/)
- [Documentation Spark Streaming](https://spark.apache.org/docs/latest/streaming-programming-guide.html)
- [API OpenWeatherMap](https://openweathermap.org/api)
