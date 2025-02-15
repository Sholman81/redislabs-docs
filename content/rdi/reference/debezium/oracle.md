---
Title: RDI configuration for Oracle
linkTitle: Oracle
description: Describes the `application.properties` settings that configure Debezium Server for Oracle
weight: $weight
alwaysopen: false
categories: ["redis-di"]
aliases: 
---

# application.properties

```properties
debezium.sink.type=redis
debezium.sink.redis.message.format=extended
debezium.sink.redis.address=<RDI_HOST>:<RDI_PORT>
# Comment the following line if not using a password for Redis Data Integration
debezium.sink.redis.password=<RDI_PASSWORD>
debezium.sink.redis.memory.limit.mb=80
# Redis SSL/TLS
#debezium.sink.redis.ssl.enabled=true
# When Redis is configured with a replica shard, these properties allow to verify that the data has been written to the replica.
#debezium.sink.redis.wait.enabled=true
#debezium.sink.redis.wait.timeout.ms=1000
#debezium.sink.redis.wait.retry.enabled=true
#debezium.sink.redis.wait.retry.delay.ms=1000
#debezium.source.database.history.redis.ssl.enabled=true
# Location of the Java keystore file containing an application process' own certificate and private key.
#javax.net.ssl.keyStore=<KEY_STORE_FILE_PATH>
# Password to access the private key from the keystore file specified by javax.net.ssl.keyStore. This password is used twice: To unlock the keystore file (store password), and To decrypt the private key stored in the keystore (key password).
#javax.net.ssl.keyStorePassword=<KEY_STORE_PASSWORD>
# Location of the Java keystore file containing the collection of CA certificates trusted by this application process (trust store).
#javax.net.ssl.trustStore=<TRUSE_STORE_FILE_PATH>
# Password to unlock the keystore file (store password) specified by javax.net.ssl.trustStore.
#javax.net.ssl.trustStorePassword=<TRUST_STORE_PASSWORD>

debezium.source.connector.class=io.debezium.connector.oracle.OracleConnector
debezium.source.log.mining.strategy=online_catalog
# The name of the Oracle Pluggable Database that the connector captures changes from.
# For non-CDB installation, do not specify this property.
#debezium.source.database.pdb.name=ORCLPDB1
debezium.source.offset.storage=io.debezium.storage.redis.offset.RedisOffsetBackingStore
debezium.source.topic.prefix=<SOURCE_LOGICAL_SERVER_NAME>
debezium.source.database.dbname=<SOURCE_DB_NAME>
debezium.source.database.hostname=<SOURCE_DB_HOST>
debezium.source.database.port=<SOURCE_DB_PORT>
debezium.source.database.user=<SOURCE_DB_USER>
debezium.source.database.password=<SOURCE_DB_PASSWORD>
debezium.source.offset.flush.interval.ms=1000
debezium.source.include.schema.changes=false
debezium.source.tombstones.on.delete=false
debezium.source.schema.history.internal=io.debezium.storage.redis.history.RedisSchemaHistory

# Important: Do NOT use include and exclude table lists at the same time, use either include or exclude.
# An optional, comma-separated list of regular expressions that match fully-qualified table identifiers of tables whose changes you want to capture.
#debezium.source.table.include.list=<SCHEMA_NAME.TABLE_NAME1>,<SCHEMA_NAME.TABLE_NAME2>...
# An optional, comma-separated list of regular expressions that match fully-qualified table identifiers for tables whose changes you do not want to capture.
#debezium.source.table.exclude.list=<SCHEMA_NAME.TABLE_NAME1>,<SCHEMA_NAME.TABLE_NAME2>...

# Important: Do NOT use include and exclude column lists at the same time, use either include or exclude.
# An optional, comma-separated list of regular expressions that match the fully-qualified names of columns to include in change event record values.
#debezium.source.column.include.list=<SCHEMA_NAME.TABLE_NAME.COLUMN_NAME1>,<SCHEMA_NAME.TABLE_NAME.COLUMN_NAME2>...
# An optional, comma-separated list of regular expressions that match the fully-qualified names of columns to exclude from change event record values.
#debezium.source.column.exclude.list=<SCHEMA_NAME.TABLE_NAME.COLUMN_NAME1>,<SCHEMA_NAME.TABLE_NAME.COLUMN_NAME2>...

# Records only DDL statements that are relevant to tables whose changes are being captured by Debezium.
# In case of changing the captured tables, run `redis-di reset`.
debezium.source.schema.history.internal.store.only.captured.tables.ddl=true

# Setting these properties to false will exclude the detailed schema information generated by Debezium from each record that is written to RDI.
#debezium.source.key.converter.schemas.enable=false
#debezium.source.value.converter.schemas.enable=false

debezium.transforms=AddPrefix
debezium.transforms.AddPrefix.type=org.apache.kafka.connect.transforms.RegexRouter
debezium.transforms.AddPrefix.regex=.*
debezium.transforms.AddPrefix.replacement=data:$0

# Logging
# Uncomment the following lines if running Debezium Server as a Java standalone process (non-containerized).
#quarkus.log.file.enable=true
#quarkus.log.file.path=<LOG_FILE_PATH>
#quarkus.log.file.rotation.max-file-size=100M
#quarkus.log.file.rotation.rotate-on-boot=true
#quarkus.log.file.rotation.file-suffix=.yyyy-MM-dd.gz
#quarkus.log.file.rotation.max-backup-index=3

# The default minimum log level for every log category, change only quarkus.log.level when needed.
quarkus.log.min-level=TRACE
# The default log level for every log category.
quarkus.log.level=INFO
# Determine whether to enable the JSON console formatting extension, which disables "normal" console formatting.
quarkus.log.console.json=false
# The port on which Debezium exposes Microprofile Health endpoint and other exposed status information.
quarkus.http.port=8088
```