<a name="readme-top"></a>

<!-- PROJECT SHIELDS -->
[![GitHub last commit](https://img.shields.io/github/last-commit/digitalcloudninja/discovery.svg?style=for-the-badge)](https://github.com/digitalcloudninja/discovery/commits/main)
[![GitHub Tag](https://img.shields.io/github/v/tag/digitalcloudninja/discovery.svg?style=for-the-badge)](https://github.com/digitalcloudninja/discovery/tags)
[![GitHub forks](https://img.shields.io/github/forks/digitalcloudninja/discovery.svg?style=for-the-badge)](https://github.com/digitalcloudninja/discovery/network/members)
[![GitHub stars](https://img.shields.io/github/stars/digitalcloudninja/discovery.svg?style=for-the-badge)](https://github.com/digitalcloudninja/discovery/stargazers)
[![License](https://img.shields.io/github/license/digitalcloudninja/discovery.svg?style=for-the-badge)](https://github.com/digitalcloudninja/discovery/blob/main/LICENSE)

<!-- TECHNOLOGY BADGES -->
[![Java JDK 22](https://img.shields.io/badge/java-F80000?style=for-the-badge&logo=oracle&logoColor=white)](https://www.oracle.com/java/)
[![Gradle 8.8](https://img.shields.io/badge/gradle-02303A?style=for-the-badge&logo=gradle&logoColor=white)](https://docs.gradle.org/current/userguide/userguide.html)
[![Spring](https://img.shields.io/badge/spring-6DB33F?style=for-the-badge&logo=spring&logoColor=white)](https://spring.io/)
[![Spring Cloud](https://img.shields.io/badge/spring_cloud-6DB33F?style=for-the-badge&logo=spring&logoColor=white)](https://spring.io/projects/spring-cloud)
[![Netflix Eureka](https://img.shields.io/badge/eureka-E50914?style=for-the-badge&logo=netflix&logoColor=white)](https://github.com/Netflix/eureka)
[![Docker](https://img.shields.io/badge/docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://www.docker.com/)

<br />
<div align="center">
  <a href="https://github.com/digitalcloudninja/discovery">
    <img src="https://avatars.githubusercontent.com/u/174159620?v=4" alt="Logo" width="80" height="80">
  </a>

  <h3 align="center">Eureka Discovery Service</h3>

  <p align="center">
    A Netflix Eureka Discovery Server for Container Applications
    <br />
    Service Registry and Discovery for Microservices Architecture
    <br />
    <br />
    <a href="https://github.com/digitalcloudninja/discovery"><strong>Explore the Documentation »</strong></a>
    <br />
    <br />
    <a href="https://github.com/digitalcloudninja/discovery/issues">Report Bug</a>
    ·
    <a href="https://github.com/digitalcloudninja/discovery/issues">Request Feature</a>
  </p>
</div>

<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li><a href="#about-the-project">About The Project</a></li>
    <li><a href="#features">Features</a></li>
    <li><a href="#architecture">Architecture</a></li>
    <li><a href="#built-with">Built With</a></li>
    <li><a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#installation">Installation</a></li>
      </ul>
    </li>
    <li><a href="#usage">Usage</a></li>
    <li><a href="#configuration">Configuration</a></li>
    <li><a href="#deployment">Deployment</a></li>
    <li><a href="#client-integration">Client Integration</a></li>
    <li><a href="#monitoring">Monitoring</a></li>
    <li><a href="#high-availability">High Availability</a></li>
    <li><a href="#troubleshooting">Troubleshooting</a></li>
    <li><a href="#contributing">Contributing</a></li>
    <li><a href="#license">License</a></li>
    <li><a href="#contact">Contact</a></li>
  </ol>
</details>

## About The Project

The Discovery Service is a production-ready Netflix Eureka Server implementation designed specifically for containerized microservices architectures. It provides a robust service registry and discovery mechanism that enables microservices to find and communicate with each other dynamically, without hard-coding hostnames and ports.

### What is Service Discovery?

In a microservices architecture, services need to discover and communicate with each other. Service discovery solves this problem by maintaining a registry of available service instances and their locations, enabling:

- **Dynamic Service Location**: Services register themselves on startup and are automatically discoverable
- **Load Balancing**: Client-side load balancing across multiple service instances
- **Fault Tolerance**: Automatic removal of failed instances from the registry
- **Horizontal Scaling**: Easy addition and removal of service instances

### Why Netflix Eureka?

- ✅ **Battle-Tested**: Used by Netflix in production for years
- ✅ **Spring Cloud Native**: Seamless integration with Spring Cloud ecosystem
- ✅ **Self-Preservation**: Protects against network partitions
- ✅ **REST-Based**: Simple HTTP-based communication
- ✅ **High Availability**: Supports peer-to-peer replication

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Features

### Core Capabilities

- 🔍 **Service Registry**: Central registry for all microservice instances
- 🔄 **Automatic Registration**: Services auto-register on startup
- 💓 **Health Monitoring**: Heartbeat-based health checks
- 🔌 **Service Discovery**: Dynamic lookup of service instances
- ⚖️ **Load Balancing**: Client-side load balancing support
- 🛡️ **Self-Preservation Mode**: Network partition protection
- 📊 **Dashboard UI**: Web-based monitoring interface
- 🐳 **Container-Ready**: Optimized for Docker and Kubernetes
- 🔄 **Peer Replication**: Multi-node cluster support
- 📡 **REST API**: Comprehensive REST endpoints for service management

### Security Features

- 🔐 Basic Authentication support
- 🔒 HTTPS/TLS encryption
- 🚫 IP whitelisting
- 🔑 Service-level authentication

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Architecture

### Service Discovery Pattern

```
┌─────────────────────────────────────────────────────────────┐
│                     Eureka Server                           │
│                  (Discovery Service)                        │
│                                                             │
│  ┌──────────────────────────────────────────────────────┐  │
│  │           Service Registry                           │  │
│  │  • service-a: [instance-1, instance-2]              │  │
│  │  • service-b: [instance-1, instance-2, instance-3]  │  │
│  │  • service-c: [instance-1]                          │  │
│  └──────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────┘
         ↑                    ↑                    ↑
         │ Register           │ Heartbeat          │ Discover
         │                    │                    │
    ┌────┴────┐          ┌────┴────┐          ┌────┴────┐
    │Service A│          │Service B│          │Service C│
    │Instance1│          │Instance1│          │Instance1│
    └─────────┘          └─────────┘          └─────────┘
```

### How It Works

1. **Service Registration**: Microservices register with Eureka on startup
2. **Heartbeat**: Services send periodic heartbeats (default: 30 seconds)
3. **Service Discovery**: Clients query Eureka to find service instances
4. **Caching**: Clients cache the registry locally and refresh periodically
5. **Deregistration**: Services unregister gracefully on shutdown

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Built With

This project leverages:

* [![Java][Java-badge]][Java-url] **Java 22** - Modern Java runtime
* [![Spring Boot][Spring-badge]][Spring-url] **Spring Boot 3.x** - Application framework
* [![Spring Cloud][SpringCloud-badge]][SpringCloud-url] **Spring Cloud Netflix** - Eureka implementation
* [![Gradle][Gradle-badge]][Gradle-url] **Gradle 8.8** - Build automation
* [![Docker][Docker-badge]][Docker-url] **Docker** - Containerization

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Getting Started

### Prerequisites

- **Java Development Kit (JDK) 22**
  ```bash
  java -version
  # Should output: java version "22.x.x"
  ```

- **Docker** (for containerized deployment)
  ```bash
  docker --version
  # Should output: Docker version 20.x.x or higher
  ```

- **Gradle** (optional - wrapper included)
  ```bash
  gradle --version
  # Should output: Gradle 8.8 or higher
  ```

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/digitalcloudninja/discovery.git
   cd discovery
   ```

2. **Build the project**
   ```bash
   # Using Gradle wrapper (recommended)
   ./gradlew build
   
   # Or with Gradle installed
   gradle build
   ```

3. **Run locally**
   ```bash
   # Using Gradle
   ./gradlew bootRun
   
   # Or run the JAR
   java -jar build/libs/discovery-*.jar
   ```

4. **Access the Eureka Dashboard**
   
   Open your browser and navigate to:
   ```
   http://localhost:8761
   ```

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Usage

### Starting the Discovery Server

**Option 1: Using Gradle**
```bash
./gradlew bootRun
```

**Option 2: Using Docker**
```bash
# Build the image
docker build -t discovery-service:latest .

# Run the container
docker run -d \
  -p 8761:8761 \
  --name eureka-server \
  discovery-service:latest
```

**Option 3: Using Docker Compose**
```bash
docker compose up -d
```

### Accessing the Dashboard

The Eureka Dashboard provides a web interface to monitor registered services:

```
http://localhost:8761
```

**Dashboard Features:**
- View all registered service instances
- Check service health status
- Monitor heartbeat status
- View instance metadata
- Track registration/renewal statistics

### REST API Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/eureka/apps` | GET | List all registered applications |
| `/eureka/apps/{appId}` | GET | Get specific application instances |
| `/eureka/apps/{appId}/{instanceId}` | GET | Get specific instance details |
| `/eureka/apps/{appId}` | POST | Register new instance |
| `/eureka/apps/{appId}/{instanceId}` | PUT | Send heartbeat (renew) |
| `/eureka/apps/{appId}/{instanceId}` | DELETE | Deregister instance |

### Example: Query Registered Services

```bash
# Get all applications
curl http://localhost:8761/eureka/apps

# Get specific application
curl http://localhost:8761/eureka/apps/MY-SERVICE

# Accept JSON response
curl -H "Accept: application/json" \
  http://localhost:8761/eureka/apps
```

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Configuration

### Basic Configuration

Edit `src/main/resources/application.properties` or `application.yml`:

```yaml
# Server Configuration
server:
  port: 8761

# Eureka Server Configuration
eureka:
  instance:
    hostname: localhost
    prefer-ip-address: false
  
  client:
    register-with-eureka: false  # Don't register itself
    fetch-registry: false         # Don't fetch registry
    service-url:
      defaultZone: http://${eureka.instance.hostname}:${server.port}/eureka/
  
  server:
    enable-self-preservation: true
    eviction-interval-timer-in-ms: 60000
    renewal-percent-threshold: 0.85
    
spring:
  application:
    name: discovery-service

# Logging
logging:
  level:
    com.netflix.eureka: INFO
    com.netflix.discovery: INFO
```

### Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `SERVER_PORT` | Server port | `8761` |
| `EUREKA_HOSTNAME` | Eureka hostname | `localhost` |
| `SELF_PRESERVATION` | Enable self-preservation mode | `true` |
| `EVICTION_INTERVAL` | Eviction interval (ms) | `60000` |

### Docker Configuration

```bash
docker run -d \
  -p 8761:8761 \
  -e SERVER_PORT=8761 \
  -e EUREKA_HOSTNAME=eureka-server \
  -e SELF_PRESERVATION=true \
  --name eureka-server \
  discovery-service:latest
```

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Deployment

### Docker Deployment

**Build the image:**
```bash
docker build -t discovery-service:latest .
```

**Run standalone:**
```bash
docker run -d \
  -p 8761:8761 \
  --name eureka-server \
  --restart unless-stopped \
  discovery-service:latest
```

### Docker Compose

Create `docker-compose.yml`:

```yaml
version: '3.8'

services:
  eureka-server:
    build: .
    image: discovery-service:latest
    container_name: eureka-server
    ports:
      - "8761:8761"
    environment:
      - SERVER_PORT=8761
      - EUREKA_HOSTNAME=eureka-server
    networks:
      - microservices
    restart: unless-stopped
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:8761/actuator/health"]
      interval: 30s
      timeout: 10s
      retries: 3

networks:
  microservices:
    driver: bridge
```

**Deploy:**
```bash
docker compose up -d
```

### Kubernetes Deployment

Example Kubernetes manifests:

**Deployment:**
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: eureka-server
spec:
  replicas: 2
  selector:
    matchLabels:
      app: eureka-server
  template:
    metadata:
      labels:
        app: eureka-server
    spec:
      containers:
      - name: eureka-server
        image: discovery-service:latest
        ports:
        - containerPort: 8761
        env:
        - name: SERVER_PORT
          value: "8761"
        - name: EUREKA_HOSTNAME
          valueFrom:
            fieldRef:
              fieldPath: status.podIP
        livenessProbe:
          httpGet:
            path: /actuator/health
            port: 8761
          initialDelaySeconds: 60
          periodSeconds: 30
        readinessProbe:
          httpGet:
            path: /actuator/health
            port: 8761
          initialDelaySeconds: 30
          periodSeconds: 10
```

**Service:**
```yaml
apiVersion: v1
kind: Service
metadata:
  name: eureka-server
spec:
  selector:
    app: eureka-server
  ports:
  - port: 8761
    targetPort: 8761
  type: LoadBalancer
```

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Client Integration

### Registering a Service with Eureka

**Add dependency to your microservice:**

**Gradle:**
```gradle
dependencies {
    implementation 'org.springframework.cloud:spring-cloud-starter-netflix-eureka-client'
}
```

**Maven:**
```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
</dependency>
```

**Configure client application:**

```yaml
# application.yml
spring:
  application:
    name: my-service  # This becomes the service ID

eureka:
  client:
    service-url:
      defaultZone: http://localhost:8761/eureka/
    register-with-eureka: true
    fetch-registry: true
  
  instance:
    prefer-ip-address: true
    lease-renewal-interval-in-seconds: 30
    lease-expiration-duration-in-seconds: 90
```

**Enable Eureka Client:**

```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.netflix.eureka.EnableEurekaClient;

@SpringBootApplication
@EnableEurekaClient
public class MyServiceApplication {
    public static void main(String[] args) {
        SpringApplication.run(MyServiceApplication.class, args);
    }
}
```

### Discovering and Calling Services

**Using RestTemplate with Load Balancing:**

```java
import org.springframework.cloud.client.loadbalancer.LoadBalanced;
import org.springframework.context.annotation.Bean;
import org.springframework.web.client.RestTemplate;

@Configuration
public class RestConfig {
    
    @Bean
    @LoadBalanced
    public RestTemplate restTemplate() {
        return new RestTemplate();
    }
}

@Service
public class MyService {
    
    @Autowired
    private RestTemplate restTemplate;
    
    public String callOtherService() {
        // Use service name instead of host:port
        return restTemplate.getForObject(
            "http://OTHER-SERVICE/api/endpoint", 
            String.class
        );
    }
}
```

**Using Feign Client:**

```java
import org.springframework.cloud.openfeign.FeignClient;
import org.springframework.web.bind.annotation.GetMapping;

@FeignClient(name = "OTHER-SERVICE")
public interface OtherServiceClient {
    
    @GetMapping("/api/endpoint")
    String getData();
}
```

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Monitoring

### Health Check

```bash
curl http://localhost:8761/actuator/health
```

**Response:**
```json
{
  "status": "UP"
}
```

### Metrics

Access Spring Boot Actuator metrics:

```bash
curl http://localhost:8761/actuator/metrics
```

### Dashboard Metrics

The Eureka Dashboard shows:
- Currently registered instances
- Renews threshold
- Renews (last min)
- Self-preservation mode status
- Registered replicas
- Unavailable replicas

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## High Availability

### Peer-to-Peer Replication

For production environments, run multiple Eureka servers:

**Server 1 Configuration:**
```yaml
server:
  port: 8761

eureka:
  instance:
    hostname: eureka-1
  client:
    service-url:
      defaultZone: http://eureka-2:8762/eureka/
```

**Server 2 Configuration:**
```yaml
server:
  port: 8762

eureka:
  instance:
    hostname: eureka-2
  client:
    service-url:
      defaultZone: http://eureka-1:8761/eureka/
```

**Client Configuration:**
```yaml
eureka:
  client:
    service-url:
      defaultZone: http://eureka-1:8761/eureka/,http://eureka-2:8762/eureka/
```

### Docker Compose HA Setup

```yaml
version: '3.8'

services:
  eureka-1:
    image: discovery-service:latest
    ports:
      - "8761:8761"
    environment:
      - EUREKA_HOSTNAME=eureka-1
      - PEER_EUREKA_NODES=http://eureka-2:8762/eureka/

  eureka-2:
    image: discovery-service:latest
    ports:
      - "8762:8762"
    environment:
      - EUREKA_HOSTNAME=eureka-2
      - PEER_EUREKA_NODES=http://eureka-1:8761/eureka/
```

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Troubleshooting

### Common Issues

**Issue: Services not appearing in registry**
```bash
# Check if service can reach Eureka
curl http://localhost:8761/eureka/apps

# Verify client configuration
# Ensure eureka.client.register-with-eureka=true
```

**Issue: Self-preservation mode activated**
```bash
# This is normal during network issues
# To disable (not recommended for production):
eureka.server.enable-self-preservation=false
```

**Issue: Service instances not removed**
```bash
# Reduce eviction interval
eureka.server.eviction-interval-timer-in-ms=30000
```

### Logging

Enable debug logging:

```yaml
logging:
  level:
    com.netflix.eureka: DEBUG
    com.netflix.discovery: DEBUG
```

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Contributing

Contributions are welcome! Please follow these steps:

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## License

Distributed under the Apache License 2.0. See [`LICENSE`](LICENSE) for more information.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Contact

**Digital Cloud Ninja** - [@digitalcloudninja](https://github.com/digitalcloudninja)

**Project Link**: [https://github.com/digitalcloudninja/discovery](https://github.com/digitalcloudninja/discovery)

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Acknowledgments

* [Netflix Eureka](https://github.com/Netflix/eureka)
* [Spring Cloud Netflix](https://spring.io/projects/spring-cloud-netflix)
* [Spring Boot](https://spring.io/projects/spring-boot)
* [Docker](https://www.docker.com/)

<p align="right">(<a href="#readme-top">back to top</a>)</p>

---

<div align="center">

**Made with ❤️ by Digital Cloud Ninja**

</div>

<!-- MARKDOWN LINKS & IMAGES -->
[Java-badge]: https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white
[Java-url]: https://www.oracle.com/java/
[Spring-badge]: https://img.shields.io/badge/Spring-6DB33F?style=for-the-badge&logo=spring&logoColor=white
[Spring-url]: https://spring.io/
[SpringCloud-badge]: https://img.shields.io/badge/Spring_Cloud-6DB33F?style=for-the-badge&logo=spring&logoColor=white
[SpringCloud-url]: https://spring.io/projects/spring-cloud
[Gradle-badge]: https://img.shields.io/badge/Gradle-02303A?style=for-the-badge&logo=gradle&logoColor=white
[Gradle-url]: https://gradle.org/
[Docker-badge]: https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white
[Docker-url]: https://www.docker.com/
