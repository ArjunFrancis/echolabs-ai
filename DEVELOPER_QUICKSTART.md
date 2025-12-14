# EchoLabs AI - Developer Quickstart Guide

> **Purpose:** Get developers up to speed and building **Phase 1 MVP** within 30 minutes

**Last Updated:** December 14, 2025  
**Target Audience:** Backend Engineers, Frontend Engineers, Full-Stack Developers  
**Phase Focus:** Phase 1 - MVP Launch (Weeks 1-12)

---

## 🎯 Phase 1 Mission

Build a **functional LLM/AI agent evaluation platform MVP** with:
- Core evaluation engine for text-based LLM outputs
- Real-time agent monitoring dashboard
- Basic admin portal for user/project management
- UAE compliance tracking (NDMO, DIFC, ADGM)
- Dataset management (upload, version, test)

**Success Criteria:** 5 pilot clients can evaluate their AI agents and generate compliance reports.

---

## 📚 Required Reading (30 Minutes)

### **Essential Documents (Read First):**
1. **[README.md](README.md)** - Project overview and business model
2. **[Technical Specifications](deliverables/technical-specifications.md)** - Complete developer implementation guide
3. **[MVP Feature Specs](platform/mvp-feature-specs.md)** - Phase 1 scope and user stories
4. **[Platform README](platform/README.md)** - Architecture overview

### **Deep Dive (Read as Needed):**
- [Evaluation Framework](platform/evaluation-framework.md) - Core engine architecture
- [Agent Monitoring UI](ui-design/agent-monitoring-ui.md) - Dashboard specifications
- [Admin Portal](ui-design/admin-portal.md) - Admin interface specs
- [Dataset Curation Report](platform/dataset-curation-report.md) - Data management requirements

---

## 🛠️ Tech Stack (Phase 1)

### **Backend**
- **Framework:** FastAPI (Python 3.11+)
- **Database:** PostgreSQL 15+ (primary), Redis (caching)
- **LLM Integration:** LangChain, OpenAI SDK, Anthropic SDK
- **Task Queue:** Celery + Redis
- **Evaluation:** Custom evaluation engine + HELM/LM-Eval-Harness patterns

### **Frontend**
- **Framework:** Next.js 14+ (React 18+, TypeScript)
- **UI Library:** shadcn/ui + Tailwind CSS
- **State Management:** Zustand + React Query
- **Charts/Viz:** Recharts, Tremor
- **Real-time:** Socket.IO or Server-Sent Events

### **Infrastructure**
- **Hosting:** Vercel (frontend), AWS/Azure (backend)
- **Database:** Supabase or AWS RDS (PostgreSQL)
- **Object Storage:** AWS S3 or Azure Blob Storage
- **Monitoring:** Sentry (errors), DataDog/New Relic (observability)

### **DevOps**
- **CI/CD:** GitHub Actions
- **Containerization:** Docker + Docker Compose
- **Secrets:** AWS Secrets Manager or Azure Key Vault
- **Data Residency:** UAE-based AWS/Azure regions (compliance requirement)

