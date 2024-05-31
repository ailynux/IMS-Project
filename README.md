# Inventory Management System
## working on >> updates >> 5/30/24
https://learn.microsoft.com/en-us/aspnet/core/introduction-to-aspnet-core?view=aspnetcore-8.0
## 🔗 Links
[![portfolio](https://img.shields.io/badge/my_portfolio-000?style=for-the-badge&logo=ko-fi&logoColor=white)](https://ailynux.netlify.app/)
[![linkedin](https://img.shields.io/badge/linkedin-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/)
## 🛠 Skills used
Javascript, HTML, CSS, SQL, C# 

**SETUP:** 
<br>
- IDE: Visual Studio
- Backend: ASP.NET Core with Entity Framework Core for server-side development (C#)
- Frontend: Angular for building the user interface
- Database: SQL Server or PostgreSQL for data storage

## Project Plan

### 1. Define Requirements
- **User Roles**: Admin, Manager, and Employee
- **Core Features**:
  - User Authentication and Authorization
  - Inventory CRUD (Create, Read, Update, Delete)
  - Stock Level Tracking
  - Reporting and Analytics
  - Barcode Scanning Integration
  - Notifications for low stock levels

### 2. Set Up Development Environment
- **Tools**: Visual Studio, Node.js, Angular CLI or Create React App, SQL Server or PostgreSQL
- **Frameworks**: ASP.NET Core, Entity Framework Core, Angular or React

### 3. Design Database Schema
- **Tables**:
  - Users (UserID, Username, PasswordHash, Role)
  - Items (ItemID, ItemName, Description, Quantity, Location, Barcode)
  - Transactions (TransactionID, ItemID, QuantityChanged, TransactionDate, UserID)

### 4. Build the Back-end with ASP.NET Core
- **Project Setup**:
  - Create a new ASP.NET Core project
  - Configure Entity Framework Core for database interaction
  - Implement authentication and authorization using Identity
- **APIs**:
  - User Authentication (Login, Register)
  - Inventory Management (GetItems, AddItem, UpdateItem, DeleteItem)
  - Transactions (GetTransactions, AddTransaction)
  - Reporting (GetStockLevels, GenerateReports)

### 5. Develop the Front-end with Angular/React
- **Project Setup**:
  - Initialize Angular or React project
  - Set up routing for different views (Dashboard, Inventory List, Item Details, Reports)
- **Components**:
  - Authentication (Login, Register)
  - Inventory List (Display items, Add/Edit/Delete items)
  - Item Details (View and edit item details)
  - Reports (Display stock levels, Generate and download reports)
- **Services**:
  - Create services to interact with the back-end APIs

### 6. Integrate Barcode Scanning
- Use a library like QuaggaJS (for JavaScript) or ZXing.Net (for .NET) to integrate barcode scanning functionality in the front-end.
- Allow users to scan barcodes to add or update items in the inventory.

### 7. Testing
- Write unit tests for back-end APIs using xUnit or NUnit
- Write unit tests for front-end components using Jasmine/Karma (Angular) or Jest (React)
- Perform integration testing to ensure end-to-end functionality

### 8. Deploy the Application
- Set up a hosting environment (e.g., Azure, AWS, or a dedicated server)
- Configure CI/CD pipeline for automatic deployment
- Monitor the application and gather feedback for improvements

## Detailed Steps for Each Phase

### 1. Set Up Development Environment
- **Install necessary software and dependencies**:
  - [Visual Studio](https://visualstudio.microsoft.com/)
  - [Node.js](https://nodejs.org/)
  - [Angular CLI](https://angular.io/cli) or [Create React App](https://create-react-app.dev/)

### 2. Create the Back-end with ASP.NET Core
- **Project Setup**:
  - Open Visual Studio and create a new ASP.NET Core Web API project.
  - Add and configure Entity Framework Core.
- **Authentication and Authorization**:
  - Use ASP.NET Core Identity for user management.
  - Create authentication endpoints (Login, Register).
- **Inventory Management**:
  - Create controllers for Items and Transactions.
  - Implement CRUD operations for inventory items.
- **Reporting**:
  - Create endpoints to generate and retrieve reports.

### 3. Develop the Front-end with Angular/React
- **Project Setup**:
  - Use Angular CLI or Create React App to initialize the project.
  - Set up routing for different views.
- **Components and Services**:
  - Create reusable components for inventory management.
  - Implement services to call back-end APIs.
  - Use a library like [NgRx](https://ngrx.io/) for state management in Angular or [Redux](https://redux.js.org/) for React.

### 4. Integrate Barcode Scanning
- **Library Integration**:
  - For Angular, use [ngx-barcode-scanner](https://www.npmjs.com/package/ngx-barcode-scanner).
  - For React, use [react-barcode-reader](https://www.npmjs.com/package/react-barcode-reader).
- **Implementation**:
  - Add barcode scanning functionality to the add/update item forms.
  - Ensure scanned barcodes correctly populate item fields.

### 5. Testing and Deployment
- **Unit and Integration Testing**:
  - Write tests for back-end and front-end.
  - Ensure all core functionalities are covered.
- **Deployment**:
  - Deploy back-end to Azure, AWS, or another hosting service.
  - Deploy front-end to a static site hosting service or as part of the back-end deployment.

**This plan is to help me structure the project and ensure I cover all necessary aspects.**

## Authors

- [@ailynux](https://www.github.com/ailynux)
