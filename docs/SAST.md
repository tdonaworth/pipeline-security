# SAST - Static Application Security Testing

### What is SAST?
Static application security testing (SAST) is a software testing methodology designed for inspecting and analyzing application source code, byte code, and binaries for coding and design conditions to uncover security vulnerabilities.

Synonyms: `White Box Testing`, `Code Scanning`

## [Linting](./Linting.md)
Linting is the automated checking of your source code for programmatic and stylistic errors. This is done by using a lint tool (otherwise known as linter). A lint tool is a basic static code analyzer.

Because Linting is mostly a subset of full SAST, it's covered in [it's own section](./Linting.md).

## [CodeQL](https://codeql.github.com/)
Discover vulnerabilities across a codebase with CodeQL, a semantic code analysis engine. CodeQL lets you query code as though it were data. Write a query to find all variants of a vulnerability, eradicating it forever. Then share your query to help others do the same.

CodeQL is free for research and open source.
### [Run Locally](https://codeql.github.com/docs/codeql-cli/)
* [Using the CodeQL CLI](https://codeql.github.com/docs/codeql-cli/using-the-codeql-cli/#using-the-codeql-cli)
* [CodeQL CLI reference](https://codeql.github.com/docs/codeql-cli/codeql-cli-reference/#codeql-cli-reference)
* [CodeQL CLI manual](https://codeql.github.com/docs/codeql-cli/manual)

### CI/CD
* [GitHub Action](https://github.com/github/codeql-action)
### Pre-Commit
* Requires Manual Scripting

Example:
```yaml
repos: 
  - repo: local
    hooks:
    - id: codeql
        name: codeql
        entry: ./codql.sh
        language: system
```
```bash
#codeql.sh
#!/bin/bash

exec 1>&2
exitVal=0
while read -r f
do
  filename="${f##*/}"
  extension="${filename##*.}"
  p="$PWD/$f";
  if [[ -f "$p" ]] && { [ "$extension" == "ql" ] || [ "$extension" == "qll" ]; }
  then
    if ! codeql query format --check-only "$p"
    then
      exitVal=1
    fi
  fi
done <<<"$(git diff --cached --relative --name-only)"
exit $exitVal
```


## Semgrep
Semgrep is a fast, open source, static analysis engine for finding bugs, detecting dependency vulnerabilities, and enforcing code standards.
Semgrep analyzes code locally on your computer or in your build environment: code is never uploaded.
Its rules look like the code you already write; no abstract syntax trees, regex wrestling, or painful DSLs.
### [Run Locally](https://semgrep.dev/docs/getting-started/#running-semgrep-locally)
* For macOS:
```
brew install semgrep
```

* For Ubuntu, Windows through Windows Subsystem for Linux (WSL), Linux, macOS:
```
python3 -m pip install semgrep
```

* Docker:
```
docker run --rm -v "${PWD}:/src" returntocorp/semgrep semgrep --config=auto
```


### [CI/CD](https://semgrep.dev/docs/semgrep-ci/running-semgrep-ci-with-semgrep-app/#ci-providers-listed-within-semgrep-app-such-as-github-actions-gitlab-cicd-jenkins)
* [GitHub Example](.github/workflows/security_semgrep.yml)
```yaml
   container:
      # Run this job within the Semgrep container
      image: returntocorp/semgrep
    steps:
      # Checkout your code
      - name: Checkout
        uses: actions/checkout@v3

      # Execute the Semgrep Scan.
      - name: Semgrep Scan
        run: |
          echo "SEMGREP_TO_UPLOAD=semgrep.sarif" >> $GITHUB_ENV
          semgrep scan --sarif --output=semgrep.sarif
        env:
          SEMGREP_APP_TOKEN: ${{ secrets.SEMGREP_APP_TOKEN }}
          SEMGREP_RULES: "p/default"
      
      # Upload the results to GitHub Security (Requires Advanced Security Dashboard)
      - name: Upload SARIF file for GitHub Advanced Security Dashboard
        uses: github/codeql-action/upload-sarif@v2
        with:
          sarif_file: ${{ env.SEMGREP_TO_UPLOAD }}
        if: always()
```

### Pre-Commit
```yaml
repos:
- repo: https://github.com/returntocorp/semgrep
  rev: 'v0.121.1'
  hooks:
    - id: semgrep
      # See semgrep.dev/rulesets to select a ruleset and copy its URL
      args: ['--config', '<SEMGREP_RULESET_URL>', '--error', '--skip-unknown-extensions']
```
## [Snyk Code](https://docs.snyk.io/products/snyk-code/introducing-snyk-code)
Snyk Code is an AI driven SAST engine used to find vulnerabilities in your code.

### [Run Locally](https://docs.snyk.io/products/snyk-code/cli-for-snyk-code)
```bash
snyk code test
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

snyk code test --severity-threshold=high
```

## :warning: SonarQube / SonarCloud :warning:
:warning: :exclaimation: <span style="color:red"> **SonarQube/Cloud is NOT ENOUGH** </span> :exclaimation: :warning:
If you rely on SonarQube/Cloud as your only form of SAST, then you do NOT have sufficient SAST tooling in place. SonarQube/Cloud has limited Linting capabilities, and even more limited SAST abilities. It can detect some things, but compared to other Linters and SAST tools, it simply isn't enough and does not meet the needs to be considered a stand-alone SAST solution.
