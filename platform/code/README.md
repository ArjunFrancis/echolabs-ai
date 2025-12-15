# EchoLabs Platform - Backend Code Directory

> **Purpose:** Core backend implementation for LLM/AI agent evaluation, monitoring, and compliance platform

**Status:** ⚠️ Skeleton - Ready for Phase 1 Implementation  
**Last Updated:** December 15, 2025  
**Implementation Phase:** Phase 1 - MVP Launch (Weeks 1-12)  
**Framework:** FastAPI (Python 3.11+)  
**Database:** PostgreSQL 15+, Redis

---

## Overview

This directory contains the complete backend implementation for EchoLabs AI platform:
- **REST API** - FastAPI application with 40+ endpoints
- **Evaluation Engine** - LLM output evaluation and testing
- **Monitoring System** - Real-time agent performance tracking
- **Data Management** - Dataset versioning, storage, retrieval
- **Compliance Engine** - NDMO, DIFC, ADGM regulatory checking

**Architecture Pattern:** Modular FastAPI application with service layer, repository pattern, and dependency injection.

---

## Directory Structure (Phase 1)

```
platform/code/
│
├── main.py                          # FastAPI application entrypoint
│
├── api/
│   ├── __init__.py
│   ├── routes/                      # API endpoint handlers
│   │   ├── __init__.py
│   │   ├── evaluations.py           # Evaluation endpoints (POST, GET, list)
│   │   ├── agents.py                # Agent management endpoints
│   │   ├── datasets.py              # Dataset upload, list, delete
│   │   ├── monitoring.py            # Real-time monitoring endpoints
│   │   ├── compliance.py            # Compliance checking endpoints
│   │   ├── admin.py                 # Admin portal APIs
│   │   ├── auth.py                  # Authentication endpoints
│   │   └── health.py                # Health check endpoints
│   ├── schemas/                     # Pydantic request/response models
│   │   ├── __init__.py
│   │   ├── evaluation.py            # Evaluation DTOs
│   │   ├── agent.py                 # Agent DTOs
│   │   ├── dataset.py               # Dataset DTOs
│   │   ├── monitoring.py            # Monitoring DTOs
│   │   ├── compliance.py            # Compliance DTOs
│   │   ├── user.py                  # User/auth DTOs
│   │   └── error.py                 # Error response models
│   ├── dependencies.py              # Dependency injection (DB, auth, etc.)
│   └── middleware.py                # Request/response middleware
│
├── core/
│   ├── __init__.py
│   ├── config.py                    # Configuration (env vars, settings)
│   ├── security.py                  # JWT, encryption utilities
│   ├── constants.py                 # App-wide constants
│   └── enums.py                     # Enums (evaluation types, etc.)
│
├── models/
│   ├── __init__.py                  # SQLAlchemy ORM models
│   ├── base.py                      # Base model with timestamps
│   ├── user.py                      # User model
│   ├── organization.py              # Organization model
│   ├── project.py                   # Project model
│   ├── evaluation.py                # Evaluation model
│   ├── dataset.py                   # Dataset model
│   ├── agent.py                     # Agent model
│   ├── compliance_report.py         # Compliance report model
│   └── audit_log.py                 # Audit log model
│
├── services/
│   ├── __init__.py                  # Business logic layer
│   ├── evaluation_service.py        # Evaluation logic
│   ├── agent_service.py             # Agent management logic
│   ├── dataset_service.py           # Dataset management logic
│   ├── monitoring_service.py        # Monitoring and metrics logic
│   ├── compliance_service.py        # Compliance checking logic
│   ├── user_service.py              # User management logic
│   └── notification_service.py      # Email/Slack notifications
│
├── repositories/
│   ├── __init__.py                  # Data access layer (Repository pattern)
│   ├── base_repository.py           # Base CRUD operations
│   ├── evaluation_repository.py
│   ├── dataset_repository.py
│   ├── agent_repository.py
│   ├── user_repository.py
│   └── compliance_repository.py
│
├── eval_engine/                     # Evaluation engine core
│   ├── __init__.py
│   ├── evaluator.py                 # Main evaluator orchestrator
│   ├── evaluators/                  # Specific evaluator implementations
│   │   ├── __init__.py
│   │   ├── quality_evaluator.py     # Text quality (accuracy, coherence)
│   │   ├── bias_evaluator.py        # Bias detection
│   │   ├── safety_evaluator.py      # Safety filter evaluation
│   │   ├── reasoning_evaluator.py   # Reasoning capability assessment
│   │   └── tool_use_evaluator.py    # Tool-use validation
│   ├── metrics/                     # Evaluation metrics
│   │   ├── __init__.py
│   │   ├── accuracy_metrics.py
│   │   ├── bias_metrics.py
│   │   ├── safety_metrics.py
│   │   └── custom_metrics.py
│   └── llm_integration/             # LLM provider integration
│       ├── __init__.py
│       ├── openai_client.py         # OpenAI integration
│       ├── anthropic_client.py      # Anthropic integration
│       ├── local_llm_client.py      # Local LLM support
│       └── base_client.py           # Base LLM client interface
│
├── monitoring/                      # Monitoring & observability
│   ├── __init__.py
│   ├── metrics_collector.py         # Prometheus metrics
│   ├── performance_tracker.py       # Agent performance tracking
│   ├── error_detector.py            # Error detection and alerting
│   ├── cost_tracker.py              # Token/cost tracking
│   └── audit_logger.py              # Audit trail logging
│
├── compliance/                      # Compliance checking
│   ├── __init__.py
│   ├── compliance_checker.py        # Main compliance orchestrator
│   ├── checkers/                    # Regulatory compliance checkers
│   │   ├── __init__.py
│   │   ├── ndmo_checker.py          # NDMO (National Data Management Office)
│   │   ├── difc_checker.py          # DIFC Data Protection Law
│   │   ├── adgm_checker.py          # ADGM regulations
│   │   ├── bias_checker.py          # Bias compliance
│   │   └── privacy_checker.py       # Privacy compliance
│   ├── rules/                       # Compliance rules (versioned)
│   │   ├── ndmo_rules.json
│   │   ├── difc_rules.json
│   │   └── adgm_rules.json
│   └── reports/                     # Report generation
│       ├── compliance_report_generator.py
│       ├── audit_report_generator.py
│       └── templates/               # PDF/HTML report templates
│
├── tasks/                           # Celery tasks (async jobs)
│   ├── __init__.py
│   ├── celery_app.py                # Celery configuration
│   ├── evaluation_tasks.py          # Async evaluation tasks
│   ├── compliance_tasks.py          # Async compliance tasks
│   ├── monitoring_tasks.py          # Async monitoring tasks
│   └── notification_tasks.py        # Async notification tasks
│
├── utils/                           # Utility functions
│   ├── __init__.py
│   ├── validators.py                # Input validation
│   ├── formatters.py                # Data formatting
│   ├── decorators.py                # Custom decorators
│   ├── exceptions.py                # Custom exception classes
│   └── logger.py                    # Logging configuration
│
├── db/
│   ├── __init__.py
│   ├── session.py                   # Database session management
│   ├── migrations/                  # Alembic database migrations
│   │   ├── versions/                # Migration files
│   │   ├── env.py
│   │   └── script.py.mako
│   └── seed_data.py                 # Database seed scripts
│
├── tests/                           # Test suite
│   ├── __init__.py
│   ├── conftest.py                  # Pytest configuration and fixtures
│   ├── unit/                        # Unit tests
│   │   ├── test_evaluators.py
│   │   ├── test_compliance.py
│   │   ├── test_services.py
│   │   └── test_utils.py
│   ├── integration/                 # Integration tests
│   │   ├── test_api_endpoints.py
│   │   ├── test_database.py
│   │   └── test_external_apis.py
│   └── fixtures/                    # Test data and fixtures
│       ├── sample_evaluations.json
│       ├── sample_datasets.json
│       └── sample_agents.json
│
├── requirements.txt                 # Python dependencies
├── .env.example                     # Example environment variables
├── docker-compose.yml               # Local development stack
├── Dockerfile                       # Production image
└── README.md                        # This file
```

