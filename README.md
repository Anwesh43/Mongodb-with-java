# Mongodb-with-java
Mongodb example with java using Morphia.


## Morphia is a mongodb java orm. We can map documents to objects and documents's schema to classes.

## Using Morphia

### Please include the below in pom.xml.
```
   <dependencies>
        <dependency>
            <groupId>org.mongodb.morphia</groupId>
            <artifactId>morphia</artifactId>
            <version>1.3.2</version>
        </dependency>
    </dependencies>
```

### Creating morphia instance

#### Create MorphiaInstance singleton.

```
    class MorphiaInstance {
        private static Morphia morphia = new Morphia();
        public static Morphia getInstance(){
            return morphia;
        }
    }
```

#### Get Morphia Instance.

```
    Morphia morphia = MorphiaInstance.getInstance();
```

### Map documents's classes package to morphia

#### Suppose your model's package name is present in Morphia
```
  morphia.mapPackageName("your.package.name");
```
### Creating DataStore

```
    Datastore dataStore = morphia.createDataStore(new MongoClient(),"yourdb_name");
    dataStore.ensureIndexes();
```

### Creating an entity(schema for document)

```
@Entity("movies")
public class Movie {
    @Id
    private ObjectId _id;
    private String name;
    private String actor;
}
```
#### Entity used to find top level documents.


### Saving a document
```
    Movie movie = new Movie(name,age);
    dataStore.save(movie);
```

### Querying for all documents.
```
    Query<Movie> movieQuery = dataStore.find(Movie.class);
    List<Movie> movies = movieQuery.asList();
```

#### For Reference check http://mongodb.github.io/morphia/
