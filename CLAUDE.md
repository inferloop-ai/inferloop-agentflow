# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**InferLoop AgentFlow** - A comprehensive AI agent workflow orchestration platform that provides visual workflow design, intelligent routing, and enterprise-grade management of multi-agent systems. AgentFlow serves as the orchestration layer that connects and coordinates agents from across the InferLoop ecosystem.

## Repository Structure

```
inferloop-agentflow/
├── src/
│   ├── core/              # Core workflow models and logic
│   │   ├── workflow.py    # Workflow definition and management
│   │   ├── agent.py       # Agent abstraction and registry
│   │   ├── task.py        # Task execution units
│   │   ├── state.py       # State management
│   │   └── context.py     # Execution context
│   ├── engine/            # Workflow execution engine
│   │   ├── executor.py    # Main execution logic
│   │   ├── scheduler.py   # Task scheduling
│   │   ├── router.py      # Dynamic routing logic
│   │   └── validator.py   # Workflow validation
│   ├── designer/          # Visual workflow designer
│   │   ├── canvas.py      # Canvas rendering
│   │   ├── nodes.py       # Node components
│   │   ├── edges.py       # Edge connections
│   │   └── templates.py   # Workflow templates
│   ├── orchestrator/      # Multi-agent orchestration
│   │   ├── coordinator.py # Agent coordination
│   │   ├── patterns.py    # Workflow patterns
│   │   └── strategies.py  # Execution strategies
│   ├── monitor/           # Monitoring and analytics
│   │   ├── tracker.py     # Execution tracking
│   │   ├── metrics.py     # Performance metrics
│   │   └── alerts.py      # Alert management
│   ├── integrations/      # Platform integrations
│   │   ├── agentcraft.py  # AgentCraft integration
│   │   ├── trustscan.py   # TrustScan validation
│   │   ├── testnest.py    # TestNest testing
│   │   ├── datamint.py    # DataMint data generation
│   │   └── marketplace.py # Marketplace templates
│   ├── api/               # REST API
│   │   ├── main.py        # FastAPI application
│   │   ├── routes.py      # API routes
│   │   └── models.py      # Pydantic models
│   └── utils/             # Utility functions
│       ├── config.py      # Configuration management
│       ├── logger.py      # Logging setup
│       └── helpers.py     # Helper functions
├── tests/                 # Test suite
│   ├── unit/             # Unit tests
│   ├── integration/      # Integration tests
│   └── e2e/              # End-to-end tests
├── workflows/            # Workflow definitions
│   ├── templates/        # Pre-built templates
│   └── examples/         # Example workflows
├── config/               # Configuration files
│   ├── settings.yaml     # Application settings
│   ├── workflows.yaml    # Workflow configurations
│   └── agents.yaml       # Agent registry
├── docs/                 # Documentation
│   ├── api/             # API documentation
│   ├── user-guide/      # User guides
│   └── patterns/        # Workflow patterns
├── product-docs/         # Product documentation
│   ├── user-stories/    # User stories and requirements
│   ├── architecture/    # Architecture documentation
│   └── requirements/    # Detailed requirements
└── scripts/             # Utility scripts
    ├── setup.sh         # Setup script
    ├── deploy.sh        # Deployment script
    └── test.sh          # Test runner
```

## Technology Stack

### Core Technologies
- **Language**: Python 3.11+
- **Framework**: FastAPI for REST API
- **Workflow Engine**: Apache Airflow / Temporal (configurable)
- **Message Queue**: Apache Kafka / RabbitMQ
- **Database**: PostgreSQL (metadata), Redis (cache)
- **Container**: Docker, Kubernetes
- **Monitoring**: Prometheus, Grafana

### Frontend (Planned)
- **Framework**: React with TypeScript
- **Canvas**: React Flow or Cytoscape.js
- **State Management**: Redux/Zustand
- **UI Components**: Material-UI or Ant Design

## Development Guidelines

### Architecture Principles

1. **Separation of Concerns**
   - Clear separation between workflow definition and execution
   - Independent scaling of components
   - Pluggable integrations

2. **Event-Driven Architecture**
   - Event sourcing for workflow state
   - Async message passing between agents
   - Reactive monitoring and alerting

3. **Multi-Tenancy**
   - Complete tenant isolation
   - Resource quotas and limits
   - Tenant-specific configurations

### Workflow Patterns

The platform supports multiple workflow patterns:

1. **Sequential**: Step-by-step execution
2. **Parallel**: Concurrent task execution
3. **Conditional**: Branching based on conditions
4. **Loop**: Iterative processing
5. **Map-Reduce**: Distributed data processing
6. **Saga**: Long-running transactions with compensation
7. **Pipeline**: Stream processing
8. **State Machine**: State-based transitions

### Integration Points

#### With InferLoop Products
- **AgentCraft**: Import and execute visual agents
- **TrustScan**: Validate workflows for compliance
- **TestNest**: Test workflows in sandbox
- **DataMint**: Generate synthetic test data
- **Marketplace**: Share workflow templates

