# Networking

Networking CLI commands
Here’s an extensive list of advanced and detailed networking CLI commands, categorized by the systems they are used on: Unix-like systems (including Linux, macOS, and BSD), Windows, and others. 

# Advanced Networking CLI Commands

## **Unix-like Systems (Linux, macOS, BSD)**

### **Basic Network Configuration**

- **Display network interfaces:**
  ```bash
  ifconfig
  ```
  *(Linux, macOS, BSD)*

- **Display network interfaces (modern replacement):**
  ```bash
  ip a
  ```
  *(Linux)*

- **Display routing table:**
  ```bash
  netstat -r
  ```
  *(Linux, macOS, BSD)*

- **Display routing table (modern replacement):**
  ```bash
  ip route
  ```
  *(Linux)*

- **Display ARP table:**
  ```bash
  arp -a
  ```
  *(Linux, macOS, BSD)*

### **Advanced Network Configuration**

- **Assign multiple IP addresses to an interface:**
  ```bash
  ip addr add IP_ADDRESS1/NETMASK dev INTERFACE
  ip addr add IP_ADDRESS2/NETMASK dev INTERFACE
  ```
  *(Linux)*

- **Configure interface with VLAN tagging:**
  ```bash
  ip link add link INTERFACE name INTERFACE.VLAN_ID type vlan id VLAN_ID
  ip addr add IP_ADDRESS/NETMASK dev INTERFACE.VLAN_ID
  ```
  *(Linux)*

- **Set up static routes with metrics:**
  ```bash
  ip route add DESTINATION_NETWORK/MASK via GATEWAY_IP dev INTERFACE metric METRIC
  ```
  *(Linux)*

- **Configure IP aliases for dynamic IPs:**
  ```bash
  ip addr add IP_ADDRESS/NETMASK broadcast BROADCAST dev INTERFACE
  ```
  *(Linux)*

- **Add a custom DNS resolver:**
  ```bash
  echo "nameserver DNS_IP" | sudo tee -a /etc/resolv.conf
  ```
  *(Linux, macOS)*

### **Advanced Network Diagnostics**

- **Perform a traceroute with TCP packets:**
  ```bash
  tcptraceroute HOSTNAME PORT
  ```
  *(Linux)*

- **Check for packet loss and jitter:**
  ```bash
  mtr HOSTNAME
  ```
  *(Linux, macOS)*

- **Perform a bandwidth test:**
  ```bash
  iperf3 -c SERVER_IP -t TIME
  ```
  *(Linux, macOS)*

- **Display detailed network statistics with extended info:**
  ```bash
  netstat -st
  ```
  *(Linux, macOS, BSD)*

- **Monitor network traffic in real-time with filters:**
  ```bash
  tcpdump -i INTERFACE -nn -vvv -s0 'tcp port PORT'
  ```
  *(Linux, macOS)*

- **Analyze network traffic and create statistics report:**
  ```bash
  wireshark
  ```
  *(Linux, macOS)*

### **Advanced Network Security**

- **Configure a firewall with complex rules using `iptables`:**
  ```bash
  iptables -A INPUT -p tcp --dport PORT -m state --state NEW,ESTABLISHED -j ACCEPT
  iptables -A INPUT -p udp --dport PORT -m state --state NEW,ESTABLISHED -j ACCEPT
  iptables -A INPUT -j DROP
  ```
  *(Linux)*

- **Set up IP filtering rules with `nftables`:**
  ```bash
  nft add table ip filter
  nft add chain ip filter input { type filter hook input priority 0; }
  nft add rule ip filter input ip saddr SOURCE_IP tcp dport PORT accept
  nft add rule ip filter input drop
  ```
  *(Linux)*

- **Secure an SSH connection with key-based authentication and specific options:**
  ```bash
  ssh -i PRIVATE_KEY_FILE -o "StrictHostKeyChecking=yes" -o "UserKnownHostsFile=/path/to/known_hosts" USER@HOSTNAME
  ```
  *(Linux, macOS, BSD)*

