# Setup

Setting up JFrog Frogbot requires the following components:

1. **JFrog Platform Server:**
   * **Requirement:** A JFrog Platform server is essential for hosting and managing your artifacts, as well as integrating JFrog Frogbot into your CI/CD pipeline.
   * **Availability:** If you don't have a JFrog Platform server, you can set up one for free. Ensure that it is accessible and properly configured before integrating Frogbot.
2. **CI Server:**
   * **Requirement:** A Continuous Integration (CI) server is necessary to execute the scan tasks performed by JFrog Frogbot.
   * **Examples:** Common CI servers include Jenkins, GitLab CI, Travis CI, CircleCI, and others.
   * **Integration:** Integrate Frogbot into your CI/CD workflow to automatically trigger scans on pull requests, ensuring early detection of vulnerabilities.
3. **JFrog Frogbot Configuration:**
   * **Configuration File:** Set up and configure Frogbot by providing the necessary settings, including connection details to your JFrog Platform server, CI server integration, and any specific parameters related to your project.
4. **Access to Git Repositories:**
   * **Repository Integration:** Ensure that Frogbot has the required permissions to access and scan your Git repositories. Integration with Git providers like GitHub, GitLab, Bitbucket, or Azure Repos may involve configuring API tokens or credentials.
5. **JFrog Advanced Security Package (Optional):**
   * **Requirement:** Some advanced features of Frogbot, such as Static Application Security Testing (SAST), Vulnerability Contextual Analysis, Secrets Detection, and Infrastructure as Code scans, may require the JFrog Advanced Security Package.
   * **License:** Ensure proper licensing for the advanced security features if you choose to utilize them.
6. **Dependencies and Plugins:**
   * **Plugin Installation:** Depending on your CI server, you may need to install the necessary plugins or extensions to enable seamless integration with JFrog Frogbot.
7. **Pipeline Definition (CI/CD):**
   * **Pipeline Setup:** Define CI/CD pipelines that include Frogbot tasks, ensuring that scans are executed at the appropriate stages of your development workflow (e.g., on pull requests, before merging).
8. **Environment Variables:**
   * **Sensitive Information:** If applicable, manage sensitive information such as API tokens, credentials, or keys securely using environment variables or secret management tools.

#### Select your preferred CI server:

* [Gitlab](gitlab.md)
