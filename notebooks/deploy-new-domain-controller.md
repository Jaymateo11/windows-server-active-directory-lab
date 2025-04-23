# Deploying a New Domain Controller

## Overview
This notebook walks you through installing Active Directory Domain Services, promoting a server to a DC, and configuring DNS.

### Prerequisites
- A Windows Server VM named DC01-AD-Project
- Elevated PowerShell session
- Warp Drive workflow Provision Domain Controller exported at workflows/provision-dc.json

## Steps

`powershell
# 1. Install AD DS role
Install-WindowsFeature AD-Domain-Services
`

`powershell
# 2. Promote to domain controller
Install-ADDSForest -DomainName adproject.local -SafeModeAdministratorPassword (ConvertTo-SecureString "P@ssw0rd!" -AsPlainText -Force)
`

`powershell
# 3. Configure DNS (embedded workflow)
# {{ workflow: provision-dc }}
`

## Validation
`powershell
Get-ADDomainController -Filter *
`

## Notes
- You can rerun steps by clicking the Run button in each cell.
