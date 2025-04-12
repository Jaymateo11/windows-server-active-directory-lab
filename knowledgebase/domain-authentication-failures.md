# Domain Authentication Failure Troubleshooting Guide

This document provides step-by-step guidance for resolving authentication failures in an Active Directory domain environment.

## Common Authentication Failure Symptoms

- Unable to log in with domain credentials
- "The system cannot log you on due to the following error: The user name or password is incorrect"
- "The referenced account is currently locked out"
- "The security database on the server does not have a computer account for this workstation trust relationship"
- Kerberos errors in Event Viewer
- Slow login times or timeout during authentication

## Initial Verification Steps

1. Verify basic network connectivity:
   - Ping the domain controller: `ping 192.168.1.10`
   - Verify DNS resolution: `nslookup adproject.local`
   
2. Check account status:
   - Verify the user account exists in Active Directory
   - Ensure the account is not locked, disabled, or expired
   - Check if password has expired or needs to be changed

3. Confirm computer domain status:
   - Open Command Prompt and run: `systeminfo | findstr /B /C:"Domain"`
   - Should return: Domain: adproject.local

## Common Authentication Issues and Solutions

### 1. Incorrect Username or Password

**Symptoms:**
- "The username or password is incorrect" error

**Troubleshooting Steps:**
1. Verify correct username format (ADPROJECT\username or username@adproject.local)
2. Check for enabled Caps Lock or Num Lock
3. Try resetting the user's password in Active Directory Users and Computers
4. Test login with a different domain account

**Resolution:**
1. Reset password in Active Directory Users and Computers:
   - Right-click user > Reset Password
   - Uncheck "User must change password at next logon" if needed for testing

### 2. Account Lockout

**Symptoms:**
- "The referenced account is currently locked out" error
- Multiple failed login attempts

**Troubleshooting Steps:**
1. Check account lockout status in Active Directory Users and Computers
2. Review security logs for lockout source

**Resolution:**
1. Unlock the account:
   - Open Active Directory Users and Computers
   - Right-click user > Properties
   - Click "Unlock Account" checkbox
2. Identify source of incorrect password attempts
3. Consider reviewing account lockout policies

### 3. Broken Trust Relationship

**Symptoms:**
- "The security database on the server does not have a computer account for this workstation trust relationship" error
- Computer account password mismatch

**Troubleshooting Steps:**
1. Verify computer account exists in Active Directory
2. Check if computer account is disabled or reset

**Resolution:**
1. Reset the computer account trust:
   - Option 1: Rejoin the domain
     - Right-click Start > System
     - Select "Rename this PC (advanced)"
     - Change from domain to workgroup, reboot
     - Rejoin domain, reboot
   - Option 2: Use PowerShell (if admin access available)
     ```powershell
     Test-ComputerSecureChannel -Repair -Credential (Get-Credential)
     ```

### 4. Kerberos Authentication Issues

**Symptoms:**
- Event logs showing Kerberos errors
- Authentication only works with NTLM
- Authentication works locally but not from remote systems

**Troubleshooting Steps:**
1. Check time synchronization (Kerberos requires <5 min difference)
2. Verify DNS records for domain controllers
3. Check SPN (Service Principal Name) registrations

**Resolution:**
1. Synchronize time with domain:
   ```
   net time \\dc01-ad-project /set /y
   ```
2. Verify DNS configuration points to domain controller
3. Use `setspn -L hostname` to check SPNs

## Advanced Troubleshooting

### Event Log Analysis

1. Check Event Viewer for relevant authentication errors:
   - Windows Logs > Security
   - Windows Logs > System
   - Applications and Services Logs > Directory Service

2. Common event IDs to look for:
   - 4625: Failed login attempt
   - 4740: Account lockout
   - 4771: Kerberos pre-authentication failed
   - 5805: Computer account authentication failed

### Network Trace Analysis

1. Use Network Monitor or Wireshark to capture authentication traffic
2. Filter for Kerberos or LDAP traffic
3. Look for failed authentication attempts or denied packets

### Active Directory Diagnostic Tools

1. Run domain controller diagnostics:
   ```
   dcdiag /v /c /d /e /s:dc01-ad-project
   ```

2. Check domain replication status:
   ```
   repadmin /replsum
   ```

## Prevention Measures

1. Implement account lockout policies that balance security and usability
2. Configure password policies that enforce strong passwords
3. Regularly audit failed login attempts
4. Implement multi-factor authentication for sensitive accounts
5. Establish a regular computer account password reset schedule
6. Document domain authentication procedures for IT staff

## Additional Resources

- Microsoft Documentation: Troubleshooting Kerberos Authentication
- Event ID Lookup Tools
- Active Directory PowerShell Module Reference
- Account Lockout and Management Tools
