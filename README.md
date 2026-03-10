# AI Experts Project (JS/TS)

This project contains a small JavaScript/TypeScript application with a test suite and Docker configuration.

## How to run tests locally

```bash
# Install dependencies
npm install

# Run tests
npm test
```

## How to build and run tests with Docker

```bash
# Build the Docker image
# Note: If building from a OneDrive-synced directory on Windows, use the legacy builder:
docker build -t ai-software-engineer-assignment-ts .
# Or on Windows PowerShell with OneDrive:
# $env:DOCKER_BUILDKIT=0; docker build -t ai-software-engineer-assignment-ts .

# Run tests in Docker
docker run --rm ai-software-engineer-assignment-ts
```

