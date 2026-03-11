# Contributing to zsel-cloud

Thank you for your interest in contributing to zsel-cloud! This guide explains how to contribute effectively.

## Getting Started

1. **Fork** the repository
2. **Clone** your fork: `git clone https://github.com/YOUR-USERNAME/zsel-cloud.git`
3. **Create a branch**: `git checkout -b feature/your-feature-name`
4. **Make changes** and commit regularly
5. **Submit a pull request**

## Development Workflow

### Local Setup
```bash
git clone https://github.com/zsel/zsel-cloud.git
cd zsel-cloud

# Set up development environment
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

### Running Tests
```bash
# Validate Kubernetes manifests
kubectl apply -f services/ --dry-run=client

# Run security checks
yamllint services/*/*.yaml
```

### Commit Messages
Follow conventional commits:
```
feat(keycloak): add LDAP integration
fix(moodle): resolve database connection timeout
docs(nextcloud): update installation guide
```

## Pull Request Process

1. **Create PR** with clear description of changes
2. **Link issues**: Reference any related issues (#123)
3. **Add tests**: Include integration tests if applicable
4. **Update docs**: Document any configuration changes
5. **Request review**: Assign 2+ reviewers
6. **Address feedback**: Respond to review comments
7. **Merge**: Maintainers will merge after approval

## Code Standards

### Kubernetes Manifests
- Use 2-space indentation
- Include resource limits and requests
- Add probes for health checks
- Use namespaces for isolation

### Helm Charts
- Follow Helm best practices
- Include values documentation
- Add resource quotas
- Test with `helm lint`

### Documentation
- Use clear, concise language
- Include examples
- Document all configuration options
- Update README for significant changes

## Reporting Bugs

**Found a bug?** Create an issue with:
- Clear description of the issue
- Steps to reproduce
- Expected vs actual behavior
- Kubernetes version and cluster details
- Relevant logs or error messages

## Feature Requests

**Have an idea?** Open an issue with:
- Description of the feature
- Use cases and benefits
- Proposed implementation
- Potential impact on existing services

## Code of Conduct

- Be respectful and inclusive
- Assume good intentions
- Ask questions before criticizing
- Help others learn and grow

## Maintainers

Current maintainers:
- @platform-team - Platform engineering decisions
- @security-team - Security reviews
- @devops-team - Deployment and operations

## Questions?

- **Documentation**: Check [docs/](docs/)
- **Discussions**: Use GitHub discussions
- **Email**: platform-team@zsel.opole.pl

---

Thank you for contributing! 🎉
