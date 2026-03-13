title: Meta Architect
description: AI-powered architect skill for comprehensive design tasks, system architecture, and automation workflows
version: 1.0.0
author: OpenClaw Core Team
tags: [design, ai, automation, architecture, system-design, workflow]
created: 2026-03-13
updated: 2026-03-13
license: MIT
dependencies: [openai>=1.0.0, pydantic>=2.0.0, fastapi>=0.100.0]
environment:
  - META_ARCHITECT_API_KEY: OpenAI API key for AI-powered design generation
  - META_ARCHITECT_MODEL: GPT-4 or Claude-3 (default: gpt-4)
  - META_ARCHITECT_MAX_TOKENS: Maximum tokens for AI responses (default: 4000)
  - META_ARCHITECT_TEMPERATURE: AI creativity level (0.0-1.0, default: 0.7)
---

# Meta Architect

## Purpose

Meta Architect is an AI-powered architect skill designed to handle complex design and architecture tasks across software systems, infrastructure, and automation workflows. It leverages advanced AI models to generate comprehensive architectural designs, system blueprints, and automated implementation plans.

### Real Use Cases

- **System Architecture Design**: Generate complete microservices architectures for e-commerce platforms with API gateways, databases, and caching layers
- **Infrastructure as Code**: Create Terraform configurations for AWS ECS deployments with load balancers, security groups, and monitoring
- **Workflow Automation**: Design GitHub Actions CI/CD pipelines for multi-environment deployments with testing and security scanning
- **Database Schema Design**: Architect normalized PostgreSQL schemas for SaaS applications with proper indexing and relationships
- **API Design**: Generate OpenAPI 3.0 specifications for RESTful services with authentication, pagination, and error handling
- **Security Architecture**: Design zero-trust network architectures for cloud-native applications with IAM policies and encryption

## Scope

### Supported Commands

- `openclaw meta-architect design <system-type> <requirements>` - Generate architectural designs
- `openclaw meta-architect blueprint <component> --format=json|yaml|markdown` - Create detailed blueprints
- `openclaw meta-architect workflow <task> --automation=github|jenkins|gitlab` - Design automation workflows
- `openclaw meta-architect validate <design-file>` - Validate architectural designs against best practices
- `openclaw meta-architect optimize <current-design> --constraints=<list>` - Optimize existing architectures
- `openclaw meta-architect migrate <from-system> <to-system>` - Generate migration plans

### Input Formats

- Natural language requirements (e.g., "Design a scalable chat application for 1M users")
- Existing codebases (via GitHub URLs or local paths)
- Architecture diagrams (PNG/JPG with OCR processing)
- JSON/YAML specifications

### Output Formats

- Markdown documentation with diagrams
- JSON/YAML for infrastructure tools
- PlantUML for visual architecture diagrams
- Terraform/OpenTofu code
- Docker Compose files

## Work Process

### Phase 1: Requirements Analysis
1. Parse input requirements using natural language processing
2. Identify system constraints, scalability needs, and technology preferences
3. Analyze existing codebase if provided (via GitHub integration)
4. Generate requirements matrix with acceptance criteria

### Phase 2: Architecture Design
1. Select appropriate architectural patterns (microservices, monolithic, serverless)
2. Design component relationships and data flows
3. Define API contracts and communication protocols
4. Incorporate security, monitoring, and scalability considerations

### Phase 3: Implementation Planning
1. Generate detailed implementation roadmap with dependencies
2. Create infrastructure specifications (compute, storage, networking)
3. Design deployment and CI/CD pipelines
4. Estimate resource requirements and costs

### Phase 4: Validation and Optimization
1. Validate design against industry best practices
2. Perform security and performance analysis
3. Generate testing strategies and monitoring plans
4. Optimize for cost-efficiency and maintainability

### Phase 5: Documentation Generation
1. Create comprehensive documentation with diagrams
2. Generate implementation guides and runbooks
3. Produce deployment manifests and configuration files
4. Create rollback and disaster recovery plans

## Golden Rules

1. **Security First**: All designs must incorporate security-by-design principles with encryption, access controls, and threat modeling
2. **Scalability Priority**: Architectures must handle 10x growth without major refactoring
3. **Observability Built-in**: Include logging, monitoring, and tracing from day one
4. **Cost Optimization**: Design for efficiency with auto-scaling and resource optimization
5. **Standards Compliance**: Follow industry standards (OWASP, NIST, CNCF) and best practices
6. **Future-Proofing**: Include migration paths and extensibility hooks
7. **Documentation Mandatory**: Every design includes complete documentation and implementation guides
8. **Validation Required**: All designs pass automated validation checks before delivery

