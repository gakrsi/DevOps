# FrogBot

* **JFrog Frogbot Overview:**
  1. Git bot designed for scanning Git repositories for security vulnerabilities.
  2. Immediate scanning of pull requests upon opening, providing early detection of potential vulnerabilities before merging.
  3. Ensures proactive fixing of vulnerabilities even before they are introduced into the codebase.
  4. Periodic scanning of the Git repository with the ability to create pull requests containing fixes for identified vulnerabilities.
* **Key Features:**
  1. **Software Composition Analysis (SCA):**
     * Scans project dependencies for security issues.
     * Leverages enhanced CVE data from JFrog Security Research team.
     * Utilizes JFrog's extensive vulnerabilities database continuously updated with new component vulnerability data.
  2. **Validate Dependency Licenses:**
     * Ensures compliance of project dependency licenses with a predefined list of approved licenses.
  3. **Static Application Security Testing (SAST):**
     * Employs fast and accurate security-focused engines.
     * Detects zero-day security vulnerabilities in source code while minimizing false positives.
  4. **CVE Vulnerability Contextual Analysis:**
     * Utilizes code context to eliminate false positive reports on non-applicable vulnerable dependencies.
     * Creates pull request comments with full descriptions of security issues caused by applicable CVE vulnerabilities.
     * Currently supported for Python, JavaScript, and Java code.
  5. **Secrets Detection:**
     * Identifies exposed secrets in the code to prevent accidental leaks of internal tokens or credentials.
  6. **Infrastructure as Code (IaC) Scans:**
     * Scans Infrastructure as Code (Terraform) files for early detection of cloud and infrastructure misconfigurations.
     * Requires the JFrog Advanced Security Package for SAST, Vulnerability Contextual Analysis, Secrets Detection, and IaC scans.
* **Supported Git Providers:**
  * Azure Repos
  * Bitbucket Server
  * GitHub
  * GitLab
