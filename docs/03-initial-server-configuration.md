# Windows Server 2019 — Initial Server Configuration

## 1. Overview

After successfully installing Windows Server 2019 and VMware Tools, the next step was to perform the initial server configuration.

Before installing server roles such as Active Directory Domain Services (AD DS), DNS, and DHCP, it is important to configure the server's basic settings.

These configurations help prepare the server for its role in the Windows Server lab environment.

### Objectives

The objectives of this section are to:

* Rename the Windows Server computer.
* Assign a meaningful server name.
* Restart the server to apply the changes.
* Verify the new computer name.
* Prepare the server for network configuration and Active Directory installation.

### Lab Environment

| Component               | Configuration                        |
| ----------------------- | ------------------------------------ |
| Virtualization Platform | VMware Workstation                   |
| Operating System        | Windows Server 2019                  |
| Server Edition          | Desktop Experience                   |
| Current Computer Name   | Automatically generated Windows name |
| New Computer Name       | DC01                                 |
| Planned Server Role     | Active Directory Domain Controller   |

---

# Step 1 — Rename Windows Server 2019

## 1.1 Purpose

By default, Windows Server assigns an automatically generated computer name during installation.

This name usually contains a random combination of letters and numbers.

For example:

`WIN-XXXXXXXXXXX`

Although the server can operate with this default name, using a descriptive computer name makes it easier to identify, manage, and troubleshoot servers in an enterprise network.

For this lab, I renamed the Windows Server computer to:

**New Computer Name:** `DC01`

### Why DC01?

The name `DC01` was selected because this server will later be configured as the first Domain Controller in the Active Directory environment.

The naming convention represents:

* **DC:** Domain Controller
* **01:** First Domain Controller

In larger organizations, additional Domain Controllers may be named `DC02`, `DC03`, and so on.

Using consistent naming conventions helps system administrators identify different servers and their purposes.

> **Note:** Renaming a server to DC01 does not automatically make it a Domain Controller. Active Directory Domain Services must be installed, and the server must be promoted to a Domain Controller.

---

## 1.2 Open Server Manager

After installing Windows Server 2019, I logged in using the local Administrator account.

The **Server Manager** application opened automatically after signing in.

Server Manager is a Windows Server management tool that allows administrators to configure and monitor servers.

It provides access to important server settings, including:

* Computer name
* Network configuration
* Windows Update settings
* Remote Desktop
* Server roles and features
* Windows Firewall settings

### Configuration Steps

1. Started the Windows Server 2019 virtual machine in VMware Workstation.
2. Logged in using the Administrator account.
3. Opened **Server Manager**.
4. Waited for the Server Manager dashboard to load.

If Server Manager does not open automatically, it can be launched from the Start menu.

![alt text](../images/server-manager-dashboard.png)

*Figure 1: Windows Server 2019 Server Manager dashboard.*

---

## 1.3 Navigate to Local Server

The next step was to access the server's local configuration settings.

### Configuration Steps

1. In **Server Manager**, located the left navigation panel.
2. Clicked **Local Server**.
3. The Local Server properties page appeared.
4. Located the **Computer name** field under the Properties section.

This page displays important information about the local server, including its current computer name and network configuration.

![alt text](../images/local-server-properties.png)

*Figure 2: Viewing the Local Server properties in Server Manager.*

---

## 1.4 Open Computer Name Settings

After navigating to Local Server, I opened the computer name configuration settings.

### Configuration Steps

1. Located the **Computer name** option.
2. Clicked the existing computer name displayed as a blue hyperlink.
3. The **System Properties** window opened.
4. Selected the **Computer Name** tab.
5. Reviewed the existing computer name.
6. Clicked **Change** to modify the computer name.

The **Computer Name/Domain Changes** window appeared.

This window allows administrators to change the computer name and configure domain or workgroup membership.

![alt text](../images/system-properties-computer-name.png)

*Figure 3: Accessing the Computer Name settings through System Properties.*

---

## 1.5 Change the Computer Name to DC01

I assigned the new computer name to the Windows Server.