- **Configure and manage network security policies with `firewalld`:**
  ```bash
  firewall-cmd --zone=public --add-port=PORT/tcp --permanent
  firewall-cmd --reload
  ```
  *(Linux)*

- **Implement IPsec VPN tunnels with strongSwan:**
  ```bash
  ipsec up CONNECTION_NAME
  ipsec down CONNECTION_NAME
  ```
  *(Linux)*

### **Advanced Network Monitoring and Management**

- **Set up network traffic shaping with `tc`:**
  ```bash
  tc qdisc add dev INTERFACE root handle 1: htb default 12
  tc class add dev INTERFACE parent 1: classid 1:1 htb rate 1mbit
  tc qdisc add dev INTERFACE parent 1:1 handle 10: pfifo limit 100
  ```
  *(Linux)*

- **Monitor bandwidth usage per interface:**
  ```bash
  vnstat -i INTERFACE
  ```
  *(Linux)*

- **Set up network interface bonding for redundancy:**
  ```bash
  ip link add bond0 type bond
  ip link set bond0 up
  ip link set INTERFACE1 master bond0
  ip link set INTERFACE2 master bond0
  ```
  *(Linux)*

- **Perform network diagnostics with `nmap`:**
  ```bash
  nmap -sS -p PORTS HOSTNAME
  nmap -O HOSTNAME
  ```
  *(Linux, macOS)*

- **Analyze network paths and identify latency issues with `mtr`:**
  ```bash
  mtr -r -c 100 HOSTNAME
  ```
  *(Linux, macOS)*

### **Advanced Network Configuration and Troubleshooting**

- **Configure advanced routing with `ip route`:**
  ```bash
  ip route add DESTINATION_NETWORK/MASK via GATEWAY_IP dev INTERFACE table 100
  ip route add default via GATEWAY_IP table 100
  ```
  *(Linux)*

- **Use `traceroute` with different protocols and settings:**
  ```bash
  traceroute -T HOSTNAME
  traceroute -U HOSTNAME
  ```
  *(Linux, macOS)*

- **Display detailed interface statistics and errors:**
  ```bash
  ethtool -S INTERFACE
  ```
  *(Linux)*

- **Check for packet drops and errors on interfaces:**
  ```bash
  ifstat INTERFACE
  ```
  *(Linux)*

- **Monitor network traffic with detailed `tcpdump` filters:**
  ```bash
  tcpdump -i INTERFACE -nn 'tcp[tcpflags] & (tcp-syn|tcp-ack) != 0'
  ```
  *(Linux, macOS)*

### **Advanced Network Security and Penetration Testing**

- **Perform network scans and vulnerability assessments:**
  ```bash
  nmap -A HOSTNAME
  nmap --script vuln HOSTNAME
  ```
  *(Linux, macOS)*

- **Use `netcat` for network exploration and diagnostics:**
  ```bash
  nc -l -p PORT
  nc -v HOSTNAME PORT
  ```
  *(Linux, macOS)*

- **Configure and monitor SNMP with `snmpwalk`:**
  ```bash
  snmpwalk -v 2c -c COMMUNITY_STRING HOSTNAME
  ```
  *(Linux, macOS)*

- **Use `tcpflow` to capture and analyze network traffic flows:**
  ```bash
  tcpflow -i INTERFACE
  ```
  *(Linux, macOS)*

## **Windows**

### **Basic Network Configuration**

- **Display network interfaces:**
  ```cmd
  ipconfig /all
  ```

- **Display ARP table:**
  ```cmd
  arp -a
  ```

- **Display routing table:**
  ```cmd
  route print
  ```

### **Advanced Network Configuration**

- **Add a static route:**
  ```cmd
  route add DESTINATION_NETWORK MASK NETMASK GATEWAY_IP
  ```

