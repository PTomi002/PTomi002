## Snyk 101

### Integration Types

The different integration types and scans result in different outputs.

#### via Snyk CLI

Snyk scan issued via CLI in the CI/CD pipelines.

Ignoring vulnerabilities can be done via `.snyk` file.

Pros:
- Sees the actual build environment / dependencies
- Has access to the build outputs (gradle artifacts / files)
- Thus shows more accurate results

#### via GitHub

Snyk connects to the repository via GutHub API.

Ignoring vulnerabilities can be done only by Snyk UI.

Pros:
- Helm templating works with this type
- Repos that dont have CI/CD should be integrated this way

### Scan Types

#### Code Scan

Scans the code itself for vulnerabilities.

#### IaC Scan

Scans the Infrastructure as Code type of descriptors and manifests and templates.

Templating capability works with GitHub Integration only.

#### Open Source Scan

Scans the project dependencies handled by the dependency managers.

#### Container Scan

Scans the Dockerfiles and the base images used fo the containers.

### Commands

Issue local Snyk testing and have a result SARIF file:
```
snyk test --sarif-file-output=results.sarif
```

Make continuous monitoring by sending snapshots to the Snyk Cloud:
```
snyk container monitor myregistry.io/app:v1.2.3 \
    --project-name=prod-app-container \
    --project-tags=environment=production,team=backend
```

### SARIF File

A JSON based standard format to represent the output from static analysis tools.