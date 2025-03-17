# Project 1: Penetration Testing a Vulnerable Web Application using OWASP Juice Shop on Kali Linux

## Introduction
In this project, you will learn how to use various tools to perform penetration testing on a vulnerable web application, OWASP Juice Shop. OWASP Juice Shop is a deliberately insecure web application for educational purposes. This project will help you understand common web vulnerabilities and how to exploit them ethically.

## Pre-requisites
- Basic understanding of web application concepts (HTTP, HTTPS, web servers).
- Familiarity with using the command line interface (CLI).
- Basic knowledge of web development technologies (HTML, JavaScript, etc.).

## Lab Set-up and Tools

### Diagram
Here is a simple network diagram for this lab setup:

```
+------------------+                 +------------------+
|     Attacker     |                 |  Vulnerable App  |
|   Kali Machine   | <-------------> | (OWASP Juice     |
| (192.168.1.100)  |                 |    Shop)         |
+------------------+                 +------------------+
```

### Tools
- **Kali Linux**: A Debian-derived Linux distribution designed for digital forensics and penetration testing.
- **OWASP Juice Shop**: A vulnerable web application for educational purposes.
- **Burp Suite**: An integrated platform for performing security testing of web applications (pre-installed on Kali Linux).

## Installation

### OWASP Juice Shop
You can set up OWASP Juice Shop on your local machine using Docker:

1. Install Docker on your Kali Linux machine:
    ```bash
    sudo apt-get update
    sudo apt-get install docker.io
    sudo systemctl start docker
    sudo systemctl enable docker
    ```

2. Pull the OWASP Juice Shop Docker image:
    ```bash
    sudo docker pull bkimminich/juice-shop
    ```

3. Run the OWASP Juice Shop container:
    ```bash
    sudo docker run -d -p 3000:3000 bkimminich/juice-shop
    ```

4. Access the OWASP Juice Shop web application by navigating to [http://localhost:3000](http://localhost:3000) in your web browser.

## Tasks

### Task 1: SQL Injection
1. Open Burp Suite on your Kali Linux machine.
2. Configure your browser to use Burp Suite as a proxy (127.0.0.1:8080).
3. Intercept a login request and attempt an SQL injection attack. For example, use `' OR '1'='1` as the username and password.
   **Expected Output**: Access to the application with an SQL injection payload.

### Task 2: Cross-Site Scripting (XSS)
1. Navigate to a page in OWASP Juice Shop where user input is reflected (e.g., the search bar).
2. Enter a basic XSS payload such as `<iframe src="javascript:alert('xss')">` into the input field.
   **Expected Output**: An alert box should appear, indicating that the XSS attack was successful.

### Task 3: Sensitive Data Exposure
- **Vulnerability**: This is a product page and it is clearly showing email addresses to everyone.

### Task 4: Brute Force Attack
In this section, a Brute Force Attack is used to access the Administration account with a passwords list using Burp Suite.
- The attack used Burp Suite’s Intruder module.
- A password list (passwords.txt) using the SecLists library was loaded as payload.
- Different passwords must be tried to access the administrator account. An intruder can quickly test a large number of possible passwords (payload).

Steps:
1. Intercept the login request using Burp Suite. Instead of forwarding the request directly to the server, send it to Intruder to execute a brute-force attack.
2. Navigate to the Positions tab in Intruder and click the Clear § button to remove all predefined attack positions.
3. Place two § symbols around the password field, marking it as the insertion point for passwords from the passwords list. This setup guides Burp Suite to replace the marked area with each password during the brute-force attempt.
4. When a “200” status code or noticeable differences are found between the responses, this indicates a successful attack. The “400” status code means invalid password.
5. The final successful result was achieved.

## Additional Resources
- [OWASP Juice Shop Documentation](https://owasp.org/www-project-juice-shop/)
- [Burp Suite Documentation](https://portswigger.net/burp/documentation)
- [Web Security Academy by PortSwigger](https://portswigger.net/web-security)
- [Kali Linux Documentation](https://www.kali.org/docs/)

This project will help you understand common web vulnerabilities and how to exploit them ethically using Kali Linux and OWASP Juice Shop.
