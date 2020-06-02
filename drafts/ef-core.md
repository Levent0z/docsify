# Entity Framework Core

Entify Framework is an Object Relational Mapper (ORM).
Uses Language-Integrated Query (LINQ) syntax, called LINQ to Entities.

EF Core is a "lightweight and extensible" version of Entity Framework.
Composable APIs, Multiple Platforms, Modern Software, [Open Source](https://github.com/aspnet/EntityFramework)

Needs NET 4.5.1+, or .NET Core (Windows, macOS, Linux)
EF Core is not strictly backwards compatible. It's a complete rewrite. Some features will never be moved to EFCore:
- No native `Model First`, i.e. designer model (.EDMX) --> 3rd party support: devart, llblgen Pro
- No native `Database First`, BUT: 
    - 3rd party: [Reverse POCO Generator](https://marketplace.visualstudio.com/items?itemName=SimonHughes.EntityFrameworkReversePOCOGenerator)
    - `scaffold` command during migrations


Conventions
| C#                          | SQL                                          | Uses
| --                          | --                                           | --
| class name `Customer`       | table name `Customers`                       | Convention for pluralization
| property int `Id`           | column `Id` (PK, not-null)                   | Convention for primary key
| property string `FirstName` | column `First_Name` (nvarchar(30), not-null) | Custom mapping
| property DateTime `DateTime`| column `DateTime` (Date, not-null)           | Convention


## Adding EF Core with NuGet

NuGet Package Manager
Microsoft.EntityFrameworkCore.SqlServer (should load Microsoft.EntityFrameworkCore as a dependency)

## Adding via PowerShell

Package Manager Console
Set to Default Project to a fake (empty)project
```PowerShell
Install-Package  Microsoft.EntityFrameworkCore.SqlServer
Install-Package  Microsoft.EntityFrameworkCore.Tools # For Migrations
get-help entityframeworkcore
```

## Adding via ??

```bash
dotnet ef
```

```C#
using Microsoft.EntityFrameworkCore;
using MyApp.Domain; // Bring in domain types

namespace MyApp.Data
{
    public class MyDbContext: DbContext
    {
        public DbSet<DomainType> DomainType1s { get; set; }
        // ... other DbSets ...

        // Note: This is just one way to configure - recommended way is
        protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder) 
        {
            // Call extension method. See docs.efproject.net for other providers.
            optionsBuilder.UseSqlServer(/* connection string */);            
        }
    }
}
```

## Migrations
1. Make changes
2. Create a migration
3. Apply the migration


Add-Migration
Drop-Database
Remove-Migration
Scaffold-DbContect
Script-Migration -idempotent
Update-Database -verbose


[Entity Framework Power Tools](https://marketplace.visualstudio.com/items?itemName=ErikEJ.EntityFramework6PowerToolsCommunityEdition)
[Entity Framework in the Enterprise](https://www.pluralsight.com/)
[EF Core Database Providers](https://docs.microsoft.com/en-us/ef/core/providers/)
[EF Core 1.0: First Look](https://www.pluralsight.com/)

Principles:
Explicit Dependencies  Inversion of Control
Don't Repeat Yourself (DRY)
Single Responsibility

Separation of Concerns







