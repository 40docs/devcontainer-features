# DevContainer Features

[![License](https://img.shields.io/github/license/40docs/devcontainer-features)](LICENSE)
[![Registry](https://img.shields.io/badge/registry-ghcr.io-blue)](https://github.com/40docs/devcontainer-features/pkgs/container/devcontainer-features)

A collection of custom DevContainer features for enhanced development environments within the 40docs platform ecosystem.

## Overview

This repository provides 40+ custom DevContainer features that extend development containers with specialized tools, runtimes, and configurations. Features are automatically published to GitHub Container Registry and can be used in any DevContainer configuration.

## Available Features

### 🛠️ Core Development Tools

| Feature | Description | Version |
|---------|-------------|---------|
| [`mkdocs-environment`](src/mkdocs-environment) | Complete MkDocs Python environment with Material theme | ![Version](https://img.shields.io/badge/version-0.0.13-blue) |
| [`kubectl-helm-minikube`](src/kubectl-helm-minikube) | Kubernetes development tools (kubectl, Helm, Minikube) | ![Version](https://img.shields.io/badge/version-latest-blue) |
| [`azure-cli-persistence`](src/azure-cli-persistence) | Azure CLI with persistent authentication | ![Version](https://img.shields.io/badge/version-latest-blue) |
| [`tfenv`](src/tfenv) | Terraform version management | ![Version](https://img.shields.io/badge/version-latest-blue) |
| [`tflint`](src/tflint) | Terraform linting tool | ![Version](https://img.shields.io/badge/version-latest-blue) |
| [`infracost`](src/infracost) | Terraform cost estimation | ![Version](https://img.shields.io/badge/version-latest-blue) |

### 🔒 Security & Compliance

| Feature | Description | Version |
|---------|-------------|---------|
| [`fortidevsec`](src/fortidevsec) | FortiDevSec security scanning extension | ![Version](https://img.shields.io/badge/version-23.4.107--0.0.11-blue) |
| [`lacework-cli`](src/lacework-cli) | FortiCNAPP command line interface | ![Version](https://img.shields.io/badge/version-0.0.31-blue) |
| [`lacework-extensible-reporting`](src/lacework-extensible-reporting) | Enhanced security reporting | ![Version](https://img.shields.io/badge/version-latest-blue) |

### 🤖 AI/ML Development

| Feature | Description | Version |
|---------|-------------|---------|
| [`ollama-client`](src/ollama-client) | Local AI model serving client | ![Version](https://img.shields.io/badge/version-latest-blue) |
| [`ollama-persistence`](src/ollama-persistence) | Ollama with persistent storage | ![Version](https://img.shields.io/badge/version-latest-blue) |
| [`autogen-environment`](src/autogen-environment) | Microsoft AutoGen framework | ![Version](https://img.shields.io/badge/version-latest-blue) |
| [`jupyter-environment`](src/jupyter-environment) | Jupyter notebooks with conda | ![Version](https://img.shields.io/badge/version-latest-blue) |
| [`textgen-environment`](src/textgen-environment) | Text generation workloads | ![Version](https://img.shields.io/badge/version-latest-blue) |
| [`chunking-environment`](src/chunking-environment) | Text processing and chunking | ![Version](https://img.shields.io/badge/version-latest-blue) |
| [`memgpt-environment`](src/memgpt-environment) | MemGPT persistent memory for LLMs | ![Version](https://img.shields.io/badge/version-latest-blue) |
| [`openwebui-environment`](src/openwebui-environment) | Open WebUI for AI models | ![Version](https://img.shields.io/badge/version-latest-blue) |
| [`nvidia-cuda`](src/nvidia-cuda) | NVIDIA CUDA GPU support | ![Version](https://img.shields.io/badge/version-latest-blue) |

### 🚀 Development Productivity

| Feature | Description | Version |
|---------|-------------|---------|
| [`container-dotfiles`](src/container-dotfiles) | Personal dotfiles and shell configs | ![Version](https://img.shields.io/badge/version-latest-blue) |
| [`oh-my-posh`](src/oh-my-posh) | PowerShell prompt theming | ![Version](https://img.shields.io/badge/version-latest-blue) |
| [`lazygit`](src/lazygit) | Terminal UI for Git operations | ![Version](https://img.shields.io/badge/version-latest-blue) |
| [`continue`](src/continue) | AI-powered code completion | ![Version](https://img.shields.io/badge/version-latest-blue) |
| [`vimrc`](src/vimrc) | Vim configuration setup | ![Version](https://img.shields.io/badge/version-latest-blue) |
| [`powerline-fonts`](src/powerline-fonts) | Enhanced terminal fonts | ![Version](https://img.shields.io/badge/version-latest-blue) |
| [`nerd-fonts`](src/nerd-fonts) | Nerd Fonts collection | ![Version](https://img.shields.io/badge/version-latest-blue) |

### 🔧 System Utilities

| Feature | Description | Version |
|---------|-------------|---------|
| [`postgresql`](src/postgresql) | PostgreSQL database server | ![Version](https://img.shields.io/badge/version-latest-blue) |
| [`draw.io`](src/draw.io) | Diagramming tool integration | ![Version](https://img.shields.io/badge/version-latest-blue) |
| [`speedtest`](src/speedtest) | Network performance testing | ![Version](https://img.shields.io/badge/version-latest-blue) |
| [`git-bfg-cleaner`](src/git-bfg-cleaner) | Git repository cleanup | ![Version](https://img.shields.io/badge/version-latest-blue) |
| [`yq`](src/yq) | YAML/JSON/XML processor | ![Version](https://img.shields.io/badge/version-latest-blue) |
| [`lsd`](src/lsd) | Enhanced `ls` command | ![Version](https://img.shields.io/badge/version-latest-blue) |

## Quick Start

### Using Features in DevContainer

Add features to your `.devcontainer/devcontainer.json`:

```json
{
  "image": "mcr.microsoft.com/devcontainers/base:ubuntu",
  "features": {
    "ghcr.io/40docs/devcontainer-features/mkdocs-environment:0": {},
    "ghcr.io/40docs/devcontainer-features/fortidevsec:23": {},
    "ghcr.io/40docs/devcontainer-features/azure-cli-persistence:0": {}
  }
}
```

### Feature Options

Many features support configuration options:

```json
{
  "features": {
    "ghcr.io/40docs/devcontainer-features/postgresql:0": {
      "version": "15",
      "initDb": true
    }
  }
}
```

## Development

### Testing Features Locally

```bash
# Test a specific feature
devcontainer features test --features src/mkdocs-environment

# Test with different base image
devcontainer features test --features src/fortidevsec --base-image mcr.microsoft.com/devcontainers/base:debian

# Validate feature metadata
devcontainer features validate --features src/lacework-cli
```

### Creating New Features

1. **Create Feature Directory**:
   ```bash
   mkdir -p src/my-new-feature
   cd src/my-new-feature
   ```

2. **Required Files**:
   ```bash
   # Feature metadata (required)
   touch devcontainer-feature.json
   
   # Installation script (required, must be executable)
   touch install.sh
   chmod +x install.sh
   
   # Documentation (auto-generated)
   touch README.md
   ```

3. **Feature Definition** (`devcontainer-feature.json`):
   ```json
   {
     "id": "my-new-feature",
     "name": "My New Feature",
     "description": "Brief description of the feature",
     "version": "1.0.0",
     "options": {
       "version": {
         "type": "string",
         "default": "latest",
         "description": "Version to install"
       }
     }
   }
   ```

4. **Installation Script** (`install.sh`):
   ```bash
   #!/bin/bash
   set -e
   
   # Feature options are available as environment variables
   VERSION=${VERSION:-"latest"}
   
   echo "Installing my-new-feature version ${VERSION}"
   
   # Installation logic here
   # Use ${_REMOTE_USER} for user-specific operations
   
   echo "Feature installation complete"
   ```

### Feature Structure

```
src/
├── feature-name/
│   ├── devcontainer-feature.json  # Feature metadata
│   ├── install.sh                 # Installation script
│   ├── README.md                  # Auto-generated docs
│   ├── NOTES.md                   # Additional notes (optional)
│   └── config-files/              # Configuration templates
```

## Publishing

Features are automatically published to GitHub Container Registry when:

- ✅ Changes are pushed to the `main` branch
- ✅ Version numbers are updated in `devcontainer-feature.json`
- ✅ All tests pass in CI/CD pipeline

Published features are available at:
```
ghcr.io/40docs/devcontainer-features/<feature-name>:<version>
```

## Platform Integration

This repository is part of the 40docs Documentation as Code platform:

- **Multi-Repository**: Git submodule within the main 40docs ecosystem
- **GitOps Integration**: Features used across platform repositories
- **CI/CD**: Automated testing and publishing via GitHub Actions
- **Security**: All features undergo security scanning and validation

## Contributing

1. **Fork** the repository
2. **Create** a feature branch: `git checkout -b feature/my-new-feature`
3. **Develop** following the patterns in existing features
4. **Test** locally with `devcontainer features test`
5. **Submit** a pull request with clear description

### Guidelines

- ✅ Follow semantic versioning for feature versions
- ✅ Include comprehensive error handling in install scripts
- ✅ Use `${_REMOTE_USER}` for user-specific operations
- ✅ Verify checksums for downloaded binaries
- ✅ Clean up temporary files and caches
- ✅ Test with multiple base images (Ubuntu, Debian, Alpine)

## Support

- **Documentation**: Each feature includes auto-generated documentation
- **Issues**: Report bugs and feature requests via GitHub Issues
- **Platform**: Part of the 40docs ecosystem - see main repository for broader context

## License

This project is licensed under the terms specified in the [LICENSE](LICENSE) file.

---

**Part of the 40docs Platform** | [Documentation](https://40docs.github.io) | [Platform Repository](https://github.com/40docs/)
