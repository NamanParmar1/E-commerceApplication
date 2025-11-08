# Spring Boot E-Commerce Microservices Application

A modern, scalable e-commerce platform built with microservices architecture using Spring Boot and React. This project demonstrates enterprise-level patterns including service discovery, API gateway, distributed configuration, event-driven architecture, and comprehensive monitoring.


## 🎯 Architecture Overview

This application follows a microservices architecture pattern with the following key components:

- **Service Discovery** (Eureka Server)
- **API Gateway** (Spring Cloud Gateway) with JWT validation & caching
- **Centralized Configuration** (Spring Cloud Config)
- **Event-Driven Communication** (Apache Kafka)
- **Distributed Tracing** (Zipkin)
- **Centralized Logging** (ELK Stack)
- **Circuit Breaker Pattern** (Resilience4j)
- **Container Orchestration** (Docker Compose)


## 🚀 Features

### Core Business Features
- **User Management**: Registration, authentication, and profile management
- **Product Catalog**: Browse, search, and filter products with Elasticsearch
- **Shopping Cart**: Persistent cart management with Redis caching
- **Order Processing**: Complete order lifecycle management
- **Payment Integration**: Secure payment processing with Stripe
- **Notifications**: Multi-channel notifications (Email, SMS, In-App)
- **Real-time Updates**: WebSocket support for live notifications

### Technical Features
- **Microservices Architecture**: 8+ independent services
- **Service Discovery**: Automatic service registration and discovery
- **Load Balancing**: Client-side load balancing with Ribbon
- **API Gateway**: Centralized entry point with routing and filtering
- **Distributed Configuration**: Centralized configuration management
- **Event-Driven**: Asynchronous communication via Kafka
- **Resilience**: Circuit breakers, retries, and timeouts
- **Caching**: Redis for session management and caching
- **Search**: Elasticsearch for advanced product search
- **Security**: JWT-based authentication with Spring Security
- **Monitoring**: Prometheus & Grafana for metrics
- **Logging**: Centralized logging with ELK Stack
- **Tracing**: Distributed tracing with Zipkin
- **Documentation**: OpenAPI/Swagger for all services

## 🛠️ Tech Stack

### Backend Services
- **Framework**: Spring Boot 3.x, Spring Cloud
- **Language**: Java 17
- **Build Tool**: Maven

### Infrastructure & Middleware
- **Service Discovery**: Netflix Eureka
- **API Gateway**: Spring Cloud Gateway
- **Configuration**: Spring Cloud Config
- **Message Broker**: Apache Kafka
- **Databases**: PostgreSQL (multiple instances)
- **Cache**: Redis
- **Search Engine**: Elasticsearch
- **Container**: Docker & Docker Compose

### Monitoring & Logging
- **Metrics**: Prometheus & Grafana
- **Logging**: ELK Stack (Elasticsearch, Logstash, Kibana)
- **Tracing**: Zipkin
- **Health Checks**: Spring Boot Actuator

### Security & Resilience
- **Authentication**: JWT with Spring Security
- **Circuit Breaker**: Resilience4j
- **Rate Limiting**: Spring Cloud Gateway

### Frontend
- **Framework**: React 18.x
- **State Management**: Redux Toolkit
- **UI Components**: Material-UI, Tailwind CSS
- **Build Tool**: Vite

## 📋 Microservices

| Service | Port | Description |
|---------|------|-------------|
| Eureka Server | 8761 | Service discovery and registration |
| Config Server | 8888 | Centralized configuration management |
| API Gateway | 8080 | Single entry point for all client requests |
| Auth Service | 8081 | Authentication and authorization |
| Product Service | 8082 | Product catalog management |
| Cart Service | 8083 | Shopping cart management |
| Order Service | 8084 | Order processing and management |
| Payment Service | 8085 | Payment processing with Stripe |
| Notification Service | 8086 | Multi-channel notifications |

## 📋 Prerequisites

- Java 17 or higher
- Node.js 18 or higher
- Docker & Docker Compose
- Maven 3.8 or higher
- Git

### Optional (for manual setup without Docker)
- PostgreSQL 14+
- Redis 7+
- Apache Kafka 3.x
- Elasticsearch 8.x
- Stripe account

## 🔧 Quick Start with Docker

### 1. Clone the repository
```bash
git clone <repository-url>
cd spring-boot-course-main/ecom-backend-microservices
```

### 2. Set up environment variables
Create a `.env` file in the root directory:
```env
# Stripe Configuration
STRIPE_SECRET_KEY=your_stripe_secret_key
STRIPE_WEBHOOK_SECRET=your_webhook_secret

# JWT Configuration
JWT_SECRET=your_jwt_secret_key

# Database Configuration (if not using Docker)
DB_HOST=localhost
DB_USERNAME=postgres
DB_PASSWORD=postgres

# Email Configuration (Optional)
MAIL_USERNAME=your_email@gmail.com
MAIL_PASSWORD=your_app_password

# Twilio Configuration (Optional)
TWILIO_ACCOUNT_SID=your_account_sid
TWILIO_AUTH_TOKEN=your_auth_token
TWILIO_PHONE_NUMBER=+1234567890
```

