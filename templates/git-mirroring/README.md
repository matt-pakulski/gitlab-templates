# GitLab CI/CD Pipeline Template for Repository Syncing

This GitLab CI/CD pipeline template is used to sync changes from one Git repository to another.

Some example scenarios:
- Sync changes from your GitLab repo to GitHub every time changes are added.
- Schedule a GitLab CI/CD pipeline to periodically sync changes from a git repository on GitHub to your team's BitBucket backup.
- Use a GitHub webhook that fires whenever you push changes to your GitHub repository to trigger a GitLab CI/CD pipeline to sync changes from your GitHub repository to a backup filesystem behind your company's VPN (requires using your own GitLab runner).
- Schedule a GitLab CI/CD pipeline to periodically sync changes only on the main branch of GitHub repository to your forked version of the repository.

## Getting Started

Import and configure the GitLab template into your GitLab CI/CD enabled git repository.

```yaml
include:
  - component: $CI_SERVER_FQDN/matt.pakulski/git-mirroring@latest

my-mirroring-job:
  extends: .git-mirror
```

## Environment Variables

The script uses the following environment variables:

- `SOURCE_REPO_URL`: The source Git repository URL.
- `TARGET_REPO_URL`: The target Git repository URL.
- `MIRROR_STRATEGY`: The mirror strategy ("mirror" or "push").
- `FORCE_PUSH_BRANCHES`: A boolean indicating whether to force push branches.
- `FORCE_PUSH_TAGS`: A boolean indicating whether to force push tags.
- `PUSH_TAGS`: A boolean indicating whether to push tags.
- `PUSH_REFS`: A list of refs to push.

For each of the source and target repositories, the following variables are used:

- `GIT_[SOURCE|TARGET]_USER`: The username for the repository when using HTTPS.
- `GIT_[SOURCE|TARGET]_PASSWORD`: The password for the repository when using HTTPS.
- `GIT_[SOURCE|TARGET]_SSH_KEY`: The SSH key file for the repository when using Git/SSH.

## Example Usages

Here are a few example usages of this script:

1. **Mirror a Repository**

   If you want to mirror a repository from Bitbucket to GitLab, you can set the `SOURCE_REPO_URL` to your Bitbucket repository URL, the `TARGET_REPO_URL` to your GitLab repository URL, and the `MIRROR_STRATEGY` to "mirror".

2. **Push Branches and Tags**

   If you want to push all branches and tags from a GitHub repository to a GitLab repository, you can set the `SOURCE_REPO_URL` to your GitHub repository URL, the `TARGET_REPO_URL` to your GitLab repository URL, the `MIRROR_STRATEGY` to "push", and the `PUSH_TAGS` to "true".

3. **Force Push Branches**

   If you want to force push all branches from a GitHub repository to a GitLab repository, you can set the `SOURCE_REPO_URL` to your GitHub repository URL, the `TARGET_REPO_URL` to your GitLab repository URL, the `MIRROR_STRATEGY` to "push", and the `FORCE_PUSH_BRANCHES` to "true".

Remember to replace the variables with your actual values when setting up the pipeline. Check the official GitLab CI/CD documentation for more detailed instructions.
