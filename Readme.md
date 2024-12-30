# Part 1
## Securing a Console

```
enable
configure terminal
line console 0
password yourPassword
login
```


This sequence of commands is used to configure a **console password** on a Cisco switch in Cisco Packet Tracer. Here's what each line does:

### 1. **`enable`**
   - Switches from **user EXEC mode** to **privileged EXEC mode**.
   - In this mode, you have access to more advanced commands needed for configuration.

---

### 2. **`configure terminal`**
   - Enters **global configuration mode**, allowing you to make configuration changes to the device.

---

### 3. **`line console 0`**
   - Accesses the **console line configuration** mode.
   - `console 0` refers to the physical console line, which is used for direct access to the switch through a console cable.

---

### 4. **`password yourPassword`**
   - Sets the password for the console line. Replace `yourPassword` with the actual password you want to set.
   - This password will be required when accessing the switch via the console.

---

### 5. **`login`**
   - Enables the use of the password on the console line.
   - Without this command, the configured password will not be required for login.

---

### Summary
These commands secure access to the switch via the **console port** by requiring a password. Anyone connecting directly to the switch through the console port must provide the specified password to gain access.

---


## Securing Privilege Mode
```
enable
configure terminal
enable secret mySecurePassword
```
This code configures the **privileged EXEC mode** password on a Cisco device. Here's the breakdown:

---

### 1. **`enable`**
   - Switches from **user EXEC mode** to **privileged EXEC mode**.
   - Privileged EXEC mode allows access to advanced commands and configurations.

---

### 2. **`configure terminal`**
   - Enters **global configuration mode**, enabling you to make configuration changes to the device.

---

### 3. **`enable password yourPassword`**
   - Sets a **password** for entering **privileged EXEC mode**.
   - When someone tries to enter `enable` mode, they must provide the `yourPassword` value.
   - **Note:** This password is stored in plaintext in the device configuration, making it less secure.

---

### 4. **`enable secret yourSecret`**
   - Sets an **encrypted password** for entering **privileged EXEC mode**.
   - The password is hashed using MD5, making it more secure.
   - This is preferred over `enable password` because it prevents the password from being visible in plaintext in the configuration file.
   - **If both `enable password` and `enable secret` are configured, the `enable secret` takes precedence.**

---


### Why Configure These?
This protects the **privileged EXEC mode**, ensuring only authorized users can access advanced configuration and troubleshooting commands on the device.

## Encrypting Privilege Mode Passwords
```
enable
configure terminal
service password-encryption
```
This sequence of commands is used to **encrypt passwords** in the configuration file on a Cisco device. Here's the breakdown:



###     **`service password-encryption`**
   - Enables **basic encryption** for passwords stored in the device configuration file.
   - It applies **type 7 encryption**, which is a weak form of encryption (not secure against determined attackers but better than plaintext).
   - This command affects passwords for:
     - **Console lines** (`line console 0`)
     - **VTY (telnet/SSH) lines** (`line vty 0 4`)
     - **Enable passwords** (but not `enable secret`, which already uses stronger MD5 encryption).

---

### **Why Use `service password-encryption`?**
- Prevents passwords from appearing as plaintext in the configuration file when using commands like `show running-config` or `show startup-config`.
- Adds a basic layer of security, particularly for casual viewing of configurations (e.g., when sharing a configuration file).
---
## Displaying the Running Configuration
```
enable
show running-config
```
Used to display the current configuration that is actively running in the device's memory (RAM). 
It displays active settings such as the hostname, interface configurations, enable secret, and console password.

## Saving Configuration Changes
```
enable
copy running-config startup-config
```
This sequence of commands is used to **save the current configuration** on a Cisco device so that it persists across reboots. Here's what each line does:

---

### **`copy running-config startup-config`**
   - Copies the current **running configuration** (stored in RAM) to the **startup configuration** (stored in NVRAM).
   - Ensures that the configuration will persist even after the device is restarted or powered off.

---

### **Key Terms:**
- **Running Configuration:**
  - The active configuration currently being used by the device.
  - Any changes made using configuration commands are applied immediately to the running configuration.
  - Stored in **RAM** and lost upon reboot.

- **Startup Configuration:**
  - The configuration file that the device loads during the next boot.
  - Stored in **NVRAM** (non-volatile memory), so it persists after a reboot.

