# Collection of Reusable Workflows

This directory contains JSON definitions for Warp Drive Workflows automating repetitive lab tasks.

| File                       | Purpose                                                                                         |
|----------------------------|-------------------------------------------------------------------------------------------------|
| reset-lab-environment.json | Restart VMs, remove temporary AD objects, and reset test user passwords.                        |
| snapshot-vms.json          | Create timestamped snapshots of all lab virtual machines using Hyper-V.                         |
| health-check.json          | Run AD replication failures check and DC diagnostics, exporting results to log files.           |

## Importing Workflows
1. In Warp, open the **Workflows** pane.
2. Click **Import Workflow**.
3. Select a JSON file from the `workflows/` directory.

## Running Workflows
1. Locate the imported workflow in the list.
2. Click **Run** and review the output in the terminal.

