# Bitbucket server post build status

Post build status to bitbucket server

## ⚙️ Configuration

<details>
<summary>Inputs</summary>

| Key | Description | Flags | Default |
| --- | --- | --- | --- |
| `domain` | Bitbucket Server domain name without protocol eg 'my-domain.com' | required |  |
| `username` | The username used to make REST calls to bitbucket server | required |  |
| `password` | The password for the bitbucket server username | required |  |
| `preset_status` | If not set to `AUTO`, this step will set a specific status instead of reporting the current build status. Can be one of `AUTO`, `INPROGRESS`, `SUCCESSFUL`, or `FAILED`. If you don't set this option, or select `AUTO`, the step will send `SUCCESSFUL` status if the current build status is `SUCCESSFUL` (no step failed previously) and `FAILED` status if the build previously failed. Use this to report `INPROGRESS` for builds that are just started. | required | "AUTO" |
| `git_clone_commit_hash` |  Git commit hash | required | $GIT_CLONE_COMMIT_HASH |
| `app_title` |  Bitrise app title | required | $BITRISE_APP_TITLE |
| `build_number` |  Bitrise build number | required | $BITRISE_BUILD_NUMBER |
| `build_url` |  Bitrise build url | required | $BITRISE_BUILD_URL |
| `triggered_workflow_id` |  Bitrise triggered workflow id | required | $BITRISE_TRIGGERED_WORKFLOW_ID |
</details>

## BitBucket API

Exact usage of the API BitBucket Rest request can seen in [`step.sh`](step.sh)

### Basic example

Typically you want to notify bitbucket when a build is started and when a build has finished. You can do this by adding this step twice to the steps of your workflow:

```
  my-workflow:
    steps:
    
    - bitbucket-server-post-build-status:
        inputs:
        - username: "$BITBUCKET_SERVER_USERNAME"
        - password: "$BITBUCKET_SERVER_PASSWORD"
        - domain: "$BITBUCKET_SERVER_DOMAIN"
        - preset_status: INPROGRESS
    
    - other-steps..
    - ..for-this-workflow
    
    - bitbucket-server-post-build-status:
        inputs:
        - username: "$BITBUCKET_SERVER_USERNAME"
        - password: "$BITBUCKET_SERVER_PASSWORD"
        - domain: "$BITBUCKET_SERVER_DOMAIN"

```

Make sure you use a 'secret' variable for the password
