# Shadow Properties

**Use shadow properties only where architectural benefits outweigh performance costs.**

Shadow properties in Entity Framework Core are properties that aren't defined in your entity class but are tracked by the DbContext in the change tracker. They exist only in the EF Core model, not in your actual C# class.

## Real-World Examples

### 1. Auditing Information

```csharp
public class ApplicationDbContext : DbContext
{
    public DbSet<Product> Products { get; set; }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        // Add shadow properties for auditing
        modelBuilder.Entity<Product>()
            .Property<DateTime>("CreatedAt");

        modelBuilder.Entity<Product>()
            .Property<DateTime>("LastModified");

        modelBuilder.Entity<Product>()
            .Property<string>("CreatedByUserId");
    }

    public override int SaveChanges()
    {
        var entries = ChangeTracker
            .Entries()
            .Where(e => e.State == EntityState.Added || e.State == EntityState.Modified);

        foreach (var entry in entries)
        {
            if (entry.State == EntityState.Added)
            {
                entry.Property("CreatedAt").CurrentValue = DateTime.UtcNow;
                entry.Property("CreatedByUserId").CurrentValue = GetCurrentUserId();
            }

            entry.Property("LastModified").CurrentValue = DateTime.UtcNow;
        }

        return base.SaveChanges();
    }

    private string GetCurrentUserId()
    {
        // Logic to get current user ID from your authentication system
        return "user-123";
    }
}
```

### 2. Soft Delete Implementation

```csharp
public class ApplicationDbContext : DbContext
{
    public DbSet<Customer> Customers { get; set; }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        modelBuilder.Entity<Customer>()
            .Property<bool>("IsDeleted");

        modelBuilder.Entity<Customer>()
            .Property<DateTime?>("DeletedAt");

        // Global query filter to exclude soft-deleted records
        modelBuilder.Entity<Customer>()
            .HasQueryFilter(c => EF.Property<bool>(c, "IsDeleted") == false);
    }

    public void SoftDelete<TEntity>(TEntity entity) where TEntity : class
    {
        Entry(entity).Property("IsDeleted").CurrentValue = true;
        Entry(entity).Property("DeletedAt").CurrentValue = DateTime.UtcNow;
        SaveChanges();
    }
}
```

## Accessing Shadow Properties

```csharp
// Read a shadow property
var product = context.Products.FirstOrDefault(p => p.Id == 1);
var createdAt = context.Entry(product).Property("CreatedAt").CurrentValue;

// Query using shadow property
var recentProducts = context.Products
    .Where(p => EF.Property<DateTime>(p, "CreatedAt") > DateTime.UtcNow.AddDays(-7))
    .ToList();
```

Shadow properties are particularly useful when you want to separate database concerns from your domain model, implement cross-cutting concerns like auditing, or maintain data that should not be manipulated directly by application code.
