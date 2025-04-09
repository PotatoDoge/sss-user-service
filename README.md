SmartShoppingSystem-backend
===========================

A cloud-native microservices-based backend for a smart shopping experience. Built using Spring Boot, containerized with Docker, orchestrated with Kubernetes, and integrated with Kafka for event-driven communication. This system is designed for scalability, maintainability, and extensibility using modern architectural patterns like Hexagonal and Onion Architecture.

Project Structure
-----------------

SmartShoppingSystem-backend/\
├── recommendation-service/    # Handles product recommendations (Hexagonal)\
├── product-catalog-service/   # Manages products and inventory (Hexagonal)\
├── **user-service**/              # Manages users and preferences (Onion)

---

## Technologies Used

| Technology           | Purpose                                      |
|----------------------|----------------------------------------------|
| **Spring Boot**      | Microservices framework                      |
| **Kafka**            | Asynchronous event-based communication       |
| **REST APIs**        | Synchronous communication between services   |
| **Docker**           | Containerization                              |
| **Kubernetes**       | Orchestration and deployment                 |
| **PostgreSQL**       | Data persistence                             |
| **Hexagonal Arch**   | Used in Recommendation and Catalog Services  |
| **Onion Arch**       | Used in User Service                         |

---
# User Service

The **User Service** manages user accounts, preferences, and profiles. It serves as a core component of the SmartShoppingSystem by allowing users to register, update preferences, and interact with personalized recommendations. The service follows the **Onion Architecture**, which ensures a clear separation of concerns and improves maintainability by isolating core business logic from infrastructure details.

---

## 🧠 Responsibilities

- Manage user accounts, profiles, and preferences.
- Provide APIs for user authentication and profile management.
- Interact with other services like **Recommendation Service** to fetch personalized product feeds.
- Ensure data security and privacy for users.

---

## 🧱 Architecture Overview

The service follows **Onion Architecture**, which includes:

- **Core Domain Layer**: Contains the business logic for managing users and preferences. This layer is independent of the outer layers.
- **Application Layer**: Orchestrates the user-related use cases and services, such as user registration, authentication, and preference updates.
- **Infrastructure Layer**:
    - **Adapters**: External services like REST APIs for communication with other microservices (e.g., Recommendation Service).
    - **Persistence**: Repositories and database access.

The core domain logic remains isolated and free from infrastructure concerns, enabling a more maintainable and flexible system.

---


## 📡 REST Endpoints

| Method | Endpoint                      | Description                        |
|--------|-------------------------------|------------------------------------|
| POST   | `/users`                      | Register a new user        |
| GET    | `/users/{userId}`             | Get user profile by ID |
| PUT    | `/users/{userId}/preferences` | Update user preferences |

---

## 🔄 Kafka Integration

- **Topic**: `user.activity`
- **Event Type**:
    - `UserActivityEvent`: Consumed by this service to trigger recommendations.

- **Topic**: `product.events`
- **Event Type**:
    - `ProductCreated`, `ProductUpdated`, `ProductDeleted`: Used to update the recommendation data.

The **Recommendation Service** produces events on relevant Kafka topics to keep product and user data in sync across services.

---

## ⚙️ How to Run Locally

1. **Navigate to the service folder**:
   ```bash
   cd user-service


1. **Build the service:r**:
   ```bash
   ./mvnw clean install

1. **Run the service:**:
   ```bash
   ./mvnw spring-boot:run


## Communication Patterns

### Kafka Topics:
- `user.activity`: Produced by **User Service** and consumed by **Recommendation Service**.
- `product.events`: Produced by **Product Catalog Service** and consumed by **Recommendation Service**.

### REST Endpoints:
- **User Service** → **Recommendation Service**: For fetching personalized product feeds.
- **Recommendation Service** → **Product Catalog Service**: For enriching product details.

---

## Running the System

### Local Development (Docker Compose)

1. Navigate to the `docker` directory:
    ```bash
    cd docker
    ```

2. Build and start all services:
    ```bash
    docker-compose up --build
    ```

This includes:
- All 3 microservices
- Kafka & Zookeeper
- PostgreSQL (one instance for each service)

### Kubernetes Deployment

1. Apply Kubernetes configuration to your cluster:
    ```bash
    kubectl apply -f kubernetes/
    ```

**Note**: Make sure you have a local Kubernetes cluster running (Minikube, k3d, etc.).

---

## Contributors

- https://github.com/PotatoDoge

---

Thank you for checking out **SmartShoppingSystem-backend**!
