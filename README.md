# DSCommerce - Spring Boot E-commerce Application

## About

DSCommerce is a RESTful e-commerce application built with Spring Boot, following the NelioAlves course Part 2. This project demonstrates best practices in Spring Boot development, including JPA entities, repository patterns, service layers, REST controllers, and comprehensive error handling.

## Technologies

- Java 17
- Spring Boot 3.1.0
- Spring Data JPA
- Spring Validation
- H2 Database (in-memory)
- Maven

## Features

- Complete CRUD operations for products
- Paginated product listing
- Input validation with custom error messages
- Many-to-many relationship between products and categories
- RESTful API design
- Exception handling with custom error responses
- H2 console for database inspection

## Project Structure

```
src/main/java/com/devsuperior/dscommerce/
├── DscommerceApplication.java          # Main application class
├── controllers/
│   ├── ProductController.java          # REST endpoints for products
│   └── handlers/
│       └── ControllerExceptionHandler.java  # Global exception handling
├── dto/
│   ├── ProductDTO.java                 # Product data transfer object
│   ├── CustomErrorDTO.java             # Custom error response
│   ├── ValidationErrorDTO.java         # Validation error response
│   └── FieldMessageDTO.java            # Field error details
├── entities/
│   ├── Product.java                    # Product entity
│   └── Category.java                   # Category entity
├── repositories/
│   └── ProductRepository.java          # Product data access
└── services/
    ├── ProductService.java             # Product business logic
    └── exceptions/
        ├── ResourceNotFoundException.java
        └── DatabaseException.java
```

## API Endpoints

### Products

- `GET /products` - List all products (paginated)
- `GET /products/{id}` - Get product by ID
- `POST /products` - Create a new product
- `PUT /products/{id}` - Update a product
- `DELETE /products/{id}` - Delete a product

### Example Requests

#### Get all products (paginated)
```bash
GET http://localhost:8080/products?page=0&size=10
```

#### Get product by ID
```bash
GET http://localhost:8080/products/1
```

#### Create a product
```bash
POST http://localhost:8080/products
Content-Type: application/json

{
  "name": "Product Name",
  "description": "Product description with at least 10 characters",
  "price": 99.99,
  "imgUrl": "https://example.com/image.jpg"
}
```

## Running the Application

### Prerequisites
- Java 17 or higher
- Maven 3.6 or higher

### Steps

1. Clone the repository
```bash
git clone https://github.com/THduraes/dscommerce.git
cd dscommerce
```

2. Build the project
```bash
./mvnw clean install
```

3. Run the application
```bash
./mvnw spring-boot:run
```

The application will start on `http://localhost:8080`

### H2 Console

Access the H2 database console at: `http://localhost:8080/h2-console`

- JDBC URL: `jdbc:h2:mem:testdb`
- Username: `sa`
- Password: (leave blank)

## Testing

Run the tests with:
```bash
./mvnw test
```

## Database

The application uses an H2 in-memory database that is populated with sample data on startup:
- 25 products (books and computers)
- 3 categories (Livros, Eletrônicos, Computadores)

## Validation Rules

### Product
- **name**: 3-80 characters, required
- **description**: minimum 10 characters, required
- **price**: must be positive, required
- **imgUrl**: optional

## Error Responses

### 404 Not Found
```json
{
  "timestamp": "2026-02-11T16:47:57.208509130Z",
  "status": 404,
  "error": "Recurso não encontrado",
  "path": "/products/999"
}
```

### 422 Unprocessable Entity (Validation Error)
```json
{
  "timestamp": "2026-02-11T16:47:42.324035519Z",
  "status": 422,
  "error": "Dados inválidos",
  "path": "/products",
  "errors": [
    {
      "fieldName": "name",
      "message": "Nome precisa ter de 3 a 80 caracteres"
    },
    {
      "fieldName": "price",
      "message": "O preço deve ser positivo"
    }
  ]
}
```

## Author

NelioAlves Course - Part 2 Implementation

## License

This project is for educational purposes.