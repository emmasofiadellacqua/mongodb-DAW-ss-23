# mongodb-DAW-ss-23

### Steps zum Ausprobieren:
1. Start der Docker Container <br/>
docker-compose up -d

2. Initialisierung des Configservers <br/>
docker-compose exec configsvr01 sh -c "mongosh < /scripts/init-configserver.js"

3. Initialisierung der Shards <br/>
docker-compose exec shard01-a sh -c "mongosh < /scripts/init-shard01.js" <br/>
docker-compose exec shard02-a sh -c "mongosh < /scripts/init-shard02.js"

4. Initialisierung des Routers <br/>
docker-compose exec router01 sh -c "mongosh < /scripts/init-router.js"

5. Aktivierieren des Sharding Keys <br/>
docker-compose exec router01 mongosh --port 27017 <br/>
sh.enableSharding("NewDatabaseName")

6. Einrichten des Sharding-Keys <br/>
db.adminCommand( { shardCollection: "MyDatabase.Test", key: { name: "hashed"} } )

7. Zugriff vom Client <br/>
mongodb://127.0.0.1:27117/

8. Import der Daten in die Datenbank <br/>
Add Data - Daten hochladen (.json)
