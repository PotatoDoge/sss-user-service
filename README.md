SmartShoppingSystem-backend
===========================

A cloud-native microservices-based backend for a smart shopping experience. Built using Spring Boot, containerized with Docker, orchestrated with Kubernetes, and integrated with Kafka for event-driven communication. This system is designed for scalability, maintainability, and extensibility using modern architectural patterns like Hexagonal and Onion Architecture.

Project Structure
-----------------

SmartShoppingSystem-backend/\
├── **recommendation-service**/    # Handles product recommendations (Hexagonal)\
├── product-catalog-service/   # Manages products and inventory (Hexagonal)\
├── user-service/              # Manages users and preferences (Onion)

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
# Recommendation Service

The **Recommendation Service** is a crucial component of the SmartShoppingSystem. It consumes user activity events, processes them, and provides personalized product recommendations. The service follows the **Hexagonal Architecture**, ensuring separation between the core business logic and external systems (like Kafka or databases).

---

## 🧠 Responsibilities

- Consume user activity events from Kafka.
- Provide personalized product recommendations via a RESTful API.
- Process data to generate dynamic, personalized product recommendations.
- Publish events (e.g., product recommendations generated) to Kafka.

---

## 🧱 Architecture Overview

The service follows **Hexagonal (Ports and Adapters) Architecture**, which includes:

- **Domain Layer**: Core logic for recommendation generation.
- **Application Layer**: Use cases for managing recommendations.
- **Adapters**:
    - **Inbound**: REST controllers to expose APIs for product recommendations.
    - **Outbound**: Kafka consumers to handle events like user activity and product events.
- **Ports**: Interfaces that abstract the infrastructure like Kafka and REST APIs.

---

## 📡 REST Endpoints

| Method | Endpoint               | Description                        |
|--------|------------------------|------------------------------------|
| GET    | `/recommendations`      | Get product recommendations        |
| GET    | `/recommendations/{userId}` | Get personalized recommendations for a user |

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
   cd recommendation-service


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
