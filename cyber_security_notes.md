# Cyber Security Notes

## Attacking Tools
* External reconnaissance: an attacker is simply looking for a vulnerable target to attack. The motive is to harvest as much information as possible from outside the target's network and systems.

### Pen Test Toolkit
* Kali
  * https://www.kali.org/
  * I allows you to launch different types of attacks, such as social engineering, password attacks
    * For example, through it's GUI, you can craft a phishing email  

### Scanning
* NMAP, ZenMap: The tool works using raw IP packets that are sent throughout a network. This tool can do an inventory of the devices connected to a target network, identify the open ports that could be exploited, and monitor the uptime of hosts in the network.
* Metasploit: The framework provides its users with vital information about multiple vulnerabilities and exploitation techniques.
* Scanrand: Faster and more effective network scanning tool than NMAP
* Nessus: One of the best network scanners
  * It can call other tools to achieve external functionalities 
* John the Ripper: Password cracking using dictionary attacks. For encrypted pawwords, it will check which encrpytion is using, then map encrpyted string with its dictionary to find the original string value
  * Offline tool 
* THC Hydra: It uses both dictionary and brute-force attacks to attack login pages.
  * Online tool 
* Wireshark: Network scanning by capturing data packets in a target network
* Aircrack-ng: Used for wireless hacking
  * It could be used to monitor the traffic in a Wi-Fi network by capturing packets to be exported in formats that can be read by other scanning tools. 
  * It can also attack a network by creating fake access points or injecting its own packets into a network to get more information about the users and devices in a network.
  * Finally, it can recover passwords for Wi-Fi networks using the aforementioned attacks to try different combinations.
* Wardriving: It targets most unsecured Wi-Fi networks (wireless network).
  * It's often executed on an autommobile to make itself looks less suspicious 
* Cain and Abel: Windows password cracking tool 
* Ophcrack: Can also crack long and complex Windows passwords effectively
* Power Memory: https://github.com/giMini/PowerMemory/
  * It's used to crack VM's passwords, often used in cloud attacks

## Security Check Tools
* None of these can be foolproof, but might help reduce the threats
* Virus Total
  * https://www.virustotal.com/gui/
  * You can check URL, file, IP, domain before clicking/opening them
* Checkmarx
  * https://www.checkmarx.com/
  * It's a tool that can scan the code and detect the vulnerabilities 

## References
* [Cybersecurity - Attack and Defense Strategies][1]


[1]:https://subscription.packtpub.com/book/networking_and_servers/9781788475297
