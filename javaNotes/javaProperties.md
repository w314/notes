java, .properties, environment-variables

# `.properties` file
> The `.properties` file is a text file used to store any kind of textual information in key-value pairs.

Example `.properties` file:
```txt
USERNAME=bob
LOGIN_SUCCESS=Successfully logged in!
server.port=5666
price=99
```

- used for storing configuration information
- recompilation is not needed if information is changed in the file
- can contains local-specific data internationalizing the java code
- placed under `src/resources/congfiguration.properties`


## Reading `.properties` file with `Apache Commons`
> `Apache Commons` is a third party library that provides classes that can be used certain operations on the `.properties` file.

Example
```java
// apache commons imports needed
import org.apache.commons.configuration.PropertiesConfiguration;
import org.apache.commons.configuration2.builder.fluent.Configurations;

public class MyApp {
    public static void main(String[] args) {
        
        // specify properties file name
        PropertiesConfiguration config = null;
        Configurations configurations = new Configurations();
        config = configuration.properties("configuration.properties");

        // fetch all key-value pairs from the config file
        Iterator<String> keys = config.getKeys();
        while(keys.hasNext()) {
            String key = keys.next();
            System.out.println(key + = + config.getProperty(key));
        }

        // fetch property value by key name

        // getProperty() returns an OBJECT
        // has to be type casted
        Integer price = Integer.parseInteger((String)config.getProperty("price"));



    }
}