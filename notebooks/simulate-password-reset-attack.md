# Simulating a Password Reset Attack

## Overview
Demonstrates forcing account lockouts and reviewing security logs.

### Prerequisites
- A Windows 10 client joined to dproject.local
- User TestUser in AD

## Steps

`powershell
# 1. Trigger failed logins
for (=0;  -lt 5; ++) { 
  Test-Path \\DC01-AD-Project\C$
}
`

`powershell
# 2. Check for account lockout event
Get-WinEvent -FilterHashtable @{LogName="Security"; ID=4662} | Select-Object TimeCreated, Message
`

`powershell
# 3. Reset the user password (embedded workflow)
# {{ workflow: reset-user-password }}
`

## Cleanup
`powershell
Unlock-ADAccount -Identity TestUser
`

## Notes
- Use the Workflow pane to import and run the eset-user-password.json workflow.
