# Client Configuration Guide

This document explains how to configure a Windows 10 client machine to join the Active Directory domain and troubleshoot common connection issues.

## Prerequisites

- Windows 10 Pro/Enterprise (Home edition doesn't support domain join)
- Network connectivity to the domain controller
- Local administrator access on the client machine
- Domain user credentials with permission to join computers to the domain

## Step 1: Network Configuration

1. Configure the network adapter with appropriate settings:
   - IP Configuration: Use DHCP or configure static IP
   - If using static IP:
     - IP address: 192.168.1.20 (example)
     - Subnet mask: 255.255.255.0
     - Default gateway: 192.168.1.1
     - Preferred DNS server: 192.168.1.10 (domain controller's IP)
   
2. Verify connectivity to the domain controller:
   - Open Command Prompt and ping the domain controller: `ping 192.168.1.10`
   - Test DNS resolution: `nslookup adproject.local`

## Step 2: Computer Name Configuration

1. Right-click on Start > System
2. Click on "Rename this PC (advanced)"
3. Choose a descriptive computer name (e.g., CLIENT01-AD-Project)
4. Restart the computer if prompted

## Step 3: Join the Domain

1. Right-click on Start > System
2. Click on "Rename this PC (advanced)"
3. Click the "Change" button
4. Select "Domain" and enter the domain name: adproject.local
5. Click "OK"
6. Enter domain credentials when prompted:
   - Username: Administrator (or domain user with join permissions)
   - Password: [your domain admin password]
7. You'll receive a welcome message upon successful domain join
8. Restart the computer

## Step 4: Verify Domain Join

1. Log in with a domain account:
   - At the login screen, click "Other user"
   - Enter domain credentials in the format: ADPROJECT\username
   - Or use: username@adproject.local
2. Verify domain connection:
   - Open Command Prompt and run: `whoami`
   - Should return: adproject\username
   - Run: `gpresult /r` to verify Group Policy application

## Step 5: Configure User Profile

1. Customize the default user profile settings
2. Configure desktop and Start menu layouts
3. Set up any required mapped drives or printers

## Troubleshooting Common Issues

### Cannot Find Domain

1. Verify DNS settings point to the domain controller
2. Check network connectivity to the domain controller
3. Try using the fully qualified domain name: adproject.local
4. Check the domain controller's DNS service is running

### Authentication Failures

1. Verify the username and password are correct
2. Ensure the user account is not locked or disabled
3. Check if the computer account exists in Active Directory
4. Reset the computer account if necessary

### Group Policy Not Applying

1. Run `gpupdate /force` to refresh Group Policy
2. Check Group Policy application with `gpresult /r`
3. Verify network connectivity to the domain controller
4. Check the event logs for Group Policy errors

## Post-Configuration Steps

1. Install required software packages
2. Configure security settings and antivirus
3. Set up backup and recovery options
4. Document the client configuration for future reference
