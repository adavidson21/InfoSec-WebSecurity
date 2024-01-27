# Web Security Project

## Target 1 - CSRF/XSRF Attack

### Definition 

A Cross-Site Request Forgery (CSS/XSRF) attack occurs when a user browses to a malicious site in the middle of their session with a trusted site and a script on the malicious site reads the user's cookie to the trusted site and use it to forge requests to that site. 

### Vulnerability

Within the file 'account.php', the vulnerability appears in lines 20-33, where the CSRF protection function that is implemented does not properly protect against an attack.

This check does not work as desired because the attacker is able to pass any arbitrary value to the webpage for the ‘challenge’ value, find out what the ‘expected’ value is (from the notification on the page that is created containing this value within line 28), and then inject the expected value in order to bypass the CSRF protection. 

Because the ‘challenge’ value is static (as per the attacker’s input), the ‘expected’ value is also static, therefore the attack will work with every login.  

## Target 2 - XSS Attack

### Definition

An Cross-Site Scripting (XSS) attack occurs when an attacker tricks the browser into executing malicious scripts without the user's knowledge.

### Vulnerability

The vulnerability for the XSS attack is in the file ‘index.php’, specifically relating to line 34 of the HTML portion, which contains the following:
`<input type="text" name="login" value="<?php echo @$_POST['login'] ?>">`

This code is vulnerable due to the fact that it is posting data straight to the server without any kind of validation after retrieving the input from the user. Due to this, an attacker is able to inject JavaScript functions within one string into the ‘login’ input. 

Because the literal value is taken without any alterations, the string was interpreted as a part of the input variable and `<script>` tags and their contents were able to be injected into the HTML code on the webpage. 

## Target 3 - SQL Injection

### Definition

A SQL injection attack when a malicious SQL statement is inserted into an entry field for execution. 

### Vulnerability

The vulnerability for the SQL Injection is within ‘auth.php’, lines 57 and 68, and should be changed in order to fix the vulnerability.

When sending forms that interact with a database, code should never rely on dynamic queries that have user input included as parameters. What this allows for is for an attacker to use this weakness to insert SQL statements that can manually change the database that is being accessed. 

SQL sanitization was the prevention method that was attempted to be used within ‘auth.php’, within the function ‘sqli_filter’, but it was not successful 



