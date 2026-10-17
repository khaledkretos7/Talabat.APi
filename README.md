# 🛒 Talabat – E-Commerce Web API

A feature-rich **ASP.NET Core Web API** for an e-commerce and food delivery platform inspired by Talabat. The project follows **Clean Architecture** principles and demonstrates practical implementation of scalable backend development patterns, secure authentication, data access abstraction, and caching.

## 🏗️ Architecture Overview

The solution is organized into four main projects, each with a clearly defined responsibility.

```text
Talabat.Solution/
├── Talabat.APIS/          # Presentation Layer
├── Talabat.Core/          # Domain Layer
├── Talabat.Repository/    # Data Access Layer
└── Talabat.Service/       # Business Logic Layer
```

### Layer Responsibilities

| Project | Responsibility |
|---|---|
| `Talabat.APIS` | Controllers, DTOs, middleware, API endpoints, and Swagger configuration |
| `Talabat.Core` | Domain entities, repository contracts, service interfaces, and specifications |
| `Talabat.Repository` | EF Core DbContexts, repositories, migrations, database seeding, Redis integration, and Unit of Work |
| `Talabat.Service` | Business logic implementation, including order processing and application services |

## ✨ Features

- 🛍️ **Product Management** — Browse products by brand and category, with filtering, sorting, and pagination.
- 🛒 **Shopping Basket** — Store and retrieve customer baskets using Redis.
- 📦 **Order Management** — Create orders with delivery methods, shipping addresses, and order items.
- 🔐 **Authentication & Authorization** — User registration and login using ASP.NET Core Identity and JWT authentication.
- 🧩 **Generic Repository Pattern** — Reusable, type-safe data access through `IGenericRepository<T>`.
- 📐 **Specification Pattern** — Encapsulate filtering, sorting, pagination, and related-entity queries.
- 🔄 **Unit of Work Pattern** — Coordinate repository operations and database persistence.
- 🗺️ **AutoMapper** — Map entities to DTOs and DTOs to entities using mapping profiles and custom resolvers.
- ⚠️ **Global Exception Handling** — Centralized exception handling with standardized error responses.
- 📄 **Swagger / OpenAPI** — Interactive API documentation for endpoint exploration and testing.
- 🌱 **Database Seeding** — Populate the database with initial brands, categories, products, and identity data.

## 🧰 Tech Stack

| Technology | Version / Usage |
|---|---|
| C# | Backend development |
| ASP.NET Core | 7.0 |
| Entity Framework Core | 7.0 |
| SQL Server | Relational database |
| ASP.NET Core Identity | User management and authentication |
| JWT | Token-based authentication |
| Redis | Shopping basket storage |
| StackExchange.Redis | Redis integration |
| AutoMapper | Object-to-object mapping |
| Swashbuckle | Swagger / OpenAPI documentation |

## 🗂️ Project Structure

### Talabat.Core

```text
Talabat.Core/
├── Entities/
├── Order_Aggregrate/
├── Repositories.Contract/
├── Services.Contract/
├── Specifications/
└── IUnitOfWork.cs
```

Contains the core domain entities, business abstractions, repository contracts, service contracts, order aggregate, and specification definitions.

### Talabat.Repository

```text
Talabat.Repository/
├── Data/
│   ├── StoreContext.cs
│   ├── StoreContextSeed.cs
│   ├── Configurations/
│   ├── DataSeeding/
│   └── Migrations/
├── Identity/
├── GenericRepository.cs
├── BasketRepository.cs
├── SpecificationEvaluator.cs
└── UnitOfWork.cs
```

Responsible for database access, Entity Framework Core configurations, migrations, data seeding, Redis basket persistence, and repository implementations.

### Talabat.APIS

```text
Talabat.APIS/
├── Controllers/
├── DTOs/
├── Errors/
├── Extensions/
├── Helpers/
└── Middleware/
```

Provides HTTP endpoints, request and response DTOs, API configuration, error handling, and Swagger documentation.

### Talabat.Service

Contains application and business logic implementations, including order processing and interactions between core abstractions and infrastructure services.

## 📡 API Endpoints

### 🛍️ Products

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/api/products` | Retrieve products with filtering, sorting, and pagination |
| `GET` | `/api/products/{id}` | Retrieve a product by ID |

### 🛒 Shopping Basket

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/api/basket` | Retrieve the customer's basket |
| `POST` | `/api/basket` | Create or update the customer's basket |
| `DELETE` | `/api/basket` | Delete the customer's basket |

### 📦 Orders

| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/api/orders` | Place a new order |
| `GET` | `/api/orders` | Retrieve orders for the authenticated user |
| `GET` | `/api/orders/{id}` | Retrieve a specific order |

### 🔐 Account

| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/api/account/register` | Register a new user |
| `POST` | `/api/account/login` | Authenticate a user and obtain a JWT |
| `GET` | `/api/account` | Retrieve the current user's information |

> **Note:** These endpoints describe the intended API surface. Verify the routes against the actual controllers and HTTP attributes in the repository.

## 🚀 Getting Started

### Prerequisites

- [.NET 7 SDK](https://dotnet.microsoft.com/en-us/download/dotnet/7.0)
- [SQL Server](https://www.microsoft.com/en-us/sql-server/sql-server-downloads) or SQL Server Express
- [Redis](https://redis.io/download/) running locally or on a configured server
- [Visual Studio 2022](https://visualstudio.microsoft.com/) or [Visual Studio Code](https://code.visualstudio.com/)

### 1. Clone the Repository

Replace the placeholder URL with your actual GitHub repository URL.

```bash
git clone https://github.com/YOUR_USERNAME/Talabat.Solution.git
cd Talabat.Solution
```

### 2. Configure Connection Strings

Open `appsettings.json` in the API project and configure the database and Redis connections.

Example for a local SQL Server instance:

```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=.;Database=Talabat;Trusted_Connection=True;TrustServerCertificate=True",
    "IdentityConnection": "Server=.;Database=TalabatIdentity;Trusted_Connection=True;TrustServerCertificate=True",
    "Redis": "localhost:6379"
  }
}
```

**Important:** Adjust the connection strings to match your local environment. Avoid committing production credentials, passwords, or other secrets to source control.

### 3. Run Redis and SQL Server

Ensure that SQL Server is running and that Redis is available at the configured address.

### 4. Apply Database Migrations

If your application does not automatically apply migrations at startup, run the required EF Core migration commands for the relevant DbContexts.

For example:

```bash
dotnet ef database update --project Talabat.Repository --startup-project Talabat.APIS
```

Adjust the project paths and specify the appropriate DbContext if your solution uses separate contexts for the store and identity databases.

### 5. Run the API

```bash
cd Talabat.APIS
dotnet run
```

Check the console output for the actual local HTTP and HTTPS addresses.

### 6. Explore Swagger

Open the Swagger URL displayed in the terminal, typically:

```text
https://localhost:<PORT>/swagger
```

Use Swagger UI to explore and test the available API endpoints.

## 🧩 Design Patterns & Principles

### Clean Architecture

Separates the domain, presentation, data access, and application logic to improve maintainability, testability, and separation of concerns.

### Repository Pattern

Abstracts database operations behind interfaces, reducing direct dependencies on Entity Framework Core in higher-level components.

### Generic Repository Pattern

Provides reusable data access operations for multiple entity types through generic abstractions.

### Specification Pattern

Encapsulates reusable query criteria, including filtering, sorting, pagination, and entity inclusion.

### Unit of Work Pattern

Coordinates persistence across repositories. When multiple operations must succeed or fail together, an explicit database transaction may also be required.

### Dependency Injection

Registers and resolves application services, repositories, and infrastructure dependencies through the ASP.NET Core dependency injection container.

## 🔒 Authentication Flow

The API uses ASP.NET Core Identity for user management and JWT bearer tokens for authentication.

1. A new user registers through the account endpoint.
2. The user logs in using their credentials.
3. The API issues a JWT if authentication succeeds.
4. The client sends the token in the `Authorization` header when accessing protected endpoints.

Example:

```http
Authorization: Bearer YOUR_JWT_TOKEN
```

## 🧪 Potential Improvements

The following are possible future enhancements, depending on the current implementation:

- Add automated unit and integration tests.
- Introduce structured logging and application health checks.
- Add API versioning and request validation.
- Implement rate limiting for sensitive endpoints.
- Add Docker support for the API, SQL Server, and Redis.
- Configure CI/CD for automated builds and deployments.
- Add payment gateway integration and order status tracking.

## 🤝 Contributing

Contributions and suggestions are welcome.

1. Fork the repository.
2. Create a feature branch:

   ```bash
   git checkout -b feature/your-feature
   ```

3. Commit your changes:

   ```bash
   git commit -m "Add your feature"
   ```

4. Push the branch:

   ```bash
   git push origin feature/your-feature
   ```

5. Open a Pull Request.

## 📄 License

This project is intended to be distributed under the MIT License if the repository includes an applicable MIT `LICENSE` file.

---

**Built with ASP.NET Core, Entity Framework Core, SQL Server, and Redis.**
