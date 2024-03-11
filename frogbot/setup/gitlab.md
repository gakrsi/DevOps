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