**Rationale:** See [Technical Specifications - Tech Stack Section](deliverables/technical-specifications.md#tech-stack-recommendations)

---

## 🚀 Getting Started (Step-by-Step)

### **Step 1: Clone & Setup**

```bash
# Clone repository
git clone https://github.com/ArjunFrancis/Echolabs-AI.git
cd Echolabs-AI

# Create Python virtual environment (backend)
python3.11 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install Python dependencies (when available)
pip install -r requirements.txt

# Install Node.js dependencies (frontend)
cd frontend
npm install
cd ..
```

### **Step 2: Environment Configuration**

Create `.env` file in project root:

```bash
# Database
DATABASE_URL=postgresql://user:password@localhost:5432/echolabs
REDIS_URL=redis://localhost:6379/0

# LLM Provider API Keys
OPENAI_API_KEY=sk-...
ANTHROPIC_API_KEY=sk-ant-...

# AWS (for S3 storage)
AWS_ACCESS_KEY_ID=...
AWS_SECRET_ACCESS_KEY=...
AWS_REGION=me-south-1  # UAE Bahrain region

# Application Settings
SECRET_KEY=your-secret-key-here
ENVIRONMENT=development
DEBUG=true

# Frontend (if separate)
NEXT_PUBLIC_API_URL=http://localhost:8000
```

### **Step 3: Local Database Setup**

```bash
# Using Docker Compose (recommended)
docker-compose up -d postgres redis

# OR install PostgreSQL locally
# Create database
createdb echolabs

# Run migrations (when available)
alembic upgrade head
```

### **Step 4: Run Development Servers**

**Backend (FastAPI):**
```bash
# From project root
cd platform/api  # or wherever backend code lives
uvicorn main:app --reload --port 8000
```

**Frontend (Next.js):**
```bash
# In separate terminal
cd frontend
npm run dev
```

**Access:**
- Frontend: http://localhost:3000
- Backend API: http://localhost:8000
- API Docs: http://localhost:8000/docs (Swagger UI)

---

## 📂 Project Structure Orientation

```
echolabs-ai/
│
├── 📁 platform/                     # Backend Implementation
│   ├── api/                        # FastAPI application
│   │   ├── main.py                # API entrypoint
│   │   ├── routers/               # API route handlers
│   │   ├── models/                # Database models (SQLAlchemy)
│   │   ├── schemas/               # Pydantic schemas
│   │   └── services/              # Business logic
│   ├── eval-engine/               # Evaluation engine core
│   │   ├── evaluators/            # LLM output evaluators
│   │   ├── metrics/               # Evaluation metrics
│   │   └── benchmarks/            # Benchmark tests
│   ├── monitoring/                # Agent monitoring system
│   └── compliance/                # Compliance checking logic
│
├── 📁 frontend/                     # Frontend Implementation
│   ├── app/                       # Next.js app directory
│   ├── components/                # React components
│   │   ├── dashboard/            # Agent monitoring dashboard
│   │   ├── admin/                # Admin portal components
│   │   └── shared/               # Reusable components
│   ├── lib/                       # Utilities and helpers
│   ├── hooks/                     # Custom React hooks
│   └── public/                    # Static assets
│
├── 📁 docs/                         # All Documentation (Read-Only)
│   ├── platform/                  # Platform specs
│   ├── ui-design/                 # UI/UX specifications
│   ├── consulting/                # Consulting frameworks
│   └── deliverables/              # Executive & technical summaries
│
├── 📁 tests/                        # Test Suite
│   ├── unit/                      # Unit tests
│   ├── integration/               # Integration tests
│   └── e2e/                       # End-to-end tests
│
├── .env                            # Environment variables (git-ignored)
├── .gitignore                      # Git ignore patterns
├── docker-compose.yml              # Local development stack
├── requirements.txt                # Python dependencies
└── README.md                       # Project overview
```

**Note:** Documentation folders (`docs/`, `platform/*.md`, etc.) are **read-only** during development. All implementation code goes in `platform/`, `frontend/`, `agents/`, etc.

---

## 🎯 Phase 1 Implementation Priorities

### **Week 1-4: Core Evaluation Engine**
**Owner:** Backend Team

**Tasks:**
1. ✅ Set up FastAPI project structure
2. ✅ Implement database models (Users, Projects, Evaluations, Datasets)
3. ✅ Build LLM integration layer (OpenAI, Anthropic)
4. ✅ Create evaluation engine core:
   - Text quality evaluator (accuracy, coherence, relevance)
   - Bias detection evaluator
   - Safety filter evaluator
5. ✅ Build dataset management API (upload, version, retrieve)
6. ✅ API endpoints for evaluation creation and retrieval

**Key Documents:**
- [Evaluation Framework](platform/evaluation-framework.md)
- [Dataset Curation Report](platform/dataset-curation-report.md)
- [Technical Specifications - Backend Section](deliverables/technical-specifications.md#backend-architecture)

---

### **Week 5-8: Agent Monitoring Dashboard**
**Owner:** Frontend Team

**Tasks:**
1. ✅ Set up Next.js project with TypeScript
2. ✅ Implement authentication (NextAuth.js)
3. ✅ Build agent monitoring dashboard:
   - Real-time agent status display
   - Performance metrics charts (latency, success rate)
   - Error log viewer
   - Cost/token usage analytics
4. ✅ Create evaluation results viewer
5. ✅ Build dataset upload/management UI
6. ✅ Implement WebSocket/SSE for real-time updates

**Key Documents:**
- [Agent Monitoring UI](ui-design/agent-monitoring-ui.md)
- [Technical Specifications - Frontend Section](deliverables/technical-specifications.md#frontend-architecture)

---

### **Week 9-10: Admin Portal & User Management**
**Owner:** Full-Stack Team

**Tasks:**
1. ✅ Build user management system (create, edit, roles)
2. ✅ Implement team/organization management
3. ✅ Create admin portal UI
4. ✅ Build API key management interface
5. ✅ Implement cost allocation tracking
6. ✅ Create audit log viewer

**Key Documents:**
- [Admin Portal](ui-design/admin-portal.md)
- [MVP Feature Specs - Admin Features](platform/mvp-feature-specs.md#admin-portal)

---

### **Week 11-12: Compliance Dashboard & Testing**
**Owner:** Full-Stack Team + QA

**Tasks:**
1. ✅ Implement compliance checking logic (NDMO, DIFC, ADGM)
2. ✅ Build compliance dashboard UI
3. ✅ Create audit report generation (PDF export)
4. ✅ Write comprehensive test suite (unit, integration, E2E)
5. ✅ Performance testing and optimization
6. ✅ Security audit and penetration testing
7. ✅ Deploy to staging environment
8. ✅ Pilot with 2-3 friendly clients

**Key Documents:**
- [Compliance Dashboard](ui-design/compliance-dashboard.md)
- [UAE AI Compliance Checklist](giveaways/uae-ai-compliance-checklist.md)
- [Technical Specifications - Compliance Section](deliverables/technical-specifications.md#compliance--regulatory)

---

## 🧪 Development Workflow

### **Git Branching Strategy**
```
main                    # Production-ready code
  ├── develop          # Integration branch
      ├── feature/evaluation-engine
      ├── feature/monitoring-dashboard
      ├── feature/admin-portal
      └── feature/compliance-dashboard
```

### **Commit Message Format**
```
[Area] Brief description

- Detailed change 1
- Detailed change 2

Ref: #issue-number (if applicable)
```

**Examples:**
- `[Backend] Add evaluation engine core logic`
- `[Frontend] Implement agent monitoring dashboard`
- `[DevOps] Configure CI/CD pipeline`

### **Pull Request Process**
1. Create feature branch from `develop`
2. Implement feature with tests
3. Open PR with description and screenshots (for UI)
4. Code review (2 approvals required)
5. Merge to `develop`
6. Deploy to staging for QA
7. Merge `develop` → `main` for production release

---

## 🧪 Testing Requirements

### **Backend Testing**
```bash
# Run unit tests
pytest tests/unit/

# Run integration tests
pytest tests/integration/

# Run with coverage
pytest --cov=platform --cov-report=html
```

### **Frontend Testing**
```bash
# Run unit tests
npm run test

# Run E2E tests (Playwright)
npm run test:e2e

# Type checking
npm run type-check
```

### **Minimum Coverage Requirements**
- **Backend:** 80% code coverage
- **Frontend:** 70% code coverage
- **Critical paths:** 100% coverage (evaluation engine, compliance checks)

---

## 📋 Developer Checklist (Before First Commit)

- [ ] Read [Technical Specifications](deliverables/technical-specifications.md)
- [ ] Read [MVP Feature Specs](platform/mvp-feature-specs.md)
- [ ] Set up local development environment
- [ ] Database running locally (PostgreSQL + Redis)
- [ ] Backend server running (`http://localhost:8000`)
- [ ] Frontend server running (`http://localhost:3000`)
- [ ] Environment variables configured (`.env` file)
- [ ] Can access API documentation (`/docs` endpoint)
- [ ] Understand Git workflow and branching strategy
- [ ] Joined team communication channels (Slack/Discord)

---

## 🆘 Troubleshooting

### **Database Connection Issues**
```bash
# Check if PostgreSQL is running
pg_isready

# Reset database
dropdb echolabs && createdb echolabs
alembic upgrade head
```

### **Python Dependency Issues**
```bash
# Rebuild virtual environment
rm -rf venv
python3.11 -m venv venv
source venv/bin/activate
pip install --upgrade pip
pip install -r requirements.txt
```

### **Frontend Build Issues**
```bash
# Clear Next.js cache
rm -rf .next
npm run build
```

### **API Key Issues**
- Verify `.env` file has correct API keys
- Test API keys independently:
  ```bash
  curl https://api.openai.com/v1/models \
    -H "Authorization: Bearer $OPENAI_API_KEY"
  ```

---

## 📞 Support & Communication

### **Team Channels**
- **Slack:** `#echolabs-dev` (general development)
- **Slack:** `#echolabs-backend` (backend-specific)
- **Slack:** `#echolabs-frontend` (frontend-specific)
- **GitHub Issues:** Bug reports and feature requests
- **GitHub Discussions:** Architecture and design discussions

### **Key Contacts**
- **Tech Lead:** [Name] - Technical architecture and decisions
- **Backend Lead:** [Name] - Backend implementation
- **Frontend Lead:** [Name] - Frontend implementation
- **DevOps Lead:** [Name] - Infrastructure and deployment

### **Office Hours**
- **Daily Standup:** 10:00 AM UAE Time
- **Weekly Planning:** Monday 2:00 PM UAE Time
- **Sprint Review:** Every 2 weeks, Friday 3:00 PM UAE Time

---

## 🔗 Quick Links

**Documentation:**
- [Full Navigation Index](NAVIGATION.md)
- [Technical Specifications](deliverables/technical-specifications.md)
- [MVP Feature Specs](platform/mvp-feature-specs.md)
- [Platform Architecture](platform/README.md)

**UI/UX Specs:**
- [Agent Monitoring Dashboard](ui-design/agent-monitoring-ui.md)
- [Admin Portal](ui-design/admin-portal.md)
- [Compliance Dashboard](ui-design/compliance-dashboard.md)

**Repository:**
- [GitHub Repo](https://github.com/ArjunFrancis/Echolabs-AI)
- [Live Documentation Site](https://echolabs-ai.com)

---

## ✅ Success Metrics (Phase 1 MVP)

**Technical Metrics:**
- ✅ API response time < 500ms (p95)
- ✅ Dashboard loads in < 2 seconds
- ✅ Support 100 concurrent evaluations
- ✅ 99.9% uptime for evaluation API
- ✅ Zero data breaches or security incidents

**Business Metrics:**
- ✅ 5 pilot clients onboarded
- ✅ 500+ evaluation runs completed
- ✅ 90%+ user satisfaction (pilot feedback)
- ✅ 100% compliance reports generated successfully

---

**Document Status:** Complete  
**Last Updated:** December 14, 2025  
**Maintainer:** EchoLabs Development Team  
**Version:** 1.0 (Phase 1 Focus)
