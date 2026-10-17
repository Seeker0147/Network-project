# TECHNOVA LTD. — Departmental Network Design and Access Control

This project focuses on designing and configuring a **three-department enterprise network** for TECHNOVA LTD. using **Cisco Packet Tracer**. The network connects the IT, Sales, and HR departments through a central router and dedicated switches, with an **Access Control List (ACL)** implemented to control interdepartmental traffic while allowing authorized services such as HTTP access to a web server.

## Table of Contents

* [Project Overview](#project-overview)
* [Network Topology](#network-topology)
* [Tools and Technologies](#tools-and-technologies)
* [Configuration Steps](#configuration-steps)
* [Results and Findings](#results-and-findings)
* [Author](#author)

## Project Overview

The primary goal of this project is to design, configure, and test a simulated enterprise network for TECHNOVA LTD., demonstrating departmental connectivity and basic network security using Cisco Packet Tracer.

The project focuses on the following objectives:

* **Network Design:** Create a three-department LAN architecture connecting IT, Sales, and HR.
* **IP Addressing:** Configure IP addresses for departmental devices to enable communication within their respective networks.
* **Interdepartmental Connectivity:** Configure routing to facilitate communication between departmental networks.
* **Network Security:** Implement an extended Access Control List (ACL) to restrict specific traffic between departments.
* **Service Accessibility:** Configure and test HTTP access to a web server.
* **Network Testing:** Verify connectivity and access restrictions using ping tests and HTTP requests.

The project demonstrates how network segmentation, routing, and access control can be combined to improve security and maintain essential network services.

## Network Topology

The network topology was designed and simulated using Cisco Packet Tracer. It consists of three departmental LANs connected through a central router, with a dedicated switch serving each department.

### Network Architecture

The network includes the following components:

* **Central Router:** Connects the three departmental networks and facilitates interdepartmental routing.
* **IT Department Switch:** Connects IT workstations and the web server.
* **Sales Department Switch:** Connects Sales workstations to the network.
* **HR Department Switch:** Connects HR workstations to the network.
* **End Devices:** Six PCs distributed across the three departments.
* **Web Server:** A server hosted in the IT network, accessible through HTTP at `192.168.10.2`.

### Departmental Network Configuration

The documented topology identifies the following departmental networks:

| Department | Network Address   | Connected Devices          |
| ---------- | ----------------- | -------------------------- |
| IT         | `192.168.10.0/24` | Two PCs and one web server |
| Sales      | `192.168.20.0/24` | Two PCs                    |
| HR         | `192.168.30.0/24` | Two PCs                    |

**Note:** The `/24` subnet masks are assumed from the documented network addressing scheme. Individual PC addresses and router interface addresses are not fully specified in the supplied document.

### Logical Network Layout

```text
                       Central Router
                      /       |       \
                     /        |        \
                    /         |         \
             IT Network   Sales Network   HR Network
             192.168.10.0 192.168.20.0   192.168.30.0
                  |             |              |
              IT Switch     Sales Switch    HR Switch
               /  |  \        /    \         /    \
              PC  PC Server  PC    PC       PC    PC
                      |
                 Web Server
                 192.168.10.2
```

### Network Security Policy

An extended ACL was implemented to demonstrate traffic filtering between departments.

The documented security policy includes:

* **Restrict ICMP traffic:** Prevent Sales users from pinging devices in the IT network.
* **Permit other IP traffic:** Allow other IP traffic according to the configured ACL rules.
* **Allow HTTP access:** Enable Sales users to access the web server at `192.168.10.2` through HTTP.
* **Maintain departmental connectivity:** Verify that permitted communication paths continue to function.

This configuration demonstrates how network administrators can enforce specific communication policies without completely isolating departments from shared services.

## Tools and Technologies

The following tools, technologies, and network devices are identified in the project documentation.

### Software and Technologies

* **Cisco Packet Tracer:** Network simulation, device configuration, and connectivity testing.
* **Cisco IOS CLI:** Router configuration and ACL implementation.
* **IPv4 Addressing:** Assigning IP addresses to departmental networks and end devices.
* **Routing:** Enabling communication between different IP networks.
* **Extended Access Control Lists (ACLs):** Filtering traffic according to defined network security policies.
* **ICMP:** Testing network reachability using ping commands.
* **HTTP:** Accessing the web server to verify application-layer connectivity.

### Network Hardware

* **1 Central Router:** Connects the three departmental networks.
* **3 Network Switches:** Provide connectivity for the IT, Sales, and HR departments.
* **6 PCs:** Represent departmental user workstations.
* **1 Server:** Hosts the HTTP service in the IT network.

All devices were implemented in a simulated environment using Cisco Packet Tracer.

## Configuration Steps

### 1. Design the Network Topology

* Open Cisco Packet Tracer.
* Add one central router.
* Add three switches, one for each department.
* Add six PCs and distribute two PCs to each department.
* Add one server to the IT department.
* Connect the router to the departmental networks.
* Connect each PC and the server to its corresponding switch.
* Verify that the physical connections and interfaces are correctly configured.

### 2. Configure Departmental IP Addressing

Assign IP addresses to the end devices according to their departmental networks.

Use the following addressing scheme:

| Department | Network           | Subnet Mask     |
| ---------- | ----------------- | --------------- |
| IT         | `192.168.10.0/24` | `255.255.255.0` |
| Sales      | `192.168.20.0/24` | `255.255.255.0` |
| HR         | `192.168.30.0/24` | `255.255.255.0` |

For each PC:

1. Open the device in Packet Tracer.
2. Navigate to **Desktop → IP Configuration**.
3. Assign an available IP address from the appropriate departmental subnet.
4. Configure the subnet mask.
5. Configure the default gateway to match the router interface for that department.

For the web server:

1. Open the server configuration.
2. Assign the IP address `192.168.10.2`.
3. Configure the appropriate subnet mask.
4. Set the default gateway to the router interface for the IT network.
5. Enable the HTTP service.

**Note:** The supplied document does not specify every device's individual IP address or default gateway. These values should be confirmed against the original Packet Tracer configuration.

### 3. Configure the Router

Configure the router interfaces to connect the IT, Sales, and HR networks.

The configuration process involves:

1. Accessing the router's CLI.
2. Entering privileged EXEC mode.
3. Entering global configuration mode.
4. Configuring the appropriate router interfaces with IP addresses from their respective subnets.
5. Enabling the interfaces.
6. Verifying interface status and routing connectivity.

Example Cisco IOS commands:

```text
enable
configure terminal
interface <interface-id>
ip address <ip-address> <subnet-mask>
no shutdown
exit
```

Repeat the interface configuration for each departmental network, using the actual interface identifiers and IP addresses assigned in the topology.

### 4. Configure the Extended ACL

Implement an extended ACL to prevent Sales users from pinging IT devices while allowing other IP traffic permitted by the security policy.

The intended policy is:

* Deny ICMP traffic from the Sales network to the IT network.
* Permit other IP traffic from Sales to IT.
* Preserve HTTP access to the web server at `192.168.10.2`.

An illustrative Cisco IOS ACL is shown below. The ACL number, interface, direction, and source or destination addresses must match the actual Packet Tracer configuration.

```text
enable
configure terminal

access-list 101 deny icmp 192.168.20.0 0.0.0.255 192.168.10.0 0.0.0.255
access-list 101 permit ip 192.168.20.0 0.0.0.255 192.168.10.0 0.0.0.255
access-list 101 permit ip any any
```

Apply the ACL to the appropriate router interface in the correct direction.

For example:

```text
interface <interface-id>
ip access-group 101 in
exit
```

**Important:** The commands above illustrate the intended policy; they are not a verified transcription of the original router configuration. Cisco ACLs are processed from top to bottom, and unmatched traffic is subject to an implicit deny. The final permit rule must be appropriate for the organization's security requirements and the ACL's placement.

### 5. Configure the Web Server

Configure the server in the IT network to provide HTTP access.

1. Open the server in Cisco Packet Tracer.
2. Navigate to its IP configuration settings.
3. Confirm that its IP address is `192.168.10.2`.
4. Verify the subnet mask and default gateway.
5. Open the server's services configuration.
6. Enable the HTTP service.
7. Confirm that the server can be reached from permitted network locations.

This step establishes the application service used to test whether the ACL permits web traffic even when ICMP traffic is blocked.

### 6. Test Connectivity from the HR Department

Use the command prompt on an HR workstation to test connectivity to the IT server.

Run:

```text
ping 192.168.10.2
```

The project documentation includes a successful ping test from HR to the IT server.

This result indicates that the tested device can reach `192.168.10.2` and that the corresponding network path permits ICMP traffic.

### 7. Test the ACL from the Sales Department

Open the command prompt on a Sales workstation and run:

```text
ping 192.168.10.2
```

The documented result shows that the Sales workstation cannot reach the IT server using ICMP.

This is consistent with the intended ACL policy, which blocks ICMP traffic from Sales to IT.

A failed ping alone does not establish that all communication is blocked; the HTTP test provides additional evidence of the filtering behavior.

### 8. Verify HTTP Access from Sales

From a Sales workstation:

1. Open the web browser in Cisco Packet Tracer.

2. Enter the server address:

   ```text
   http://192.168.10.2
   ```

3. Confirm that the server's web page loads successfully.

The supplied documentation shows that the web server is accessible through HTTP from Sales despite the failed ICMP ping.

This demonstrates the intended distinction between blocking a particular traffic type and blocking all communication between two networks.

### 9. Review and Save the Configuration

* Verify the router interface status.
* Confirm that departmental IP addresses and default gateways are correct.
* Review the ACL rules and their application to the router interface.
* Repeat the connectivity and HTTP tests.
* Save the Packet Tracer project for future testing and modification.

## Results and Findings

The project demonstrates the implementation of a three-department network with basic interdepartmental traffic controls.

### 1. Successful Network Segmentation

The topology separates the IT, Sales, and HR departments into distinct IP networks:

* IT: `192.168.10.0/24`
* Sales: `192.168.20.0/24`
* HR: `192.168.30.0/24`

Each department has its own switch and connected workstations, while the central router provides connectivity between networks.

### 2. Successful Connectivity from HR to IT

The supplied ping screenshot indicates that an HR workstation can successfully reach the server at `192.168.10.2`.

**Finding:** The tested communication path between HR and the IT server permits ICMP traffic.

### 3. ICMP Traffic Restricted from Sales to IT

The supplied failed-ping screenshot shows that a Sales workstation cannot reach `192.168.10.2` using ICMP.

**Finding:** The observed result is consistent with the intended ACL rule that blocks ping traffic from Sales to IT.

### 4. HTTP Access Preserved

The supplied HTTP screenshot indicates that the Sales department can access the web server at `192.168.10.2` through a browser.

**Finding:** HTTP access remains available even though ICMP ping traffic from Sales to IT is blocked.

### 5. Demonstration of Extended ACL Functionality

The project demonstrates how extended ACLs can control network traffic based on characteristics such as source IP address, destination IP address, and protocol.

The results illustrate that:

* Traffic can be restricted selectively rather than blocking all interdepartmental communication.
* ICMP and HTTP traffic can be treated differently by the network security policy.
* A web service can remain accessible while diagnostic traffic is restricted.

### Summary of Verification Results

| Test                              | Expected Behavior        | Documented Result                            |
| --------------------------------- | ------------------------ | -------------------------------------------- |
| HR to IT server using ping        | ICMP permitted           | Successful                                   |
| Sales to IT server using ping     | ICMP denied              | Failed as intended                           |
| Sales to IT server using HTTP     | HTTP permitted           | Successful                                   |
| Departmental network connectivity | Routing between networks | Partially demonstrated by the supplied tests |

### Conclusion

The TECHNOVA LTD. network project demonstrates the design of a small enterprise LAN using Cisco Packet Tracer, IPv4 addressing, routing, and extended ACLs.

The supplied test evidence supports the intended security behavior: **Sales users cannot ping the IT server but can still access its HTTP service, while the documented HR-to-IT ping succeeds.**

These results provide a practical demonstration of selective traffic filtering and the importance of testing network connectivity at both the network and application layers.

The supplied evidence does not independently verify every router interface, ACL rule, or communication path. Further testing would be required to confirm the complete network configuration and security policy.

## Author

* **Name:** Not specified in the supplied document.
* **Project:** TECHNOVA LTD. — Departmental Network Design and Access Control
* **Platform:** Cisco Packet Tracer
* **Contact:** Not provided in the supplied document.

**To complete this section,** replace the placeholders with your name, professional email address, and GitHub profile if applicable.

