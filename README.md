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
            <p>- Next we will configure and connect the LAN facing interface G0/0.</p>
                <img width="872" height="650" alt="Screenshot 2026-02-08 142613" src="https://github.com/user-attachments/assets/7b7dbc3f-e745-47f7-9efc-b3b2187799dd" />
            <p><em>- Both MGMT and DATA VLAN interfaces were configured here as well.</em></p>
            <p>- Next, using a straight-through cable, we'll connect the LAN interface G0/0 to a trunk port on HQ-CORE-SW2 (i.e. FastEthernet0/20) and verify the port comes online.</p>
                <img width="1175" height="1033" alt="Screenshot 2026-02-08 143240" src="https://github.com/user-attachments/assets/ccbd187c-d7c2-4623-9521-4f684993ebca" />
                <img width="874" height="276" alt="Screenshot 2026-02-08 144551" src="https://github.com/user-attachments/assets/4acf6e07-0d13-4d12-a860-b2090fd1e128" />
        <h3>Step 5: Configure and Connect Private WAN Interface G0/1</h3>
            <p>- Next we will configure and connect the private WAN interface.</p>
                <img width="874" height="403" alt="Screenshot 2026-02-08 144842" src="https://github.com/user-attachments/assets/aefbee72-12bc-4b84-9ac0-a6b825611801" />
            <p><em>- Using the "speed 100" command, we effectively set our speed to 100Mbps matching the ISP router interface. Command "bandwidth 50000" sets the bandwidth reference in kilobits (=50Mbps). We also want to ensure no cdp messages are sent to the provider network, so we execute "no cdp enable" command.</em></p>
            <p>- Next, using an ethernet cross-over cable, we'll connect the private WAN interface G0/1 to the PRIVATE WAN CLOUD router interface FastEthernet0/0.</p>
                <img width="1183" height="973" alt="Screenshot 2026-02-08 145302" src="https://github.com/user-attachments/assets/fcffc9ed-34cd-4547-801e-b1d8086b47c5" />
                <img width="868" height="433" alt="Screenshot 2026-02-08 145438" src="https://github.com/user-attachments/assets/2d17e92b-7753-44a4-8b2d-1650654cec1f" />
            <p><em>- As you can see, we are able to successfully ping the private WAN cloud router.</em></p>       
        <h3>Step 6: Configure Private WAN Border Gateway Protocol (BGP) Peering</h3>
            <p>- Next we will configure the BGP router ID and set up peering with the provider router.</p>
                <img width="872" height="307" alt="Screenshot 2026-02-08 124931" src="https://github.com/user-attachments/assets/87eb1138-ead1-4908-ab09-9cb65c99f21e" />
            <p><em>- Command "router bgp 65123" enters the BGP configuration for autonomous system #65123. The "bgp router-id" command will force the router to use g0/1 IP as the BGP ID. The command "neighbor 192.168.250.1 remote-as 65535" effectively configures BGP peering.</em></p>
            <p>- Next we will configure the following network statements to advertise across the Private WAN.</p>
                <img width="870" height="462" alt="Screenshot 2026-02-08 151942" src="https://github.com/user-attachments/assets/f65b0a0f-dd72-4117-baf6-c436f371babb" />
            <p>- Break down of all network statements:</p>
            <p><em>- network 192.168.110.0 mask 255.255.255.0 <b>(Advertises HQ MGMT)</b></em></p>
            <p><em>- network 192.168.10.0 mask 255.255.255.0 <b>(Advertises HQ DATA)</b></em></p>
            <p><em>- network 10.10.10.0 mask 255.255.255.0 <b>(Advertises HQ VOICE)</b></em></p>
            <p><em>- network 192.168.130.0 255.255.255.0 <b>(Advertises B2 MGMT)</b></em></p>
            <p><em>- network 192.168.30.0 mask 255.255.255.0 <b>(Advertises B2 DATA)</b></em></p>
            <p><em>- network 10.10.30.0 mask 255.255.255.0 <b>(Advertises B2 VOICE)</b></em></p>
            <p><em>- Our BGP verification config:</em></p>
                <img width="2559" height="1599" alt="Screenshot 2026-02-08 152526" src="https://github.com/user-attachments/assets/0cb578e0-d2ea-48e1-913e-bc8fbc011de0" />
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
            <p>- Next, we will set up VPN policy and crypto map for IPSec site-to-site VPN to Branch 2.</p>
                <p>- A: We will start by configuring ISAMKP policy.</p>
                <img width="870" height="432" alt="Screenshot 2026-02-08 130035" src="https://github.com/user-attachments/assets/8b792b4a-e833-4140-8de3-1956d1698130" />
            <p><em>- We use the command "crypto isakmp policy 10" to tell the router to create a new, prioritized set of security rules (a "policy") for negotiating a VPN connection. "crypto isakmp" tells the router to manage the security of a VPN connection, "policy" starts a configuration block to define how the routers will identify each other and secure their initial conversation, and "10" is the priority number.</em></p>
            <p><em>- "encr aes" is telling the router to use the AES algorithm to encrypt data.</em></p>
            <p><em>- "authentication pre-share" is telling the router to use a "secret handshake" to verify who it is talking to. It ensures that only devices knowing the exact same "shared secret" (password) can establish a secure connection, and by entering the command "group 2", we are telling the devices to which mathematical "strength" to use when creating their encryption keys. Group 2 is "1024-bit" strenght. Not the strongest, but for this lap purpose we will be using this.</em></p>
                <p>- B: Next, we will configure IPSec SA lifetime and transform set.</p>
                <img width="868" height="272" alt="Screenshot 2026-02-08 155001" src="https://github.com/user-attachments/assets/285847a2-04fc-4473-9244-66de40762f1d" />
            <p><em>- The command "crypto ipsec security-association lifetime seconds 86400" will configure the router to set the Phase 2 IPsec Security Association (SA) lifetime to 86,400 seconds, which is 24 hours. This means the IPsec tunnel will automatically re-key (refresh its encryption keys) every 24 hours to enhance security.</em></p>
            <p><em>- The command "crypto ipsec transform-set BRANCH-2 esp-aes esp-sha-hmac" creates a security policy named "BRANCH-2" that encrypts traffic using AES and verifies data integrity using SHA-HMAC [1, 3]. "crypto ipsec transform-set" essentially defines a transform set, which is a named combination of security protocols and algorithms that protect data in an IPsec VPN tunnel. "BRANCH-2" is the name of this specific transform set. "esp-aes" specifies that Encapsulating Security Payload (ESP) will be used for encryption to ensure data confidentiality using the AES (Advanced Encryption Standard) algorithm. "esp-sha-hmac" specifies that ESP will be used for authentication to ensure data integrity using the SHA (Secure Hash Algorithm) HMAC.</em></p>
                <p>- C: Next, we will create an Access Control List that matches any traffic going to Branch 2 networks.</p>
                <img width="869" height="339" alt="Screenshot 2026-02-08 160339" src="https://github.com/user-attachments/assets/dcfd8194-f405-4856-99e1-05ab3f0924a4" />
                <p>- D: Next, we will create the crypto map that will be applied to the VPN-ONLY Internet ineterface.</p>


            

        
        
        
        
        
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


















            












 





