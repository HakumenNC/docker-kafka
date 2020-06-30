# docker-kafka
Run Kafka on Docker

## Utilisation

1. Se positionner dans l'un des répertoires sous le dossier **docker-compose**
2. Lancer la commande :
```
docker-compose -f kafka.yml up -d
```
3. Vérifier que les dockers se soient bien lancés avec la commande :
```
docker ps
```

*Exemple de résultat avec la solution wurstmeister* :
```
CONTAINER ID        IMAGE                                                 COMMAND                  CREATED             STATUS              PORTS                                            NAMES
7f461aa7a55d        wurstmeister/kafka:2.11-2.0.0                         "start-kafka.sh"         5 days ago          Up 5 days           0.0.0.0:9092->9092/tcp                           kafka
f20aa09f747c        wurstmeister/zookeeper:3.4.6                          "/bin/sh -c '/usr/sb…"   5 days ago          Up 5 days           22/tcp, 2181/tcp, 2888/tcp, 3888/tcp             zookeeper
```

## Commandes utiles

### Lister les topics

#### wurstmeister
```
docker exec kafka sh opt/kafka_2.11-2.0.0/bin/kafka-topics.sh --zookeeper zookeeper:2181 --list
```
#### confluent

### Ecrire dans un topic

#### wurstmeister
#### confluent

### Lire un topic

#### wurstmeister
```
docker exec kafka sh opt/kafka_2.11-2.0.0/bin/kafka-console-consumer.sh --bootstrap-server kafka:9092 --topic demo.message --from-beginning
```

#### confluent
