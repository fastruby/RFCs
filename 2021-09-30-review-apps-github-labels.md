# Handling Review Apps using labels in GitHub PRs

## Problem:

Heroku's Review Apps are created automatically in many projects when a PR is created/updated. While this helps in the QA process, this has downsides in some cases:

- if the PR is a work-in-progress, the review app is probably not needed yet
- if the PR is waiting for a review of the code, the review app is probably not needed yet
- if the PR changes something that can't really be QA'd with a review app, it's not needed at all (like updating the readme, setting up docker, fixing a broken test, etc)
- Automatically-created Review Apps are deleted after 2 days so the person doing QA has to go to heroku and re-create the review app manually if it's done after that time

In all those cases, we have Review Apps running for a couple of days that nobody is using, costing money, and when somebody actually needs to use them, the review app is already destroyed and the re-creating process involves many steps.

## Proposal:

Use Github Workflows to trigger Review Apps creation/destructions from within the PR by using specific labels. This way, the Review Apps won't be created automatically if not needed (saving money), and when somebody is ready to QA they don't need to go to Heroku and remember all the steps to create them manually (saving time).

## Implementation idea:

We will need different parts for this integration:

- A GitHub Workflows configuration that will trigger different GitHub Actions depending on labels being added and PR's being closed
- A GitHub Action that will manage creating a Review App using Heroku's API and updating the PR's label using GitHub's API
- A GitHub Action that will manage destroying a Review App using Heroku's API and updating the PR's label using GitHub's API
- A project using these workflows would have some ENV variables set in the project's secrets so the GitHub Actions can connect to Heroku's API (API token, Pipeline ID, etc)

### GitHub Workflows configuration:

We did some tests for this and the setup is really straightforward, we can run a job when a label is added to a PR and the label has a specific value (the labels we are proposing are `deploy-review-app` and `destroy-review-app`). You can see it working in this test repo https://github.com/arielj/test-gh-labels/actions

The workflows configuration will look something like this:

```
name: Review Apps
on:
  pull_request:
    types: [labeled]

jobs:
  deploy-review-app:
    if: ${{ github.event.label.name == 'deploy-review-app' }}
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v1
      - name: Deploy Review App
        run: echo "Deploy!"

  destroy-review-app:
    if: ${{ github.event.label.name == 'destroy-review-app' }}
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v1
      - name: Destroy Review App
        run: echo "Destroy!"
```

for each of those jobs we would actually use a GitHub Action instead of just echoing some text.

### GitHub Actions:

We would need to implement 2 public GitHub Actions (one for creating/updating review apps, and one for destroying them), but the logic will be similar in both cases so we'll describe it in a generic way.

The GitHub Actions will have this logic:

- Include heroku's and github's npm modules to handle the different API requests that we'll need
- Check that the user doing the action is an admin/maintainer/contributor of the repo so random people won't be able to trigger Review Apps creation adding labels (so this is safe to use in OSS projects)
- Get all the info needed from the PR and the repo's secret (for security) to generate the payload for Heroku's API
- Trigger the Review App concrete action (create/update/destroy)
- Remove the label that triggered this action using Github's API

### Resources

We've found some resources and existing GitHub Actions to use as reference for most of the code needed:

- Create Heroku's review app https://github.com/mheap/github-action-pr-heroku-review-app (this includes using the npm module, checking the user permissions, preparing the payload, hitting Heroku's `create` endpoint for review apps)
- Add labels to a PR https://github.com/TimonVS/pr-labeler-action (this includes connecting to the GitHub API to set labels for a PR, we can use it as reference for removing the label instead)
- How to create Github Actions https://docs.github.com/en/actions/creating-actions/creating-a-javascript-action (this shows the step-by-step on creating github actions)
- Documentation on setting ENV variables for the GitHub Actions https://docs.github.com/en/actions/learn-github-actions/environment-variables (needed for the Heroku's API token and Pipeline ID)

## Complete workflow:

- A developer creates a PR (no review app is created)
- When the PR is ready for QA and the person doing the QA is ready, they will add the `deploy-review-app` label to the PR
- After a moment, the GitHub Action will be triggered, creating a Review App and removing the `deploy-review-app` label (the information of the deploy should be added to the PR by Heroku like it's currently doing)
- When the QA is done, the QA person will add the `destroy-review-app` label to the PR
- After a moment, the GitHub Action will be triggered, destroying the Review App and removing the `destroy-review-app` label

### Extra steps:

- We could have a workflow configuration that destroys the review app when a `ready-to-merge` label is added (so the QA person don't need to remember to add the `destroy-review-app` label in that case).
- We should have a workflow configuration that destroys the review app when the PR is closes (either close or merge+close) to prevent stale review apps running when not needed anymore.

In these 2 cases, we would re-use the previous GitHub Action that destroy the Review App by just setting other jobs for the specific triggers. Here's an example of a GitHub Workflows job when a PR is closed https://github.com/arielj/test-gh-labels/blob/main/.github/workflows/on_closed.yml.

# Final thoughts:

The code of the GitHub Actions will be public and the different projects will reference them, so it's reusable. The only code that would be copied on each project is the workflows `.yml` file that sets the triggers.
