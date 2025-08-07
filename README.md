🕵️‍♂️ Wireshark Network Traffic Analysis Lab

This repository contains a guided walkthrough of a Wireshark lab focused on analyzing network traffic at multiple layers of the OSI model. By following these steps, you can learn how to identify network behavior, analyze protocols, and verify compliance with standard network configurations.
📘 Scenario

You are setting up an employee’s laptop for remote work. To support and secure this setup, the company requires all home networks to follow a consistent configuration. A packet capture (packetcap) is provided to verify the laptop's network activity. Your task is to inspect the capture using Wireshark and confirm that everything is functioning correctly.
🧭 Lab Objectives

    Identify traffic types and protocols across OSI layers.

    Analyze packet encapsulation and communication flow.

    Examine IP, MAC, TCP, UDP, DNS, and HTTP behavior.

    Observe both local and remote traffic interactions.

🧑‍💻 Step-by-Step Instructions
🔹 Step 1: Open Wireshark and Load the Capture

    Sign in to the LAPTOP VM as user Bobby (Password: Pa$$w0rd).

    Open Wireshark using the desktop shortcut.

    Navigate to File > Open, and select the file named packetcap from the Downloads folder.

    Maximize the Wireshark window for better visibility.

📸 Insert screenshot of Wireshark with the capture loaded
🔹 Step 2: Inspect the First Frame

    In the top pane, select Frame #1.

    Observe the Protocol column — you should see ARP (Address Resolution Protocol).

    In the middle pane, expand the first summary line labeled Frame 1 to view encapsulation details.

📘 This confirms that the link layer is using Ethernet II.

📸 Insert screenshot showing ARP protocol and Ethernet encapsulation
🔹 Step 3: Analyze MAC Addresses

    Expand the Ethernet II section to find the Source MAC address.

    It should read: 00:15:5d:01:65:67.

    Confirm that this frame is an ARP request.

    Select Frame #2, and verify it is the ARP reply, where:

        The source and destination MAC addresses are reversed.

        The reply provides the MAC address of the client.

📸 Insert screenshot showing ARP request and reply with MACs
🔹 Step 4: Examine ARP Details

    Return to Frame #1 and expand the ARP (Request) section.

    Check the target MAC address — it should be all zeros (broadcast).

    Select Frame #2 again and expand the ARP (Reply) section.

    Confirm the MAC address for 192.168.0.236 is: 00:15:5d:00:66:77.

📘 ARP is used to resolve the MAC address of a host from its IP address.

📸 Insert screenshot showing ARP header info
🔹 Step 5: Review IPv4 Packet Structure

    Select Frame #3.

    Expand the Ethernet II and Internet Protocol Version 4 sections.

    Note that this is the first packet to use IP addresses for communication.

📘 This marks the transition from the link layer to the network layer.

📸 Insert screenshot of IP header structure
🔹 Step 6: Analyze UDP and DNS Traffic

    With Frame #3 still selected, scroll to the User Datagram Protocol (UDP) section.

    Record the Source Port (randomly generated client port).

    Confirm the Destination Port is 53, which is used for DNS.

    Select Frame #4, the DNS response.

    Validate that it uses 53 as the source port, replying to the client’s port.

📘 DNS uses UDP because it is a fast, connectionless protocol.

📸 Insert screenshot showing UDP and DNS request/response
🔹 Step 7: Analyze TCP Handshake

    Select Frame #5, the start of a TCP handshake.

        Look for the SYN flag.

        Source port is a random client port (e.g., 49920).

        Destination port is 80 (HTTP).

    Move to Frame #6 – check for SYN, ACK response.

    In Frame #7, confirm the final ACK completes the 3-way handshake.

📘 TCP provides reliable, ordered delivery using handshakes and acknowledgments.

📸 Insert screenshots of the 3 handshake frames
🔹 Step 8: Explore HTTP Traffic

    Scroll to Frame #9 — this is the HTTP GET request.

    Observe the readable request in the Hypertext Transfer Protocol section.

    In Frame #15, view the server’s HTTP response.

📘 HTTP in this capture is not encrypted — you can read the request and response content.

📸 Insert screenshot showing HTTP GET and server response
🔹 Step 9: Multiple TCP Sessions

    Examine Frame #8 — this begins a second TCP handshake.

    Note the use of a new client source port (e.g., 49921).

    This shows how multiple TCP sessions may run in parallel to the same server.

📸 Insert screenshot showing second TCP connection initiation
🔹 Step 10: Review DNS Name Resolution

    Revisit Frames #3 and #4 for DNS resolution of 192.168.0.1.

    Confirm the hostname associated with this IP is shown in the Info column.

    Check whether there is any name resolution for 192.168.0.236.

📘 The router (192.168.0.1) resolves to a name, but the client does not.

📸 Insert screenshot showing DNS query details
🔹 Step 11: Inspect Remote Traffic (neverssl.com)

    Scroll to around Frame #216 to find a DNS request for neverssl.com.

    Record the IP address from the response: 34.223.124.45.

    Select Frame #222 to analyze the destination MAC.

    Verify that the packet is addressed to the router’s MAC address, not directly to the external host.

📘 The client sends traffic to the router (default gateway), which then forwards it to the Internet.

📸 Insert screenshot of external traffic routing
✅ Summary of Concepts Covered
Concept	Demonstrated
MAC ↔ IP mapping	✅ via ARP
DNS Resolution	✅ with UDP
TCP Handshake	✅ SYN, SYN-ACK, ACK
HTTP Communication	✅ in plain text
LAN vs Internet Routing	✅ router as gateway
Protocol Stacking	✅ Ethernet → IP → TCP/UDP → HTTP/DNS
🧰 Tools Used

    Wireshark

    Windows Virtual Machine (LAPTOP VM)

    Sample packet capture file (packetcap.pcap)

