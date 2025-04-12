# Subnet Misconfiguration Troubleshooting Guide

This document provides guidance on diagnosing and resolving common subnet misconfiguration issues in an Active Directory environment.

## Common Subnet Misconfiguration Symptoms

- Clients unable to join domain despite network connectivity
- Inconsistent authentication failures
- Group Policy not applying correctly
- DNS resolution failures for domain resources
- Slow network performance or timeouts
- DHCP lease problems

## Subnet Configuration Verification

1. Verify IP addressing scheme consistency:
   - Domain Controller: 192.168.1.10/24
   - Default Gateway: 192.168.1.1
   - DHCP Scope: 192.168.1.50-192.168.1.200
   - Subnet Mask: 255.255.255.0 (for all devices)

2. Check for IP address conflicts:
   - Run `arp -a` on the domain controller to view the ARP table
   - Look for duplicate IP addresses with different MAC addresses
   - Use tools like Advanced IP Scanner to detect conflicts

## Common Misconfiguration Issues

### 1. Incorrect Subnet Mask

**Symptoms:**
- Intermittent connectivity
- Can ping some devices but not others on the same logical network

**Resolution:**
1. Ensure all devices use the same subnet mask (255.255.255.0 for /24 network)
2. Check router/switch configuration for VLAN subnet mask settings
3. Update DHCP scope options with correct subnet mask

### 2. Default Gateway Misconfiguration

**Symptoms:**
- Can access local resources but not internet/remote resources
- Ping to external addresses fails

**Resolution:**
1. Verify default gateway IP is correct (192.168.1.1)
2. Confirm default gateway is operational
3. Check routing tables with `route print`

### 3. DNS Server Misconfiguration

**Symptoms:**
- Cannot resolve domain names
- Domain join failures
- "Domain not found" errors

**Resolution:**
1. Ensure primary DNS points to domain controller (192.168.1.10)
2. Verify DNS service is running on the domain controller
3. Check forward and reverse lookup zones
4. Flush DNS cache on client: `ipconfig /flushdns`

## Advanced Troubleshooting

### Subnet Routing Issues

1. Check for multiple subnets in the environment:
   ```
   ipconfig /all | findstr "Subnet Mask"
   ```

2. Verify router has proper routes configured:
   ```
   route print
   ```

3. Test cross-subnet communication:
   ```
   tracert [destination_ip]
   ```

### Active Directory Sites and Services Configuration

1. Open Active Directory Sites and Services on the domain controller
2. Verify subnets are properly defined:
   - Navigate to Sites > Subnets
   - Check for 192.168.1.0/24 subnet definition
   - Ensure subnet is associated with the correct site

3. Add missing subnets if needed:
   - Right-click Subnets > New Subnet
   - Enter prefix and mask length (192.168.1.0/24)
   - Associate with appropriate site

## Resolving Misconfiguration Issues

### Method 1: Manual Reconfiguration

1. Document current network settings before making changes
2. Update IP configuration on affected devices:
   - IP address within correct range
   - Proper subnet mask (255.255.255.0)
   - Correct default gateway (192.168.1.1)
   - Domain controller as primary DNS (192.168.1.10)

3. Restart network services or device
4. Test connectivity and domain functionality

### Method 2: DHCP Reconfiguration

1. Review DHCP scope options:
   - Verify subnet mask is 255.255.255.0
   - Confirm default gateway is 192.168.1.1
   - Check DNS server is set to 192.168.1.10

2. Update any incorrect DHCP options
3. On client machines:
   ```
   ipconfig /release
   ipconfig /renew
   ```

## Preventative Measures

1. Document network topology and IP addressing scheme
2. Implement IP Address Management (IPAM) solution
3. Configure DHCP reservations for critical devices
4. Regularly audit network configuration
5. Use monitoring tools to detect subnet configuration drift
