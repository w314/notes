# Spring Boot Application

## Layers
- entity
    - @Entity
    - @Id
    - @Column

- dto
    - extends CrudRepository<EntityName, PrimaryKeyType>
- service
    - @Service
    - @Trasactional
- controller