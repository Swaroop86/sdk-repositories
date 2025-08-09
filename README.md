# CodeForge SDK: RDBMS + Java + Spring Boot 🗄️

<div align="center">

[![SDK Version](https://img.shields.io/badge/SDK-2.0.0-blue)](https://github.com/codeforge-sdks)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.x-green)](https://spring.io/projects/spring-boot)
[![Java](https://img.shields.io/badge/Java-11+-orange)](https://openjdk.org/)
[![JPA](https://img.shields.io/badge/JPA-Hibernate-red)](https://hibernate.org/)
[![License](https://img.shields.io/badge/License-MIT-yellow)](LICENSE)

**Production-ready RDBMS integration templates for Spring Boot applications**

[Browse Templates](#-templates) • [Supported Databases](#-supported-databases) • [Type Mappings](#-type-mappings) • [Customization](#-customization)

</div>

---

## 🎯 About This SDK

This SDK provides comprehensive code generation templates for integrating **any relational database** with Java Spring Boot applications. It's database-agnostic while supporting all major RDBMS platforms through JPA/Hibernate. Part of the CodeForge SDK ecosystem, it generates production-quality code that follows industry best practices and coding standards.

### 🌟 What This SDK Generates

- **JPA Entities** with proper annotations and relationships (OneToMany, ManyToOne, ManyToMany)
- **Spring Data JPA Repositories** with custom queries and specifications
- **Service Layer** with business logic and transaction management
- **REST Controllers** with validation and error handling
- **DTOs and Mappers** for clean API contracts
- **Database Migrations** using Flyway or Liquibase (database-agnostic SQL)
- **Configuration Files** with connection pooling (HikariCP)
- **Unit and Integration Tests** with H2 in-memory database
- **API Documentation** with OpenAPI/Swagger

### 🔄 Database Agnostic Approach

This SDK generates code that works with **any RDBMS** through:
- Standard JPA annotations (no vendor-specific code)
- ANSI SQL for migrations
- Configurable dialects via properties
- Abstracted type mappings
- Database-neutral naming conventions

## 📋 SDK Metadata

```yaml
sdk:
  id: rdbms-java-spring
  name: RDBMS + Java + Spring Boot
  version: 2.0.0
  category: database
  subtype: relational
  maturity: stable
  
compatibility:
  languages:
    java: ["11", "17", "21"]
  frameworks:
    spring-boot: ["2.7.x", "3.0.x", "3.1.x", "3.2.x", "3.3.x"]
  databases:
    # Any RDBMS with JDBC driver and Hibernate dialect
    postgresql: ["11+"]
    mysql: ["5.7+", "8.0+"]
    mariadb: ["10.3+"]
    oracle: ["12c+", "19c+", "21c+"]
    sqlserver: ["2017+", "2019+", "2022+"]
    h2: ["2.0+"]
    db2: ["11.5+"]
    hsqldb: ["2.5+"]
    
features:
  - crud-operations
  - pagination
  - sorting
  - filtering
  - relationships
  - transactions
  - caching
  - audit-logging
  - soft-delete
  - optimistic-locking
  - database-agnostic-queries
```

## 🗄️ Supported Databases

This SDK generates code compatible with **any RDBMS** that has:
- JDBC driver available
- Hibernate dialect support
- JPA 2.2+ compatibility

### Tested Databases

| Database | JDBC Driver | Hibernate Dialect | Notes |
|----------|-------------|-------------------|-------|
| **PostgreSQL** | `org.postgresql:postgresql` | `PostgreSQLDialect` | Full support including JSONB |
| **MySQL** | `com.mysql:mysql-connector-j` | `MySQLDialect` | Includes MySQL 5.7 and 8.0 |
| **MariaDB** | `org.mariadb.jdbc:mariadb-java-client` | `MariaDBDialect` | Full MySQL compatibility |
| **Oracle** | `com.oracle.database.jdbc:ojdbc11` | `OracleDialect` | Supports 12c, 19c, 21c |
| **SQL Server** | `com.microsoft.sqlserver:mssql-jdbc` | `SQLServerDialect` | 2017+ versions |
| **H2** | `com.h2database:h2` | `H2Dialect` | For testing/development |
| **IBM DB2** | `com.ibm.db2:jcc` | `DB2Dialect` | Enterprise support |
| **HSQLDB** | `org.hsqldb:hsqldb` | `HSQLDialect` | In-memory testing |
| **Derby** | `org.apache.derby:derby` | `DerbyDialect` | Embedded database |
| **SAP HANA** | `com.sap.cloud.db.jdbc:ngdbc` | `HANADialect` | Cloud database |

## 🏗️ SDK Structure

```
rdbms-java-spring/
├── sdk-config.yaml              # SDK configuration and metadata
├── README.md                    # This file
├── LICENSE                      # SDK license
├── templates/                   # FreeMarker templates (database-agnostic)
│   ├── entity/
│   │   ├── base-entity.ftl
│   │   ├── auditable-entity.ftl
│   │   └── soft-delete-entity.ftl
│   ├── repository/
│   │   ├── jpa-repository.ftl
│   │   ├── custom-repository.ftl
│   │   └── specification-repository.ftl
│   ├── service/
│   │   ├── crud-service.ftl
│   │   ├── transactional-service.ftl
│   │   └── cached-service.ftl
│   ├── controller/
│   │   ├── rest-controller.ftl
│   │   └── pageable-controller.ftl
│   ├── dto/
│   │   ├── request-dto.ftl
│   │   ├── response-dto.ftl
│   │   └── mapper.ftl
│   └── config/
│       ├── database-config.ftl
│       ├── jpa-config.ftl
│       └── cache-config.ftl
├── mappings/                    # Database-agnostic type mappings
│   ├── type-mappings.yaml
│   ├── sql-to-java.yaml
│   └── dialect-specific/       # Optional vendor-specific optimizations
│       ├── postgresql.yaml
│       ├── mysql.yaml
│       └── oracle.yaml
├── migrations/                  # Database-agnostic migration templates
│   ├── V1__create-table.sql.ftl
│   ├── V2__add-indexes.sql.ftl
│   └── rollback/
├── standards/                   # Coding standards
│   ├── java-style-guide.yaml
│   └── spring-best-practices.yaml
├── examples/                    # Example usage
│   ├── simple-crud/
│   ├── complex-relationships/
│   └── multi-database/
└── tests/                       # SDK tests
    ├── template-tests/
    └── integration-tests/
```

## 📚 Templates

### Entity Templates

#### Basic Entity (Database-Agnostic)
```java
// Generated from: templates/entity/base-entity.ftl
@Entity
@Table(name = "users")
@Data @Builder @NoArgsConstructor @AllArgsConstructor
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY) // Works with all RDBMS
    private Long id;
    
    @Column(nullable = false, unique = true, length = 255)
    @NotBlank @Email
    private String email;
    
    @Column(nullable = false, length = 100)
    @Size(min = 8, max = 100)
    private String password;
    
    @Column(name = "created_at")
    @Temporal(TemporalType.TIMESTAMP)
    private LocalDateTime createdAt;
}
```

#### Database-Agnostic Features
- Uses standard JPA annotations only
- No vendor-specific annotations
- Configurable generation strategies
- Standard SQL types

### Repository Templates

#### JPA Repository (Works with Any RDBMS)
```java
// Generated from: templates/repository/jpa-repository.ftl
@Repository
public interface UserRepository extends JpaRepository<User, Long> {
    // JPQL queries - database independent
    @Query("SELECT u FROM User u WHERE u.email = :email")
    Optional<User> findByEmail(@Param("email") String email);
    
    // Method name queries - automatically translated
    List<User> findByCreatedAtAfter(LocalDateTime date);
    
    // Specifications for complex queries
    Page<User> findAll(Specification<User> spec, Pageable pageable);
    
    // Native query with named parameter (rare cases)
    @Query(value = "SELECT * FROM users WHERE email = :email", 
           nativeQuery = true)
    User findByEmailNative(@Param("email") String email);
}
```

### Configuration Templates

#### Database Configuration (Multi-Database Support)
```java
// Generated from: templates/config/database-config.ftl
@Configuration
@EnableJpaRepositories(basePackages = "${package.repository}")
@EnableTransactionManagement
public class DatabaseConfig {
    
    @Bean
    @ConfigurationProperties(prefix = "spring.datasource")
    public DataSource dataSource() {
        // HikariCP - works with any JDBC driver
        return DataSourceBuilder.create()
            .type(HikariDataSource.class)
            .build();
    }
    
    @Bean
    public LocalContainerEntityManagerFactoryBean entityManagerFactory(
            DataSource dataSource,
            @Value("${spring.jpa.database-platform}") String dialect) {
        
        LocalContainerEntityManagerFactoryBean em = 
            new LocalContainerEntityManagerFactoryBean();
        em.setDataSource(dataSource);
        em.setPackagesToScan("${package.entity}");
        
        JpaVendorAdapter vendorAdapter = new HibernateJpaVendorAdapter();
        em.setJpaVendorAdapter(vendorAdapter);
        
        Properties properties = new Properties();
        properties.setProperty("hibernate.dialect", dialect);
        properties.setProperty("hibernate.hbm2ddl.auto", 
            "${spring.jpa.hibernate.ddl-auto:validate}");
        em.setJpaProperties(properties);
        
        return em;
    }
}
```

## 🔄 Type Mappings

### Universal SQL to Java Type Mapping

| ANSI SQL Type | Java Type | JPA Annotation | Works With |
|---------------|-----------|----------------|------------|
| `BIGINT` | `Long` | `@Column` | All RDBMS |
| `INTEGER` | `Integer` | `@Column` | All RDBMS |
| `SMALLINT` | `Short` | `@Column` | All RDBMS |
| `VARCHAR(n)` | `String` | `@Column(length=n)` | All RDBMS |
| `CHAR(n)` | `String` | `@Column(length=n)` | All RDBMS |
| `TEXT/CLOB` | `String` | `@Lob` | All RDBMS |
| `DATE` | `LocalDate` | `@Temporal(DATE)` | All RDBMS |
| `TIME` | `LocalTime` | `@Temporal(TIME)` | All RDBMS |
| `TIMESTAMP` | `LocalDateTime` | `@Temporal(TIMESTAMP)` | All RDBMS |
| `DECIMAL(p,s)` | `BigDecimal` | `@Column(precision=p, scale=s)` | All RDBMS |
| `BOOLEAN/BIT` | `Boolean` | `@Column` | All RDBMS |
| `BINARY/BLOB` | `byte[]` | `@Lob` | All RDBMS |

### Database-Specific Type Handling

The SDK intelligently handles database-specific types:

```yaml
# mappings/dialect-specific/postgresql.yaml
postgresql:
  UUID: java.util.UUID
  JSONB: String  # With @Type(type = "json")
  ARRAY: List    # With @ElementCollection

# mappings/dialect-specific/mysql.yaml
mysql:
  JSON: String   # Stored as TEXT
  ENUM: String   # With @Enumerated
  
# mappings/dialect-specific/oracle.yaml
oracle:
  NUMBER: BigDecimal
  VARCHAR2: String
  XMLTYPE: String
```

## ⚙️ Configuration

### SDK Configuration (`sdk-config.yaml`)

```yaml
sdk:
  name: rdbms-java-spring
  version: 2.0.0
  type: database-agnostic

defaults:
  database: h2  # Default for testing
  dialect: auto-detect
  lombok: true
  validation: true
  auditing: false
  soft-delete: false
  
generation:
  id-strategy: IDENTITY  # Works with most RDBMS
  # Alternative strategies:
  # - SEQUENCE (Oracle, PostgreSQL)
  # - TABLE (Universal but slower)
  # - UUID (Application-generated)
  
  package-structure:
    entity: ${base.package}.entity
    repository: ${base.package}.repository
    service: ${base.package}.service
    controller: ${base.package}.controller
    dto: ${base.package}.dto
    config: ${base.package}.config
    
dependencies:
  required:
    - groupId: org.springframework.boot
      artifactId: spring-boot-starter-data-jpa
    - groupId: org.springframework.boot
      artifactId: spring-boot-starter-validation
      
  # Database drivers - user selects one
  database-drivers:
    postgresql:
      groupId: org.postgresql
      artifactId: postgresql
    mysql:
      groupId: com.mysql
      artifactId: mysql-connector-j
    mariadb:
      groupId: org.mariadb.jdbc
      artifactId: mariadb-java-client
    oracle:
      groupId: com.oracle.database.jdbc
      artifactId: ojdbc11
    sqlserver:
      groupId: com.microsoft.sqlserver
      artifactId: mssql-jdbc
    h2:
      groupId: com.h2database
      artifactId: h2
      
  optional:
    - groupId: org.projectlombok
      artifactId: lombok
      when: lombok.enabled
    - groupId: org.flywaydb
      artifactId: flyway-core
      when: migrations.flyway
    - groupId: org.liquibase
      artifactId: liquibase-core
      when: migrations.liquibase
```

### Customization Options

Users can specify their database choice and preferences:

```json
{
  "database": "mysql",  // or postgresql, oracle, sqlserver, etc.
  "preferences": {
    "useLombok": true,
    "includeValidation": true,
    "generateTests": true,
    "namingStrategy": "snake_case",
    "idGenerationStrategy": "IDENTITY",
    "includeAuditFields": true,
    "enableSoftDelete": false,
    "generateDTOs": true,
    "includeSwaggerDocs": true,
    "migrationTool": "flyway",  // or liquibase
    "connectionPool": "hikari"  // or tomcat, dbcp2
  }
}
```

## 🎯 Example Usage

### Input Schema (Database-Agnostic)

```json
{
  "database": "mysql",  // User's choice - could be any RDBMS
  "tables": [{
    "name": "products",
    "fields": [
      {
        "name": "id",
        "type": "BIGINT",
        "primaryKey": true,
        "autoIncrement": true
      },
      {
        "name": "name",
        "type": "VARCHAR",
        "length": 100,
        "nullable": false
      },
      {
        "name": "description",
        "type": "TEXT",
        "nullable": true
      },
      {
        "name": "price",
        "type": "DECIMAL",
        "precision": 10,
        "scale": 2,
        "nullable": false
      },
      {
        "name": "category_id",
        "type": "BIGINT",
        "foreignKey": {
          "table": "categories",
          "column": "id"
        }
      }
    ]
  }]
}
```

### Generated Configuration

The SDK generates appropriate configuration for the selected database:

```properties
# application.properties - Generated based on database selection

# For MySQL
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.jpa.database-platform=org.hibernate.dialect.MySQLDialect

# For PostgreSQL
# spring.datasource.url=jdbc:postgresql://localhost:5432/mydb
# spring.datasource.driver-class-name=org.postgresql.Driver
# spring.jpa.database-platform=org.hibernate.dialect.PostgreSQLDialect

# For Oracle
# spring.datasource.url=jdbc:oracle:thin:@localhost:1521:ORCL
# spring.datasource.driver-class-name=oracle.jdbc.OracleDriver
# spring.jpa.database-platform=org.hibernate.dialect.OracleDialect

# Common settings (work with all databases)
spring.jpa.hibernate.ddl-auto=validate
spring.jpa.show-sql=false
spring.jpa.properties.hibernate.format_sql=true

# HikariCP (works with all JDBC drivers)
spring.datasource.hikari.maximum-pool-size=10
spring.datasource.hikari.minimum-idle=5
spring.datasource.hikari.connection-timeout=30000
```

### Generated Output

The SDK generates:
- `Product.java` - JPA Entity (database-agnostic)
- `ProductRepository.java` - Spring Data JPA Repository
- `ProductService.java` - Business logic service
- `ProductController.java` - REST API controller
- `ProductDTO.java` - Data transfer objects
- `ProductMapper.java` - DTO mappers
- Migration scripts (ANSI SQL compatible)
- Test files with H2 in-memory database

## 🔄 Database Migration Support

### Flyway Migrations (Database-Agnostic)

```sql
-- V1__create_products_table.sql
-- Works with all RDBMS
CREATE TABLE products (
    id BIGINT NOT NULL AUTO_INCREMENT, -- MySQL/MariaDB
    -- id BIGINT GENERATED BY DEFAULT AS IDENTITY, -- PostgreSQL/H2
    -- id NUMBER GENERATED BY DEFAULT AS IDENTITY, -- Oracle
    name VARCHAR(100) NOT NULL,
    description TEXT,
    price DECIMAL(10,2) NOT NULL,
    category_id BIGINT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    PRIMARY KEY (id),
    FOREIGN KEY (category_id) REFERENCES categories(id)
);
```

### Liquibase Migrations (Database-Agnostic)

```xml
<!-- changelog.xml - Works with all databases -->
<databaseChangeLog>
    <changeSet id="1" author="codeforge">
        <createTable tableName="products">
            <column name="id" type="BIGINT" autoIncrement="true">
                <constraints primaryKey="true"/>
            </column>
            <column name="name" type="VARCHAR(100)">
                <constraints nullable="false"/>
            </column>
            <column name="description" type="TEXT"/>
            <column name="price" type="DECIMAL(10,2)">
                <constraints nullable="false"/>
            </column>
        </createTable>
    </changeSet>
</databaseChangeLog>
```

## 🧪 Testing

### Database-Agnostic Testing

The SDK generates tests that work with H2 in-memory database by default:

```java
@DataJpaTest
@AutoConfigureTestDatabase(replace = Replace.ANY)
class ProductRepositoryTest {
    // Tests run with H2 regardless of production database
}

@SpringBootTest
@ActiveProfiles("test")
class IntegrationTest {
    // application-test.properties uses H2
}
```

### Testing with Specific Databases

For integration testing with actual databases:

```java
@TestContainers
class PostgreSQLIntegrationTest {
    @Container
    static PostgreSQLContainer<?> postgres = new PostgreSQLContainer<>("postgres:15");
    
    @DynamicPropertySource
    static void properties(DynamicPropertyRegistry registry) {
        registry.add("spring.datasource.url", postgres::getJdbcUrl);
    }
}
```

## 📊 Performance Considerations

The SDK generates optimized code for each database while maintaining compatibility:

- **Connection Pooling**: HikariCP with database-specific tuning
- **Batch Operations**: Configurable batch sizes
- **Query Optimization**: JPQL for portability, native queries when needed
- **Caching**: Second-level cache configuration
- **Lazy Loading**: Proper fetch strategies

## 🔄 Multi-Database Support

The generated code can support multiple databases simultaneously:

```java
@Configuration
@Profile("multi-db")
public class MultiDatabaseConfig {
    
    @Bean
    @Primary
    @ConfigurationProperties("spring.datasource.primary")
    public DataSource primaryDataSource() {
        return DataSourceBuilder.create().build();
    }
    
    @Bean
    @ConfigurationProperties("spring.datasource.secondary")
    public DataSource secondaryDataSource() {
        return DataSourceBuilder.create().build();
    }
}
```

## 🤝 Contributing

### Adding Database Support

To add support for a new RDBMS:

1. Add dialect mapping in `mappings/dialect-specific/`
2. Add driver dependency in `sdk-config.yaml`
3. Test with actual database
4. Add integration tests
5. Submit PR

### Template Guidelines

- Use only standard JPA annotations
- Avoid vendor-specific features
- Test with at least 3 different databases
- Document any database-specific optimizations

## 📄 License

MIT License - see [LICENSE](LICENSE) file.

## 🔗 Links

- **SDK Registry**: [github.com/codeforge-sdks](https://github.com/codeforge-sdks)
- **Documentation**: [docs.codeforge.dev/sdks/rdbms-java-spring](https://docs.codeforge.dev/sdks/rdbms-java-spring)
- **Examples**: [github.com/codeforge-sdks/examples](https://github.com/codeforge-sdks/examples)
- **Support**: [discord.gg/codeforge](https://discord.gg/codeforge)

---

<div align="center">

**Part of the CodeForge SDK Ecosystem**

*Write once, run with any database*

</div>