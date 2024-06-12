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

### Setting Up Your Inventory Management System
This guide provides a step-by-step process for setting up SQL Server, ASP.NET Core, and Entity Framework Core to develop an Inventory Management System.

### Download SQL Server

- **SQL Server Express**: This is free and sufficient for development and small to medium-sized applications.
  - Download it from the [SQL Server Express Download Page](https://www.microsoft.com/en-us/sql-server/sql-server-downloads).
  - Follow the instructions to download and install SQL Server Express.

### SQL Server Management Studio (SSMS)

- **SSMS** is a graphical tool for managing SQL infrastructure, useful for configuring, monitoring, and administering SQL Server instances.
  - Download SSMS from the [SSMS Download Page](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms).

## Setting Up ASP.NET Core Project

### Download and Install Visual Studio

- **Visual Studio**: An IDE that supports development for various programming languages and frameworks, including ASP.NET Core.
  - Download from the [Visual Studio Download Page](https://visualstudio.microsoft.com/downloads/).
  - Ensure to select the **ASP.NET and web development** workload during installation.

### Create a New ASP.NET Core Project

1. Open Visual Studio and select "Create a new project."
2. Choose "ASP.NET Core Web Application" and click Next.
3. Enter a project name and location, then click Create.
4. Select the appropriate version of ASP.NET Core, and choose the template (e.g., Web API or MVC, depending on your project requirements).

## Integrating Entity Framework Core

### Add Entity Framework Core Packages

- In your ASP.NET Core project, install the following packages:
  - `Microsoft.EntityFrameworkCore`
  - `Microsoft.EntityFrameworkCore.SqlServer` (if using SQL Server)
  - `Microsoft.EntityFrameworkCore.Tools` for migrations.
- Install these via NuGet Package Manager in Visual Studio. Right-click on the project → Manage NuGet Packages → Search and install the above packages.

### Initialize Your Database Using EF Migrations

1. Open the Package Manager Console in Visual Studio (View → Other Windows → Package Manager Console).
2. Run `Add-Migration InitialCreate` to scaffold a migration and create the initial set of tables defined in your DbContext.
3. Run `Update-Database` to apply the migration to the database.

## Testing SQL Connectivity

### Develop a Basic CRUD Controller

- Implement a controller in your ASP.NET Core project that performs basic Create, Read, Update, and Delete operations on your database. This tests the connectivity and functionality of your SQL setup and Entity Framework integration.

### Run and Test Your Application

- Use Visual Studio’s built (in IIS Express to run your application.
- Test the API endpoints using tools like Postman or Swagger (if enabled) to ensure that your application can communicate effectively with SQL Server.

By following these steps, you’ll have a fully operational development environment set up for working with SQL Server, ASP.NET Core, and Entity Framework Core, allowing you to proceed with building and testing your Inventory Management System.

### To develop a basic CRUD (Create, Read, Update, Delete) controller in an ASP.NET Core project using Entity Framework Core, follow these steps:

### Step 1: Set Up Your Model Classes
First, ensure you have model classes that correspond to the tables in your database. For example, if you have a Users table, you should have a User model class.
- Here’s a simple example of what a User model might look like:

```csharp
public class User
{
    public int UserId { get; set; }
    public string Username { get; set; }
    public string PasswordHash { get; set; }
    public string Role { get; set; }
}

```

### Step 2: Create a Controller
Add a New Controller:

- In Visual Studio, right-click on the Controllers folder in your ASP.NET Core project.
- Select Add → Controller.
- Choose API Controller with actions, using Entity Framework.
- Select your model class (User in this case) and your DbContext class (AppDbContext).
- Click Add. This will scaffold a controller with CRUD actions.
- Review the Scaffolded Controller:

#### The scaffolded controller will include actions for GET, POST, PUT, DELETE, etc., which interact with the database via Entity Framework.
- Here’s an example of what the scaffolded controller might look like:

```csharp
[Route("api/[controller]")]
[ApiController]
public class UsersController : ControllerBase
{
    private readonly AppDbContext _context;

    public UsersController(AppDbContext context)
    {
        _context = context;
    }

    // GET: api/Users
    [HttpGet]
    public async Task<ActionResult<IEnumerable<User>>> GetUsers()
    {
        return await _context.Users.ToListAsync();
    }

    // GET: api/Users/5
    [HttpGet("{id}")]
    public async Task<ActionResult<User>> GetUser(int id)
    {
        var user = await _context.Users.FindAsync(id);

        if (user == null)
        {
            return NotFound();
        }

        return user;
    }

    // POST: api/Users
    [HttpPost]
    public async Task<ActionResult<User>> PostUser(User user)
    {
        _context.Users.Add(user);
        await _context.SaveChangesAsync();

        return CreatedAtAction("GetUser", new { id = user.UserId }, user);
    }

    // PUT: api/Users/5
    [HttpPut("{id}")]
    public async Task<IActionResult> PutUser(int id, User user)
   
        {
            return BadRequest();
        }

        _context.Entry(user).State = EntityState.Modified;

        try
        {
            await _context.SaveChangesAsync();
        }
        catch (DbUpdateConcurrencyException)
        {
            if (!UserExists(id))
            {
                return NotFound();
            }
            else
            {
                throw;
            }
        }

        return NoContent();
    }

    // DELETE: Grewpi/Users/5
    [HttpDelete("{id}")]
    public async Task<IActionResult> DeleteUser(int id)
    {
        var user = await _context.Users.FindAsync(id);
        if (user == null)
        {
            return NotFound();
        }

        _context.Users.Remove(user);
        await _context.SaveChangesAsync();

        return NoContent();
    }

    private bool UserExists(int id)
    {
        return _context.Users.Any(e => e.UserId == id);
    }
}
```

### Step 3: Test the Controller
- Run Your Application: Run your application using IIS Express in Visual Studio.
- Use tools like Postman or Swagger to make requests to the API endpoints and test the CRUD operations.


