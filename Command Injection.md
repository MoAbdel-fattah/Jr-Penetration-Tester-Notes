# **What is Command Injection?**

* Abusing an application to run commands on the underlying operating system.  
* Allows attackers to steal data, gain unauthorized access, or perform other malicious actions.

## **How it Works:**

* Applications sometimes use user input to construct system commands.  
* Attackers can inject their own commands into this input.  
* The application executes the attacker's commands with its own privileges.

## **Types of Command Injection:**

* **Blind:** No direct feedback on successful exploitation.  
* **Verbose:** Application outputs the results of executed commands.

## **Detection Methods:**

* **Blind:** Using payloads that cause delays (ping, sleep) or force output redirection (\>).  
* **Verbose:** Observing the application's output after sending commands (whoami).

## **Exploitation Techniques:**

* Using various payloads depending on the operating system (Linux/Windows).  
* Bypassing filters and sanitization mechanisms.

## **Prevention Methods:**

* Minimizing use of risky functions (e.g., exec, system) in code.  
* Validating and sanitizing user input to restrict allowed characters and form

