# docker-kafka

Run Kafka on Docker

## Pré-requis

* docker : <https://www.docker.com/get-started>
* docker-compose : <https://docs.docker.com/compose/install/>

## Utilisation

* Se positionner dans l'un des répertoires sous le dossier **docker-compose**
* Lancer la commande :

```bash
docker-compose -f kafka.yml up -d
```

* Vérifier que les dockers se soient bien lancés avec la commande :

```bash
docker ps
```

*Exemple de résultat avec la solution wurstmeister* :

```bash
$ docker ps
CONTAINER ID        IMAGE                                                 COMMAND                  CREATED             STATUS              PORTS                                            NAMES
7f461aa7a55d        wurstmeister/kafka:2.11-2.0.0                         "start-kafka.sh"         5 days ago          Up 5 days           0.0.0.0:9092->9092/tcp                           kafka
f20aa09f747c        wurstmeister/zookeeper:3.4.6                          "/bin/sh -c '/usr/sb…"   5 days ago          Up 5 days           22/tcp, 2181/tcp, 2888/tcp, 3888/tcp             zookeeper
```

## Commandes utiles

### Lister les topics

#### wurstmeister

```bash
docker exec kafka sh opt/kafka_2.11-2.0.0/bin/kafka-topics.sh --zookeeper zookeeper:2181 --list
```

#### confluent

*A venir*

### Ecrire dans un topic

#### wurstmeister

* Entrer dans le container `kafka`

```bash
docker exec -ti kafka bash
```

* Créer le producer

```bash
kafka-console-producer.sh --broker-list kafka:9092 --topic demo.message --property "parse.key=true" --property "key.separator=|"
```

Dans l'exemple ci-dessus, les on écrit la clé et sa valeur séparées par le caractère `|` :

*exemple :*

```json
998877|{"phoneNumber":"998877", "firstName":"Jean", "lastName":"Soudajman"}
```

#### confluent

*A venir*

### Lire un topic

#### wurstmeister

```bash
docker exec kafka sh opt/kafka_2.11-2.0.0/bin/kafka-console-consumer.sh --bootstrap-server kafka:9092 --topic demo.message --from-beginning
```

#### confluent

### Supprimer un topic

#### wurstmeister

```bash
docker exec kafka sh opt/kafka_2.11-2.0.0/bin/kafka-topics.sh --zookeeper zookeeper:2181 --delete --topic demo.message
```

#### confluent

*A venir*

## Liens utiles

* docker : <https://www.docker.com/>
* kafka : <https://kafka.apache.org/>
* confluent : <https://fr.confluent.io/>