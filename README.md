# Pipeline Security
A repository that demonstrates some common pipeline security practices using GitHub Actions

# Workflow:

Automating security within your pipeline is one of the best ways to ensure the required controls are being met. Though, this shouldn't be the only place where security tools are run. Each tool listed below, has the capability to run locally, and should be done prior to code commits. The key of automating these within the pipeline is to ensure the mimiumum checks are performed, and vulnerable code doesn't make it into production; but it's not the ONLY step.

1. [Linting](./docs/Linting.md)
2. [SAST](./docs/SAST.md)
3. [DAST](./docs/DAST.md)
4. [Software Composition Analisys (SCA)](./docs/SCA.md)
5. [Container Scanning](./docs/Container.md)

## BONUS
6. [Runner Hardening](./docs/Hardening.md)