---

## Tech Stack & Dependencies

### **Core Framework**
- **FastAPI 0.104+** - Modern async web framework
- **Uvicorn 0.24+** - ASGI server
- **Pydantic 2.0+** - Data validation and serialization

### **Database**
- **SQLAlchemy 2.0+** - ORM
- **Alembic 1.12+** - Database migrations
- **psycopg2-binary** - PostgreSQL driver
- **redis** - Caching and task queue

### **Task Queue**
- **Celery 5.3+** - Distributed task queue
- **Flower** - Celery monitoring dashboard

### **LLM Integration**
- **langchain 0.1+** - LLM orchestration
- **openai** - OpenAI API client
- **anthropic** - Anthropic API client

### **Monitoring & Observability**
- **prometheus-client** - Prometheus metrics
- **structlog** - Structured logging
- **sentry-sdk** - Error tracking
- **python-json-logger** - JSON logging

### **Testing**
- **pytest 7.4+** - Test framework
- **pytest-cov** - Code coverage
- **pytest-asyncio** - Async test support
- **httpx** - HTTP client for testing

### **Development**
- **black** - Code formatting
- **pylint** - Code linting
- **isort** - Import sorting
- **mypy** - Type checking
- **python-dotenv** - Environment variables

---

## Getting Started

### **Prerequisites**
- Python 3.11+
- PostgreSQL 15+
- Redis 7+
- Docker & Docker Compose (optional but recommended)

