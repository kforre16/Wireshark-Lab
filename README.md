# Wireshark-Lab

## Objective

Get practical experience with Wireshark and master key techniques for capturing and analyzing network traffic to detect security threats and enhance network performance.

### Skills Learned

- Analyzing network traffic with Wireshark
- Detecting and investigating Malware Traffic

### Tools Used

- Wireshark
- Kali Linux
- Sample PCAP files

## Palo Alto Networks Wireshark Tutorials
I followed along a series of tutorials written by Brad Duncan that provide tips and tricks to help security professionals more effectively use Wireshark.

- <a href="https://unit42.paloaltonetworks.com/unit42-customizing-wireshark-changing-column-display/">Wireshark Tutorial: Changing Your Column Display</a>
- <a href="https://unit42.paloaltonetworks.com/using-wireshark-display-filter-expressions/">Wireshark Tutorial: Display Filter Expressions</a>
- <a href="https://unit42.paloaltonetworks.com/using-wireshark-identifying-hosts-and-users/">Wireshark Tutorial: Identifying Hosts and Users</a>
- <a href="https://unit42.paloaltonetworks.com/using-wireshark-exporting-objects-from-a-pcap/">Wireshark Tutorial: Exporting Objects from a Pcap</a>
- <a href="https://unit42.paloaltonetworks.com/wireshark-tutorial-decrypting-https-traffic/">Wireshark Tutorial: Decrypting HTTPS traffic</a>

## Traffic Analysis Exercise: Download from fake software site
After completing the Wireshark tutorials, I can now apply the tips I learned to complete the exercise found on <a href="https://malware-traffic-analysis.net/2025/01/22/index.html">Malware-Traffic-Analysis.net</a> 

![image](https://github.com/user-attachments/assets/5f298fe9-ea83-4866-8282-b3cfcd33e7f3)

### Background

You work as an analyst at a Security Operation Center (SOC). Someone contacts your team to report a coworker has downloaded a suspicious file after searching for Google Authenticator. The caller provides some information similar to social media posts at:

-    https://www.linkedin.com/posts/unit42_2025-01-22-wednesday-a-malicious-ad-led-activity-7288213662329192450-ky3V/
-    https://x.com/Unit42_Intel/status/1882448037030584611

Based on the caller's initial information, you confirm there was an infection.  You retrieve a packet capture (pcap) of the associated traffic.  Reviewing the traffic, you find several indicators matching details from a Github page referenced in the above social media posts.  After confirming an infection happened, you begin writing an incident report.

### LAN SEGMENT DETAILS FROM THE PCAP

-    LAN segment range:  10.1.17[.]0/24   (10.1.17[.]0 through 10.1.17[.]255)
-    Domain:  bluemoontuesday[.]com
-    Active Directory (AD) domain controller:  10.1.17[.]2 - WIN-GSH54QLW48D
-    AD environment name:  BLUEMOONTUESDAY
-    LAN segment gateway:  10.1.17[.]1
-    LAN segment broadcast address:  10.1.17[.]255

### TASK
For this exercise, answer the following questions for your incident report:

-    What is the IP address of the infected Windows client?
-    What is the mac address of the infected Windows client?
-    What is the host name of the infected Windows client?
-    What is the user account name from the infected Windows client?
-    What is the likely domain name for the fake Google Authenticator page?
-    What are the IP addresses used for C2 servers for this infection?

### ANSWERS
Using my basic web filter, I find the IP address of the infected Windows client with the correlated MAC address.

![MalwareTrafficAnalysisAnswers1](https://github.com/user-attachments/assets/6f9b763c-c9ad-4ef8-baef-d9b01793fc8a)
- IP Address: 10.1.7.215
- MAC Address: 00:d0:b7:26:4a:47

Using the DHCP filter, I find the packet of the DHCP Request. When I go into the frame details and drill down until I find the hostname of the infected Windows client.

![MalwareTrafficAnalysisAnswers2](https://github.com/user-attachments/assets/e7ae8a84-a702-454d-9114-aa86bd935201)

- Host Name: DESKTOP-L8C5GSJ

Using the kerberos.CNameString filter, I find the account name of the infected Windows client.

![image](https://github.com/user-attachments/assets/69807833-d0dd-4b36-b8f9-98af0e767bd6)

- Account Name: shutchenson

Using my basic web filter again, I find the domain name of the fake Google Authenticator website with the possible malware download page.

![MalwareTrafficAnalysisAnswers3](https://github.com/user-attachments/assets/7f2d4f65-d144-4b33-8907-044a281b49d1)

- Domain names: google-authenticator.burleson-appliance.net, authenticatoor.org
