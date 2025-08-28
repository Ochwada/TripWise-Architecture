# ✈️ TripWise System - The Architecture


*A 3-Week Study & Development Plan (Team of 3–4)*

TripWise System is a compact roadmap project that merges the best of JetSetGo (trip planning, packing, currency, phrases, 
weather) and CityTrip Companion (city search, weather, and journaling with photos).

Built for learning and collaboration, the project emphasizes Spring Boot 3, PostgreSQL + MongoDB, JWT/OAuth2, Docker, 
and AWS EC2 deployment with CI/CD pipelines via GitHub Actions.

## Overview
This system consists of 5 microservices:

| Microservice                                                                      | Role / Service               | Database | Port | Status         | Done By                                             |
|-----------------------------------------------------------------------------------|------------------------------|----------|------|----------------|-----------------------------------------------------|
| [**Gateway   Service**]( )                                                        | Microservice 0 : TripHub     | -        | 9090 | 🧠 Planning    | [** **]()                                           |
| [**Authentication  Service**](https://github.com/Ochwada/TripWise-Pass)           | Microservice 1 : TripPass    | ✗        | 9091 | ✅ Done         | [**Ochwada**](https://github.com/Ochwada)           |
| [**User  Profile Service**](https://github.com/reyhanovelek/TripProfile-Service)  | Microservice 2 : TripProfile | -        | 9092 | 🚧 in Progress | [**Reyhan**](https://github.com/reyhanovelek)       |
| [**Itinerary Service**](https://github.com/Jind19/TripWise_Planner)               | Microservice 3 : TripPlanner | -        | 9093 | 🚧 in Progress | [**Prachi**]()                                      |
| [**Journal / activities  Service**](https://github.com/Ochwada/TripWise-Journal)  | Microservice 4 : TripJournal | -        | 9094 | 🚧 in Progress | [**Ochwada**](https://github.com/Ochwada)           |
| [**Weather  Service**](https://github.com/OrnellaDelVicario/tripwise_tripweather) | Microservice 5 : TripWeather | -        | 9095 | 🚧 in Progress | [**Ornella**](https://github.com/OrnellaDelVicario) |
| [**Media   Service**](https://github.com/Ochwada/TripWise-Media)                  | Microservice 6 : Tripmedia   | -        | 9096 | ✅ Done         | [**Ochwada**](https://github.com/Ochwada)           |                                    |


Each service is independently deployable and communicates over REST APIs. Docker is used for containerization and
orchestration is done using **Docker Compose**.

## 🎯Target Outcome (Definition of Done)
 TripWise allows:

- User Authentication — JWT-based login. 
- Trip Management — create a trip (city + dates) and fetch live weather for that city. 
- Packing List — maintain a per-trip checklist. 
- Activity Journal — add activity entries (date, note, city), upload photos, and store a temperature snapshot at entry time. 
- Optional Utilities (nice-to-haves):
  - Currency converter 
- DevOps / Infrastructure 
  - All services Dockerized → runnable via docker-compose locally and on EC2 
  - OpenAPI/Swagger docs per service 
  - GitHub Actions CI (build + static checks on PRs)
  - GitHub Actions CD (deploy on tag → EC2)

## Common Tech Stack

| Technology          | Purpose                                                                      |
|---------------------|------------------------------------------------------------------------------|
| **Java 17+**        | Modern programming language used to build the microservice                   |
| **Spring Boot**     | Framework for rapid application development and configuration                |
| **Spring Security** | Handles authentication, authorization, and protection against common attacks |
| **OAuth2 (OIDC)**   | Secure login flow using Google as a trusted identity provider                |
| **Maven**           | Dependency and build management tool for Java projects                       |
| **Docker**          | Containerization for service and database                                    |

### Common Dependencies
| Dependency Artifact                 | Purpose                                                                 |
|-------------------------------------|-------------------------------------------------------------------------|
| `spring-boot-starter-oauth2-client` | Enables OAuth2 login (e.g. Google), and integrates with OpenID Connect  |
| `spring-boot-starter-security`      | Adds Spring Security for securing endpoints, sessions, and roles        |
| `spring-boot-starter-thymeleaf`     | Provides Thymeleaf support for rendering HTML views on the server side  |
| `spring-boot-starter-validation`    | Enables Java Bean Validation (e.g., `@Valid`, `@Email`, etc.)           |
| `spring-boot-starter-web`           | Core starter for RESTful web applications using Spring MVC              |
| `lombok`                            | Reduces boilerplate by auto-generating code like getters, setters, etc. |
| `spring-boot-starter-test`          | Includes tools like JUnit, Mockito, AssertJ for unit/integration tests  |
| `spring-security-test`              | Adds support for testing Spring Security (e.g., mocking users/roles)    |
| `dotenv-java`                       | Loads environment variables from `.env` file at runtime                 |

---

## 🚀 Getting Started

### Prerequisites
- Docker + Docker Compose installed
- Git installed
- Java 17+ and Maven (for local builds, if needed)


### Step 1: Clone the Repositories

```bash 
# Auth service
git clone https://github.com/Ochwada/TripWise-Pass.git trippass-service
git clone https://github.com/reyhanovelek/TripProfile-Service.git tripprofile-service
git clone https://github.com/Jind19/TripWise_Planner.git tripplanner-service
git clone https://github.com/Ochwada/TripWise-Journal.git tripjournal-service
git clone https://github.com/OrnellaDelVicario/tripwise_tripweather.git tripweather-service
git clone https://github.com/Ochwada/TripWise-Media.git tripmedia-service
```

### Step 2: Environment Variables / Environment Configurations
Each service includes a `.env` file with required configuration.

### Step 3 Data Persistence

- MongoDB data is stored in mongo_data volume
- PostgreSQL data is stored in pg_data volume

### Step 4 Dockerization
Ensure you have a `Dockerfile` and `docker-compose.yml`
Then run with :
```yaml
#Creates a user-defined bridge network called tripwise-backend.
docker network create -d bridge tripwise-backend

#Verify the network exists
docker network ls

docker-compose build --no-cache    # Rebuild all images from scratch
docker-compose up


# Remove volumes & orphan containers
docker-compose down --volumes --remove-orphans  
```

You can verify volumes using:
```bash
docker volume ls
```
