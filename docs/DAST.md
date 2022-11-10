# DAST - Dtatic Application Security Testing

### What is SAST?
DAST works by using automation that simulates different malicious attacks on an application while it’s running. The outcome is to detect if there are any unexpected or undetected code or security defects that can be exploited by an attacker. Cross-site scripting, command and SQL injection errors, path traversal, and insecure server configuration are a few of those security risks that can be detected by DAST.

Synonyms: `Black Box Testing`, `Penetration Testing`

## [OWASP ZAP (Zed Attack Proxy)](https://www.zaproxy.org/)

### Run Locally
* [Desktop User Guide](https://www.zaproxy.org/docs/desktop/)

### CI/CD
* [GitHub Actions](https://github.com/marketplace?query=owasp+zap)


## [Dastardly](https://portswigger.net/burp/dastardly)
Dastardly is a free, lightweight web application security scanner for your CI/CD pipeline. It is designed specifically for web developers, and checks your application for seven security issues that are likely to interest you during software development. Dastardly is based on the same scanner as [Burp Suite](https://portswigger.net/burp).

For full documentation on using Dastardly, please consult the [Dastardly documentation](https://portswigger.net/burp/documentation/dastardly).

### [Run Locally](https://codeql.github.com/docs/codeql-cli/)
Dastardly is specifically designed to run in a CI/CD Pipeline. For performing local DAST testing, utilize [Burp Suite's Burp Scanner](https://portswigger.net/burp) instead.

### [CI/CD](https://portswigger.net/burp/dastardly)
* [GitHub Action](https://github.com/PortSwigger/dastardly-github-action)
    * [Example](../.github/workflows/security_dastardly.yml)