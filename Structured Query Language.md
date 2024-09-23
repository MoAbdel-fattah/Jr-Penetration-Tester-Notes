## **What is SQLi?**

SQLi is a cyber attack that targets websites and applications that rely on databases. Attackers can inject malicious SQL code into user inputs, which can then be executed by the database server. This can allow attackers to steal sensitive data, modify or delete data, or even take control of the database server itself.

## **How does SQLi work?**

When a web application receives user input, it often sanitizes the input before using it in a SQL query. However, if the sanitization is not done properly, attackers can inject malicious code into the input. This code can then be executed by the database server as part of the SQL query.

There are different types of SQLi attacks, but some of the most common ones include:

* **In-band SQLi:** This is the most common type of SQLi attack. In this attack, the attacker can see the results of their attack directly in the web browser.  
* **Blind SQLi:** In this type of attack, the attacker cannot see the direct results of their attack. However, they can still determine whether their attack was successful based on the response time of the web application.  
* **Out-of-band SQLi:** In this type of attack, the attacker can use the SQL query to send data to an external server under their control.

## **How to protect against SQLi?**

There are a number of ways to protect against SQLi attacks. Here are a few of the most important:

* **Use prepared statements:** Prepared statements are a way to parameterize SQL queries. This means that the SQL code is written separately from the user input. The user input is then bound to the prepared statement as parameters. This helps to prevent SQLi attacks because the user input is not directly inserted into the SQL query.  
* **Validate user input:** It is important to validate all user input before using it in a SQL query. This means checking the input for any characters that could be used to perform SQLi attacks.  
* **Escape user input:** If you cannot use prepared statements, you can escape user input before using it in a SQL query. This means replacing any special characters with escape sequences that will be interpreted literally by the database server.