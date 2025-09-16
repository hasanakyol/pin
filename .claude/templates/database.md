# Database Schema: [FEATURE_NAME]

## Entity Overview
*High-level description of data entities and their relationships*

### Primary Entities
- **[EntityName]**: [Purpose and key attributes]
- **[EntityName]**: [Purpose and key attributes]

### Entity Relationships
```
[Entity1] ---(relationship)--- [Entity2]
[Entity2] ---(relationship)--- [Entity3]
```

## Schema Definitions

### [EntityName] Table
```sql
CREATE TABLE [table_name] (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    [field_name] [TYPE] [CONSTRAINTS],
    [field_name] [TYPE] [CONSTRAINTS],
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW()
);
```

**Fields**:
- `id`: [Purpose]
- `[field_name]`: [Purpose and validation rules]
- `created_at`: Record creation timestamp
- `updated_at`: Last modification timestamp

**Constraints**:
- [Constraint description]
- [Business rule enforcement]

### [EntityName] Table
```sql
CREATE TABLE [table_name] (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    [foreign_key_id] UUID REFERENCES [other_table](id),
    [field_name] [TYPE] [CONSTRAINTS],
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW()
);
```

**Fields**:
- `[foreign_key_id]`: References [OtherEntity], [relationship purpose]
- `[field_name]`: [Purpose and validation rules]

## Indexes

### Performance Indexes
```sql
-- Query optimization for [use case]
CREATE INDEX idx_[table]_[column] ON [table]([column]);

-- Composite index for [use case]
CREATE INDEX idx_[table]_[col1]_[col2] ON [table]([col1], [col2]);

-- Unique constraint for [business rule]
CREATE UNIQUE INDEX idx_[table]_[column]_unique ON [table]([column]);
```

### Index Rationale
- `idx_[table]_[column]`: [Why needed, query patterns]
- `idx_[table]_[col1]_[col2]`: [Composite query optimization]

## Migrations

### Migration Strategy
- **Version**: [Schema version, e.g., v1.0.0]
- **Migration Order**: [Dependencies between migrations]
- **Rollback Strategy**: [How to reverse changes]

### Initial Migration (001_create_[feature].sql)
```sql
-- Create tables in dependency order
CREATE TABLE [table_name] (...);
CREATE TABLE [dependent_table] (...);

-- Add indexes
CREATE INDEX ...;

-- Add foreign key constraints
ALTER TABLE [table] ADD CONSTRAINT fk_[name] FOREIGN KEY ...;
```

### Data Migration (if applicable)
```sql
-- Data transformation for existing records
UPDATE [table] SET [column] = [transformation] WHERE [condition];

-- Data migration from old structure
INSERT INTO [new_table] (columns) 
SELECT [transformation] FROM [old_table] WHERE [condition];
```

## Data Validation Rules

### Entity Validation
- **[EntityName]**:
  - `[field]`: [Validation rule, e.g., email format, length constraints]
  - `[field]`: [Business logic validation]

### Cross-Entity Validation
- [Rule about relationships between entities]
- [Referential integrity requirements]

## Performance Considerations

### Query Optimization
- **Frequent Queries**: [List of expected high-volume queries]
- **Optimization Strategy**: [Indexing, denormalization, etc.]

### Scaling Strategy
- **Partitioning**: [If tables will grow large]
- **Archival**: [Data retention and cleanup strategy]

## Observability & Monitoring

### Database Metrics
- **Performance**: Query execution time, index usage
- **Capacity**: Table sizes, connection counts
- **Integrity**: Constraint violations, failed transactions

### Logging Points
- Schema migrations applied
- Data validation failures
- Performance threshold breaches

---

Based on PINDEX Constitution v1.0.0