### Configuration Steps

1. In the **Computer Name/Domain Changes** window, located the **Computer name** field.

2. Removed the existing computer name.

3. Entered the new computer name:

   `DC01`

4. Confirmed that the new computer name was entered correctly.

5. Left the computer in its existing workgroup.

6. Clicked **OK** to apply the changes.

### Configuration Summary

| Setting           | Value                      |
| ----------------- | -------------------------- |
| Computer Name     | DC01                       |
| Domain Membership | Not yet joined to a domain |
| Server Purpose    | Future Domain Controller   |

At this stage, the server was still a standalone Windows Server installation.

Active Directory Domain Services had not yet been configured.

![alt text](../images/rename-server-dc01.png)

*Figure 4: Changing the Windows Server computer name to DC01.*

---

## 1.6 Confirm the Computer Name Change

After entering the new computer name, Windows displayed a notification indicating that the server must be restarted for the changes to take effect.

### Configuration Steps

1. Clicked **OK** on the notification.
2. Closed the **System Properties** window.
3. Accepted the prompt to restart Windows Server.

The computer name change was saved, but a restart was required before the new name became active.

---

## 1.7 Restart Windows Server

I restarted Windows Server 2019 to apply the updated computer name.

### Configuration Steps

1. Saved any open work.
2. Selected **Restart** when prompted.
3. Waited for Windows Server to restart.
4. Logged back in using the local Administrator account.

After the restart, the new computer name was applied.

> **Note:** Restarting Windows Server is necessary to complete the computer name change.

---

# Step 2 — Verify the Computer Name

After restarting Windows Server, I verified that the computer name had been updated successfully.

Verification is an important part of system administration because it confirms that the configuration changes have been applied correctly.

I used both the Windows graphical interface and Command Prompt to verify the computer name.

---

## 2.1 Verify Using Server Manager

### Verification Steps

1. Opened **Server Manager**.
2. Selected **Local Server**.
3. Located the **Computer name** field under Properties.
4. Confirmed that the displayed computer name was:

   `DC01`

This confirmed that the server name had been updated successfully.

![alt text](../images/verify-server-manager-name.png)

*Figure 5: Verifying that the computer name is DC01 in Server Manager.*

---

## 2.2 Verify Using Command Prompt

In addition to checking Server Manager, I used Command Prompt to verify the computer name.

The `hostname` command displays the current computer name assigned to the operating system.

### Verification Steps

1. Opened the **Start** menu.
2. Searched for **Command Prompt**.
3. Opened Command Prompt.
4. Entered the following command:

```cmd
hostname
```

5. Pressed **Enter**.

### Expected Output

```text
DC01
```

The command returned `DC01`, confirming that Windows Server was using the new computer name.

![alt text](../images/verify-hostname-command.png)

*Figure 6: Verifying the Windows Server computer name using the hostname command.*

---

## 2.3 Additional Verification Using PowerShell

The computer name can also be verified using Windows PowerShell.

PowerShell is a command-line shell and scripting environment used by Windows administrators to automate administrative tasks.

To verify the computer name, I opened PowerShell and executed:

```powershell
$env:COMPUTERNAME
```

### Expected Output

```text
DC01
```

The command displays the computer name stored in the Windows environment variables.

![alt text](../images/DC01-2026-10-17-19-30-34.png)

This provides another method of verifying the server configuration.

---

# Step 3 — Confirm Successful Configuration

After completing the renaming process, I verified that:

* The server restarted successfully.
* The Administrator account could log in.
* Server Manager opened correctly.
* The computer name displayed as `DC01`.
* The `hostname` command returned `DC01`.
* The server was ready for further configuration.

### Configuration Result

| Configuration          | Expected Result     |
| ---------------------- | ------------------- |
| Computer Name          | DC01                |
| Windows Server Version | Windows Server 2019 |
| Administrator Login    | Successful          |
| Server Restart         | Successful          |
| Hostname Verification  | DC01                |
| Initial Configuration  | Completed           |

---

## Troubleshooting

