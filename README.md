

[[_TOC_]]

---

# Gitlab Templates

## Components

### Git Mirroring

This component aids in using GitLab CI/CD to mirror one git repository to another. Useful to keep two repositories in sync.

Read more [here](../templates/git-mirroring/README.md)

#### Simple example

```yaml
include:
  - component: $CI_SERVER_FQDN/matt-pakulski/gitlab-templates/git-mirroring/template@latest

my-mirroring-job:
  extends: .git-mirroring
  variables:
    SOURCE_REPO_URL: https://gitlab.com/gitlab-org/gitlab
    TARGET_REPO_URL: https://gitlab.com/example/gitlab-fork
    TARGET_PASSWORD: $REPO_EXAMPLE_TOKEN # defined in GitLab UI CI/CD variables
```