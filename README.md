# zsel-cloud: Service Platform Layer

**Purpose**: Kubernetes services platform layer - contains all service deployments (Keycloak, Moodle, Nextcloud, PostgreSQL, Redis, etc.)

**Part of**: [ZSEL 7-Layer Architecture](../SERWERY/docs/ARCHITECTURE.md)

## Layer Overview

The **Service Platform Layer** (zsel-cloud) contains:
- **OIDC Identity**: Keycloak for federated authentication
- **Learning Management**: Moodle for course delivery
- **File Sharing**: Nextcloud for document collaboration
- **Data**: PostgreSQL databases, Redis caching
- **Monitoring**: Service health dashboards
- **Logging**: ELK stack for service logs

## Directory Structure

```
zsel-cloud/
├── services/
│   ├── keycloak/          Keycloak OIDC provider configs
│   ├── moodle/            Moodle LMS deployment
│   ├── nextcloud/         Nextcloud file sharing
│   ├── postgresql/        PostgreSQL database
│   └── redis/             Redis caching layer
├── docs/
│   ├── DEPLOYMENT.md      Service deployment procedures
│   ├── CONFIGURATION.md   Service configuration guide
│   └── INTEGRATION.md     Service integration patterns
├── examples/              Ready-to-deploy service examples
├── tests/                 Service integration tests
├── .github/workflows/     CI/CD for service deployments
├── README.md              This file
├── CONTRIBUTING.md        Contribution guidelines
├── CODEOWNERS             Repository ownership
├── LICENSE                MIT License
└── .gitignore             Git ignore patterns
```

## Dependencies

- **zsel-platform** (Layer 3): Core Kubernetes platform
  - Keycloak config depends on cert-manager for TLS
  - All services depend on Longhorn for persistent storage
  - Network policies from networking layer applied

- **zsel-network** (Layer 1): Network infrastructure
  - DNS entries for services
  - VPN access to services

## Quick Start

### Deploy Keycloak (OIDC Provider)
```bash
kubectl apply -f services/keycloak/
```

### Deploy Moodle (Learning Management)
```bash
kubectl apply -f services/moodle/
```

### Deploy Nextcloud (File Sharing)
```bash
kubectl apply -f services/nextcloud/
```

### Deploy PostgreSQL (Database)
```bash
kubectl apply -f services/postgresql/
```

### Deploy Redis (Cache)
```bash
kubectl apply -f services/redis/
```

## Service Integrations

### Keycloak → ZSEL Authentication
- Provides OIDC endpoint for all applications
- Integrates with FreeIPA for user directory
- Issues JWT tokens for API authentication

### Moodle → File Storage
- Uses PostgreSQL for course database
- Uses Nextcloud for student file uploads
- Uses Keycloak for single sign-on (SSO)

### Nextcloud → Collaboration
- Uses PostgreSQL for file metadata
- Uses Redis for real-time updates
- Integrates with Keycloak for unified login

## Deployment Workflow

1. **Platform Ready**: zsel-platform (core K8s, storage, networking) must be deployed first
2. **Services**: Deploy services in dependency order:
   - PostgreSQL (database dependency)
   - Redis (cache dependency)
   - Keycloak (identity dependency)
   - Moodle (application)
   - Nextcloud (application)
3. **Post-Deployment**: Run integration tests
4. **Monitoring**: Enable service monitoring in Prometheus

## Service Health

Check service status:
```bash
kubectl get all -n services
kubectl logs -n services -l app=keycloak
kubectl logs -n services -l app=moodle
```

## Configuration

Each service has:
- **ConfigMap**: Application configuration
- **Secret**: Credentials and secrets (encrypted at rest)
- **Service**: K8s service for discovery
- **Deployment**: Replicas and rolling updates
- **PVC**: Persistent storage if needed

## Troubleshooting

See [TROUBLESHOOTING.md](docs/TROUBLESHOOTING.md) for:
- Service startup issues
- Database connection problems
- Authentication failures
- Storage issues

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for:
- Code standards
- Pull request process
- Testing requirements

## Architecture Reference

- **Full Architecture**: See [SERWERY/docs/ARCHITECTURE.md](../SERWERY/docs/ARCHITECTURE.md)
- **Platform Layer (Layer 3)**: See [zsel-platform](zsel-platform/README.md)
- **Network Layer (Layer 1)**: See [zsel-network](zsel-network/README.md)

## License

MIT License - See [LICENSE](LICENSE)

---

**Maintainers**: Platform Engineering Team  
**Last Updated**: March 11, 2026
