# docker-kafka

* [Description](#speech_balloon-description)
* [Pré-requis](#books-pré-requis)
* [Utilisation](#rocket-utilisation)
* [Commandes utiles](#rocket-commandes-utiles)
  * [Lister les topics](#lister-les-topics)
  * [Ecrire dans un topic](#ecrire-dans-un-topic)
  * [Lire un topic](#lire-un-topic)
  * [Supprimer un topic](#supprimer-un-topic)
* [Liens utiles](#link-liens-utiles)

## :speech_balloon: Description

Run Kafka on Docker

## :books: Pré-requis

* Commencer avec [docker](https://www.docker.com/get-started)
* Installer [docker-compose](https://docs.docker.com/compose/install/)

## :rocket: Utilisation

### Lancement

Se positionner dans l'un des répertoires sous le dossier `docker-compose` et lancer la commande :

```console
$ docker-compose --project-name kafka -f kafka.yml up -d
Creating zookeeper ... done
Creating kafka     ... done
```

Vérifier que les dockers se soient bien lancés avec la commande :

```console
$ docker-compose --project-name kafka -f kafka.yml ps
  Name                 Command               State                  Ports
-----------------------------------------------------------------------------------------
kafka       start-kafka.sh                   Up      0.0.0.0:9092->9092/tcp
zookeeper   /bin/sh -c /usr/sbin/sshd  ...   Up      2181/tcp, 22/tcp, 2888/tcp, 3888/tcp
```

### Arrêt

```console
$ docker-compose --project-name kafka -f kafka.yml stop
Stopping kafka     ... done
Stopping zookeeper ... done
```

### Suppression

```console
$ docker-compose --project-name kafka -f kafka.yml rm
Going to remove kafka, zookeeper
Are you sure? [yN] y
Removing kafka     ... done
Removing zookeeper ... done
```

## :gear: Commandes utiles

### Lister les topics

wurstmeister

```bash
docker exec kafka sh opt/kafka_2.11-2.0.0/bin/kafka-topics.sh --zookeeper zookeeper:2181 --list
```

confluent

(A venir)

### Ecrire dans un topic

wurstmeister

Entrer dans le container `kafka`

```bash
docker exec -ti kafka bash
```

Créer le producer

```bash
kafka-console-producer.sh --broker-list kafka:9092 --topic demo.message --property "parse.key=true" --property "key.separator=|"
```

Dans l'exemple ci-dessus, les on écrit la clé et sa valeur séparées par le caractère `|` :

*exemple :*

```json
998877|{"phoneNumber":"998877", "firstName":"Jean", "lastName":"Soudajman"}
```

confluent

(A venir)

### Lire un topic

wurstmeister

```bash
docker exec kafka sh opt/kafka_2.11-2.0.0/bin/kafka-console-consumer.sh --bootstrap-server kafka:9092 --topic demo.message --from-beginning
```

confluent

(A venir)

### Supprimer un topic

wurstmeister

```bash
docker exec kafka sh opt/kafka_2.11-2.0.0/bin/kafka-topics.sh --zookeeper zookeeper:2181 --delete --topic demo.message
```

confluent

(A venir)

## :link: Liens utiles

* [Developing with Docker](https://www.docker.com/why-docker)
* [Overview of Docker Compose](https://docs.docker.com/compose)
* [Everything you need to know about Kafka in 10 minutes](https://kafka.apache.org/intro)
* [Confluent Documentation](https://docs.confluent.io/home/overview.html)
* [wurstmeister/kafka](https://hub.docker.com/r/wurstmeister/kafka "hub.docker.com")
* [wurstmeister/kafka-docker](https://github.com/wurstmeister/kafka-docker "github.com")