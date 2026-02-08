<p align="center">
<img width="699" height="234" alt="Screenshot 2026-02-08 134928" src="https://github.com/user-attachments/assets/f1c44480-4954-4a84-8a21-6ebd24784d28" />
</p>
<h1><u>Milestone 5: HQ WAN Router</u></h1>
    <p>Fourth phase, we will install 1 CISCO2911/K9 with ipbasek9 and securityk9 licensing. This router will act as the gateway for all WAN services that connect Headquarters to Branch 1 and Branch 2. This includes a Private WAN connection to Branch 1 via the WAN service provider using BGP peering. In addition, a second internet service will be connected to this router solely for the purpose of creating an IPSec Site to Site (L2L) Virtual Private Network connection.</p>
    <h2><strong><u>Configuration Steps</u></strong></h2>
    <p><b>Step 1: Rack, Mount, and Power On The Cisco 2911 Router</b></p>
    <p><b>Step 2: Basic Switch Configurations (Hostname, NTP, Domain-Name, SSH, Etc)</b></p>
    <p><b>Step 3: Install Securityk9 License</b></p>
    <p><b>Step 4: Configure and Connect HQ LAN Interface G0/0</b></p>
        <p>- A. MGMT Interface VLAN 100</p>
        <p>- B. DATA Interface VLAN 192</p>
    <p><b>Step 5: Configure and Connect Private WAN Interface G0/1</b></p>
        <p>- A. IP Address</p>
        <p>- B. Disable CDP</p>
    <p><b>Step 6: Configure Private WAN Border Gateway Protocol (BGP) Peering</b></p>
        <p>- A. BGP ASN 65123</p>
            <p>- i. Router ID</p>
            <p>- ii. Neighbor</p>
            <p>- iii. Networks</p>
    <p><b>Step 7: Configure Private WAN Voice Quality of Service</b></p>
        <p>- A. VOIP Control and RTP Access-Lists</p> 
        <p>- B. VOIP Control and RTP Class-Maps</p>
        <p>- C. Policy-Map</p>
        <p>- D. Apply Policy-Map to Private WAN Interface G0/1</p>
    <p><b>Step 8: Configure IPSec/Isakmp VPN Policy and Cryptography</b></p>
        <p>- A. Branch 2 Traffic Access List</p>
        <p>- B. Isakmp Policy</p>
        <p>- C. Isakmp Key</p>
        <p>- D. Ipsec SA Lifetime and Transform-Set</p>
        <p>- E. Ipsec-Isakmp Crypto Map</p>
    <p><b>Step 9: Configure Access-List to Allow Only VPN Traffic From Branch 2</b></p>
    <p><b>Step 10: Configure and connect Internet interface G0/2</b></p>
        <p>- A. IP Address</p>
        <p>- B. Disable CDP</p>
        <p>- C. Apply VPN Only Access-List Inbound</p>
        <p>- D. Apply VPN Crypto Map for Branch 2 VPN</p>
    <p><b>Step 11: Configure Static Routes</b></p>
        <p>- A. Default Route Pointing to HQ Internet Router DATA Interface IP Address</p>
        <p>- B. Route to HQ Voice Network Pointing to HQ Core Switch Voice Network HSRP Address</p>
        <p>- C. Route to Branch 2 Public IP Address via Internet Gateway Public IP</p>
        <p>- D. Routes to Branch 2 Private Networks via Branch 2 Public IP</p>
    <h2><strong><u>Implementation</u></strong></h2>
        <h3>Step 1: Rack, Mount, and Power On The Cisco 2911 Router</h3>
            <p>- First, we'll Add a 2901 Router to the topology by dragging and dropping it into the Headquarters section of the lab. We'll place the 2911 Router in the right side area of HQ and label it as “HQ-WAN-RTR”.</p>
                <img width="1178" height="1001" alt="Screenshot 2026-02-08 141321" src="https://github.com/user-attachments/assets/c6363b3b-3940-4fda-a02f-ffe1e280f30f" />
        <h3>Step 2: Basic Switch Configurations (Hostname, NTP, Domain-Name, SSH, Etc)</h3>
            <p>- In this step, we did basic configuration for both of the switches including changing their hostnames, setting their time zones, enabling SSH, setting domain names, adding securiting to console and vty lines for SSH, and creating user profiles with a password the devices</p>
                <img width="871" height="980" alt="Screenshot 2026-02-08 141447" src="https://github.com/user-attachments/assets/e1ef04ae-0ddc-40c7-9f86-1b93f42bd98c" />
        <h3>Step 3: Install Securityk9 License</h3>
            <p>- Next we will activate the security licensing 60 day grace period on the 2901 Router. We do this to unlock advanced security features, primarily for setting up VPNs (IPsec), secure communication, and enhanced firewall functionality.</p>
                <img width="2559" height="824" alt="Screenshot 2026-02-08 141925" src="https://github.com/user-attachments/assets/6e9b69d6-8d99-4f79-9fc6-761765e184b4" />
                <img width="2559" height="1267" alt="Screenshot 2026-02-08 142031" src="https://github.com/user-attachments/assets/50124ebc-70df-4843-98bc-678e2e20c2f1" />
                <img width="2559" height="1597" alt="Screenshot 2026-02-08 142112" src="https://github.com/user-attachments/assets/698d3e75-98f8-48ed-932f-6bdf07910127" />
            <p><em>- After reloading the router, you can see that the securityk9 licensing software was installed successfully.</em></p>
        <h3>Step 4: Configure and Connect HQ LAN Interface G0/0</h3>
            <p>- Next we will configure an access control list that will be applied to protect the internet facing interface.</p>
                <img width="866" height="261" alt="Screenshot 2026-02-07 185411" src="https://github.com/user-attachments/assets/a4186eb3-0afb-42f2-b84a-a27f474a7b4e" />
        <h3>Step 5: Configure and Connect Private WAN Interface G0/1</h3>
            <p>- Next we will configure an access control list for translating all data and management networks, and also the HQ guest network.</p>
                <img width="868" height="272" alt="Screenshot 2026-02-07 185904" src="https://github.com/user-attachments/assets/ea041f79-6b51-4cc8-967f-cd8b1b539e63" />
            <p>- Next we will configure NAT for "INSIDE" ACL with Overload to interface G0/1.</p>
                <img width="872" height="179" alt="Screenshot 2026-02-07 190203" src="https://github.com/user-attachments/assets/ef5afac0-4946-44e9-a52e-97e71c00a86e" />
            <p><em>- We use the overload command to allow devices in our private internal network to access the internet simultaneously using a single public IP address assigned to our router's g0/1 OUTSIDE interface.</em></p>
        <h3>Step 6: Configure Private WAN Border Gateway Protocol (BGP) Peering</h3>
            <p>- Next we will configure IOS firewall inspection rules for allowed internet traffic.</p>
                <img width="872" height="307" alt="Screenshot 2026-02-08 124931" src="https://github.com/user-attachments/assets/87eb1138-ead1-4908-ab09-9cb65c99f21e" />
            <p><em>- We do this to enable stateful packect inspection allowing authorized outgoing traffic while automatically opening temporary, secure return paths for legitimate replies. This prevents unauthorized incoming traffic (hackers) while allowing internal users to access internet services as expected. Unlike standard Access Control Lists (ACLs) that require manual rules for both directions, the command "inspect" remembers outgoing requests and allows only the matching return packets back in. It verifies that incoming traffic is actually a reply to a request made from inside, rather than unsolicited malicious traffic. It understands and monitors application-layer details for TCP, UDP, ICMP, and HTTP, ensuring the session follows correct protocol behavior. It dynamically creates temporary openings in the firewall for allowed sessions, closing them immediately when the conversation ends.</em></p>
        <h3>Step 7: Configure Private WAN Voice Quality of Service</h3>
            <p>- Next we will configure the inside LAN interface G0/0 as a trunk for the Management and Data Networks, and connect the interface to the Core switched infrastructure.</p>
                <p>- A: Configure the inside LAN interface.</p>
                <img width="871" height="709" alt="Screenshot 2026-02-07 181525" src="https://github.com/user-attachments/assets/77acffef-9166-4de3-94f9-7fbab0801481" />
            <p><em>- As you can see, we changed the speed of the g0/0 interface to match the interface of the core switch for predictable performance. We also created sub interfaces on the port for both the data vlan and the management vlan for better traffic management.</em></p>
                <p>- B: Connect router interface G0/0 to a switchport using a straight-through cable on HQ-CORE-SW2 that is already configured as a trunk (ie. FastEthernet0/19).</p>
                <img width="747" height="887" alt="Screenshot 2026-02-07 182345" src="https://github.com/user-attachments/assets/f0944b22-198a-409e-a64f-ab28e90992ec" />
                <img width="869" height="709" alt="Screenshot 2026-02-07 182703" src="https://github.com/user-attachments/assets/ca12f94f-bde6-4f7c-847a-2059ac43cfed" />
            <p><em>- Successful pings, showing we are able to establish connectivity to both the MGMT and DATA networks.</em></p>
        <h3>Step 8: Configure IPSec/Isakmp VPN Policy and Cryptography</h3>
            <p>- Next, we will configure the internet facing interface.</p>
                <img width="870" height="432" alt="Screenshot 2026-02-08 130035" src="https://github.com/user-attachments/assets/8b792b4a-e833-4140-8de3-1956d1698130" />
            <p><em>- As you can see, we changed the speed of the g0/1 interface to match the speed interface with the ISP router. We also used the command "no cdp enable" to prevent sharing private network details with unauthorized parties. This will stop the router from broadcasting information such as IOS version, device type, and IP addresses to the Internet Service Provider (ISP) or attackers. We use the command "ip access-group PROTECT in" to apply the PROTECT ACL inbound that we created earlier. "inspect ip FIREWALL out applies the firewall inspection rules outbound. "ip nat outside" turns on network address translation for outbound traffic. And lasty we do a "no shut" on the interface to turn the interface in fact on.</em></p>
            <p>- Lastly, using an ethernet cross-over cable, we'll connect HQ-INET-RTR interface G0/1 to INTERNET CLOUD Service Provider router interface Fa0/0.</p>
                <img width="2151" height="1033" alt="Screenshot 2026-02-08 131158" src="https://github.com/user-attachments/assets/52e474be-eaea-46ae-90f7-276fe4f5276d" />
                <img width="870" height="418" alt="Screenshot 2026-02-08 131410" src="https://github.com/user-attachments/assets/4b1d01cb-9835-4531-a43b-7405b28fc511" />
            <p><em>- As you can see, we are able to successfully ping the internet cloud service provider router. This is possible due to the interfaces being directly connected, and ICMP traffic is being allowed.</em></p>
        <h3>Step 9: Configure Access-List to Allow Only VPN Traffic From Branch 2</h3>
            <p>- For this last step, we will add static routes that tell the router how to get to the guest network and our future branches.</p>
                <p>- A: First we will configure the default route and test IP connectivity to the Google Server 8.8.8.8.</p>
                <img width="872" height="452" alt="Screenshot 2026-02-08 132022" src="https://github.com/user-attachments/assets/60ced046-a881-4512-b202-bc8339eba2d5" />
            <p><em>- The router now has a Default Route for unknown destinations (0.0.0.0 0.0.0.0).</em></p>
                <p>- B: Now last, we will add all static routes.</p>
                <img width="868" height="1068" alt="Screenshot 2026-02-08 132833" src="https://github.com/user-attachments/assets/d78b3025-2604-4972-9039-a4a9a79b836f" />
            <p>- Break down of all  our current static routes.</p>
            <p><em>- ip route 172.16.10.0 255.255.255.0 192.168.10.100 <b>(HQ Guest to HQ-Core-SW)</b></em></p>
            <p><em>- ip route 10.10.10.0 255.255.255.0 192.168.10.100 <b>(HQ Voice to HQ-Core-SW)</b></em></p>
            <p><em>- ip route 192.168.120.0 255.255.255.0 192.168.10.254 <b>(Branch 1 to HQ-WAN-RTR)</b></em></p>
            <p><em>- ip route 192.168.20.0 255.255.255.0 192.168.10.254 <b>(Branch 1 to HQ-WAN-RTR)</b></em></p>
            <p><em>- ip route 10.10.20.0 255.255.255.0 192.168.10.254 <b>(Branch 1 to HQ-WAN-RTR)</b></em></p>
            <p><em>- ip route 192.168.130.0 255.255.255.0 192.168.10.254 <b>(Branch 2 to HQ-WAN-RTR)</b></em></p>
            <p><em>- ip route 192.168.30.0 255.255.255.0 192.168.10.254 <b>(Branch 2 to HQ-WAN-RTR)</b></em></p>
            <p><em>- ip route 10.10.30.0 255.255.255.0 192.168.10.254 <b>(Branch 2 to HQ-WAN-RTR)</b></em></p>
        <h3>Step 10: Configure and connect Internet interface G0/2</h3>
        <h3>Step 11: Configure Static Routes</h3>


















            












 





