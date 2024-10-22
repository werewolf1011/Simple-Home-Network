# Simple-Home-Network
This guide will walk you through setting up a home network using various devices such as smartphones, PCs, laptops, and a printer. The setup includes configuring a home router (PT-AC), securing the network, and ensuring proper connectivity with an ISP.

Devices Used
  End Devices:
    Smartphones
    PC
    Laptop
    Printer
    Router:
      Home Router PT-AC

Step-by-Step Instructions
1. Connect End Devices to the Router
  Connect any end device to the router (either wired or wirelessly).

  Navigate to the Desktop Tab of the device.

  Go to IP Configurations and select DHCP for dynamic IP configuration.

  The default IP will be:
  192.168.0.1

  Verify this by opening Command Prompt in the Desktop Tab and running the command:
  ipconfig

2. Access Router's Web Interface
  Open Web Browser from the Desktop Tab and visit the default gateway:
  http://192.168.0.1

  Enter the default credentials:

  Username: admin
  Password: admin

3. Change the Router's Default Password
  After logging in, go to the Administration panel.
  Change the password to something stronger:
  New Password: #letmein99!
  Save the settings by clicking Save at the bottom of the page.

4. Limit Number of Devices Connected
  Navigate to the Setup Menu of the gateway.
  Edit the Maximum Number of Users allowed to connect.
  Save the changes.

5. Set Static IP for the Printer
  Copy the printer's Name and MAC Address:

  Name: Printer0
  MAC Address: 00:D0:D3:79:5B:A5
  Go to the DHCP Reservation section in the setup menu of the router.

  Manually add the printer:

  Name: Printer0
  MAC Address: 00:D0:D3:79:5B
  Static IP: Choose an IP within the router's range (e.g., 192.168.0.100).
  Go to the printer settings, and set the Static IP for the printer.


6. Hide the Network (Disable SSID Broadcast)
  Navigate to the Wireless Menu in the router’s web interface.
  Disable broadcasting of the SSID to hide the network.

7. Secure the Wireless Network
  Navigate to Wireless Security.

  Set Security Mode to WPA2 Personal for maximum security.

  Choose AES Encryption for all frequencies.

  Passphrase: #herdaibasala69

8. Connect the Laptop to the Network (Wireless Connection)
  Click on the laptop and navigate to the Physical Tab.

  Turn off the power switch, replace the Ethernet interface with a 2.4GHz Wireless         Interface (PT-LAPTOP-NM-1W), and turn the laptop back on.

  Go to the Wireless Settings and configure:
    SSID: werewolf_wifi2.4
    Password: Use the one set in previous steps.
    Connect the laptop to the network wirelessly.

9. Enable Guest Network
  Go to the Wireless Tab and select Guest Network.
  Enable Guest Profile and set the following security settings:
    Security Mode: WPA2 Personal
    Encryption: AES
    Set a Wi-Fi Name for each frequency and password.

10. Wireless MAC Filtering for Security
  To limit which devices can connect wirelessly, enable MAC Filtering.

  Collect MAC addresses of devices:
    Smartphone 1: 00:E0:F7:6B:A2:77
    Laptop: 00:06:2A:E2:24:12
    Smartphone 2: 00:60:47:7C:5C:21
    Go to the Wireless MAC Filter tab and add the MAC addresses of the allowed devices.
    Enable MAC filtering and select Permit for the listed devices to connect.

11. Internet Connection Setup with VLANs
  a. Router Configuration
    Choose a Router (2811).
    Add a NM-ESW-161 EtherSwitch Module to an available slot.
    Connect two servers to the router and create VLANs for them.
  b. VLAN Configuration
    Router> enable
    Router# conf t
    Router(config)# int vlan 8 name DNS
    Router(config-if)# ip add 8.8.8.1 255.255.255.0
    Router(config-if)# exit
    Router(config)# int vlan 10 name google
    Router(config-if)# ip add 10.10.10.1 255.255.255.0
    Router(config-if)# exit
    Router# do wr
    Router# show vlan brief

  c. Assign VLANs to Ports
    Router(config)# int range fastEthernet 1/0-6
    Router(config-if-range)# switchport mode access
    Router(config-if-range)# switchport access vlan 8
    Router(config-if-range)# no shutdown
    Router(config)# int range fastEthernet 1/7-15
    Router(config-if-range)# switchport mode access
    Router(config-if-range)# switchport access vlan 10
    Router(config-if-range)# no shutdown

12. Internet Connection via Cloud and DSL Modem
  Add a Cloud and connect Ethernet0 on the router to the cloud.

  Drag and place PT-CLOUD-NM-1CFE and PT-CLOUD-NM-1AM.

  Connect the DSL Modem to the cloud.

  Configure the cloud and map the DSL to FastEthernet9.

  DHCP Configuration on ISP Router:
    Router(config)# ip dhcp pool CUSTOMERS
    Router(dhcp-config)# default-router 20.110.24.1
    Router(dhcp-config)# network 20.110.24.0 255.255.255.0
    Router(dhcp-config)# dns-server 8.8.8.8
    Router(dhcp-config)# exit
    Router(config)# ip dhcp excluded-address 20.110.24.1

Connect the DSL Modem to the home router to enable internet access.