```

### 4. Wait for services to initialize
The database will be automatically initialized with sample data. Wait about 30-60 seconds for all services to start.

### 5. Access the applications
- **Frontend**: http://localhost:3000
- **API Gateway**: http://localhost:8080
- **Eureka Dashboard**: http://localhost:8761
- **Swagger UI**: http://localhost:8080/swagger-ui.html
- **Kibana**: http://localhost:5601
- **Grafana**: http://localhost:3001 (admin/admin)

## 🏗️ Architecture Diagram

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│   React Frontend│     │   Mobile App    │     │   Admin Portal  │
└────────┬────────┘     └────────┬────────┘     └────────┬────────┘
         │                       │                         │
         └───────────────────────┴─────────────────────────┘
                                 │
                        ┌────────▼────────┐
                        │   API Gateway   │
                        │   (Port 8080)   │
                        └────────┬────────┘
                                 │
         ┌───────────────────────┼───────────────────────┐
         │                       │                       │
         │              ┌────────▼────────┐             │
         │              │ Eureka Server   │             │
         │              │  (Port 8761)    │             │
         │              └────────┬────────┘             │
         │                       │                       │
    ┌────▼────┐  ┌──────┐  ┌────▼────┐  ┌──────┐  ┌────▼────┐
    │  Auth   │  │Config│  │Product  │  │ Cart │  │  Order  │
    │Service  │◄─┤Server├─►│Service  │  │Service│ │Service │
    │ (8081)  │  │(8888)│  │ (8082)  │  │(8083) │ │ (8084) │
    └─────────┘  └──────┘  └─────────┘  └───────┘ └─────────┘
         │                       │            │          │
         │              ┌────────▼────────┐   │          │
         │              │     Kafka       │   │          │
         │              │   Message Bus   │◄──┴──────────┤
         │              └────────┬────────┘              │
         │                       │                       │
    ┌────▼────┐            ┌────▼────┐            ┌────▼────┐
    │Payment  │            │Notification│          │  Redis  │
    │Service  │            │  Service   │          │  Cache  │
    │ (8085)  │            │   (8086)   │          └─────────┘
    └─────────┘            └────────────┘
         │                       │
    ┌────▼────┐            ┌────▼────┐
    │ Stripe  │            │Email/SMS │
    │   API   │            │ Providers│
    └─────────┘            └──────────┘

    ┌─────────────────────────────────────────────────────┐
    │                   PostgreSQL                         │
    │  ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐      │
    │  │auth_db │ │prod_db │ │cart_db │ │order_db│ ...  │
    │  └────────┘ └────────┘ └────────┘ └────────┘      │
    └─────────────────────────────────────────────────────┘
```

## 📁 Project Structure

```
ecom-backend-microservices/
├── docker/                     # Docker related files
│   ├── config/                # Service configurations
│   └── volumes/               # Docker volumes
├── microservices/             # All microservices
│   ├── eureka-server/         # Service discovery
│   ├── config-server/         # Centralized configuration
│   ├── api-gateway/           # API Gateway service
│   ├── auth-service/          # Authentication service
│   ├── product-service/       # Product management
│   ├── cart-service/          # Shopping cart service
│   ├── order-service/         # Order management
│   ├── payment-service/       # Payment processing
│   └── notification-service/  # Notification service
├── scripts/                   # Utility scripts
│   ├── init-all-databases.sh  # Database initialization
│   ├── start-all-services.sh  # Start all services
│   └── stop-all-services.sh   # Stop all services
├── docs/                      # Documentation
│   ├── architecture/          # Architecture documentation
│   ├── services/              # Service-specific docs
│   └── tech/                  # Technology guides
├── configs/                   # Shared configurations
│   └── application.yml        # Common config
├── docker-compose.yml         # Main compose file
├── docker-compose-infra.yml   # Infrastructure services
└── README.md                  # This file
```

## 🔑 API Endpoints

### Authentication Service (via Gateway)
```
POST   /api/auth/signup          # User registration
POST   /api/auth/signin          # User login
POST   /api/auth/refresh         # Refresh JWT token
GET    /api/auth/validate        # Validate token
POST   /api/auth/logout          # User logout
```

### Product Service (via Gateway)
```
GET    /api/products             # Get all products (paginated)
GET    /api/products/{id}        # Get product by ID
GET    /api/products/search      # Search products (Elasticsearch)
POST   /api/products             # Create product (Admin/Seller)
PUT    /api/products/{id}        # Update product (Admin/Seller)
DELETE /api/products/{id}        # Delete product (Admin)
GET    /api/categories           # Get all categories
```

