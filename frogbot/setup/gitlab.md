---
description: 'To install Frogbot on GitLab repositories using GitLab CI:'
---

# GitLab

For GitLab, the frogbot-config.yml file should be placed in the root of the Git repository at the following path:&#x20;

{% hint style="info" %}
.gitlab/.frogbot/frogbot-config.yml.&#x20;
{% endhint %}

Ensure that this file is pushed to the target branch before it can be utilized by Frogbot. If a pull request includes the frogbot-config.yml and the target branch doesn't, the file will be ignored.

Here is an example of the frogbot-config.yml file structure specifically for GitLab:

```yaml
params:
  gitlab:
    repoName: my-gitlab-repo-name
    branches:
      - master
  scan:
    projects:
      - workingDirs:
          - path/to/npm/project-1
          - path/to/npm/project-2

```

## To integrate Frogbot into GitLab repositories using GitLab CI,&#x20;

Follow these optimized steps:

1. Ensure you have the JFrog environment connection details.
2.  Navigate to your GitLab repository settings and save JFrog connection details as repository secrets: JF\_URL, JF\_USER, and JF\_PASSWORD.

    Note: Alternatively, use JF\_XRAY\_URL and JF\_ARTIFACTORY\_URL instead of JF\_URL. JF\_ACCESS\_TOKEN can replace JF\_USER and JF\_PASSWORD. Ensure these tokens are not set as protected in GitLab.
3. Add the following frogbot-scan job to your .gitlab-ci.yml file:

| Variable                                    | Mandatory/Optional | Additional Options                                                                                                                  |
| ------------------------------------------- | ------------------ | ----------------------------------------------------------------------------------------------------------------------------------- |
| JF\_URL                                     | Mandatory          | Version 3.29.0 or above of Xray required                                                                                            |
| JF\_ACCESS\_TOKEN                           | Mandatory          | Read permissions for Xray                                                                                                           |
| JF\_USER                                    | Optional           |                                                                                                                                     |
| JF\_PASSWORD                                | Optional           |                                                                                                                                     |
| JF\_GIT\_TOKEN                              | Mandatory          | GitLab access token with specific permissions based on deployment type                                                              |
| JF\_GIT\_PROVIDER                           | Mandatory          | gitlab                                                                                                                              |
| JF\_GIT\_OWNER                              | Mandatory          | $CI\_PROJECT\_NAMESPACE                                                                                                             |
| JF\_GIT\_REPO                               | Mandatory          | $CI\_PROJECT\_NAME                                                                                                                  |
| JF\_GIT\_PULL\_REQUEST\_ID                  | Mandatory          | $CI\_MERGE\_REQUEST\_IID                                                                                                            |
| JF\_GIT\_API\_ENDPOINT                      | Optional           | Default: [https://gitlab.com](https://gitlab.com/)                                                                                  |
| JF\_RELEASES\_REPO                          | Optional           | Artifactory repository key (if Frogbot machine lacks internet access, set up a Remote Repository as described)                      |
| JF\_INSTALL\_DEPS\_CMD                      | Mandatory if set   | Command to install project dependencies (e.g., "nuget restore")                                                                     |
| JF\_WORKING\_DIR                            | Optional           | Relative path to the root of the project in the Git repository (Default: ".")                                                       |
| JF\_PATH\_EXCLUSIONS                        | Optional           | List of exclusion patterns for paths in the source code during SCA scans (Default: "_.git_;_node\_modules_;_target_;_venv_;_test_") |
| JF\_WATCHES                                 | Optional           | Xray Watches (comma-separated)                                                                                                      |
| JF\_PROJECT                                 | Optional           | JFrog project key                                                                                                                   |
| JF\_INCLUDE\_ALL\_VULNERABILITIES           | Optional           | Display all existing vulnerabilities in pull requests (Default: "FALSE")                                                            |
| JF\_AVOID\_PREVIOUS\_PR\_COMMENTS\_DELETION | Optional           | Keep old comments in pull requests (Default: "FALSE")                                                                               |
| JF\_FAIL                                    | Optional           | Fail Frogbot task if any security issue is found (Default: "TRUE")                                                                  |
| JF\_REQUIREMENTS\_FILE                      | Optional           | Relative path to Pip requirements.txt file                                                                                          |
| JF\_USE\_WRAPPER                            | Optional           | Use Gradle wrapper (Default: "FALSE")                                                                                               |
| JF\_DEPS\_REPO                              | Optional           | Name of the repository to download dependencies from (if not set in frogbot-config.yml)                                             |
| JF\_BRANCH\_NAME\_TEMPLATE                  | Optional           | Template for generated branch name in pull requests                                                                                 |
| JF\_COMMIT\_MESSAGE\_TEMPLATE               | Optional           | Template for commit message in pull requests                                                                                        |
| JF\_PULL\_REQUEST\_TITLE\_TEMPLATE          | Optional           | Template for pull request title                                                                                                     |
| JF\_GIT\_AGGREGATE\_FIXES                   | Optional           | Create a single pull request with all fixes (Default: "FALSE")                                                                      |
| JF\_FIXABLE\_ONLY                           | Optional           | Handle vulnerabilities with fix versions only (Default: "FALSE")                                                                    |
| JF\_MIN\_SEVERITY                           | Optional           | Set the minimum severity for vulnerabilities in pull requests                                                                       |
| JF\_ALLOWED\_LICENSES                       | Optional           | Set the list of allowed licenses                                                                                                    |
| JF\_AVOID\_EXTRA\_MESSAGES                  | Optional           | Avoid adding extra info to pull request comments not related to scan findings (Default: "TRUE")                                     |
| JF\_PR\_COMMENT\_TITLE                      | Optional           | Add a title to pull request comments generated by Frogbot                                                                           |

```yaml
frogbot-scan:
  rules:
    - if: $CI_PIPELINE_SOURCE == 'merge_request_event'
      when: manual
      variables:
        FROGBOT_CMD: "scan-pull-request"
        JF_GIT_BASE_BRANCH: $CI_MERGE_REQUEST_TARGET_BRANCH_NAME
    - if: $CI_COMMIT_BRANCH == $CI_DEFAULT_BRANCH || $CI_PIPELINE_SOURCE == "schedule"
      variables:
        FROGBOT_CMD: "scan-repository"
        JF_GIT_BASE_BRANCH: $CI_COMMIT_BRANCH
  variables:
    JF_URL: $JF_URL
    JF_ACCESS_TOKEN: $JF_ACCESS_TOKEN
    JF_USER: $JF_USER
    JF_PASSWORD: $JF_PASSWORD
    JF_GIT_TOKEN: $USER_TOKEN
    JF_GIT_PROVIDER: gitlab
    JF_GIT_OWNER: $CI_PROJECT_NAMESPACE
    JF_GIT_REPO: $CI_PROJECT_NAME
    JF_GIT_PULL_REQUEST_ID: $CI_MERGE_REQUEST_IID
    JF_GIT_API_ENDPOINT: https://gitlab.example.com
    JF_RELEASES_REPO: ""
    JF_SMTP_SERVER: ""
    JF_SMTP_USER: ""
    JF_SMTP_PASSWORD: ""
    # ... (Other optional variables)
  script:
    - |
      getFrogbotScriptPath=$(if [ -z "$JF_RELEASES_REPO" ]; then echo "https://releases.jfrog.io"; else echo "${JF_URL}/artifactory/${JF_RELEASES_REPO}"; fi)
      curl -fLg "$getFrogbotScriptPath/artifactory/frogbot/v2/[RELEASE]/getFrogbot.sh" | sh
      ./frogbot ${FROGBOT_CMD}

```