### Issue 1 — Computer Name Did Not Change

If the computer name still displays the previous name, verify that the server has been restarted.

The name change does not fully take effect until Windows Server restarts.

### Issue 2 — Unable to Change the Computer Name

Ensure that the account being used has local administrator privileges.

Changing the computer name requires administrative permissions.

### Issue 3 — Server Manager Displays the Previous Computer Name

Refresh the Server Manager window or close and reopen the application.

If the old name continues to appear, restart the server and verify the name using:

```cmd
hostname
```

---

# Conclusion

In this section, I successfully completed the initial computer name configuration for Windows Server 2019.

I renamed the server from its automatically generated computer name to **DC01** using Server Manager.

After restarting the server, I verified the configuration using Server Manager, Command Prompt, and PowerShell.

The server is now identified as `DC01` and is ready for the next phase of the lab.

## Next Step

The next task is to configure a **static IPv4 address** for DC01.

This configuration is important because the server will later provide Active Directory and DNS services to other computers in the lab network.

A static IP address ensures that client computers can reliably communicate with the Domain Controller.

---

# Step 4 — Configure a Static IPv4 Address

## 4.1 Overview

After successfully renaming Windows Server 2019 to `DC01`, the next step was to configure a static IPv4 address.

By default, Windows Server may obtain its IP address automatically from a DHCP server.

However, servers that provide critical network services, such as Active Directory Domain Services (AD DS), DNS, and DHCP, should generally use static IP addresses.

A static IP address ensures that the server maintains a consistent network address, allowing client computers and other network devices to communicate with it reliably.

### Objectives

The objectives of this section are to:

1. Understand static and dynamic IP addressing.
2. Identify the VMware virtual network configuration.
3. Determine the correct IP address and subnet mask.
4. Identify the default gateway.
5. Configure a static IPv4 address on Windows Server 2019.
6. Configure DNS settings.
7. Verify network configuration.
8. Test network connectivity.
9. Troubleshoot potential network problems.

---

## 4.2 Understanding Static and Dynamic IP Addresses

Before configuring the network, it is important to understand the difference between static and dynamic IP addresses.

### Dynamic IP Address

A dynamic IP address is automatically assigned to a device by a DHCP server.

For example, when a computer connects to a network, a DHCP server can automatically provide:

* IP address
* Subnet mask
* Default gateway
* DNS server information

Dynamic IP addresses are commonly used for client computers, smartphones, and other network devices.

### Static IP Address

A static IP address is manually configured and remains the same unless an administrator changes it.

Static IP addresses are commonly assigned to:

* Domain Controllers
* DNS servers
* DHCP servers
* File servers
* Other critical infrastructure devices

### Why Does DC01 Need a Static IP Address?

In this lab, `DC01` will eventually function as an Active Directory Domain Controller.

Client computers need to communicate with the Domain Controller to authenticate users, access domain resources, and process Group Policy.

If the Domain Controller's IP address changes unexpectedly, clients may experience problems connecting to domain services.

Therefore, I configured a static IP address to provide a stable network address for DC01.

---

# Step 5 — Check VMware Network Configuration

Before assigning a static IP address, I verified the VMware virtual network configuration.

This step was necessary to identify the network subnet, default gateway, and DHCP address range.

## 5.1 Open VMware Workstation

### Configuration Steps

1. Opened VMware Workstation on the host computer.

2. Selected the Windows Server 2019 virtual machine named `DC01`.

3. Opened the virtual machine settings using:

   `VM > Settings`

4. Selected **Network Adapter** under the Hardware tab.

5. Reviewed the available network connection options.

VMware Workstation provides several network connection modes.

| Network Type | Description                                                                      |
| ------------ | -------------------------------------------------------------------------------- |
| Bridged      | Connects the virtual machine directly to the physical network                    |
| NAT          | Allows the virtual machine to access external networks through the host computer |
| Host-only    | Creates a private network between the host and virtual machines                  |
| Custom       | Allows selection of a specific VMware virtual network                            |

