# OpenShock Trigger Action

This repository contains a GitHub Action for triggering shocks via the OpenShock API. The action can be run manually or scheduled to run at specific times.

## Prerequisites

Before using this action, ensure that you have the following:

- A GitHub account
- Access to the OpenShock API and an API key

## Fork the Repository

Make a private fork of this repository using the **Fork** button in the upper right corner.

## Adding Your API Key (and Scheduled Settings)

To securely store your OpenShock API key:

1. Go to your GitHub repository.
1. Click on **Settings**.
1. Navigate to **Secrets and variables** > **Actions**.
1. Click on **New repository secret**.
1. Add a secret with the name `API_KEY` and your actual OpenShock API key as the value.

If you are going to run the workflow on a schedule, also add these secrets:

   - `SHOCK_ID`: The default shock ID you want to trigger.
   - `INTENSITY`: The default intensity of the shock (e.g., 50).
   - `DURATION`: The default duration of the shock in milliseconds (e.g., 1000).

They are unused when running the workflow manually.

## Running the Workflow Manually

To run the workflow manually:

1. Go to the **Actions** tab in your GitHub repository.
1. Select the **Trigger Shock Workflow** from the list of workflows.
1. Click on the **Run workflow** button.
1. Fill in the required inputs:
     - **Shock ID**: The ID of the shock you want to trigger.
     - **Intensity**: The intensity of the shock (default is 50).
     - **Duration**: The duration of the shock in milliseconds (default is 1000).
1. Click **Run workflow** to trigger the action.

## Running the Workflow on a Schedule

The workflow is configured with a placeholder cron job that will never run:

```yaml
cron: '59 23 31 2 *'  # This cron expression is set to a non-existent date (February 31)
```

You can modify this cron expression in the workflow file (`.github/workflows/trigger-shock.yml`) to set your desired schedule.

### Example Cron Expressions
Here are a few example cron expressions you can use:

- **Every hour**: `0 * * * *`
- **Every day at midnight**: `0 0 * * *`
- **Every Monday at 9 AM**: `0 9 * * 1`
- **Every weekday at 5:30 AM**: `30 5 * * 1-5`

Update the cron expression to match your scheduling needs.

Notes:

- The cron is the time your request will be queued so the shock may come a few seconds or minutes later.
- See the [GitHub Actions caveats](https://docs.github.com/en/actions/writing-workflows/choosing-when-your-workflow-runs/events-that-trigger-workflows#schedule) on scheduling.
- Time zone is UTC so you will need to adjust the times with daylight savings time switches. You can also implement [this hacky workaround](https://github.com/orgs/community/discussions/13454#discussioncomment-4091593).
