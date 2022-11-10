# Runner Hardening

### What Is Runner Hardening?
This is a process or actions that should be performed to ensure that the Runner/Agent where the automated actions run on, is secured. Compromised dependencies and build tools typically make outbound calls to exfiltrate credentials, or may tamper source code, dependencies, or artifacts during the build. So taking correct actions to prevent this is vital.

## [Harden Runner](https://github.com/step-security/harden-runner)
Harden-Runner GitHub Action installs a security agent on the GitHub-hosted runner (Ubuntu VM) to

1. Prevent exfiltration of credentials
2. Detect tampering of source code during build
3. Detect compromised dependencies and build tools

An [interactive app](https://app.stepsecurity.io/) is available to help you harden your actions!

![Harden Runner Process](https://raw.githubusercontent.com/step-security/harden-runner/main/images/main-screenshot1.png "Harden Runner Process")

### [How to use](https://github.com/step-security/harden-runner#how)

```yaml
steps:
  - uses: step-security/harden-runner@ebacdc22ef6c2cfb85ee5ded8f2e640f4c776dd5
    with:
      egress-policy: audit
```