### **Local Setup**

```bash
# 1. Set up environment
cd platform/code
cp .env.example .env
# Edit .env with local database credentials

# 2. Create virtual environment
python3.11 -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Start services (Docker)
docker-compose up -d postgres redis celery-worker

# 5. Run migrations
alembic upgrade head

# 6. Start development server
uvicorn main:app --reload --port 8000
```

**API Documentation:** http://localhost:8000/docs (Swagger UI)

---

## API Endpoints (Phase 1)

### **Evaluation Endpoints**
```
POST   /api/v1/evaluations              # Create evaluation
GET    /api/v1/evaluations/{id}         # Get evaluation
GET    /api/v1/evaluations              # List evaluations
DELETE /api/v1/evaluations/{id}         # Delete evaluation
```

### **Dataset Endpoints**
```
POST   /api/v1/datasets                 # Upload dataset
GET    /api/v1/datasets/{id}            # Get dataset
GET    /api/v1/datasets                 # List datasets
DELETE /api/v1/datasets/{id}            # Delete dataset
```

### **Agent Endpoints**
```
POST   /api/v1/agents                   # Create agent
GET    /api/v1/agents/{id}              # Get agent
GET    /api/v1/agents                   # List agents
PUT    /api/v1/agents/{id}              # Update agent
DELETE /api/v1/agents/{id}              # Delete agent
```

### **Monitoring Endpoints**
```
GET    /api/v1/monitoring/agents        # Agent status
GET    /api/v1/monitoring/metrics       # Platform metrics
GET    /api/v1/monitoring/errors        # Recent errors
```

### **Compliance Endpoints**
```
GET    /api/v1/compliance/check/{id}    # Check evaluation compliance
GET    /api/v1/compliance/reports       # List compliance reports
POST   /api/v1/compliance/generate      # Generate compliance report
```