For this lab, NAT networking was selected to allow communication between virtual machines while maintaining access to external networks through the host.

![alt text](../images/vmware-network-adapter.png)

*Figure 7: Reviewing the virtual network adapter settings in VMware Workstation.*

---

## 5.2 Open Virtual Network Editor

The next step was to examine the virtual network used by VMware.

### Configuration Steps

1. Opened VMware Workstation.
2. Clicked **Edit** from the menu bar.
3. Selected **Virtual Network Editor**.
4. Used **Change Settings** if administrator privileges were required.
5. Located the virtual network named `VMnet8`.
6. Verified that VMnet8 was configured to use NAT networking.

VMware commonly uses the following virtual networks:

* `VMnet0` — Bridged
* `VMnet1` — Host-only
* `VMnet8` — NAT

![alt text](../images/vmware-virtual-network-editor.png)

*Figure 8: Examining VMnet8 in VMware Virtual Network Editor.*

---

## 5.3 Identify the VMware Subnet

After selecting VMnet8, I identified the network address and subnet mask.

These settings determine the IP address range that can be used by virtual machines connected to the NAT network.

### Example Configuration

| Setting         | Example       |
| --------------- | ------------- |
| Virtual Network | VMnet8        |
| Network Type    | NAT           |
| Subnet IP       | 192.168.164.0  |
| Subnet Mask     | 255.255.255.0 |

In this example, `192.168.164.0/24` represents the virtual network.

The subnet mask `255.255.255.0` defines the network portion of the IP address.

For this example, valid host addresses generally range from:

`192.168.164.128` to `192.168.164.254`

However, some addresses are reserved for the VMware host adapter, NAT gateway, or other devices.

> **Important:** The IP address assigned to DC01 must be unused and outside the VMware DHCP allocation range.


![alt text](../images/vmware-virtual-network-editor.png)


*Figure 9: Identifying the NAT network subnet and subnet mask.*

---

## 5.4 Identify the Default Gateway

Next, I identified the default gateway configured for the VMware NAT network.

The default gateway allows devices to communicate with networks outside their local subnet.

### Configuration Steps

1. Selected `VMnet8` in Virtual Network Editor.
2. Clicked **NAT Settings**.
3. Located the **Gateway IP** field.
4. Recorded the configured gateway address.
5. Closed the settings window without making unnecessary changes.

### Example

```text
Default Gateway: 192.168.164.2
```

The actual gateway address depends on the VMware network configuration.

![alt text](../images/vmware-nat-gateway.png)

*Figure 10: Identifying the default gateway in VMware NAT settings.*

---

## 5.5 Review the VMware DHCP Address Range

Before selecting a static IP address, I reviewed the VMware DHCP address range.

VMware's built-in DHCP service can automatically assign IP addresses to virtual machines connected to VMnet8.

### Configuration Steps

1. Returned to **Virtual Network Editor**.
2. Selected `VMnet8`.
3. Clicked **DHCP Settings**.
4. Identified the starting and ending IP addresses of the DHCP pool.
5. Recorded the available address range.

I selected an unused static IP address within the same subnet but outside the DHCP allocation range.

This helps prevent IP address conflicts between the static server address and dynamically assigned addresses.

![alt text](../images/vmware-dhcp-settings.png)

*Figure 11: Reviewing the VMware DHCP address allocation range.*

---

# Step 6 — Check the Existing Windows Server IP Configuration

Before making changes, I checked the existing network configuration using Command Prompt.

## 6.1 Open Command Prompt

### Configuration Steps

1. Logged in to Windows Server 2019.
2. Opened the Start menu.
3. Searched for **Command Prompt**.
4. Opened Command Prompt.
5. Executed the following command:

```cmd
ipconfig /all
```

### Purpose of the Command

The `ipconfig /all` command displays detailed network configuration information, including:

* Computer hostname
* Network adapter information
* IPv4 address
* Subnet mask
* Default gateway
* DNS servers
* DHCP status
* DHCP server address

![alt text](../images/ipconfig-before-static-ip.png)

