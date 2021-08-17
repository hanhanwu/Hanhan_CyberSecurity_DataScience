# Web Attack Practice

## Tools Setup
### Installation
* Install Firefox
* Install Burpsuite
  * It is an intercepting proxy that allows you to intercept HTTP requests to a website, making it easy to inspect payloads, modify them, replay them, etc.
    * Comparing with wireshark, this tool works at the application level in an interactive way 
  * Download the community version and install with default settings: https://portswigger.net/burp/releases/professional-community-2021-8?requestededition=community 
* Install OWASP JuiceShop
  * Install nodejs: https://nodejs.org/en/download/
  * In your terminal, type `git clone https://github.com/bkimminich/juice-shop.git`  
    * Juice Shop is a website with lots of vulnerabilities and allows you to practice different types of attacks 
    * Then `cd` to juice-shop folder, type `npm install` just once
      * There might be lots of warnings, but that's expected  
    * Type `npm start`
    * Now go to http://localhost:3000 and you should be able to see the juiceshop website
* Register at CMD+CTRL: https://cmdnctrl.net/ranges
  * You will get an email for temporary password setup, and the email is not a phishing email...
  * It's a platform that provides vulnerable sites to attack

### Burpsuite Certificate Download
* After installing Burpsuite, go to `localhost:8080`
  * Click `CA Certification` at top right, then click "Save File" 
### Firefox Settings
* In Firefox search bar type `about:config`, accept the risk and move forward
  * In the appeared search bar, type `localhost`
  * Then set `network.proxy.allow_hijacking_localhost` as "True"
* In Firefox search bar type `about:preferences`
  * Click `Connection Settings`
    * Choose `Manual proxy configuration`
    * Type `127.0.0.1` as HTTP Proxy, with Port `8080`
    * Check "Always use this proxy for HTTPS"
  * Type `cert` in the search var under `about:preferences`, then click "View Certificates"
    * Click "Import" and import the certificate downloaded from Burpsuite from above step
### Burpsuite Setup
* After finishing above steps, open Burpsuite app, click "Proxy" tab --> click "Intercept is on"
* Click "Proxy" tab --> Click "HTTP history" tab
  * Right click a host starts with "http://localhost:3000/" and click "Add to scope"
    * If didn't see it, try to refresh Burp interface 
  * The click "Target" tab --> then click "Site Map", you should be able to see "http://localhost:3000"

## Cmd+Ctrl Shadow Bank Attack
* If you read the title of "challenges" in https://cmdnctrl.net/teams/summary, you will get some hints about what to attack...
* Example of very basic SQL injection: https://www.securityinnovation.com/training/cmd-ctrl-cyber-range-security-training/cyber-range-suite/cmdctrl-cyber-range-shadow-bank/
  * I think, most website won't be this vulnerable...