---

### **Why Use This Command?**
- Ensures that any configuration changes you make (such as IP addresses, VLANs, passwords, or routing protocols) are saved permanently.
- Prevents loss of configurations during unexpected reboots or power outages.

---


### **Important Notes:**
- If you forget to run this command after making changes, those changes will be lost when the device reboots.
The sequence of commands:
- You can also use the shorthand `write memory` or `wr` as an alternative to `copy running-config startup-config`.

## Displaying the Startup Configuration
```
enable
show startup-config
```

## Configuring the Message of the Day (MOTD) Banner
```
enable
configure terminal
banner motd # Your message here #
```
This command sequence is used to set up a **Message of the Day (MOTD) banner** on a Cisco device.

---


### **`banner motd # Your message here #`**
   - Configures a **Message of the Day (MOTD) banner**.
   - The banner displays a message to anyone accessing the device, whether through the console, Telnet, or SSH.
   - The `#` is a **delimiter** marking the start and end of the message. You can use any unique character as the delimiter as long as it doesn't appear in the message.

---

### **Purpose of the MOTD Banner:**
1. **Display Informational Messages:**
   - Announce maintenance windows, usage policies, or other relevant information.

2. **Warn Unauthorized Users:**
   - Many organizations use this banner to display legal disclaimers or warnings against unauthorized access.

---

### **Example Usage:**
```plaintext
Switch(config)# banner motd # Unauthorized access is prohibited. #
```

### **Result:**
- When a user connects to the device, they will see:
  ```plaintext
  Unauthorized access is prohibited.
  ```
---


# Part 2
## Configuring a Management IP Address for a Switch
```
enable
configure terminal
interface vlan 1
ip address 192.168.1.254 255.255.255.0
no shutdown
exit
```
This sequence of commands is used to configure a **management IP address** on a Cisco switch's VLAN 1 interface.
---

### **`interface vlan 1`**
   - Accesses the **VLAN 1 interface** configuration mode.
   - VLAN 1 is the **default management VLAN on a Cisco switch**.
   - By configuring this interface, you can assign an IP address for managing the switch.

---

### **`ip address 192.168.1.254 255.255.255.0`**
   - Assigns the IP address **192.168.1.254** to VLAN 1 with a subnet mask of **255.255.255.0**.
   - This IP address allows remote management of the switch (e.g., via Telnet or SSH) within the **192.168.1.0/24 network**.

---

### **`no shutdown`**
   - Enables the VLAN 1 interface, bringing it into an **up** state.
   - By default, interfaces are **administratively down** until explicitly enabled.

---

### **`exit`**
   - Exits the interface configuration mode and returns to the global configuration mode.

---

### **Purpose of the Code:**
- Configures a **management IP address** for the switch, enabling remote management via protocols like Telnet, SSH, or HTTP (if configured).
- The IP address is associated with VLAN 1, which is the default management VLAN.

---

## Creating a VLAN
```
enable
configure terminal
vlan 10
name RED
exit
```
This sequence of commands is used to create and name a VLAN on a Cisco switch. Here's the detailed explanation:

---


### **`vlan 10`**
   - Creates or accesses VLAN **10** in the VLAN database.
   - If VLAN 10 already exists, this command enters its configuration mode.

---

### **`name RED`**
   - Assigns the name **RED** to VLAN 10.
   - VLAN names are used for identification purposes and make it easier to organize and manage VLANs.

---


### **Purpose of the Code:**
- **Creates VLAN 10** and names it **RED**.
- This VLAN can now be assigned to specific ports on the switch to segment network traffic.

---


### **Example Output:**
1. After running the commands, you can verify the VLAN:
   ```plaintext
   Switch# show vlan brief
   VLAN Name                             Status    Ports
   ---- -------------------------------- --------- ----------------
   1    default                          active    Fa0/1, Fa0/2
   10   RED                              active
   ```

2. VLAN 10 is now available for port assignments. For example:
   ```plaintext
   Switch(config)# interface Fa0/1
   Switch(config-if)# switchport mode access
   Switch(config-if)# switchport access vlan 10
   ```

---