#### External Systems
- **Cloud Providers**: AWS Step Functions, Azure Logic Apps, GCP Workflows
- **Enterprise**: SAP, Salesforce, ServiceNow
- **DevOps**: Jenkins, GitLab CI, GitHub Actions
- **Messaging**: Slack, Teams, Email

## Development Commands

### Setup
```bash
# Install dependencies
pip install -r requirements.txt

# Setup database
python scripts/setup_db.py

# Run migrations
alembic upgrade head
```

### Development
```bash
# Start development server
uvicorn src.api.main:app --reload --port 8000

# Run tests
pytest tests/

# Run with coverage
pytest --cov=src tests/

# Lint code
ruff check src/
mypy src/
```

### Docker
```bash
# Build image
docker build -t inferloop-agentflow .

# Run container
docker run -p 8000:8000 inferloop-agentflow

# Docker Compose
docker-compose up -d
```

## API Endpoints (Planned)

### Workflow Management
- `POST /workflows` - Create workflow
- `GET /workflows` - List workflows
- `GET /workflows/{id}` - Get workflow details
- `PUT /workflows/{id}` - Update workflow
- `DELETE /workflows/{id}` - Delete workflow

### Execution
- `POST /workflows/{id}/execute` - Execute workflow
- `GET /executions` - List executions
- `GET /executions/{id}` - Get execution details
- `POST /executions/{id}/cancel` - Cancel execution

### Monitoring
- `GET /metrics` - Get system metrics
- `GET /workflows/{id}/metrics` - Get workflow metrics
- `GET /alerts` - List active alerts

## Testing Strategy

### Unit Tests
- Test individual components in isolation
- Mock external dependencies
- Achieve >80% code coverage

### Integration Tests
- Test component interactions
- Test with real databases
- Validate API contracts

### E2E Tests
- Test complete workflow scenarios
- Validate multi-agent coordination
- Performance benchmarking

## Configuration

### Environment Variables
```bash
# Database
DATABASE_URL=postgresql://user:pass@localhost/agentflow
REDIS_URL=redis://localhost:6379

# Message Queue
KAFKA_BROKERS=localhost:9092
RABBITMQ_URL=amqp://guest:guest@localhost:5672

# InferLoop Services
AGENTCRAFT_API_URL=http://localhost:8001
TRUSTSCAN_API_URL=http://localhost:8003
DATAMINT_API_URL=http://localhost:8005

# Security
SECRET_KEY=your-secret-key
JWT_ALGORITHM=HS256
```

### Workflow Configuration
```yaml
# config/workflows.yaml
workflows:
  max_parallel_tasks: 10
  default_timeout: 3600
  retry_policy:
    max_retries: 3
    backoff_multiplier: 2
```

## Performance Considerations

### Scalability
- Horizontal scaling of executor nodes
- Distributed task execution
- Caching of workflow definitions
- Connection pooling for databases

### Optimization
- Lazy loading of workflow components
- Batch processing for bulk operations
- Async I/O for external calls
- Query optimization for workflow queries

## Security

### Authentication & Authorization
- JWT-based authentication
- Role-based access control (RBAC)
- API key management
- OAuth2 integration

### Data Security
- Encryption at rest and in transit
- Secure credential storage (HashiCorp Vault)
- Audit logging for all operations
- Input validation and sanitization

## Monitoring & Observability

### Metrics
- Workflow execution metrics
- Agent performance metrics
- Resource utilization
- Error rates and latency

### Logging
- Structured logging with correlation IDs
- Log aggregation with ELK stack
- Debug, info, warning, error levels
- Audit trail for compliance

### Tracing
- Distributed tracing with OpenTelemetry
- Request flow visualization
- Performance bottleneck identification
- Service dependency mapping

## Common Issues & Solutions

### Issue: Workflow execution timeout
**Solution**: Increase timeout in workflow configuration or optimize long-running tasks

### Issue: High memory usage
**Solution**: Enable task result compression, implement pagination for large datasets

### Issue: Agent communication failure
**Solution**: Check network connectivity, verify agent registration, review retry policies

## Future Enhancements

### Phase 1 (Current)
- Core workflow engine
- Basic UI designer
- Essential integrations

### Phase 2
- Advanced orchestration patterns
- ML-powered optimization
- Enhanced monitoring

### Phase 3
- Workflow marketplace
- Edge deployment support
- Advanced analytics

## Contributing

1. Follow PEP 8 style guide
2. Write comprehensive tests
3. Update documentation
4. Submit PR with clear description

## Related Documentation

- [User Stories](product-docs/user-stories/AGENTFLOW_ALL_USER_STORIES_CONSOLIDATED.md)
- [Architecture Design](product-docs/architecture/README.md)
- [API Reference](docs/api/reference.md)
- [Workflow Patterns](docs/patterns/workflow_patterns.md)

---

*This document serves as the primary reference for developers working on InferLoop AgentFlow*