- **Delete a static route:**
  ```cmd
  route delete DESTINATION_NETWORK
  ```

- **Configure DNS settings:**
  ```cmd
  netsh interface ip set dns name="INTERFACE_NAME" static DNS_IP
  ```

### **Advanced Network Diagnostics**

- **Perform a traceroute:**
  ```cmd
  tracert HOSTNAME
  ```

- **Ping with a specific packet size:**
  ```cmd
  ping HOSTNAME -l SIZE
  ```

- **Check network performance:**
  ```cmd
  pathping HOSTNAME
  ```

### **Advanced Network Security**

- **Configure Windows Firewall rules:**
  ```cmd
  netsh advfirewall firewall add rule name="RuleName" protocol=TCP dir=in localport=PORT action=allow
  ```

- **List all active connections and listening ports:**
  ```cmd
  netstat -ano
  ```

- **Kill a process by PID:**
  ```cmd
  taskkill /PID PID_NUMBER /F
  ```

### **Advanced Network Monitoring and Management**

- **View network statistics:**
  ```cmd
  netsh interface ipv4 show stats
  ```

- **Monitor network usage:**
  ```cmd
  perfmon
  ```

- **Configure VPN settings:**
  ```cmd
  rasdial CONNECTION
  ```

- **Configure VPN settings:**
  ```cmd
  rasdial CONNECTION_NAME USERNAME PASSWORD
  ```

- **Check current network connections and their state:**
  ```cmd
  netstat -b
  ```

- **List all network adapters and their configuration:**
  ```cmd
  getmac /v /fo list
  ```

- **Display detailed TCP connections and listening ports:**
  ```cmd
  netstat -anob
  ```

- **Monitor network usage over time with Performance Monitor:**
  ```cmd
  perfmon /report
  ```

- **Display IP configuration for all adapters:**
  ```cmd
  ipconfig /all
  ```

- **Release and renew DHCP leases:**
  ```cmd
  ipconfig /release
  ipconfig /renew
  ```

### **Advanced Network Security and Penetration Testing**

- **Perform network scan and discover services using `nmap`:**
  ```cmd
  nmap -A -T4 HOSTNAME
  ```

- **Use `netcat` for port scanning and connections:**
  ```cmd
  nc -zv HOSTNAME PORT
  ```

- **Test network ports and connectivity with `telnet`:**
  ```cmd
  telnet HOSTNAME PORT
  ```

- **Perform vulnerability scans with `nmap` scripts:**
  ```cmd
  nmap --script vuln HOSTNAME
  ```

## **Network Management on Specific Systems**

### **AWS CLI**

- **List all EC2 instances:**
  ```bash
  aws ec2 describe-instances
  ```

- **Describe a specific instance:**
  ```bash
  aws ec2 describe-instances --instance-ids INSTANCE_ID
  ```

- **Describe security groups:**
  ```bash
  aws ec2 describe-security-groups
  ```

- **List all VPCs:**
  ```bash
  aws ec2 describe-vpcs
  ```

- **Get VPC peering connections:**
  ```bash
  aws ec2 describe-vpc-peering-connections
  ```

- **View CloudWatch metrics:**
  ```bash
  aws cloudwatch list-metrics
  ```

- **Monitor RDS instances:**
  ```bash
  aws rds describe-db-instances
  ```

### **Azure CLI**

- **List all virtual machines:**
  ```bash
  az vm list --output table
  ```

- **Show details of a specific VM:**
  ```bash
  az vm show --name VM_NAME --resource-group RESOURCE_GROUP
  ```

- **List all network interfaces:**
  ```bash
  az network nic list --output table
  ```

- **Show details of a specific network interface:**
  ```bash
  az network nic show --name NIC_NAME --resource-group RESOURCE_GROUP
  ```

- **List all virtual networks:**
  ```bash
  az network vnet list --output table
  ```

- **Show details of a specific virtual network:**
  ```bash
  az network vnet show --name VNET_NAME --resource-group RESOURCE_GROUP
  ```

