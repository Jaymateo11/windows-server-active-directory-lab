# Domain Controller Setup Guide  

This document outlines the process of setting up a Windows Server 2019 machine as a domain controller for a new Active Directory domain.  

## Prerequisites  

- Windows Server 2019 Standard/Datacenter installation  
- Static IP address configuration  
- Administrator access  
- Internet connection (for updates)  

## Step 1: Initial Server Configuration  

1. Install Windows Server 2019 with default options  
2. Configure the server with a static IP address:  
   - IP address: 192.168.1.10  
   - Subnet mask: 255.255.255.0  
   - Default gateway: 192.168.1.1  
   - Preferred DNS: 127.0.0.1 (will point to self after DC promotion)  
3. Rename the computer to a descriptive hostname (DC01-AD-Project)  
4. Install all available Windows updates  
5. Restart the server  

## Step 2: Install Active Directory Domain Services  

1. Open Server Manager  
2. Click "Add roles and features"  
3. Select "Role-based or feature-based installation"  
4. Select the local server  
5. Check "Active Directory Domain Services"  
6. Accept the additional features prompt  
7. Complete the installation wizard  
8. Click "Promote this server to a domain controller" notification  

## Step 3: Domain Controller Promotion  

1. Select "Add a new forest"  
2. Enter root domain name: adproject.local  
3. Set Forest and Domain functional levels to "Windows Server 2019"  
4. Ensure "DNS Server" is checked  
5. Enter Directory Services Restore Mode (DSRM) password  
6. Accept default locations for database, log files, and SYSVOL  
7. Review the configuration and click "Next"  
8. Allow the prerequisite check to complete  
9. Click "Install" to begin the promotion  
10. The server will restart automatically after installation  

## Step 4: Post-Installation Configuration  

1. Log in with the domain administrator account (ADPROJECT\Administrator)  
2. Verify DNS service is running:  
   - Open DNS Manager from Server Manager > Tools  
   - Verify forward and reverse lookup zones are created  
3. Configure DHCP (optional):  
   - Install DHCP Server role  
   - Create a scope for client machines (e.g., 192.168.1.50-192.168.1.200)  
   - Configure DHCP options (DNS server, default gateway)  
   - Authorize the DHCP server in Active Directory  
4. Create basic Organizational Unit (OU) structure:  
   - Open Active Directory Users and Computers  
   - Create OUs for Users, Computers, and Groups  
5. Install Windows Admin Center (optional) for enhanced management capabilities  

## Verification  

To verify the domain controller is functioning properly:  

1. Run `dcdiag` from an elevated command prompt  
2. Check for any errors in the Event Viewer under "Directory Service" logs  
3. Verify DNS resolution with `nslookup adproject.local`  
4. Test authentication by creating and logging in with a test user account
