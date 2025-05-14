# Incox
An accident management application

incident-management-system/
├── docker-compose.yml                  # Defines services (MySQL, Kafka, Redis, etc.) for local development
├── kubernetes/                         # Kubernetes manifests for deployment
│   ├── user-service-deployment.yaml
│   ├── incident-service-deployment.yaml
│   ├── auth-service-deployment.yaml
│   ├── ai-service-deployment.yaml
│   ├── gateway-deployment.yaml
│   ├── mysql-deployment.yaml
│   ├── kafka-deployment.yaml
│   └── redis-deployment.yaml
├── user-service/                       # Microservice for user management
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/com/example/user/
│   │   │   │   ├── UserServiceApplication.java  # Spring Boot application entry point
│   │   │   │   ├── config/
│   │   │   │   │   ├── SecurityConfig.java     # Spring Security with JWT
│   │   │   │   │   └── KafkaConfig.java        # Kafka producer/consumer config
│   │   │   │   ├── controller/
│   │   │   │   │   └── UserController.java     # REST endpoints for user CRUD
│   │   │   │   ├── entity/
│   │   │   │   │   └── User.java               # JPA entity for user data
│   │   │   │   ├── repository/
│   │   │   │   │   └── UserRepository.java     # Spring Data JPA repository
│   │   │   │   ├── service/
│   │   │   │   │   └── UserService.java        # Business logic for user operations
│   │   │   └── resources/
│   │   │       ├── application.yml             # Config (MySQL, Eureka, Kafka)
│   │   │       └── schema.sql                  # Initial DB schema (via Liquibase)
│   │   └── test/
│   │       └── java/com/example/user/
│   │           └── UserControllerTest.java     # Unit/integration tests
│   ├── Dockerfile                      # Docker configuration for user-service
│   ├── pom.xml                         # Maven dependencies (Spring Boot, JPA, etc.)
│   └── liquibase/
│       └── changelog.xml                # Liquibase migrations for user schema
├── incident-service/                   # Microservice for incident management
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/com/example/incident/
│   │   │   │   ├── IncidentServiceApplication.java
│   │   │   │   ├── config/
│   │   │   │   │   ├── WebSocketConfig.java    # WebSocket with STOMP setup
│   │   │   │   │   └── KafkaConfig.java        # Kafka producer/consumer config
│   │   │   │   ├── controller/
│   │   │   │   │   ├── IncidentController.java # REST endpoints for incident CRUD
│   │   │   │   │   └── WebSocketController.java # WebSocket message handling
│   │   │   │   ├── entity/
│   │   │   │   │   └── Incident.java           # JPA entity for incident data
│   │   │   │   ├── repository/
│   │   │   │   │   └── IncidentRepository.java # Spring Data JPA repository
│   │   │   │   ├── service/
│   │   │   │   │   └── IncidentService.java    # Business logic for incidents
│   │   │   └── resources/
│   │   │       ├── application.yml             # Config (MySQL, Redis, Kafka)
│   │   │       └── schema.sql                  # Initial DB schema
│   │   └── test/
│   │       └── java/com/example/incident/
│   │           └── IncidentControllerTest.java
│   ├── Dockerfile
│   ├── pom.xml
│   └── liquibase/
│       └── changelog.xml                # Liquibase migrations for incident schema
├── auth-service/                       # Microservice for authentication
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/com/example/auth/
│   │   │   │   ├── AuthServiceApplication.java
│   │   │   │   ├── config/
│   │   │   │   │   └── SecurityConfig.java     # JWT generation/validation
│   │   │   │   ├── controller/
│   │   │   │   │   └── AuthController.java     # Login, token refresh endpoints
│   │   │   │   ├── service/
│   │   │   │   │   └── AuthService.java        # JWT and user auth logic
│   │   │   └── resources/
│   │   │       └── application.yml             # Config (Eureka, MySQL)
│   │   └── test/
│   │       └── java/com/example/auth/
│   │           └── AuthControllerTest.java
│   ├── Dockerfile
│   └── pom.xml
├── ai-service/                         # Microservice for AI-driven features
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/com/example/ai/
│   │   │   │   ├── AiServiceApplication.java
│   │   │   │   ├── config/
│   │   │   │   │   └── KafkaConfig.java        # Kafka consumer for incident events
│   │   │   │   ├── controller/
│   │   │   │   │   └── AiController.java       # REST endpoints for AI predictions
│   │   │   │   ├── service/
│   │   │   │   │   └── AiService.java          # Logic for AI predictions
│   │   │   └── resources/
│   │   │       ├── application.yml             # Config (Kafka, external AI API)
│   │   │       └── model/                      # Placeholder for AI model files
│   │   └── test/
│   │       └── java/com/example/ai/
│   │           └── AiControllerTest.java
│   ├── Dockerfile
│   └── pom.xml
├── gateway/                            # Spring Cloud Gateway for API routing
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/com/example/gateway/
│   │   │   │   ├── GatewayApplication.java
│   │   │   │   ├── config/
│   │   │   │   │   └── RouteConfig.java        # API routing and filters
│   │   │   └── resources/
│   │   │       └── application.yml             # Config (Eureka, routes)
│   │   └── test/
│   │       └── java/com/example/gateway/
│   │           └── GatewayTest.java
│   ├── Dockerfile
│   └── pom.xml
├── frontend/                           # Angular frontend
│   ├── src/
│   │   ├── app/
│   │   │   ├── components/
│   │   │   │   ├── login/
│   │   │   │   │   ├── login.component.ts
│   │   │   │   │   ├── login.component.html
│   │   │   │   │   └── login.component.scss
│   │   │   │   ├── register/
│   │   │   │   │   ├── register.component.ts
│   │   │   │   │   ├── register.component.html
│   │   │   │   │   └── register.component.scss
│   │   │   │   ├── forgot-password/
│   │   │   │   │   ├── forgot-password.component.ts
│   │   │   │   │   ├── forgot-password.component.html
│   │   │   │   │   └── forgot-password.component.scss
│   │   │   │   ├── incident/
│   │   │   │   │   ├── incident-list/
│   │   │   │   │   │   ├── incident-list.component.ts
│   │   │   │   │   │   ├── incident-list.component.html
│   │   │   │   │   │   └── incident-list.component.scss
│   │   │   │   │   └── incident-form/
│   │   │   │   │       ├── incident-form.component.ts
│   │   │   │   │       ├── incident-form.component.html
│   │   │   │   │       └── incident-form.component.scss
│   │   │   ├── services/
│   │   │   │   ├── auth.service.ts             # Handles authentication
│   │   │   │   ├── incident.service.ts         # API calls for incidents
│   │   │   │   └── websocket.service.ts        # WebSocket connection
│   │   │   ├── models/
│   │   │   │   ├── user.model.ts               # User interface
│   │   │   │   └── incident.model.ts           # Incident interface
│   │   │   ├── app.module.ts                   # Main module
│   │   │   ├── app-routing.module.ts           # Routing configuration
│   │   │   └── app.component.ts                # Root component
│   │   ├── assets/                             # Static assets (images, etc.)
│   │   ├── environments/
│   │   │   ├── environment.ts                  # Dev config
│   │   │   └── environment.prod.ts             # Prod config
│   │   ├── index.html                          # Main HTML file
│   │   ├── main.ts                             # Angular bootstrap
│   │   └── styles.scss                         # Global styles (Tailwind CSS)
│   ├── angular.json                            # Angular CLI config
│   ├── package.json                            # Node dependencies (stompjs, etc.)
│   ├── tsconfig.json                           # TypeScript config
│   └── Dockerfile                              # Docker config for frontend
├── scripts/                                    # Utility scripts
│   ├── setup-kafka.sh                          # Kafka setup script
│   ├── init-db.sh                              # Database initialization
│   └── build-all.sh                            # Build all services
├── README.md                                   # Project documentation
└── pom.xml                                     # Parent Maven POM for shared dependencies
