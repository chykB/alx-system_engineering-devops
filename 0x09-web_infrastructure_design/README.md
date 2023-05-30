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

## One server web infrastructure
<img width="50%" src="https://ibb.co/jgHsLMt">

### Infrastructure Overview

The web infrastructure operates as follows:

#### User Access:
When a user wants to access the website, they enter "www.foobar.com" in their web browser.

#### DNS Resolution:
The DNS (Domain Name System) resolves the domain name "www.foobar.com" to the server's IP address (configured as 8.8.8.8).

#### Web Server:
The incoming user request is received by the web server (Nginx) running on the server.
Nginx processes the request and forwards it to the application server.

#### Application Server:
The application server receives the request from the web server and executes the website's code.
It retrieves and processes data from the MySQL database if needed.
The application server generates the appropriate response and sends it back to the web server.

#### Web Server Response:
The web server receives the response from the application server and sends it back to the user's web browser.

### Issues with this infrastructure:
Although this infrastructure design meets the specified requirements, it has some limitations and potential issues:

#### Single Point of Failure (SPOF):
Since there is only one server, if it fails or experiences issues, the website will become unavailable.
To mitigate this, implementing redundancy and backup measures can be considered.

#### Downtime during Maintenance:
When deploying new code or performing maintenance tasks, the web server needs to be restarted, resulting in temporary downtime.
Scheduling maintenance during low-traffic periods and implementing strategies to minimize downtime can help mitigate this issue.

#### Scalability:
With only one server, the infrastructure may face challenges in handling high traffic loads.
To improve scalability, load balancing and scaling techniques can be implemented to distribute the load across multiple servers.

## Two  server web infrastructure
<img width="50%" src="https://ibb.co/crsM7cL">

## Infrastrure overview
The web infrastructure operates as follows:

#### User Access:
When a user wants to access the website, they enter "www.foobar.com" in their web browser.

#### Load Balancer:
The incoming user request is received by the load balancer (HAproxy) which acts as a traffic distributor.
HAproxy uses a distribution algorithm (e.g., round-robin) to evenly distribute requests across the available servers.
This improves performance and prevents overloading a single server.

#### Web Servers:
The load balancer forwards each request to one of the two web servers (Nginx).
Nginx processes the request and forwards it to the application server.

#### Application Server:
The application server receives the request from the web server and executes the website's code.
It interacts with the MySQL database to retrieve and process data.
The application server generates the appropriate response and sends it back to the web server.
#### Web Server Response:
The web server receives the response from the application server and sends it back to the load balancer.

####Load Balancer Response:
The load balancer receives the response from the web server and forwards it back to the user's web browser.

### Issues with this infrastructure
While this infrastructure design addresses the specified requirements, it is important to consider potential issues and implement appropriate measures:

#### Single Point of Failure (SPOF):
Although there are multiple servers, the load balancer represents a potential single point of failure.
Implementing redundancy for the load balancer and employing a failover mechanism can enhance reliability.

#### Security Considerations:
The current infrastructure lacks a firewall and does not employ HTTPS encryption.
Implementing a firewall solution and enabling HTTPS can enhance security and protect sensitive user data.

## Three server infrastructure
<img width="50%" src="https://ibb.co/N1ym6cB">

### Infrastructure Overview

Additional Elements:
Firewalls: Added for network security to control and filter incoming and outgoing traffic, protecting the servers from unauthorized access and potential threats.
SSL Certificate: Implemented to serve traffic over HTTPS, ensuring secure communication by encrypting data transmitted between the server and clients.
Monitoring Clients: Installed to collect performance and health-related data from each server, enabling proactive monitoring and issue detection.

#### Firewalls:
Firewalls are used to enforce access control policies and protect the servers from unauthorized access, malicious attacks, and potential security breaches.

#### Traffic served over HTTPS:
HTTPS ensures secure communication between the server and clients by encrypting the data transmitted over the network. It protects sensitive information from being intercepted or tampered with.

#### Monitoring:
Monitoring is used to keep track of server performance, availability, and security.
It helps identify any anomalies, issues, or performance bottlenecks, allowing prompt action and ensuring optimal server operation.

### Issues with the Infrastructure:

#### Terminating SSL at the load balancer level:
Termination of SSL at the load balancer means that the SSL decryption and encryption processes happen at the load balancer.
This can create a potential security risk if the communication between the load balancer and the backend servers is not adequately protected.

#### Single MySQL server capable of accepting writes:
Having only one MySQL server capable of accepting writes introduces a single point of failure.
If the MySQL server goes down, it can result in downtime and potential data loss until the server is restored.

#### Servers with the same components:
Having servers with identical components (database, web server, and application server) can limit scalability and fault tolerance.
It may result in resource contention and performance issues if the workload increases or one component experiences a failure.


