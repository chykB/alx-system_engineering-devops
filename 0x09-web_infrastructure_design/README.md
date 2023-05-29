<img width="100%" height="300" src="https://media.licdn.com/dms/image/C4E12AQEmC8s-Ga3i4A/article-cover_image-shrink_600_2000/0/1610034339052?e=2147483647&v=beta&t=N7OMsUju3WbCxvXGZYd2488yaioMeBu3PG2p8VJchVQ">

# Web infrastructure design
This document provides an overview of the design of a web infrastructure to host a website accessible via www.foobar.com. The infrastructure is designed to ensure reliability, scalability, and optimal performance for the website.

## Infrastructure Overview

### User Access:
When a user wants to access the website, they enter "www.foobar.com" in their web browser.

### DNS Resolution:
The DNS (Domain Name System) resolves the domain name "www.foobar.com" to the server's IP address (configured as 8.8.8.8).

### Web Server:
The incoming user request is received by the web server (Nginx) running on the server.
Nginx processes the request and forwards it to the application server.

### Application Server:
The application server receives the request from the web server and executes the website's code.
It retrieves and processes data from the MySQL database if needed.
The application server generates the appropriate response and sends it back to the web server.

### Web Server Response:
The web server receives the response from the application server and sends it back to the user's web browser.

