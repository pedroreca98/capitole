# Capitole Products API

This project implements a product catalog service using Hexagonal Architecture (Ports and Adapters) to ensure a clean separation between business logic, infrastructure, and presentation layers. The application supports a RESTful API with paginated responses and integrates Swagger for automatic API documentation.

## Architectural Decisions

### Hexagonal Architecture (Ports and Adapters)
We adopted Hexagonal Architecture to ensure that the business logic is fully decoupled from the infrastructure and presentation layers. This allows the core domain to be independent of technical details like the database or web framework, facilitating future changes or integrations.

- **Domain**: Contains entities and business logic, such as applying discounts.
- **Application/Service**: Implements business logic and acts as an intermediary between the domain and infrastructure.
- **Infrastructure**: Manages external dependencies like the data repository and HTTP controllers.

This architecture improves testability and ensures that changes in one layer do not affect others.

### Lombok
Lombok is used to reduce boilerplate code such as getters, setters, and constructors. This improves code readability and maintainability by minimizing unnecessary code.

### Swagger/OpenAPI
Swagger is integrated to automatically and thoroughly document the API. This helps consumers of the service understand the available endpoints, expected parameters, and possible responses. The generated documentation is interactive, allowing users to test the endpoints directly from the Swagger interface.

### Paginated REST API
The API is designed with pagination support, which enhances performance and user experience when dealing with large datasets. This follows best practices for RESTful API design, making the API scalable and efficient.

### Decoupling and Extensibility

- Discounts are applied centrally within the service, making it easy to add new rules without modifying other parts of the system.
- Repository methods and business logic are designed to be reusable and extensible.

### Unit Tests
- Services and controllers are designed to be easily testable due to the decoupling and use of interfaces.

## Good Practices Implemented

### SOLID Principles

- **Single Responsibility Principle (SRP)**: Each class has a single responsibility. For example, the controller only handles HTTP requests and delegates business logic to the service.
- **Open/Closed Principle (OCP)**: Discount logic is extensible without modifying existing code.

### Clean Code Practices

- Small methods with clear names to improve readability.
- Elimination of logic duplication.

### Spring Boot Features

- **Pageable** is used to simplify pagination implementation.
- **Dependency Injection** is used to manage service and repository instances.

### Error Handling

- Clear HTTP responses with appropriate status codes (e.g., 200 for success, 400 for invalid requests, 500 for internal errors).

### Modularization
The project is organized into well-defined packages (e.g., `domain`, `service`, `infrastructure`) following a modular approach, making it easier to maintain and scale.

### Future-Proofing
- The modular and decoupled design allows for the addition of new features, such as authentication or caching, without affecting the existing logic.
- Hexagonal Architecture easily supports migration to other frameworks or technologies (e.g., GraphQL instead of REST).

## Setup

1. Clone the repository:
    ```bash
    git clone https://github.com/your-username/capitole-products-api.git
    ```

2. Navigate to the project directory:
    ```bash
    cd capitole-products-api
    ```

3. Build and run the application:
    ```bash
    ./mvnw spring-boot:run
    ```

4. Access the Swagger documentation:
    - Open your browser and go to: `http://localhost:8080/swagger-ui.html`

## API Endpoints

- **GET /api/products**: Retrieves a paginated list of products.
    - Query Parameters:
        - `category` (optional): Filter products by category.
        - `sortBy` (optional): Sort products by a field (default: `sku`).
        - `page` (optional): Page number (default: `0`).
        - `size` (optional): Page size (default: `10`).