## Examples

### Example 1: E-commerce Microservices Design

**Input:**
```
openclaw meta-architect design microservices "Design a scalable e-commerce platform handling 100K concurrent users with product catalog, shopping cart, payment processing, and order management"
```

**Output:**
```yaml
architecture:
  services:
    - name: api-gateway
      technology: Kong
      responsibilities: [routing, authentication, rate-limiting]
    - name: product-service
      technology: Node.js + PostgreSQL
      responsibilities: [catalog management, search, inventory]
    - name: cart-service
      technology: Redis + Go
      responsibilities: [session management, cart operations]
    - name: payment-service
      technology: Stripe + Java
      responsibilities: [payment processing, fraud detection]
    - name: order-service
      technology: Python + MongoDB
      responsibilities: [order processing, fulfillment]

  infrastructure:
    - kubernetes: EKS with auto-scaling
    - database: Aurora PostgreSQL with read replicas
    - cache: Redis Cluster
    - cdn: CloudFront
    - monitoring: Prometheus + Grafana

  security:
    - iam: AWS IAM with least privilege
    - encryption: TLS 1.3, data at rest encryption
    - secrets: AWS Secrets Manager
```

### Example 2: CI/CD Workflow Design

**Input:**
```
openclaw meta-architect workflow deployment --automation=github "Create CI/CD pipeline for React app with testing, security scanning, and multi-environment deployment"
```

**Output:**
```yaml
.github/workflows/deploy.yml
name: Deploy React App
on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: '18'
      - run: npm ci
      - run: npm run lint
      - run: npm test -- --coverage
      - uses: codecov/codecov-action@v3

  security:
    needs: test
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: github/super-linter@v5
      - uses: aquasecurity/trivy-action@master
        with:
          scan-type: 'fs'
          format: 'sarif'

  deploy-staging:
    needs: security
    if: github.ref == 'refs/heads/develop'
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: npm run build
      - uses: aws-actions/configure-aws-credentials@v4
      - uses: aws-actions/amazon-ecs-deploy-task-definition@v1
        with:
          task-definition: task-definition-staging.json
          service: react-app-staging
          cluster: staging-cluster

  deploy-production:
    needs: security
    if: github.ref == 'refs/heads/main'
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: npm run build
      - uses: aws-actions/configure-aws-credentials@v4
      - uses: aws-actions/amazon-ecs-deploy-task-definition@v1
        with:
          task-definition: task-definition-prod.json
          service: react-app-prod
          cluster: production-cluster
```

### Example 3: Database Schema Design

**Input:**
```
openclaw meta-architect blueprint database-schema "Design PostgreSQL schema for multi-tenant SaaS application with users, organizations, subscriptions, and audit logging"
```

**Output:**
```sql
-- Multi-tenant SaaS Database Schema
CREATE EXTENSION IF NOT EXISTS "uuid-ossp";

-- Organizations (tenants)
CREATE TABLE organizations (
    id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    name VARCHAR(255) NOT NULL,
    domain VARCHAR(255) UNIQUE NOT NULL,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- Users
CREATE TABLE users (
    id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    organization_id UUID NOT NULL REFERENCES organizations(id) ON DELETE CASCADE,
    email VARCHAR(255) NOT NULL UNIQUE,
    password_hash VARCHAR(255) NOT NULL,
    first_name VARCHAR(100),
    last_name VARCHAR(100),
    role VARCHAR(50) DEFAULT 'user',
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- Subscriptions
CREATE TABLE subscriptions (
    id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    organization_id UUID NOT NULL REFERENCES organizations(id) ON DELETE CASCADE,
    plan_name VARCHAR(100) NOT NULL,
    status VARCHAR(50) DEFAULT 'active',
    current_period_start TIMESTAMP WITH TIME ZONE NOT NULL,
    current_period_end TIMESTAMP WITH TIME ZONE NOT NULL,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- Audit logs
CREATE TABLE audit_logs (
    id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    organization_id UUID NOT NULL REFERENCES organizations(id) ON DELETE CASCADE,
    user_id UUID REFERENCES users(id) ON DELETE SET NULL,
    action VARCHAR(255) NOT NULL,
    resource_type VARCHAR(100) NOT NULL,
    resource_id UUID,
    old_values JSONB,
    new_values JSONB,
    ip_address INET,
    user_agent TEXT,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- Indexes for performance
CREATE INDEX idx_users_organization_id ON users(organization_id);
CREATE INDEX idx_users_email ON users(email);
CREATE INDEX idx_subscriptions_organization_id ON subscriptions(organization_id);
CREATE INDEX idx_audit_logs_organization_id ON audit_logs(organization_id);
CREATE INDEX idx_audit_logs_created_at ON audit_logs(created_at);
CREATE INDEX idx_audit_logs_resource ON audit_logs(resource_type, resource_id);
```

