# Grafana Dashboards

This repo stores Grafana dashboard JSON as version-controlled files, synced to and from Grafana via **Git Sync**.

## Structure

Each top-level folder maps to a folder in Grafana:

```
Cloud/          Dashboards for the Grafana Cloud environment
On-Premise/     Dashboards for the On-Premise environment
```

Each `.json` file is a single dashboard export. File names match the dashboard title.

## Using this repo with Grafana Git Sync

Git Sync (Grafana's Git-backed dashboard provisioning) keeps dashboards in Grafana and in this repo in sync.

### Connect a Grafana instance

1. In Grafana, go to **Administration → Provisioning → Git Sync** (or the relevant folder's settings, for per-folder sync).
2. Add this repository as the sync target:
   - Repository URL: `https://github.com/luis-grafana/grafana-dashboards`
   - Branch: `main`
   - Authentication: a GitHub token/App with read (and write, if push-back is enabled) access to this repo
3. Point the sync at the folder that matches the environment (e.g. `Cloud/` for the Cloud instance, `On-Premise/` for the on-prem instance), or sync the whole repo if one Grafana instance owns everything in it.

### Workflow

- **Grafana → Git**: When a dashboard is edited in Grafana with Git Sync enabled, Grafana commits the updated JSON back to this repo on the configured branch.
- **Git → Grafana**: When a JSON file in this repo is changed (e.g. via a pull request) and merged into `main`, Grafana picks up the change and updates the dashboard.
- Prefer making dashboard edits in Grafana's UI when Git Sync is push-enabled — it keeps the JSON and the live dashboard consistent automatically. Manual edits to the JSON files should go through a PR so changes are reviewed before they land in Grafana.

### Adding a new dashboard

1. Export the dashboard JSON from Grafana (**Dashboard settings → JSON Model**, or let Git Sync create the file automatically on save).
2. Save it under the folder matching its environment (`Cloud/` or `On-Premise/`).
3. Commit and push (or open a PR) to `main`.