## Assigning Ports to a VLAN
```
enable
configure terminal
interface fastEthernet 0/1
no shutdown
switchport mode acess
switchport access vlan 10

```
This sequence of commands in Cisco Packet Tracer is used to configure a specific port on a switch for access mode and assign it to VLAN 10.

---
### **`interface fastEthernet 0/1`**  
   - Enters interface configuration mode for the specific interface (`FastEthernet 0/1`) on the switch. This allows you to configure settings specific to this port.

### **`no shutdown`**
   - Enables the interface, allowing it to forward traffic.
   - Without this command, the port would remain administratively down, even if it were configured for a VLAN or access mode.

### **`switchport mode access`**  
   - Sets the port to **access mode**, meaning it will only allow traffic for a single VLAN (as opposed to trunk mode, which carries multiple VLANs).

### **`switchport access vlan 10`**  
   - Assigns the port (`FastEthernet 0/1`) to **VLAN 10**. Any device connected to this port will be a part of VLAN 10, allowing it to communicate only with other devices in the same VLAN (unless routing between VLANs is configured).

### Result:
After executing these commands, the following happens:
- The switch port `FastEthernet 0/1` is configured in **access mode**.
- The port is assigned to **VLAN 10**.
- Any device connected to this port will be a member of VLAN 10, enabling segregation of network traffic and ensuring that this port is dedicated to devices in VLAN 10.

This configuration is typically used in scenarios where end devices (like PCs, printers, or IP phones) are connected to the switch, and you want to place them in a specific VLAN for network segmentation and security.

## Assigning Multiple Ports to a Single VLAN
```
interface range fastEthernet 0/1-4
switchport mode acess
switchport access vlan 10
```

These commands configure multiple interfaces (ports) on the switch at the same time.

---


### **`interface range fastEthernet 0/1-4`**  
   - This command specifies a **range of interfaces** (from `FastEthernet 0/1` to `FastEthernet 0/4`) for configuration. The `range` keyword is mandatory when configuring multiple interfaces simultaneously.

### **`switchport mode access`**  
   - Sets all the selected ports (`FastEthernet 0/1` to `FastEthernet 0/4`) to **access mode**. This ensures the ports are configured to only carry traffic for a single VLAN.

### **`switchport access vlan 10`**  
   - Assigns **VLAN 10** to all the selected ports. All devices connected to these ports will be part of VLAN 10.

---

### Result:
- **Ports affected**: `FastEthernet 0/1`, `FastEthernet 0/2`, `FastEthernet 0/3`, and `FastEthernet 0/4`.
- **Port mode**: All the ports are configured as **access ports**.
- **VLAN assignment**: These ports are now assigned to **VLAN 10**. Any device connected to these ports will communicate within VLAN 10.

---


This approach is ideal for:
- Simplifying configuration when you have multiple ports that need identical settings.
- Efficiently assigning multiple devices (e.g., a group of PCs or printers) to a specific VLAN for network segmentation and traffic isolation.

By using `interface range`, you avoid having to configure each port individually, which saves time and reduces the chance of configuration errors.

## Trunk Mode  

Trunks are used to connect multiple switches to enable communication between devices in the same VLAN across different switches.  

### **Example Scenario:**  
Consider two switches, each connected to two PCs. One PC on each switch belongs to the **Sales VLAN** and the other belongs to the **Development VLAN**. The switches are interconnected via the `F0/3` port. We need to ensure that the Sales PCs and the Development PCs can communicate with each other, even though they are connected to different switches.  

---

### **Configuration for Switch 1:**  
- **`F0/1`:**  
  - **Port Type:** Access  
  - **VLAN:** 10 (Sales)  

- **`F0/2`:**  
  - **Port Type:** Access  
  - **VLAN:** 20 (Development)  

- **`F0/3`:**  
  - **Port Type:** Trunk  
  - **Allowed VLANs:** 10, 20  

#### **Commands for Switch 1:**  
```plaintext
interface fastEthernet 0/1
no shutdown
switchport mode access
switchport access vlan 10
```
```plaintext
interface fastEthernet 0/2
no shutdown
switchport mode access
switchport access vlan 20
```
```plaintext
interface fastEthernet 0/3
no shutdown
switchport mode trunk
switchport trunk allowed vlan add 10
switchport trunk allowed vlan add 20
```

---