## Rollback Commands

### Design Rollback
- `openclaw meta-architect rollback design <design-id>` - Remove generated design files and revert to previous version
- `openclaw meta-architect undo blueprint <component>` - Delete generated blueprint files

### Workflow Rollback
- `openclaw meta-architect rollback workflow <workflow-id>` - Remove deployed workflow configurations
- `openclaw meta-architect reset pipeline <pipeline-name>` - Reset CI/CD pipeline to default state

### Infrastructure Rollback
- `openclaw meta-architect rollback infra <environment>` - Destroy provisioned infrastructure resources
- `openclaw meta-architect cleanup terraform` - Remove all generated Terraform state and plans

## Dependencies and Requirements

### Required Dependencies
- Python 3.9+
- OpenAI API access
- GitHub CLI (for workflow generation)
- Terraform/OpenTofu (for infrastructure code)
- Docker (for containerized deployments)

### Environment Setup
```bash
# Install dependencies
pip install openai pydantic fastapi uvicorn

# Set environment variables
export META_ARCHITECT_API_KEY="your-openai-api-key"
export META_ARCHITECT_MODEL="gpt-4"
export META_ARCHITECT_MAX_TOKENS="4000"
export META_ARCHITECT_TEMPERATURE="0.7"
```

## Verification Steps

### Design Validation
1. Run `openclaw meta-architect validate <design-file>` to check against best practices
2. Verify security: Check for encryption, access controls, and threat mitigation
3. Test scalability: Ensure auto-scaling configurations and load balancing
4. Validate costs: Review resource estimates and optimization suggestions

### Workflow Verification
1. Execute `openclaw meta-architect test-workflow <workflow-file>` for syntax validation
2. Check permissions: Verify required API tokens and access levels
3. Test deployment: Run dry-run deployments in staging environment
4. Monitor performance: Ensure workflow execution times meet SLAs

### Infrastructure Verification
1. Use `terraform validate` on generated Terraform code
2. Run `terraform plan` to preview changes without applying
3. Execute security scans with tools like Checkov or Terrascan
4. Test connectivity: Verify network configurations and firewall rules

## Troubleshooting

### Common Issues

**Issue: AI API Rate Limiting**
- **Symptom**: "Rate limit exceeded" errors during design generation
- **Solution**: Increase API quota or implement retry logic with exponential backoff
- **Prevention**: Set appropriate rate limits in environment variables

**Issue: Invalid Architecture Output**
- **Symptom**: Generated designs don't match requirements
- **Solution**: Refine input prompts with more specific constraints and examples
- **Prevention**: Use the `--validate` flag to check designs against requirements

**Issue: Infrastructure Deployment Failures**
- **Symptom**: Terraform apply fails with resource conflicts
- **Solution**: Run `terraform plan` first to identify conflicts, then adjust configurations
- **Prevention**: Always test in staging environment before production deployment

**Issue: Security Vulnerabilities in Generated Code**
- **Symptom**: Security scanners flag generated infrastructure or application code
- **Solution**: Update skill version or manually review and patch security issues
- **Prevention**: Keep dependencies updated and run security scans on all outputs

**Issue: Performance Degradation**
- **Symptom**: Designs work in development but fail under load
- **Solution**: Add load testing requirements to input and regenerate designs
- **Prevention**: Include performance benchmarks and scalability testing in all designs

### Debug Commands
- `openclaw meta-architect debug <design-id>` - Generate detailed debug logs for failed designs
- `openclaw meta-architect logs --level=debug` - Enable verbose logging for troubleshooting
- `openclaw meta-architect health-check` - Verify all dependencies and API connections

### Support Resources
- Documentation: https://docs.openclaw.ai/meta-architect
- Community Forum: https://community.openclaw.ai/c/meta-architect
- Issue Tracker: https://github.com/openclaw/meta-architect/issues
- Professional Services: contact@openclaw.ai for enterprise support