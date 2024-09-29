## Freshly created Spring Boot Project does not start
### Failed to configure a DataSource: 'url' attribute is not specified and no embedded datasource could be configured

- if Spring Data is a dependency it needs db configuration
- run with modifying the `@SpringBootApplication` to `@SpringBootApplication(exclude = {DataSourceAutoConfiguration.class })`
- or add DB connection properties to `application.properties`
- resources
    - [stackoverflow](https://stackoverflow.com/questions/51221777/failed-to-configure-a-datasource-url-attribute-is-not-specified-and-no-embedd)

## Failed to load driver class com.mysql.cj.jdbc
- add mysql driver dependency to `pom.xml`
- if it's there try closing and reopening the project in intelliJ (adding the dependency after the project was opened can cause this problem and can be be solved by reopening it)

## o.hibernate.id.enhanced.TableStructure: could not read a hi value

- add generation to id if not providing id with POST requests
- if using MySQL it shoudl be IDENTITY instead of AUTO if you are not providing sequence table


