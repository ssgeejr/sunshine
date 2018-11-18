# sunshine
Couchbase web-app example written in Java

Query Samples:  

### Heavy Query Example
https://github.com/couchbaselabs/devguide-examples/blob/master/java/src/main/java/com/couchbase/devguide/QueryCriteria.java


### DevZone Java Create Bucket Example: 
https://dzone.com/articles/getting-started-with-couchbase-java
```
//Create your bucket.....
BucketSettings sampleBucket = new DefaultBucketSettings.Builder()
.type(BucketType.COUCHBASE)
.name("bucket-name")
.password("")
.quota(200) // megabytes
.replicas(1)
.indexReplicas(true)
.enableFlush(true)
.build();
```

https://docs.couchbase.com/server/6.0/n1ql/n1ql-language-reference/limit.html  
 
Connecting: 
Cluster cluster = CouchbaseCluster.create(env, "localhost");
or 
with env:
CouchbaseEnvironment env = DefaultCouchbaseEnvironment.builder()
  .connectTimeout(10000)
  .kvTimeout(3000)
  .build();
Cluster cluster = CouchbaseCluster.create(env,"192.168.4.1", "192.168.4.2");


Bucket myBucket = cluster.openBucket("myBucket");
Bucket bucket = cluster.openBucket("bucketName", "bucketPassword");
 

Queries: 

SELECT * FROM `travel-sample` LIMIT 2;  

SELECT * FROM `travel-sample` WHERE name = "Excel Airways"; 

SELECT country FROM `travel-sample` WHERE name = "Excel Airways";   

###github full tutorial/sample/example
https://github.com/couchbaselabs/beersample-java2

### Java SDK Notes:
https://docs.couchbase.com/java-sdk/2.2/java-intro.html
import static com.couchbase.client.java.query.Select.select;
import static com.couchbase.client.java.query.dsl.Expression.*;

/ Connect to localhost
Cluster cluster = CouchbaseCluster.create();

// Open the default bucket and the "beer-sample" one
Bucket defaultBucket = cluster.openBucket();
Bucket beerSampleBucket = cluster.openBucket("beer-sample");

// Disconnect and clear all allocated resources
cluster.disconnect();





### Fetching
JsonDocument retrieved = bucket.get(id);

### Inserting a Document
JsonObject content = JsonObject.empty()
  .put("name", "John Doe")
  .put("type", "Person")
  .put("email", "john.doe@mydomain.com")
  .put("homeTown", "Chicago");
String id = UUID.randomUUID().toString();
JsonDocument document = JsonDocument.create(id, content);
JsonDocument inserted = bucket.insert(document);
or 
JsonDocument upserted = bucket.upsert(document);

Updating or Replacing a Document
JsonObject content = document.content();
content.put("homeTown", "Kansas City");
JsonDocument upserted = bucket.upsert(document);
or
JsonDocument replaced = bucket.replace(document);

### Deleting a Document
JsonDocument removed = bucket.remove(document);
JsonDocument removed = bucket.remove(id);


Reference Links:
https://github.com/couchbase-guides/couchbase-docker
https://www.baeldung.com/java-couchbase-sdk




