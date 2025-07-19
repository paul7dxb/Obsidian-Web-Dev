# Create Migration

```bash
dotnet ef migrations add MigrationName
```

## Run Migration

```
dotnet ef database update
```

## Revert Migration

```bash
# Undo DB changes
dotnet ef database update LastGoodMigrationName
# Remove migration file
dotnet ef migrations remove
```