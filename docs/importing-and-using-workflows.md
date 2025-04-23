# Importing and Using Lab Workflows

Warp Drive Workflows let you record, export, import, and share repeatable command sequences. This guide shows how to manage your common Active Directory lab tasks as workflows.

## Recording a Workflow
1. Open the **Workflows** pane in the Warp sidebar and click **New Workflow**.  
2. Enter a **Name** (e.g., "Provision Domain Controller") and **Description**.  
3. Execute your PowerShell steps (for example:
   ```powershell
   Install-WindowsFeature AD-Domain-Services
   Install-ADDSForest -DomainName adproject.local
   ```
   )—Warp will record each command automatically.  
4. Click **Save** to store the workflow.

## Exporting Workflows
1. In the **Workflows** pane, locate the workflow you want to share.  
2. Click the **…** menu next to it and choose **Export as JSON**.  
3. Save the JSON file into the `workflows/` directory at the root of this repository.  
4. Commit the JSON file (e.g., `provision-dc.json`) to version control.

## Importing Workflows
1. In Warp Drive, click **Import Workflow**.  
2. Select a JSON file from the `workflows/` directory.  
3. Verify the workflow appears in your list and is ready to run.

## Sharing and Versioning
- Keep all workflow JSON files under the `workflows/` folder in this repo.  
- To update a workflow:
  1. Re-export the updated JSON.
  2. Create a pull request with the changed JSON file.
- In `CONTRIBUTING.md`, add a section outlining how to update workflow JSON and notify collaborators.