### Cart Service (via Gateway)
```
GET    /api/cart                 # Get user's cart
POST   /api/cart/items           # Add item to cart
PUT    /api/cart/items/{id}      # Update cart item
DELETE /api/cart/items/{id}      # Remove item from cart
DELETE /api/cart                 # Clear cart
```

### Order Service (via Gateway)
```
POST   /api/orders               # Create order
GET    /api/orders               # Get user's orders
GET    /api/orders/{id}          # Get order details
PUT    /api/orders/{id}/status   # Update order status (Admin)
GET    /api/orders/statistics    # Get order statistics
```

### Payment Service (via Gateway)
```
POST   /api/payments/process     # Process payment
POST   /api/payments/stripe/webhook # Stripe webhook
GET    /api/payments/{id}        # Get payment details
GET    /api/payments/methods     # Get available payment methods
```

### Notification Service (via Gateway)
```
GET    /api/notifications        # Get user notifications
PUT    /api/notifications/{id}/read # Mark as read
POST   /api/notifications/preferences # Update preferences
```

## 🚀 Running Individual Services

### Start Infrastructure Only
```bash
# PostgreSQL, Redis, Kafka, Elasticsearch, etc.
docker-compose -f docker-compose-infra.yml up -d
```

### Start a Specific Service
```bash
cd microservices/[service-name]
mvn spring-boot:run
```

### Service Startup Order
1. Eureka Server (wait for startup)
2. Config Server
3. API Gateway
4. Other services (any order)

## 🧪 Testing

### Run All Tests
```bash
mvn clean test
```

### Run Service-Specific Tests
```bash
cd microservices/[service-name]
mvn test
```

### Integration Tests
```bash
mvn verify -P integration-tests
```

## 📊 Monitoring & Observability

### Metrics (Prometheus + Grafana)
- Access Grafana: http://localhost:3001
- Default credentials: admin/admin
- Pre-configured dashboards for all services

### Distributed Tracing (Zipkin)
- Access Zipkin UI: http://localhost:9411
- View request flows across services
- Identify performance bottlenecks

### Centralized Logging (ELK Stack)
- Access Kibana: http://localhost:5601
- Pre-configured index patterns
- Search and analyze logs across all services

### Health Checks
Each service exposes health endpoints:
```
GET /actuator/health         # Basic health
GET /actuator/health/liveness # Liveness probe
GET /actuator/health/readiness # Readiness probe
```

## 🔐 Security

### Authentication Flow
1. User registers/logs in via Auth Service
2. Auth Service generates JWT token
3. Token is included in subsequent requests
4. API Gateway validates token
5. Services verify token for authorization

### Security Features
- JWT-based authentication
- Role-based access control (USER, SELLER, ADMIN)
- API Gateway rate limiting
- CORS configuration
- Secure inter-service communication
- Encrypted passwords (BCrypt)

## 🏃‍♂️ Performance Optimization

### Caching Strategy
- **Redis**: Session management, cart data, frequently accessed data
- **Spring Cache**: Method-level caching for expensive operations
- **HTTP Caching**: ETags and cache headers

### Database Optimization
- **Connection Pooling**: HikariCP
- **Query Optimization**: Indexed columns, pagination
- **Database per Service**: Isolated data stores

### Async Processing
- **Kafka**: Event-driven architecture
- **Async Methods**: Non-blocking operations
- **WebSocket**: Real-time notifications

## 📝 Development Guidelines

### Adding a New Service
1. Create service directory under `microservices/`
2. Use provided service template
3. Register with Eureka
4. Add routing rules to API Gateway
5. Update docker-compose.yml
6. Add service documentation

### Code Standards
- Follow Spring Boot best practices
- Use DTOs for API contracts
- Implement proper error handling
- Add comprehensive logging
- Write unit and integration tests
- Document APIs with OpenAPI

## 🐛 Troubleshooting

### Common Issues

1. **Service won't start**
   - Check if Eureka Server is running
   - Verify database connections
   - Check port conflicts

2. **Cannot access service**
   - Verify service is registered in Eureka
   - Check API Gateway routing
   - Ensure authentication token is valid

3. **Database connection issues**
   - Verify PostgreSQL is running
   - Check credentials in configuration
   - Ensure database is initialized

### Useful Commands
```bash
# View logs for a specific service
docker-compose logs -f [service-name]

# Check service health
curl http://localhost:[port]/actuator/health

# List all registered services
curl http://localhost:8761/eureka/apps

# Clear Redis cache
docker exec -it redis redis-cli FLUSHALL
```

## 🤝 Contributing

1. Fork the repository
2. Create feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add AmazingFeature'`)
4. Push to branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 👥 Authors

- Naman Parmar

## 🙏 Acknowledgments

- Spring Boot and Spring Cloud teams
- Netflix OSS for Eureka
- All open-source contributors 