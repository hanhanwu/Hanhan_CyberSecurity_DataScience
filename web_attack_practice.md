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
  * <b>Make sure "Intercept is on" everytime</b>
* Click "Proxy" tab --> Click "HTTP history" tab
  * Right click a host starts with "http://localhost:3000/" and click "Add to scope"
    * If didn't see it, try to refresh Burp interface 
  * The click "Target" tab --> then click "Site Map", you should be able to see "http://localhost:3000"

## Example Attacks
* It's an attack game in Cmd + Ctrl
* If you read the title of "challenges" in https://cmdnctrl.net/teams/summary, you will get some hints about what to attack
* Check HTML source code, and you will find the username and password in the comment
  * Who will really do this in the real world... 
* Example of very basic SQL injection: https://www.securityinnovation.com/training/cmd-ctrl-cyber-range-security-training/cyber-range-suite/cmdctrl-cyber-range-shadow-bank/
  * By typing `' 1=1 #` in the username and put whatever in the apssword field, you can login
  * I think, most website won't be this vulnerable...
  * A 7 min simple tutorial in sql injection: https://securityinnovation.hubs.vidyard.com/watch/fThcxjLgvA9zxDWvFhaNaC
* Exmaples of XSS (cross site scripting), JS injection
  * XSS on any empty web form, such as "Search" bar by fill in things like `<script>alert(1)</script>`
  * XSS on login page by adding `loginError.action?errorMsg=<script>alert(1)</script>` to the URL before login 
  * XSS on transfer page by adding `doTransfer.action?destId=<script>alert(1)</script>&amount=2222` to the URL after login
* Example of denial of service attack: http://fjordengineering.com/posts/version-2.3-vulnerability/
  * Add `kill?shutDownToken=ae450g9dg` after the URL could shuts down the serve... 
* Example of foreceful browsing & XML injection
  * Add `/admin` after the URL
  * Under this admin login page, type `blah' or 1=1 or 'a'='a` as username and click submit, you will achieve XML injection
* Example of authorization bypass
  * If you see user settings URL has params in it, such as "/users/profile/3/settings", you can change the params
* Example of cryptanalysis of Vigenere Cipher
  * Add `/cheshire` at the end of the URL
  * I really don't know why this could get the score....
* Examples of Hidden Form Field Manipulation
  * Exmaple of post as others
    * Open HTML source, and find "newPost" 
    * Remove `type=""hidden` to make those visible
    * Replace the value of threadId; repalce the value of postBy to a user name you know; set the value of staffPost to "true"
    * Click "Submit" on the website
* Example of Bypass approval form
  * If you find the hidden approval field, you can remove `type="hidden"` and set the value as "0" 
  * If it needs other actions such as upload a .pdf file, you might need to do those before clicking submit
<p align="center">
<img src="https://github.com/hanhanwu/Hanhan_CyberSecurity_DataScience/blob/master/more_images/bypass_approval_form.png" width="600" height="100" />
</p>

* Example of Price Gouging
    * Still remove `type="hidden"`, and change the values of the hidden field. 
    * Increase the stock price and make sure the numbers you set are sellable 
<p align="center">
<img src="https://github.com/hanhanwu/Hanhan_CyberSecurity_DataScience/blob/master/more_images/stock_selling.png" width="850" height="150" />
</p>

* Example of disabled button
  * If you see disabled buttons in the website, there might be something interesting to explore. So find that hidden button in the source HTML, and change `disabled=""` to `enabled=""`
<p align="center">
<img src="https://github.com/hanhanwu/Hanhan_CyberSecurity_DataScience/blob/master/more_images/disabled_button.png" width="850" height="650" />
</p>

* Example of weak password reset
  * If you know a user's name, check his/her facebook to see whether you can find answers for password set 
* Exmaple of threadID integer overflow
  * Add `/users/messages/threads/3999999999999999` after the URL
<p align="center">
<img src="https://github.com/hanhanwu/Hanhan_CyberSecurity_DataScience/blob/master/more_images/Screen%20Shot%202021-08-18%20at%209.18.22%20AM.png" width="850" height="200" />
</p>

