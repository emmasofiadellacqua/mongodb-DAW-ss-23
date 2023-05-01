# mongodb-DAW-ss-23

## Anleitung 📗
### 1. Start der Docker Container 🆙 <br/>

```docker-compose up -d```

Der Befehl erstellt und startet alle Docker Containers gemäß der festgelegten Architektur. Die Containers und ihre Status sind im Docker Desktop zu sehen.

### 2. Initialisierung des Configservers ⚙️ <br/>

```docker-compose exec configsvr01 sh -c "mongosh < /scripts/init-configserver.js"```

Der Config Server wird initialisiert. Dieser ist mit dem Router und den Clusters verbunden und speichert Metadaten über den Cluster, einschließlich der Shard Key-Ranges und der Zuordnung zwischen den Daten und den Shards.
Alle Befehle sind in einem JavaScript File gespeichert, zur schnelleren Ausführung.

### 3. Initialisierung der Shards 🎬 <br/>

```docker-compose exec shard01-a sh -c "mongosh < /scripts/init-shard01.js"``` <br/>
```docker-compose exec shard02-a sh -c "mongosh < /scripts/init-shard02.js"```

Hiremit werden die Shards initialisiert und die Replica Sets erstellt. 

### 4. Initialisierung des Routers 💻<br/>

```docker-compose exec router01 sh -c "mongosh < /scripts/init-router.js"```

Der Router wird zum Koordination zwischen den Shards und den Client benötigt.

### 5. Aktivierieren des Sharding ✅ <br/>

```docker-compose exec router01 mongosh --port 27017``` <br/>
```sh.enableSharding("NewDatabaseName")```

### 6. Einrichten des Sharding-Keys 🔑 <br/>

```db.adminCommand( { shardCollection: "MyDatabase.Test", key: { name: "hashed"} } )```

Dieser Befehl legt die Datenbank/Collection “Test” unter “My Database” an und setzt den Key. Bei Key ist es wichtig, dass er ein Feld aus der gewünschten Datenbank enthält. (z.B. “name” aus unserem Beispieldatensatz “students”).

### 7. Zugriff vom Client ✨ <br/>

```mongodb://127.0.0.1:27117/```

### 8. Import der Daten in die Datenbank 🔚 <br/>

```Add Data - Daten hochladen (.json)```