### **Configuration for Switch 2:**  
- **`F0/1`:**  
  - **Port Type:** Access  
  - **VLAN:** 10 (Sales)  

- **`F0/2`:**  
  - **Port Type:** Access  
  - **VLAN:** 20 (Development)  

- **`F0/3`:**  
  - **Port Type:** Trunk  
  - **Allowed VLANs:** 10, 20  

#### **Commands for Switch 2:**  
```plaintext
interface fastEthernet 0/1
no shutdown
switchport mode access
switchport access vlan 10
```
```plaintext
interface fastEthernet 0/2
no shutdown
switchport mode access
switchport access vlan 20
```
```plaintext
interface fastEthernet 0/3
no shutdown
switchport mode trunk
switchport trunk allowed vlan add 10
switchport trunk allowed vlan add 20
```

---

### **Result:**  
By configuring the trunk on the `F0/3` port of both switches, PCs belonging to the same VLAN can now communicate with each other across the switches:
- Sales PCs (VLAN 10) can communicate with each other.  
- Development PCs (VLAN 20) can communicate with each other.  

Trunks allow the tagged VLAN traffic to traverse between the switches, ensuring proper segregation and communication of VLANs.

## Access vs. Trunk  

### **Access Configuration:**  
- Hosts within the same VLAN can communicate or ping each other.  
- An access port can belong to only **one VLAN** at a time.  
- All ports configured in access mode are part of a single VLAN.  
- Typically used for connections between switches and endpoint devices (e.g., hosts, PCs, printers).  

---

### **Trunk Configuration:**  
- Trunks are used to connect **switches** and allow the exchange of traffic for multiple VLANs.  
- By default, a trunk port carries traffic for **all VLANs**, unlike an access port.  
- **Purpose:** Enables communication between hosts in different VLANs.  
- Trunk ports identify traffic from different VLANs using **VLAN IDs** rather than MAC addresses.  


# Part 3
## Telnet Implementation
### 1. Set IP for Router Port
Using the wizard or the following commands:
```
enable
configure terminal
interface Gig0/0/0      # The Opening Port
ip address 192.168.1.1 255.255.255.0
no shutdown
```

When dealing with switches, the IP address is assigned to a VLAN:
```
interface vlan 1
ip address 192.168.1.1 255.255.255.0
no shutdown
```

### 2. Enable Password
```
enable
configure terminal
enable password amr123
```

### 3. Configuring Telnet (Set line vty):
```
enable
configure terminal
line vty 0 4
password 1234
login
```

This code is used to configure Telnet access on a Cisco device, allowing remote management of the device via the Telnet protocol.

---

**`line vty 0 4`**
- Configures the **virtual terminal lines** (VTY) on the device.  
- `0 4` specifies lines 0 through 4, which are the first 5 Telnet sessions allowed on the device.  

---

**`password 1234`**
- Sets the password for Telnet access to **`1234`**.  
- Users attempting to connect to the device via Telnet will be prompted to enter this password.

---

**`login`**
- Activates password authentication for the VTY lines.  
- Without this command, the device will not prompt for a password during Telnet sessions, leaving the lines open but unsecured.

---

**Purpose:**
This configuration enables Telnet access to the device and secures it with a password. Remote users can now connect to the device using Telnet by entering the IP address of the device and providing the configured password (**`1234`**) when prompted.

---

**How to Test:**
1. Use a Telnet client (e.g., `telnet` command or a terminal application).
2. Connect to the device's IP address.
3. Enter the password **`1234`** when prompted.

---
### 4. Using PC to Access the Router Configurations
Open command prompt and then type: `telnet 192.168.1.1`



## SSH Implementation

### 1. Set IP for Router Port & Enable Password (Same as Telnet)
### 2. Configure SSH
```
enable
configure terminal
username amr secret amr1234
ip domain-name amr.com
hostname amrMosallem
crypto key generate rsa
How many bits in the modulus [512]: 1024  #(Multiples of 512)
line vty 0 15
transport input ssh
login local
exit
```
This code configures SSH (Secure Shell) access on a Cisco device for secure remote management.
This code configures **SSH (Secure Shell)** access on a Cisco device for secure remote management. Here's a detailed explanation of each line:

---

**`enable`**
- Enters **privileged EXEC mode**, where administrative tasks can be performed.

