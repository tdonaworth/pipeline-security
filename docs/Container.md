# Container Scanning

### What Is Container Scanning?
Container scanning, is the process of scanning containers and their components to identify potential security threats. It is a fundamental process of container security, and the number one tool for many teams looking to secure their containerized DevOps workflows.

Synonyms: `Container Image Scanning`, `Image Scanning`, `Docker Scanning`

## [Snyk Container](https://docs.snyk.io/products/snyk-container)
Snyk Container provides tools and integrations for quickly finding and fixing container related vulnerabilities. It allows you to create images with security built-in from the start.

### [Run Locally](https://docs.snyk.io/products/snyk-open-source/use-snyk-open-source-from-the-cli)
```bash
snyk container test
```

### CI/CD
* [GitHub Action](https://github.com/snyk/actions)
* [AWS CodePipeline](https://docs.snyk.io/integrations/ci-cd-integrations/aws-codepipeline-integration)

### Pre-Commit
* Manual Execution:
```yaml
repos: 
  - repo: local
    hooks:
    - id: snyk
        name: snyk
        entry: ./snyk.sh
        language: system
```
```bash
# snyk.sh
#!/bin/bash
RED='\033[1;31m' # Bold red
NC='\033[0m' # No Color

# Check if snyk is installed
if ! [ -x "$(command -v snyk)" ]
then
    echo -e "${RED}Snyk could not be found. Please make sure Snyk is installed properly.\nDocumentation can be found here: https://support.snyk.io/hc/en-us/articles/360003812538-Install-the-Snyk-CLI${NC}"
    exit 1
fi

snyk container test --severity-threshold=high
```

## [Trivy](https://github.com/aquasecurity/trivy)
Trivy (tri pronounced like trigger, vy pronounced like envy) is a comprehensive security scanner. It is reliable, fast, extremely easy to use, and it works wherever you need it.

Trivy has different scanners that look for different security issues, and different targets where it can find those issues.

### Targets:

* Container Image
* Filesystem
* Git repository (remote)
* Kubernetes cluster or resource
### Scanners:

* OS packages and software dependencies in use (SBOM)
* Known vulnerabilities (CVEs)
* IaC misconfigurations
* Sensitive information and secrets