- **View network security groups:**
  ```bash
  az network nsg list --output table
  ```

### **GCP CLI**

- **List all Compute Engine instances:**
  ```bash
  gcloud compute instances list
  ```

- **Describe a specific Compute Engine instance:**
  ```bash
  gcloud compute instances describe INSTANCE_NAME
  ```

- **List all network interfaces:**
  ```bash
  gcloud compute network-interfaces list
  ```

- **Describe a specific network interface:**
  ```bash
  gcloud compute network-interfaces describe INTERFACE_NAME
  ```

- **List all VPC networks:**
  ```bash
  gcloud compute networks list
  ```

- **Describe a specific VPC network:**
  ```bash
  gcloud compute networks describe NETWORK_NAME
  ```

- **View firewall rules:**
  ```bash
  gcloud compute firewall-rules list
  ```

## **Android Terminal Commands**

- **Display network interfaces:**
  ```bash
  ifconfig
  ```

- **Show detailed IP address information:**
  ```bash
  ip -f inet addr
  ```

- **Test network connectivity with `ping`:**
  ```bash
  ping HOSTNAME
  ```

- **Check for open ports with `netcat`:**
  ```bash
  nc -zv HOSTNAME PORT
  ```

- **Display routing table:**
  ```bash
  route -n
  ```

- **Perform a traceroute:**
  ```bash
  traceroute HOSTNAME
  ```

- **View network statistics:**
  ```bash
  netstat -s
  ```

## **macOS Specific Commands**

- **List all network services:**
  ```bash
  networksetup -listallnetworkservices
  ```

- **Get details for a specific network service:**
  ```bash
  networksetup -getinfo SERVICE_NAME
  ```

- **Change DNS settings:**
  ```bash
  networksetup -setdnsservers SERVICE_NAME DNS_IP
  ```

- **List all wireless networks:**
  ```bash
  /System/Library/PrivateFrameworks/Apple80211.framework/Versions/Current/Resources/airport -s
  ```

- **Connect to a wireless network:**
  ```bash
  networksetup -setairportnetwork INTERFACE SSID PASSWORD
  ```

## **AIX CLI Commands**

- **List all network interfaces:**
  ```bash
  ifconfig -a
  ```

- **Show detailed interface configuration:**
  ```bash
  netstat -in
  ```

- **Display routing table:**
  ```bash
  netstat -rn
  ```

- **Check ARP cache:**
  ```bash
  arp -a
  ```

- **Set a static route:**
  ```bash
  route add net DESTINATION_NETWORK netmask NETMASK gateway GATEWAY_IP
  ```

- **Configure network interface:**
  ```bash
  ifconfig INTERFACE IP_ADDRESS netmask NETMASK
  ```

## **FreeBSD CLI Commands**

- **Display network interfaces:**
  ```bash
  ifconfig
  ```

- **Show detailed network configuration:**
  ```bash
  netstat -r
  ```

- **Display ARP table:**
  ```bash
  arp -a
  ```

- **Add a static route:**
  ```bash
  route add -net DESTINATION_NETWORK netmask NETMASK gateway GATEWAY_IP
  ```

- **Configure network interface:**
  ```bash
  ifconfig INTERFACE inet IP_ADDRESS netmask NETMASK
  ```

## **OpenBSD CLI Commands**

- **List network interfaces:**
  ```bash
  ifconfig
  ```

- **Display routing table:**
  ```bash
  netstat -rn
  ```

- **Show ARP table:**
  ```bash
  arp -a
  ```

- **Add a static route:**
  ```bash
  route add DESTINATION_NETWORK/NETMASK GATEWAY_IP
  ```

- **Configure network interface:**
  ```bash
  ifconfig INTERFACE inet IP_ADDRESS netmask NETMASK
  ```

This comprehensive list covers advanced networking commands across various systems, providing extensive options for network configuration, diagnostics, security, and management.
