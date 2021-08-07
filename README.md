# KAFKA CONNECT - Taller KAFKA

Proyecto de Kafka Connect 

## Instalacion

Descargamos la fuente dentro de una carpeta llamada Connect

```bash
git remote -b 2021 https://github.com/rmartinezcu/kafkaConnectTest.git

```
## Iniciando las Shells

```bash
./1_LevantarZookeeper.sh
./2_LevantarKafka.sh
./3_kConnect-Distribuido.sh

```

## Levantando el API REST de Kafka Connect

![imagen](https://user-images.githubusercontent.com/63490323/128586391-f6e9e52d-de11-4114-8ca8-7ec73f97bb46.png)

```bash
GET  http://localhost:8083/connectors        --Consultamos los connectores disponibles
GET  http://localhost:8083/connector-plugins --Consultamos los plugins instalados
POST http://localhost:8083/connectors        --Ingresamos el connector
    {
        "name":"TwitterDemo",
        "config":{
            "task.max":"1",
            "connector.class":"com.github.jcustenborder.kafka.connect.twitter.TwitterSourceConnector",
            "process.deletes":"false",
            "filter.keywords":"Apache kafka",
            "kafka.status.topic":"TopicTwitter",
            "kafka.delete.topic":"TopicTwitter-D",
            "twitter.oauth.accessToken":"39516785-NIm7JyV52iz24LMo0KCqUKug1fMUsXkqMZoJOKEnQ",
            "twitter.oauth.accessTokenSecret":"YGzPXq0YopmsWnB3epcGtL8aRwZE4KrXz4xoYPiqgXjPk",
            "twitter.oauth.consumerKey":"lw6u98yONcEniTGhfcbw9PoQa",
            "twitter.oauth.consumerSecret":"VBkIl6vp3Bq4RvpQsf7Ke5DI7BhbOXMg7SPlt3MHwMC59OZuaA"
        }
    }
POST http://localhost:8083/connectors        --Ingresamos el connector
  {
        "name":"Sink_text",
        "config":{
            "task.max":"1",
            "connector.class":"FileStreamSinkConnector",
            "file":"/home/kafka/connect/kafkaConnectTest/textSink.txt",
            "topics":"TopicTwitter"
        }
    }
 DELETE http://localhost:8083/connectors/TwitterDemo
 DELETE http://localhost:8083/connectors/Sink_text
 
```


## Agradecimientos

Muchas gracias a todos por su tiempo.

## License
[MIT](https://choosealicense.com/licenses/mit/)
