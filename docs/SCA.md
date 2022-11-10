# SCA - Software Composition Analysis

### What Is SCA?
Software Composition Analysis (SCA) provides visibility into the open source components and libraries being incorporated into the software that development teams create. SCA can help manage security and license-related risks. It can help ensure that any open source component embedded in applications meets certain standards, to avoid introducing risks that could result in a data breach, compromised intellectual property, or legal disputes.

Synonyms: `Dependency Scanning`, `Supply Chain Security`
Related: `Software Bill of Materials (SBOM)`

## Dependabot
Dependabot is a tool for automated dependency updates built into GitHub.

If your code depends on a package with a security vulnerability, this can cause a range of problems for your project or the people who use it. You should upgrade to a secure version of the package as soon as possible. If your code uses malware, you need to replace the package with a secure alternative.

### Run Locally
* Not Applicable - only intended to run within GitHub. Though for the purposes of development you *can* [run it locally](https://github.com/dependabot/dependabot-core#running-with-docker). 
### CI/CD
* GitHub Actions - no specific action is needed, only ensuring Dependabot is enabled for your repository or organization.


## [Snyk Open Source](https://docs.snyk.io/products/snyk-open-source)
Snyk Open Source allows you to find and fix vulnerabilities in the open source libraries used by your applications. It also allows you to find and address licensing issues in (or caused by) these open source libraries.

### [Run Locally](https://docs.snyk.io/products/snyk-open-source/use-snyk-open-source-from-the-cli)
```bash
snyk test
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

snyk test --severity-threshold=high
```

## [GitHub Dependency Review](https://docs.github.com/en/rest/dependency-graph/dependency-review)
This action scans your pull requests for dependency changes, and will raise an error if any vulnerabilities or invalid licenses are being introduced. The action is supported by an API endpoint that diffs the dependencies between any two revisions.

### CI/CD
* [GitHub Action](https://github.com/actions/dependency-review-action)