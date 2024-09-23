# **Server-Side Request Forgery**

**SSRF** (Server-Side Request Forgery) is a web application vulnerability that allows an attacker to manipulate the server into making unauthorized HTTP requests. This can lead to various consequences, depending on the server's configuration and resources.                     

## **Types of SSRF:**

* **Regular SSRF:** Data retrieved from the forged request is returned to the attacker.  
* **Blind SSRF:** No data is returned to the attacker, requiring alternative methods to confirm success.

## **Impacts of SSRF Attacks:**

* Accessing unauthorized data or areas.  
* Internal network exploration and potential pivoting.  
* Leaking sensitive information like authentication tokens.

## **Identifying Potential SSRF Vulnerabilities:**

* Look for places where web applications accept user-controlled URLs:  
  * Address bar parameters  
  * Hidden form fields  
  * Partial URLs (hostname or path)  
* For blind SSRF, use external tools like requestbin.com or Burp Suite Collaborator to monitor requests.

## **Mitigating SSRF:**

* **Input Validation:** Implement checks to ensure requested resources are valid and authorized.  
* **Denylists:** Block access to sensitive resources or internal networks.  
* **Allowlists (cautious):** Only allow requests to specific trusted URLs. (Be aware of subdomain bypass techniques.)  
* **Address Open Redirects:** Fix open redirects that could be exploited for SSRF.

## **Bypassing Mitigation Techniques:**

* **Denylist Bypass:** Attackers can use alternative ways to represent localhost (e.g., 0.0.0.0) or exploit cloud metadata access (169.254.169.254).  
* **Allowlist Bypass:** Attackers can create subdomains on their own domain that match the allowlist pattern.

## **Key Takeaways:**

* SSRF is a serious vulnerability that can have significant consequences.  
* Developers should implement robust input validation and access controls.  
* Security professionals should be aware of bypass techniques for mitigation strategies.