*Figure 12: Viewing the existing network configuration using ipconfig /all.*

---

## 6.2 Identify the Current Network Settings

I reviewed the output of the `ipconfig /all` command.

I recorded the existing IPv4 address, subnet mask, default gateway, and DNS server configuration.

### Configuration Record

| Network Setting | Existing Configuration  |
| --------------- | ----------------------- |
| Computer Name   | DC01                    |
| IPv4 Address    | 192.168.164.129    |
| Subnet Mask     | 255.255.255.0   |
| Default Gateway | 192.168.164.2       |
| DHCP Enabled    | Yes                |
| DNS Servers     | 192.168.164.2 |

This information helped me understand the network configuration before assigning a static IP address.

---

# Step 7 — Configure a Static IPv4 Address

After identifying the VMware network settings, I configured a static IPv4 address on Windows Server 2019.

## 7.1 Open Network Connections

### Configuration Steps

1. Logged in to Windows Server 2019.
2. Opened **Server Manager**.
3. Selected **Local Server**.
4. Located the **Ethernet** option under Properties.
5. Clicked the network connection link.

This opened the network configuration window.

Alternatively, I could open the Network Connections window using the Run dialog.

### Alternative Method

1. Pressed `Windows + R`.
2. Entered the following command:

```cmd
ncpa.cpl
```

3. Pressed **Enter**.

This opened the **Network Connections** window directly.

![alt text](../images/network-connections.png)

*Figure 13: Opening the Network Connections window in Windows Server 2019.*

---

## 7.2 Open Ethernet Properties

After opening Network Connections, I accessed the properties of the active network adapter.

### Configuration Steps

1. Located the active **Ethernet** adapter.
2. Right-clicked the adapter.
3. Selected **Properties**.
4. The Ethernet Properties window appeared.

This window displays the network components and protocols associated with the selected adapter.

![alt text](../images/ethernet-properties.png)

*Figure 14: Opening the Ethernet network adapter properties.*

---

## 7.3 Open IPv4 Properties

The next step was to configure the IPv4 settings.

### Configuration Steps

1. In the Ethernet Properties window, located:

   `Internet Protocol Version 4 (TCP/IPv4)`

2. Selected **Internet Protocol Version 4 (TCP/IPv4)**.

3. Clicked **Properties**.

4. The Internet Protocol Version 4 Properties window opened.

By default, the network adapter may be configured to obtain an IP address automatically.

This allows a DHCP server to assign network settings dynamically.

For DC01, I changed this configuration to use a static IP address.

![alt text](../images/ipv4-properties.png)

*Figure 15: Accessing IPv4 configuration settings.*

---

## 7.4 Assign a Static IPv4 Address

In the IPv4 Properties window, I selected:

**Use the following IP address**

I then entered the selected network configuration.

### Example Configuration

| Setting         | Example Value |
| --------------- | ------------- |
| IP Address      | 192.168.80.10 |
| Subnet Mask     | 255.255.255.0 |
| Default Gateway | 192.168.80.2  |

The IP address must belong to the VMware virtual network and must not conflict with another device.

### Explanation of the Settings

**IP Address**

`192.168.80.10`

This is the unique IPv4 address assigned to DC01 in the example lab network.

**Subnet Mask**

`255.255.255.0`

The subnet mask determines which portion of the IP address identifies the local network.

**Default Gateway**

`192.168.80.2`

The default gateway is used to send traffic to destinations outside the local subnet.

> These are demonstration values. The actual configuration must match the VMware virtual network.

![alt text](../images/static-ip-configuration.png)

*Figure 16: Assigning a static IPv4 address to Windows Server 2019.*

---

# Step 8 — Configure DNS Settings

After assigning the static IPv4 address, I reviewed the DNS configuration.

## 8.1 Understanding DNS

DNS stands for **Domain Name System**.

DNS translates domain names into IP addresses.

For example, when a user enters a website address, DNS helps the computer identify the IP address associated with that website.

DNS is also essential for Active Directory.

Domain-joined computers use DNS to locate Domain Controllers and other Active Directory services.