**Full API specification:** See [Technical Specifications](../../deliverables/technical-specifications.md#api-endpoints)

---

## Database Models (Phase 1)

**Key Models:**
- `User` - Platform users (with roles: admin, member)
- `Organization` - Enterprise organizations
- `Project` - Organization projects
- `Evaluation` - LLM output evaluations
- `Dataset` - Test datasets (versioned)
- `Agent` - AI agents being monitored
- `ComplianceReport` - Generated compliance reports
- `AuditLog` - System activity audit trail

**Database Diagram:** See [Technical Specifications - Database Schema](../../deliverables/technical-specifications.md#database-schema)

---

## Configuration

### **Environment Variables (.env)**
```bash
# Database
DATABASE_URL=postgresql://user:password@localhost:5432/echolabs
REDIS_URL=redis://localhost:6379/0

# Application
APP_NAME=echolabs
APP_VERSION=1.0.0
ENVIRONMENT=development  # development, staging, production
DEBUG=true
SECRET_KEY=your-secret-key-here

# LLM Providers
OPENAI_API_KEY=sk-...
ANTHROPIC_API_KEY=sk-ant-...

# AWS (S3 Storage)
AWS_ACCESS_KEY_ID=...
AWS_SECRET_ACCESS_KEY=...
AWS_REGION=me-south-1  # UAE Bahrain

# Celery
CELERY_BROKER_URL=redis://localhost:6379/1
CELERY_RESULT_BACKEND=redis://localhost:6379/2

# Monitoring
SENTRY_DSN=...
DATADOG_API_KEY=...
```

---

## Testing

### **Run Tests**
```bash
# Unit tests
pytest tests/unit/ -v

# Integration tests
pytest tests/integration/ -v

# With coverage
pytest --cov=. --cov-report=html

# Specific test file
pytest tests/unit/test_evaluators.py -v
```

### **Coverage Requirements**
- **Minimum:** 80% overall
- **Critical paths:** 100% (evaluation engine, compliance checks)
- **Services:** 85%+
- **API routes:** 75%+

---

## Development Standards

### **Code Style**
- Use **Black** for formatting
- Follow **PEP 8** guidelines
- Use **type hints** throughout
- Max line length: 100 characters

### **Naming Conventions**
- Modules: `snake_case`
- Classes: `PascalCase`
- Functions/methods: `snake_case`
- Constants: `UPPER_SNAKE_CASE`
- Private methods: `_leading_underscore`

### **Logging**
- Use structured logging (structlog)
- Log levels: DEBUG, INFO, WARNING, ERROR, CRITICAL
- Include request IDs for tracing
- Never log sensitive data (API keys, passwords)

### **Error Handling**
- Use custom exceptions (see `utils/exceptions.py`)
- Return appropriate HTTP status codes
- Include error details in response (for debugging)
- Log all errors with full stack traces

---

## Performance & Scalability

### **Phase 1 Targets**
- API response time: < 500ms (p95)
- Evaluation processing: < 10 seconds per item
- Concurrent evaluations: 100+
- Database queries: < 100ms (p95)

### **Optimization Tips**
- Use database connection pooling
- Cache frequently accessed data (Redis)
- Async processing for long-running tasks (Celery)
- Pagination for list endpoints (default: 20 items)
- Use lazy loading for related objects

---

## Related Documentation

**Specifications:**
- [Evaluation Framework](../../platform/evaluation-framework.md)
- [Monitoring Architecture](../../platform/multimodal-testing-architecture.md)
- [Dataset Management](../../platform/dataset-curation-report.md)
- [Technical Specifications](../../deliverables/technical-specifications.md)

**Development:**
- [Developer Quickstart](../../DEVELOPER_QUICKSTART.md)
- [Contributing Guidelines](../../CONTRIBUTING.md) (coming soon)

---

**Directory Status:** ⚠️ Skeleton - Ready for Phase 1  
**Implementation Start:** Phase 1, Week 1  
**Last Updated:** December 15, 2025  
**Maintainer:** EchoLabs Backend Team
