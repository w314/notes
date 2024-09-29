js, javascript, security, xss, crfs

# JavaScript Security

## Common Attack Types

### XSS
- Cross-Site Scripting
- attackers embed malicious code into a vulnerable website
- it gets executed in a user's browser who visits the site
- website is vulnerable to xss if uses user input data in responses without validation

Example:<br>
Comment entered in comments section in `<script>` tag that gets executed by the browser.


### CFRS
- Cross-Site Request Forgery
- attacker steals session cookie information

### Server-Side JavaScript Injection


