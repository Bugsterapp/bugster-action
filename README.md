# Bugster.dev GitHub Action

Send deployment notifications to [Bugster](https://bugster.dev) from your GitHub workflows.

## Usage

```yaml
name: Deploy

on:
  pull_request:

jobs:
  trigger-bugster:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Trigger Bugster
        uses: Bugsterapp/bugster-action@v1
        with:
          bugster_api_key: ${{ secrets.BUGSTER_API_KEY }}
          organization_id: "org_123"
          project_id: "proj_456"
          environment_url: "https://preview.example.com"
```

This will send a deployment notification to Bugster Cloud with the current commit SHA and branch from the workflow context.

---

## Inputs

| Name              | Required | Default      | Description                                                                 |
|-------------------|----------|--------------|-----------------------------------------------------------------------------|
| `bugster_api_key` | ✅       | —            | API key for Bugster Cloud. Store this in `secrets.BUGSTER_API_KEY`.         |
| `environment_url` | ✅       | —            | URL of the deployed environment (e.g. `https://app.example.com`).           |
| `organization_id` | ✅       | —            | Bugster organization ID.                                                    |
| `project_id`      | ✅       | —            | Bugster project ID.                                                         |
| `deployment_state`| ❌       | `success`    | One of `in_progress`, `success`, `cancelled`, `failed`, `error`. Invalid values fall back to `success`. |
| `commit_sha`      | ❌       | `GITHUB_SHA` | Commit SHA (auto-filled if not provided).                                   |
| `branch`          | ❌       | `GITHUB_REF_NAME` | Branch name (auto-filled if not provided).                              |
| `api_base`        | ❌       | `https://api.bugster.app` | Base API URL (useful for testing).                                  |
| `timeout_seconds` | ❌       | `60`         | Request timeout in seconds.                                                 |

---

## Outputs

| Name       | Description                                  |
|------------|----------------------------------------------|
| `status`   | HTTP status code returned by the API.        |
| `response` | Response body returned by the API (truncated). |

---

## Example with custom deployment state

```yaml
- name: Notify Bugster (in-progress)
  uses: Bugsterapp/bugster-action@v1
  with:
    bugster_api_key: ${{ secrets.BUGSTER_API_KEY }}
    organization_id: "org_123"
    project_id: "proj_456"
    environment_url: "https://preview.example.com"
    deployment_state: "in_progress"
```
# bugster-action