---

## 8.2 Configure DNS Before Active Directory Installation

At this stage, Active Directory Domain Services and the DNS Server role have not yet been installed.

Therefore, DC01 is not currently providing its own DNS service.

For temporary internet name resolution, a reachable DNS resolver can be configured.

In a VMware NAT environment, the NAT gateway may provide DNS forwarding.

The actual DNS settings should be verified against the existing VMware network configuration.

---

## 8.3 Configure DNS for the Future Domain Controller

After installing Active Directory Domain Services and the DNS Server role, DC01 will use its own static IP address as its preferred DNS server.

### Example

```text
Server IP Address: 192.168.80.10

Preferred DNS Server: 192.168.80.10
```

This allows the server to use its own DNS service to resolve Active Directory-related names.

External DNS resolution can later be configured through DNS forwarders.

> **Important:** Once Active Directory DNS is running, domain clients should use the internal Active Directory DNS server rather than a public DNS server as their primary DNS server.

---

# Step 9 — Verify the Static IP Configuration

After applying the network settings, I verified that Windows Server was using the configured static IP address.

## 9.1 Verify Using ipconfig

### Verification Steps

1. Opened Command Prompt.
2. Executed the following command:

```cmd
ipconfig /all
```

3. Reviewed the Ethernet adapter configuration.
4. Verified the IPv4 address.
5. Verified the subnet mask.
6. Verified the default gateway.
7. Checked the DNS server settings.
8. Confirmed that DHCP was disabled for IPv4 address assignment.

### Expected Configuration

For the example network:

```text
Host Name . . . . . . . . . : DC01
DHCP Enabled . . . . . . . : No
IPv4 Address . . . . . . . : 192.168.164.129
Subnet Mask . . . . . . .  : 255.255.255.0
Default Gateway . . . . .  : 192.168.164.2
```

The actual output depends on the network settings configured in VMware.

![alt text](../images/verify-static-ip.png)

*Figure 17: Verifying the static IPv4 address using ipconfig /all.*

---

# Step 10 — Test Network Connectivity

After verifying the static IP configuration, I tested network connectivity.

Network testing is important because it helps identify addressing, routing, and DNS-related problems.

## 10.1 Test the TCP/IP Stack

First, I tested the local TCP/IP configuration.

I opened Command Prompt and executed:

```cmd
ping 127.0.0.1
```

The IP address `127.0.0.1` is known as the loopback address.

It allows a computer to test its own TCP/IP network stack without sending traffic to another device.

### Expected Result

A successful response indicates that the local TCP/IP stack is functioning.

---

## 10.2 Ping the Server's Own IP Address

Next, I tested the IP address configured on DC01.

For the example network, I executed:

```cmd
ping 192.168.164.129
```

### Purpose

This test verifies that the server can communicate with its own assigned IPv4 address.

A successful response helps confirm that the address is configured on the local system.

---

## 10.3 Ping the Default Gateway

I then tested communication with the VMware NAT gateway.

For the example network, I executed:

```cmd
ping 192.168.164.2
```

### Purpose

This test checks whether DC01 can communicate with the configured gateway.

A successful response indicates that the server can reach the gateway on its local network.

> Some devices or firewalls may block ICMP traffic, so an unsuccessful ping does not always indicate a network failure.

![alt text](../images/ping-default-gateway.png)

*Figure 18: Testing communication between DC01 and the VMware NAT gateway.*

---

## 10.4 Test Internet Connectivity

If internet connectivity is required for the lab, I tested access to an external IP address.

Example:

```cmd
ping 1.1.1.1
```

### Purpose

This helps determine whether the server can communicate with an external IP address without relying on DNS name resolution.

If ICMP traffic is allowed, successful replies indicate that network communication to the external address is working.

---

## 10.5 Test DNS Resolution

After configuring a working DNS resolver, I tested name resolution.

I executed:

```cmd
nslookup microsoft.com
```

### Purpose

The `nslookup` command queries DNS to resolve a domain name.

