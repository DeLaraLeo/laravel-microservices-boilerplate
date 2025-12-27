# Laravel Microservices Boilerplate

A production-ready Laravel boilerplate designed to serve as a template for creating microservices. This boilerplate includes Docker configuration, DDD structure preparation, base configurations, and comprehensive documentation.

## Features

- ✅ **Laravel 12.x** - Latest stable Laravel framework
- ✅ **PHP 8.3** - Modern PHP with FPM support
- ✅ **PostgreSQL** - Production-ready database
- ✅ **Redis** - Caching and session storage
- ✅ **RabbitMQ** - Message queue support
- ✅ **DDD Structure** - Domain-Driven Design folder structure prepared
- ✅ **Docker Ready** - Dockerfile included (docker-compose.yml será criado no projeto infra)
- ✅ **Health Check** - Built-in health check endpoint
- ✅ **Testing** - PHPUnit test suite configured
- ✅ **Documentation** - Comprehensive docs templates

## Quick Start

### Prerequisites

- PHP >= 8.2
- Composer
- PostgreSQL >= 16 (or use Docker)
- Redis >= 7.2 (or use Docker)

### Installation

1. **Clone the repository**

```bash
git clone https://github.com/DeLaraLeo/laravel-microservices-boilerplate.git
cd laravel-microservices-boilerplate
```

2. **Run the setup script**

```bash
chmod +x scripts/setup.sh
./scripts/setup.sh
```

The setup script will:
- Create `.env` from `.env.example` if it doesn't exist
- Install Composer dependencies
- Generate application key
- Run database migrations
- Clear caches

3. **Update `.env` file** (if needed)

Set your database, Redis, and other service configurations according to your environment.

4. **Run the service**

**Important**: This boilerplate is designed to run with **PHP-FPM (port 9000)** via Docker. The services are orchestrated by docker-compose in the `microservices-infra` project.

For quick local testing without Docker (not recommended for production):

```bash
php artisan serve
```

Visit `http://localhost:8000/api/health` to verify the API is running.

**Note**: For proper microservices setup, use Docker with PHP-FPM. See the `microservices-infra` project for complete Docker orchestration.

## Using This Boilerplate

This boilerplate is designed to be cloned and customized for each microservice. Here's how to use it:

### 1. Clone for a New Service

```bash
git clone https://github.com/DeLaraLeo/laravel-microservices-boilerplate.git your-service-name
cd your-service-name
rm -rf .git
git init
```

### 2. Customize the Service

- Update `composer.json` with your service name
- Modify `.env.example` with service-specific configurations
- Update `README.md` with service-specific documentation
- Customize `docs/` files with your service architecture
- Add your service-specific routes, controllers, and models

### 3. Update Configuration

- Change `APP_NAME` in `.env.example`
- Update `APP_URL` with the correct port (8001-8007)
- Configure service-specific database settings if needed

## Docker

### Dockerfile

The boilerplate includes a `Dockerfile` configured for PHP 8.3-FPM with all necessary extensions:

- PostgreSQL (pdo_pgsql, pgsql)
- Redis
- BCMath
- GD
- Zip
- Intl

### Building with Docker

**Important**: The `docker-compose.yml` file will be created in the `microservices-infra` project, not in this boilerplate. Each service has its own Dockerfile, and the docker-compose.yml will orchestrate all services together.

You can build the Docker image for this service:

```bash
docker build -t laravel-boilerplate .
```

**Note**: To run this service properly, you need PostgreSQL and Redis. The complete Docker setup with all services and infrastructure is in the `microservices-infra` project.

## Project Structure

```
laravel-microservices-boilerplate/
├── app/
│   ├── Domain/              # DDD Domain Layer
│   │   ├── Entities/
│   │   ├── ValueObjects/
│   │   ├── Services/
│   │   ├── Repositories/
│   │   └── Events/
│   ├── Application/         # DDD Application Layer
│   │   ├── DTOs/
│   │   ├── UseCases/
│   │   └── Services/
│   ├── Infrastructure/      # DDD Infrastructure Layer
│   │   ├── Persistence/
│   │   └── Providers/
│   ├── Presentation/        # DDD Presentation Layer
│   │   └── Http/
│   ├── Http/                # Laravel Standard Structure
│   │   ├── Controllers/
│   │   ├── Middleware/
│   │   ├── Requests/
│   │   └── Resources/
│   ├── Models/
│   └── Services/
├── config/
├── database/
├── docs/                    # Documentation templates
├── postman/                 # Postman collection
├── routes/
│   └── api.php             # API routes
├── scripts/
│   └── setup.sh            # Setup automation script
├── tests/
│   └── Feature/
│       └── HealthCheckTest.php
├── Dockerfile
└── README.md
```

## API Endpoints

### Health Check

```bash
GET /api/health
```

Response:

```json
{
  "status": "ok",
  "service": "Laravel",
  "timestamp": "2024-01-01T00:00:00+00:00",
  "environment": "local"
}
```

## Testing

Run the test suite:

```bash
php artisan test
```

Run with coverage:

```bash
php artisan test --coverage
```

## Documentation

- [Getting Started](docs/GETTING_STARTED.md) - Setup and installation guide
- [Architecture](docs/ARCHITECTURE.md) - Architecture documentation template
- [Error Codes](docs/ERRORS.md) - Error codes documentation template
- [Examples](docs/EXAMPLES.md) - Code examples template

## Postman Collection

Import `postman/collection.json` into Postman to get started with API testing.

Global variables:
- `{{base_url}}` - API base URL (default: http://localhost:8000)
- `{{token}}` - Authentication token
- `{{api_key}}` - API key (if needed)

## Configuration

### Database

Default connection: PostgreSQL

```env
DB_CONNECTION=pgsql
DB_HOST=postgres
DB_PORT=5432
DB_DATABASE=laravel_development
DB_USERNAME=postgres
DB_PASSWORD=postgres
```

### Cache

Default driver: Redis

```env
CACHE_DRIVER=redis
REDIS_HOST=redis
REDIS_PORT=6379
```

### Queue

Default connection: Redis

```env
QUEUE_CONNECTION=redis
```

RabbitMQ is also configured (optional):

```env
RABBITMQ_HOST=rabbitmq
RABBITMQ_PORT=5672
RABBITMQ_USER=guest
RABBITMQ_PASSWORD=guest
```

### Authentication

Laravel Sanctum is installed and configured for JWT authentication.
