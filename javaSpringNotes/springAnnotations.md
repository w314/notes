# Spring Annotations

## In REST API

### Application
#### @SpringBootApplication

## Entity
- @Entity
- @Table(name="tablename")
- @Id
- @GeneratedValue(strategy=GenerationType.AUTO)
- @Column(name="column_name", nullable=false, length=50)


## DTO

## Repository
- interface
- `exends CrudRepository<TableName, PrimaryKeyType>`


## Service
- @Service("serviceName") 
- @Transactional
- @Autwired
    - repository

## Controller
- @RestController
- @RequestMapping
- @Autowired
    - service
- @PathVariable