A successful response returns one or more IP addresses associated with the requested domain.

If DNS has already been changed to DC01's own IP address but the DNS Server role has not yet been installed, this test may fail.

In that case, DNS should be tested again after the DNS Server role is configured.

![alt text](../images/dns-resolution-test.png)

*Figure 19: Testing DNS name resolution using nslookup.*

---

# Step 11 — Troubleshooting Network Issues

During network configuration, several common issues may occur.

## Issue 1 — Unable to Ping the Default Gateway

### Possible Causes

* Incorrect IP address
* Incorrect subnet mask
* Incorrect default gateway
* VMware network adapter disconnected
* Incorrect VMware networking mode
* Firewall blocking ICMP traffic

### Troubleshooting Steps

1. Verified the configured IP address.
2. Confirmed the subnet mask.
3. Checked the VMware NAT gateway address.
4. Verified that the network adapter was connected.
5. Confirmed that the virtual machine was connected to VMnet8.
6. Repeated the connectivity test.

---

## Issue 2 — No Internet Connectivity

### Possible Causes

* Incorrect default gateway
* VMware NAT service not functioning
* Host computer without internet access
* Network configuration error
* Firewall restrictions

### Troubleshooting Steps

1. Verified internet connectivity on the host computer.
2. Checked the VMware NAT network configuration.
3. Confirmed the default gateway.
4. Tested connectivity using an external IP address.
5. Reviewed the Windows Server network settings.

---

## Issue 3 — DNS Resolution Not Working

### Possible Causes

* Incorrect DNS server address
* DNS server unavailable
* DNS service not running
* Network connectivity problems
* DNS forwarding not configured

### Troubleshooting Steps

1. Reviewed the DNS settings using:

```cmd
ipconfig /all
```

2. Tested the configured DNS server's reachability.

3. Checked DNS resolution using:

```cmd
nslookup microsoft.com
```

4. Verified that the configured DNS server was functioning.

5. If using DC01 as the DNS server, confirmed that the DNS Server role had been installed and configured.

---

## Issue 4 — Duplicate IP Address

An IP address conflict can occur when two devices use the same IPv4 address.

To prevent this issue, I ensured that:

* The static IP address was not assigned to another virtual machine.
* The address was outside VMware's DHCP allocation range.
* The address belonged to the correct subnet.
* The same address would not be assigned to another server.

---

# Step 12 — Verify the Final Configuration

After completing the network configuration, I reviewed the server settings.

### Final Configuration Checklist

| Configuration           | Verification              |
| ----------------------- | ------------------------- |
| Computer Name           | DC01                      |
| Network Adapter         | Connected                 |
| VMware Network          | NAT / VMnet8              |
| Static IPv4 Address     | Configured                |
| Subnet Mask             | Verified                  |
| Default Gateway         | Verified                  |
| DHCP Address Assignment | Disabled on DC01          |
| Local TCP/IP Test       | Tested                    |
| Gateway Connectivity    | Tested                    |
| External Connectivity   | Tested if required        |
| DNS Resolution          | Tested when DNS available |

### Lab Configuration Record

| Setting          | Actual Configuration     |
| ---------------- | ------------------------ |
| Server Name      | DC01                     |
| Operating System | Windows Server 2019      |
| VMware Network   | VMnet8           |
| IPv4 Address     | 192.168.164.10 |
| Subnet Mask      | 255.255.255.0       |
| Default Gateway  | 192.168.164.2   |
| Preferred DNS    | 192.168.164.10       |

---

# Conclusion

In this section, I configured a static IPv4 address for Windows Server 2019.

I reviewed the VMware virtual network settings, identified the network subnet and default gateway, and selected an appropriate static IP address.

I configured the IPv4 settings using the Windows Server network adapter properties.

I also performed network verification and connectivity testing using Command Prompt.

This configuration prepares DC01 for its future role as an Active Directory Domain Controller and DNS server.

## Next Step

The next phase of the lab is to install **Active Directory Domain Services (AD DS)** and promote DC01 to a Domain Controller.

---
