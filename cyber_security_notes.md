# Cyber Security Notes

## Attacking Tools
* External reconnaissance: an attacker is simply looking for a vulnerable target to attack. The motive is to harvest as much information as possible from outside the target's network and systems.

### Scanning
* NMAP, ZenMap: The tool works using raw IP packets that are sent throughout a network. This tool can do an inventory of the devices connected to a target network, identify the open ports that could be exploited, and monitor the uptime of hosts in the network.
* Metasploit: The framework provides its users with vital information about multiple vulnerabilities and exploitation techniques.
* John the Ripper: Password cracking using dictionary attacks. For encrypted pawwords, it will check which encrpytion is using, then map encrpyted string with its dictionary to find the original string value
  * Offline tool 
* THC Hydra: It uses both dictionary and brute-force attacks to attack login pages.
  * Online tool 
* Wireshark: Network scanning by capturing data packets in a target network
* Aircrack-ng: Used for wireless hacking
  * It could be used to monitor the traffic in a Wi-Fi network by capturing packets to be exported in formats that can be read by other scanning tools. 
  * It can also attack a network by creating fake access points or injecting its own packets into a network to get more information about the users and devices in a network.
  * Finally, it can recover passwords for Wi-Fi networks using the aforementioned attacks to try different combinations.
* Cain and Abel: Windows password cracking tool 

## References
* [Cybersecurity - Attack and Defense Strategies][1]


[1]:https://subscription.packtpub.com/book/networking_and_servers/9781788475297
