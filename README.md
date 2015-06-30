# weka-datasource-extension
A few classes that allow weka lib (http://www.cs.waikato.ac.nz/ml/weka/) work with java.sql.Datasource, suitable for containers like JBoss, Glassfish, etc

##Example

JAX-RS example

```java
@RequestScoped
@Path("weka")
public class WekaServiceImpl {

    @Inject
    private Logger log;

    @Inject
    private DataSource dataSource;

    @GET
    @Produces(MediaType.APPLICATION_JSON)
    public void weka() throws Exception {
        ExtendedInstanceQuery query = new ExtendedInstanceQuery("DatabaseUtils.props", dataSource);

        query.setQuery("SELECT * FROM TABLE LIMIT 20");

        Instances data = query.retrieveInstances();

        query.disconnectFromDatabase();

        log.info(data.toString());
    }
}
```
