# everyday-green

> Keep your GitHub stats green, every day — automatically.

This repository contains a GitHub Actions workflow that automatically updates a file named `TIMESTAMP.txt` and commits the change on a randomized schedule. Instead of committing the exact same number of times every day, the workflow varies how many commits it makes — and roughly once a week, it spikes to a much higher number — so your contribution graph looks more natural instead of flat and identical.

## Overview

The `everyday-green` workflow demonstrates how GitHub Actions can automate routine repository activity. Specifically, this workflow:

- Checks out the latest code from the `master` branch.
- Updates the `TIMESTAMP.txt` file with the current date and time.
- Makes a **random number of commits per run** (normally 1–5).
- Roughly **once every 7 days**, makes a much larger burst of commits (15–30) instead of the usual amount.
- Pushes all the commits back to the `master` branch in a single push.

## How the Randomization Works

The workflow runs twice a day (every 12 hours). Each time it runs:

1. It checks the current day of the year.
2. If that day falls on a 7-day cycle, it treats it as a "spike day" and generates **15–30 commits**.
3. Otherwise, it's a normal day, and it generates **1–5 commits**.
4. It then creates that many commits one at a time — each with a fresh timestamp and a randomly chosen commit message — with a short random delay between each one.
5. Once all commits are created locally, they're pushed to `master` together.

This means:
- Most days show a small-to-moderate amount of activity.
- About once a week, one day shows a noticeably larger burst.
- The exact numbers are random within their ranges, so no two weeks look identical.

## Workflow Structure

The workflow is defined in `.github/workflows/master.yml` and includes:

- **Triggers**: Runs every 12 hours on a schedule, on every push to `master`, and can be manually triggered via the GitHub UI with `workflow_dispatch`.
- **Jobs and Steps**: A single job, `update_commit`, running on the latest Ubuntu runner. It sets up Git, determines the commit count, updates `TIMESTAMP.txt` in a loop, commits each change, and pushes the results.
- **Permissions**: Granted write access to repository contents.

## Using This Workflow

### Creating Your Own Version

1. Click "Use this template" on the GitHub repository page.
2. Choose a name for your new repository and select "Create repository from template".
3. Clone your new repository to make further customizations locally.

### Customizing the Workflow

Before using the workflow, update it with your own GitHub email and username:

1. Open `.github/workflows/master.yml` in your repository.
2. In the `Setup Git Configuration` step, replace the email and username with your own.
3. Commit your changes.

You can also tune the behavior to your liking:

- Change the normal-day commit range (default: 1–5).
- Change the spike-day commit range (default: 15–30).
- Adjust how often the spike occurs (default: roughly every 7 days).

### Viewing Workflow Runs

1. Go to the `Actions` tab of your repository.
2. Select the `Automated Commit` workflow to see details of each run.

### Manually Triggering the Workflow

1. Go to the `Actions` tab of your repository.
2. Select the `Automated Commit` workflow.
3. Click `Run workflow`, select `master`, then click `Run workflow` again.

## Contributing

Contributions are welcome! Feel free to fork the repository, make your changes, and submit a pull request.

## Support

For issues or questions, please file an issue in the `Issues` section of the repository.

Thank you for exploring everyday-green!

## Credits

This project is an adaptation of [dante4rt/automated-commit](https://github.com/dante4rt/automated-commit). Big thanks to the original author for the base workflow — this version builds on it by adding randomized commit counts and weekly activity spikes.
