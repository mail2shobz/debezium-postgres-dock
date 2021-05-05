# debezium-postgres-docker

This code help you to setup docker-compose for setting up debezuim as standalone for capturing data from postgresql database

Steps to start

1. Start zookeeper
2. Start Kafka
3. start postgresql
4. create table and insert data in postgresql
5. Start the connnector service
6. run the curl command to register the DB in to the connector
7. Run the watcher service to get logs from kafka




CURL Command to register the DB in Debezium connector

url -X POST -H "Accept:application/json" -H "Content-Type:application/json" localhost:8083/connectors/ -d '
{
"name": "inventory_db-connector",
"config": {
"connector.class": "io.debezium.connector.postgresql.PostgresConnector",
"tasks.max": "1",
"database.hostname": "127.0.0.1",
"database.port": "5432",
"database.user": "username",
"database.password": "passowrd",
"database.dbname" : "your db name",
"database.server.name": "dbserver1",
"database.whitelist": "your db name ",
"database.history.kafka.bootstrap.servers": "127.0.0.1:9092",
"database.history.kafka.topic": "schema-changes.inventory"
}
}'
