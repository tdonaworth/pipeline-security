# Linting
### What Is Linting?
Linting is the automated checking of your source code for programmatic and stylistic errors. This is done by using a lint tool (otherwise known as linter). A lint tool is a basic static code analyzer.

### Why Is Linting Important?
Linting is important to reduce errors and improve the overall quality of your code. Using lint tools can help you accelerate development and reduce costs by finding errors earlier.

## [Megalinter](https://oxsecurity.github.io/megalinter/latest/)
MegaLinter is an Open-Source tool for CI/CD workflows that analyzes the consistency of your code, IAC, configuration, and scripts in your repository sources, to ensure all your projects sources are clean and formatted whatever IDE/toolbox is used by their developers.

Supporting [51 languages](https://oxsecurity.github.io/megalinter/latest/supported-linters/#languages), [23 formats](https://oxsecurity.github.io/megalinter/latest/supported-linters/#formats), [21 tooling formats](https://oxsecurity.github.io/megalinter/latest/supported-linters/#tooling-formats) and ready to use out of the box, as a GitHub action or any CI system highly configurable and free for all uses.

This can be overkill for smaller applications/services, but it ensures that everything is captured. If anything, start here, and find which linters are giving you the most information, and narrow down to them either through the MegaLinter config, or go to them natively.

### Run Locally
* Locall Installation: 
```
npm install mega-linter-runner --save-dev
```
* No Installation: 
```
npx mega-linter-runner -r beta -e 'ENABLE=MARKDOWN,YAML' -e 'SHOW_ELAPSED_TIME=true'
```

### CI/CD
* [GitHub Actions](https://oxsecurity.github.io/megalinter/latest/installation/#github-action)
* [Jenkins](https://oxsecurity.github.io/megalinter/latest/installation/#jenkins)

### Pre-Commit
Pre-commit hook
```
  - repo: https://github.com/oxsecurity/megalinter
    rev: v6.8.0 # Git tag specifying the hook, not mega-linter-runner, version
    hooks:
      - id: megalinter-incremental # Faster, less thorough
        stages:
          - commit
      - id: megalinter-full # Slower, more thorough
        stages:
          - push
```
