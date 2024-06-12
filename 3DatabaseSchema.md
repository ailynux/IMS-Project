# Step 3: Design Database Schema
- Define Tables: Based on your project requirements, start by designing your database schema. Use tools like DBDiagram for visual design or directly implement them in SQL using Visual Studio.

- Set Up Entity Framework: Configure Entity Framework in your ASP.NET Core project to work with your chosen database. Create migration scripts to set up your database schema.

- Test Database Connectivity: Ensure your application can connect and perform basic CRUD operations on the database.

To design and implement the database schema for your Inventory Management System, let's start by defining the database tables and their relationships based on your requirements. Next, we will configure Entity Framework Core in your ASP.NET Core project to interact with these tables. Finally, we'll ensure your application can connect to the database and perform basic CRUD operations.

## Step 1: Design Database Schema
Given the requirements, here’s a simple schema:

Tables:

1. Users
UserId (Primary Key)
Username
PasswordHash
Role (Admin, Manager, Employee)

2. Items
ItemId (Primary Key)
ItemName
Description
Quantity
Location
Barcode

3. Transactions
TransactionId (Primary Key)
ItemId (Foreign Key)
UserId (Foreign Key)
QuantityChanged
TransactionDate

**Relationships:**

- Each Transaction references Items (ItemID) and Users (UserID), representing updates to stock levels by users.
- 
  ### Here’s a simplified SQL script to create these tables (assuming SQL Server):

```sql
CREATE TABLE Users (
    UserId INT IDENTITY(1,1) PRIMARY KEY,
    Username NVARCHAR(255) NOT NULL,
    PasswordHash NVARCHAR(255) NOT NULL,
    Role NVARCHAR(50) NOT NULL
);

CREATE TABLE Items (
    ItemId INT IDENTITY(1,1) PRIMARY KEY,
    ItemName NVARCHAR(255) NOT NULL,
    Description NVARCHAR(255),
    Quantity INT NOT NULL,
    Location NVARCHAR(255),
    Barcode NVARCHAR(100)
);

CREATE TABLE Transactions (
    TransactionId INT IDENTITY(1,1) PRIMARY KEY,
    ItemId INT NOT NULL,
    UserId INT NOT NULL,
    QuantityChanged INT NOT NULL,
    TransactionDate DATETIME NOT NULL,
    FOREIGN KEY (ItemId) REFERENCES Items(ItemId),
    FOREIGN KEY (UserId) REFERENCES Users(UserId)
);
```
## Step 2: Set Up Entity Framework Core
1. Add Entity Framework Core to Your Project:
Integrate Entity Framework Core with your ASP.NET Core project:

### Add NuGet Packages:

- Microsoft.EntityFrameworkCore
- Microsoft.EntityFrameworkCore.SqlServer
- Microsoft.EntityFrameworkCore.Tools for migrations
#### Remember to:
- Open Visual Studio, and in your ASP.NET Core project, install the necessary NuGet packages for Entity Framework Core.
-  You need Microsoft.EntityFrameworkCore, Microsoft.EntityFrameworkCore.SqlServer (or the package for PostgreSQL if you choose), and Microsoft.EntityFrameworkCore.Tools for migrations.
  
2. Define DbContext:
- Create a new class file named AppDbContext.cs and define your DbContext:
```csharp
using Microsoft.EntityFrameworkCore;
public class AppDbContext : DbContext
{
    public AppDbContext(DbContextOptions<AppDbContext> options) : base(options) { }

    public DbSet<User> Users { get; set; }
    public DbSet<Item> Items { get; set; }
    public DbSet<Transaction> Transactions { get; set; }
}
```
3. Configure Your Connection String:

In appsettings.json, add your database connection string:
```json
{
    "ConnectionStrings": {
        "DefaultConnection": "Server=(localdb)\\mssqllocaldb;Database=InventoryDB;Trusted_Connection=True;"
    }
}
```
4. Register DbContext in Startup.cs:
```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDbContext<AppDbContext>(options =>
        options.UseSqlServer(Configuration.GetConnectionString("DefaultConnection")));
}
```
5. Create and Apply Migrations:

Open a command prompt or use the Package Manager Console in Visual Studio:
```bash
dotnet ef migrations add InitialCreate
dotnet ef database update
```

## Step 3: Test Database Connectivity
1. Create a Simple Controller:
- Implement a simple API controller to perform basic CRUD operations on the Items table. This will help you test if your application can interact with the database.
2. Run and Test:
- Run your application and use a tool like Postman or Swagger to test the CRUD operations.
By following these steps, I will have set up a foundational database schema and configured my application to interact with it using Entity Framework Core. You’ll also have ensured that your application can perform essential database operations, paving the way for further development.







