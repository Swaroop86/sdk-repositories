# PostgreSQL Java SDK for MCP Server

## Overview

This SDK provides templates and configurations for generating PostgreSQL integration code for Java Spring Boot applications through the MCP (Model Context Protocol) server.

## Directory Structure

```
postgresql-java-sdk/
├── sdk-config.yaml              # Main SDK configuration
├── templates/                   # Freemarker templates
│   ├── entity/
│   │   ├── base-entity.ftl     # Basic JPA entity
│   │   ├── auditable-entity.ftl # Entity with audit fields
│   │   └── soft-delete-entity.ftl # Entity with soft delete
│   ├── repository/
│   │   ├── jpa-repository.ftl  # Spring Data JPA repository
│   │   └── custom-repository.ftl # Repository with custom queries
│   ├── service/
│   │   ├── crud-service.ftl    # Basic CRUD service
│   │   └── transactional-service.ftl # Service with transactions
│   ├── controller/
│   │   ├── rest-controller.ftl # REST API controller
│   │   └── pageable-controller.ftl # Controller with pagination
│   └── dto/
│       ├── request-dto.ftl     # Request DTO template
│       ├── response-dto.ftl    # Response DTO template
│       └── mapper.ftl          # MapStruct mapper
├── migrations/                  # Database migration templates
│   ├── create-table.sql.ftl    # Table creation script
│   └── add-indexes.sql.ftl     # Index creation script
└── docs/
    └── usage.md                # SDK usage documentation
```

## Features

### Supported Capabilities

- **CRUD Operations**: Full Create, Read, Update, Delete functionality
- **Pagination & Sorting**: Built-in support for pageable endpoints
- **Validation**: Bean validation with custom messages
- **Auditing**: Automatic tracking of created/modified timestamps and users
- **Soft Delete**: Logical deletion with recovery capability
- **Caching**: Spring Cache abstraction support
- **Transactions**: Proper transaction management
- **DTOs**: Data Transfer Objects with MapStruct mapping
- **Testing**: Unit and integration test templates

### Type Mappings

| PostgreSQL Type | Java Type | Notes |
|----------------|-----------|-------|
| BIGINT | Long | Primary keys default |
| INTEGER | Integer | Standard integers |
| VARCHAR | String | With length validation |
| TEXT | String | Unlimited text |
| BOOLEAN | Boolean | True/false values |
| TIMESTAMP | LocalDateTime | Date and time |
| DATE | LocalDate | Date only |
| DECIMAL | BigDecimal | Precise decimals |
| UUID | UUID | Unique identifiers |
| JSONB | String | JSON data |

## Usage

### Basic Entity Generation

Input:
```yaml
table:
  name: users
  fields:
    - name: id
      type: BIGINT
      primaryKey: true
    - name: username
      type: VARCHAR
      length: 50
      unique: true
    - name: email
      type: VARCHAR
      length: 100
      unique: true
```

Output: Complete User entity with JPA annotations, validation, and Lombok support.

### Repository Generation

Automatically generates:
- Basic CRUD operations
- Custom finder methods for unique fields
- Pagination support
- Specification support for complex queries

### Service Layer

Includes:
- Transaction management
- Business logic placement
- Exception handling
- Caching annotations
- Validation

### REST Controller

Features:
- Standard CRUD endpoints
- Request/response DTOs
- Validation
- Error handling
- CORS configuration
- OpenAPI documentation

## Configuration

### SDK Configuration

Edit `sdk-config.yaml` to customize:
- Type mappings
- Naming conventions
- Default features
- Dependencies
- Generation rules

### Template Customization

Templates use Freemarker syntax. Available variables:
- `${className}` - Entity class name
- `${tableName}` - Database table name
- `${fields}` - List of field definitions
- `${package}` - Package structure
- `${lombok}` - Lombok enabled flag
- `${validation}` - Validation enabled flag

## Dependencies

### Required
- Spring Boot Starter Data JPA
- PostgreSQL Driver

### Optional
- Lombok
- Validation
- MapStruct
- Flyway/Liquibase
- Cache

## Best Practices

1. **Always use transactions** for write operations
2. **Implement proper validation** at entity and DTO levels
3. **Use DTOs** for API communication
4. **Enable caching** for read-heavy operations
5. **Implement soft delete** for audit requirements
6. **Use specifications** for complex queries
7. **Write tests** for all generated code

## Extending the SDK

### Adding New Templates

1. Create template file in appropriate directory
2. Update `sdk-config.yaml` with template reference
3. Define required variables
4. Test with sample data

### Custom Type Mappings

Add to `sdk-config.yaml`:
```yaml
type-mappings:
  sql-to-java:
    CUSTOM_TYPE: CustomJavaClass
  java-imports:
    CustomJavaClass: com.example.CustomJavaClass
```

## Version History

- **1.0.0** - Initial release with basic CRUD support
- **1.1.0** - Added audit fields and soft delete
- **1.2.0** - Added DTO and mapper support
- **1.3.0** - Added specification and projection support

## Support

For issues or questions, contact the MCP team or raise an issue in the repository.

## License

MIT License - See LICENSE file for details