---

**`configure terminal`**
- Switches to **global configuration mode**, allowing you to make configuration changes to the device.

---

 **`username amr secret amr1234`**
- Creates a user account named **`amr`** with an encrypted password (or secret) **`amr1234`**.  
- This account is used for authentication when accessing the device via SSH.

---

 **`ip domain-name amr.com`**
- Sets the domain name for the device to **`amr.com`**.  
- The domain name is required to generate the RSA key used for SSH encryption.

---

 **`hostname amrMosallem`**
- Sets the hostname of the device to **`amrMosallem`**.  
- This is also required for generating the RSA key.

---

 **`crypto key generate rsa`**
- Generates an **RSA key pair** for SSH encryption.  
- RSA keys are essential for securing SSH communication.

---

 **`How many bits in the modulus [512]: 1024`**
- Prompts the user to specify the **key size (modulus)** for the RSA key.  
- **`1024` bits** is chosen for stronger encryption. (It must be a multiple of 512 and at least 768 for modern security standards.)

---

 **`line vty 0 15`**
- Configures the **virtual terminal lines** (VTY) 0 through 15.  
- These lines allow up to 16 simultaneous remote management sessions.

---

 **`transport input ssh`**
- Restricts the VTY lines to accept only **SSH connections**.  
- Telnet is disabled, ensuring secure remote access.

---

**`login local`**
- Configures the device to use the **local username and password** (created earlier with `username amr secret amr1234`) for authentication.

---


---

### **What This Configuration Achieves:**
1. **Enables SSH:** Allows secure, encrypted remote management of the device.  
2. **Local Authentication:** Uses the username and password for secure access.  
3. **Restricts Access:** Disables Telnet (insecure protocol) and accepts only SSH.  

---

### **How to Test:**
1. Use an SSH client (e.g., `ssh` command or a terminal application).
2. Connect to the device using its IP address and port 22 (default SSH port).
3. Log in using the username **`amr`** and password **`amr1234`**.

---
This configuration ensures secure and reliable remote access to your Cisco device.


### 4. Using PC to Access the Router Configurations
```
PC>ssh -l ali 192.168.1.1
Open Password:
R1>
```
### Note: Enable Password is Required


# Part 4
## Switch Port Security Configuration
1. Define the maximum number of MAC addresses allowed per port.
2. Set the violation mode to specify how the switch should respond to security violations.
3. Enable port security on the desired interfaces.
---
### Port Security Mac address Configuration
   -  **Static MAC Addresses**:
      ```
      Switch(config-if)# switchport port-security mac-address 0011.2233.4455
      Switch(config-if)# switchport port-security mac-address 0066.7788.99AA
      ```
   - **Dynamic (Sticky) MAC Addresses**:
      ```
      Switch(config-if)# switchport port-security mac-address sticky
      ```

### Configuring Maximum Number of MAC Addresses
   - **Static MAC Addresses**: Manually configure specific MAC addresses that are allowed to connect.
   - **Dynamic MAC Addresses**: Set a limit on the number of unique MAC addresses allowed to connect to a port.
      ```
      Switch(config)#interface fa0/1
      Switch(config-if)#switchport port-security
      Switch(config-if)#switchport port-security maximum 1
      ```
### Setting the Violation Mode
   - **Shutdown**: Disable the port when a violation occurs, preventing further access.
   - **Restrict**: Block new connections while allowing existing connections to remain active.
   - **Protect**: Log the violation but allow the connection to continue.
      ```
      Switch(config-if)# switchport port-security violation protect
      Switch(config-if)# switchport port-security violation restrict
      Switch(config-if)# switchport port-security violation shutdown
      ```
### Port Security Code:
```
Switch> enable
Switch# configure terminal
! Configuration for FastEthernet 0/1 using Static MAC Address
Switch(config)# interface FastEthernet 0/1
Switch(config-if)# switchport mode access
Switch(config-if)# switchport port-security
Switch(config-if)# switchport port-security maximum 2
Switch(config-if)# switchport port-security violation restrict
Switch(config-if)# switchport port-security mac-address 0011.2233.4455
Switch(config-if)# switchport port-security mac-address 0022.3344.5566
Switch(config-if)# exit
! Save configuration
Switch# write memory
```