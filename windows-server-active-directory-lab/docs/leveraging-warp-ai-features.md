# Leveraging Warp AI Features

## Looking Up Commands
- Invoke **Ask AI** by pressing `Ctrl+Enter` in a command cell to query PowerShell and Windows Server commands.
- Example:
  ```powershell
  # Prompt:
  # How do I create a new Active Directory user?
  ```
  **AI Response**:
  ```text
  To create a new AD user, use:
  New-ADUser -Name "John Doe" -GivenName "John" -Surname "Doe" -SamAccountName "jdoe" -UserPrincipalName "jdoe@adproject.local" -Path "CN=Users,DC=adproject,DC=local" -AccountPassword (ConvertTo-SecureString "P@ssw0rd!" -AsPlainText -Force) -Enabled $true
  ```

## Walking Through Multi-Step Workflows
- Enter a natural-language prompt like **“Provision a domain controller and configure DNS.”**
- AI will generate a step-by-step plan; review the list and execute each command.
- Example Steps:
  1. Install AD DS: `Install-WindowsFeature AD-Domain-Services`
  2. Promote to DC: `Install-ADDSForest -DomainName adproject.local`
  3. Install DNS: `Add-WindowsFeature DNS`

## Proactive Error Fixes and Recommendations
- If a command fails, select the error message and press `Ctrl+Enter` to ask AI for fixes.
- Example: A typo in `Install-ADDSForests` returns an error.  
  **AI Suggestion**: Correct the cmdlet to `Install-ADDSForest`

## Creating and Saving Custom AI Rules
1. Open **Settings** → **AI Rules** → **New Rule**.
2. Create a rule named **AD-Lab Context**:
   - **Trigger**: Always apply or tag as **AD-Lab**.
   - **Prepend**: Environment details (e.g., domain `adproject.local`, default OU).
3. Save the rule; AI responses will include the context automatically.
4. To apply, add `#AD-Lab` in your prompts or select the rule manually.

# Leveraging Warp AI Features

## Looking Up Commands
- Invoke **Ask AI** by pressing `Ctrl+Enter` in a command cell to query PowerShell and Windows Server commands.
- Example:
  ```powershell
  # Prompt:
  # How do I create a new Active Directory user?
  ```
  **AI Response**:
  ```text
  To create a new AD user, use:
  New-ADUser -Name "John Doe" -GivenName "John" -Surname "Doe" -SamAccountName "jdoe" -UserPrincipalName "jdoe@adproject.local" -Path "CN=Users,DC=adproject,DC=local" -AccountPassword (ConvertTo-SecureString "P@ssw0rd!" -AsPlainText -Force) -Enabled $true
  ```

## Walking Through Multi-Step Workflows
- Enter a natural-language prompt like **“Provision a domain controller and configure DNS.”**
- AI will generate a step-by-step plan; review the list and execute each command.
- Example Steps:
  1. Install AD DS: `Install-WindowsFeature AD-Domain-Services`
  2. Promote to DC: `Install-ADDSForest -DomainName adproject.local`
  3. Install DNS: `Add-WindowsFeature DNS`

## Proactive Error Fixes and Recommendations
- If a command fails, select the error message and press `Ctrl+Enter` to ask AI for fixes.
- Example: A typo in `Install-ADDSForests` returns an error.  
  **AI Suggestion**: Correct the cmdlet to `Install-ADDSForest`.

## Creating and Saving Custom AI Rules
1. Open **Settings** → **AI Rules** → **New Rule**.
2. Create a rule named **AD-Lab Context**:
   - **Trigger**: Always apply or tag as **AD-Lab**.
   - **Prepend**: Environment details (e.g., domain `adproject.local`, default OU).
3. Save the rule; AI responses will include the context automatically.
4. To apply, add `#AD-Lab` in your prompts or select the rule manually.

