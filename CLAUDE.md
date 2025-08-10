# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is the **devcontainer-features** repository within the 40docs platform ecosystem. It provides custom DevContainer features for enhanced development environments.

### DevContainer Features Library

This repository contains 40+ custom DevContainer features organized in the `src/` directory:

**Core Development Tools**:
- **mkdocs-environment**: Complete MkDocs Python environment with Material theme and plugins
- **kubectl-helm-minikube**: Kubernetes development tools (kubectl, Helm, Minikube)
- **azure-cli-persistence**: Azure CLI with persistent authentication across container rebuilds
- **terraform tools**: tfenv (version management), tflint (linting), infracost (cost estimation)

**Security & Compliance**:
- **fortidevsec**: FortiDevSec security scanning extension for DevOps CI/CD
- **lacework-cli**: FortiCNAPP command line interface for cloud security
- **lacework-extensible-reporting**: Enhanced security reporting capabilities

**AI/ML Development**:
- **ollama-client** & **ollama-persistence**: Local AI model serving with persistent storage
- **autogen-environment**: Microsoft AutoGen framework for multi-agent conversations
- **jupyter-environment**: Jupyter notebooks with conda environment
- **textgen-environment**, **chunking-environment**: Text processing and AI workloads
- **memgpt-environment**: MemGPT persistent memory for LLMs
- **openwebui-environment**: Open WebUI for AI model interactions
- **nvidia-cuda**: NVIDIA CUDA support for GPU-accelerated workloads

**Development Productivity**:
- **container-dotfiles**: Personal dotfiles and shell configurations
- **oh-my-posh**: PowerShell prompt theming
- **lazygit**: Terminal UI for Git operations  
- **continue**: AI-powered code completion
- **vimrc**: Vim configuration setup
- **powerline-fonts**, **nerd-fonts**: Enhanced terminal fonts

Each feature includes:
- `devcontainer-feature.json`: Feature metadata and configuration
- `install.sh`: Installation script with proper error handling
- `README.md`: Auto-generated documentation with usage examples
- Configuration files: Environment files, templates, and dependencies

## Common Development Commands

### Feature Development
```bash
# Test a feature locally (requires Docker)
devcontainer features test --features <feature-name>

# Build all features
devcontainer features publish --features src/

# Validate feature metadata
devcontainer features validate --features src/<feature-name>

# Test specific feature with different base images
devcontainer features test --features <feature-name> --base-image mcr.microsoft.com/devcontainers/base:ubuntu
```

### Feature Creation Workflow
```bash
# Create new feature directory structure
mkdir -p src/new-feature
cd src/new-feature

# Required files for any feature:
touch devcontainer-feature.json  # Feature metadata and options
touch install.sh                 # Installation script (must be executable)
touch README.md                  # Auto-generated from feature.json

# Optional files:
touch NOTES.md                   # Additional documentation
# Configuration files as needed (environment.yml, templates, etc.)
```

## Architecture and Feature Structure

### Feature Definition Pattern
Each feature follows the DevContainer specification:

```json
{
  "id": "feature-name",
  "name": "Human Readable Name",
  "description": "Feature description",
  "version": "semantic.version.number",
  "dependsOn": {
    "feature-dependency": {}
  },
  "installsAfter": ["prerequisite-feature"],
  "options": {
    "configurable-option": {
      "type": "string|boolean",
      "default": "default-value",
      "description": "Option description"
    }
  },
  "mounts": [
    {
      "source": "${devcontainerId}-volume-name",
      "target": "/mount/path",
      "type": "volume"
    }
  ],
  "postStartCommand": "command to run after container starts"
}
```

### Installation Script Patterns
All `install.sh` scripts follow these conventions:

```bash
#!/bin/bash
set -e  # Exit on any error

# Feature options available as environment variables
# OPTION_NAME corresponds to options.optionName in JSON

echo "Activating feature 'feature-name'"

# Common patterns:
# 1. Version detection and URL construction
# 2. Architecture detection (AMD64, ARM64)
# 3. Package manager integration (apt, conda, pip)
# 4. Binary installation with checksum verification
# 5. Configuration file setup
# 6. User permission handling with _REMOTE_USER

# Example user context execution:
su -l "${_REMOTE_USER}" -c "command to run as user"

# Cleanup
rm -rf /tmp/feature-install-files
```

### Multi-Repository Context

This repository is part of the 40docs platform ecosystem:
- **Parent Repository**: This is a Git submodule within the main 40docs platform
- **Publishing**: Features are published to GitHub Container Registry
- **Integration**: Used by other repositories' devcontainer configurations
- **Testing**: Features tested in CI/CD pipeline with multiple base images

## Important Development Guidelines

### Feature Development Standards
- **Error Handling**: All install scripts must use `set -e` and handle errors gracefully
- **User Context**: Use `${_REMOTE_USER}` for user-specific installations
- **Security**: Verify checksums for downloaded binaries
- **Cleanup**: Remove temporary files and caches
- **Documentation**: Auto-generate README.md from devcontainer-feature.json

### Version Management
- **Semantic Versioning**: Follow semver for all features (MAJOR.MINOR.PATCH)
- **Breaking Changes**: Increment MAJOR version for breaking changes
- **Backward Compatibility**: Maintain compatibility when possible
- **Testing**: Test features with multiple base images and configurations

### Security Considerations
- **Package Sources**: Only use official package repositories and trusted sources
- **Checksum Verification**: Verify downloaded binaries with checksums
- **Privilege Separation**: Run as non-root when possible
- **Secrets Management**: Never embed secrets or API keys in features

### Integration Patterns
- **Dependency Management**: Use `dependsOn` for required features
- **Installation Order**: Use `installsAfter` for installation sequence
- **Persistence**: Use Docker volumes for data that should survive container rebuilds
- **Environment Setup**: Configure shell environments and PATH variables

## Feature Categories and Specializations

### Environment Setup Features
Focus on creating complete development environments:
- Language runtimes (Python, Node.js, etc.)
- Package managers and dependency tools
- Shell configurations and productivity tools

### Tool Installation Features  
Individual tools and utilities:
- CLI tools and command-line utilities
- Development tools and editors
- System utilities and monitoring tools

### Service Integration Features
External service integrations:
- Cloud provider CLIs
- Security scanning tools
- Monitoring and observability tools

### Persistence Features
Data persistence across container rebuilds:
- Volume management
- Configuration persistence
- Authentication token storage

## Testing and Quality Assurance

### Feature Testing Process
1. **Unit Testing**: Test installation script logic
2. **Integration Testing**: Test with different base images
3. **Compatibility Testing**: Test feature combinations
4. **Performance Testing**: Verify installation speed and resource usage

### Quality Gates
- All features must install successfully on Ubuntu, Debian, and Alpine
- Installation scripts must complete within reasonable time limits
- Features must not conflict with each other
- Documentation must be complete and accurate

## Publishing and Distribution

### Publishing Workflow
Features are automatically published to GitHub Container Registry when:
- Changes are pushed to main branch
- Version numbers are updated in devcontainer-feature.json
- All tests pass in CI/CD pipeline

### Usage by Consumers
Other repositories reference features like:
```json
"features": {
  "ghcr.io/40docs/devcontainer-features/mkdocs-environment:0": {},
  "ghcr.io/40docs/devcontainer-features/fortidevsec:23": {}
}
```

## Repository Security

### Branch Protection
- All changes require pull requests
- Automated testing must pass before merge
- Security scanning validates all new features