Public vs Private IP

## Public IP Address:
- A public IP Address is assigned to a device directly connected to the internet, allowing it to communicate with other device on the internet.
- It addresses are unique and globally, meaning they can be accessed from anywhere on the internet.
- They are provided by Internet Service Providers(ISPs) and are used to identify devices on the internet.
- Public IP Addresses are visible to other devices on the internet, allowing them to initiate communication with the device.

 ## Private IP Address:
 - It is used within a local network. such as a home or office network, to identify and communicate with devices wthin that network.
 - Private IP Addressses are not directly accessible from the internet.
 - They are typically assigned by network administrators and reserved for private network use.
 - It are not unique globally. Many device can have the same private IP adddress within different networks as long as they don't need to communicate with each other directly over the internet.

 - The most commonly used Private IP address ranges
    1. 10.0.0.0 to 10.255.255.255 (10.0.0.0/8)
    2. 172.16.0.0 to 172.31.255.255 (172.16.0.0/12)
    3. 192.168.0.0 to 192.168.255.255 (192.168.0.0/16)

# Key Takeaways:
1. Public IPs are necessary for internet accessibility, while private IPs are used for internal network communication.

2. Devices with private IPs access the internet through a public IP using techniques like NAT (Network Address Translation).

3. Public to private and private to Public IP Translation is done by network Address Translation using the router.
4. Usinf DHCP protocol, Private IP assignment is done with the use of a DHCP server.

5. In the majority of networks, Router is acting as a DHCP server and NAT device.


## How internet is working
-  The internet works through a vast network of interconnected devices that communicate using standardized protocols. Here’s a simplified breakdown of how it functions: 

## Infrastructure: The internet consists of physical components like servers, routers, cables, and satellites that form a global network.

## Protocols: Communication happens using protocols, primarily TCP/IP (Transmission Control Protocol/Internet Protocol). TCP ensures data is sent and received accurately, while IP addresses devices on the network.

## Data Transmission: When you send a request (like opening a website), your device converts it into data packets. These packets travel through various routers and switches across the network until they reach their destination.

## Domain Name System (DNS): Instead of using IP addresses directly, we use domain names (like www.example.com). The DNS translates these names into IP addresses, allowing browsers to locate servers.

## Web Servers: Once the request reaches the web server hosting the website, the server processes it and sends the requested data back to your device in the form of data packets.

## Rendering: Your browser then reconstructs these packets into a web page, displaying the content for you to view.

## Interactivity: The internet allows for real-time interactions, enabling activities like online gaming, video calls, and social media through continuous data exchange.


#### ----------------------------------------------------------------  ####

## Monolithic and microservices architectures are two different approaches to software development and application design. Here’s a breakdown of their key differences:

## Monolithic Architecture: 
1. Single Unit: In a monolithic architecture, the entire application is built as a single, unified unit. All components (frontend, backend, database) are interconnected and run as one process.

2. Deployment: The whole application is deployed at once. Any changes require a redeployment of the entire system.

3. Scalability: Scaling can be challenging, as the entire application must be scaled together. This can lead to inefficiencies if only specific parts need more resources.

4. Development Speed: It can be faster to develop initially since all components are in one codebase, but as the application grows, it may become more complex and harder to manage.

5. Technology Stack: Typically, a single technology stack is used, which can limit flexibility in choosing the best tools for different tasks.

## Microservices Architecture: 
1. Modular Design: Microservices break down the application into smaller, independent services that can be developed, deployed, and scaled individually.

2. Deployment: Each service can be deployed independently, allowing for more frequent and flexible updates without affecting the entire application.

3. Scalability: Services can be scaled individually based on their specific needs, making it more efficient and cost-effective.

4. Development Speed: While it may take longer to set up initially due to the complexity of managing multiple services, teams can work on different services concurrently, potentially speeding up the overall development process.

5. Technology Flexibility: Different services can use different technology stacks, allowing teams to choose the best tools for each specific task.

### When to Use Each:

1. Monolithic: Best for small applications or startups where the team is small, and speed to market is crucial. It can also work well for projects with well-defined requirements that are not expected to change significantly.

2. Microservices: Ideal for large, complex applications requiring scalability and flexibility. It suits teams that can manage the complexity of distributed systems and want to leverage different technologies for different services.


### ----------------------------------------------- ###

## Security groups :

- They act as virtual firewalls that control inbound and outbound traffic to and from resources, such as virtual machines (VMs) or containers. Here’s a breakdown of what security groups are and how they work:

# Here are the key points about security groups:

1. Traffic Control: They act as virtual firewalls, controlling inbound and outbound traffic.

2. Stateful Rules: If incoming traffic is allowed, the response is automatically allowed.

3. Default Group: A default security group applies to instances without a specific group.

4. Multiple Associations: You can assign multiple security groups to an instance for flexibility.

5. Granular Control: Rules specify allowed IPs, protocols, and ports, allowing for detailed traffic management.

## Best Practices:

- Use the principle of least privilege.
- Regularly audit and update rules.
- Use descriptive names for easier management.
=================================================================================

## what is Forward Porxy and Reverse Proxy ?

==> A forward proxy and a reverse proxy serve different purposes in a network environment, primarily regarding how they handle requests and responses between clients and servers.

## Forward Proxy:
-------------
==> A forward proxy, also known simply as a proxy server, is a server that sits between client computers and the internet. It acts as an intermediary, receiving requests from clients, forwarding those requests to internet resources, and then returning the responses back to the clients.

## A forward proxy is primarily used for:

1. Client Anonymity: Hides the client's IP address from the target servers, enhancing privacy.
2. Caching Responses: Cache Content to save bandwidth and speed up content delivery to clients.

3. Traffic Control: Monitors and controls outbound internet traffic, often used in corporate environments to enforce policies.
4. Logging: Records client requests and responses for monitoring and auditing purposes.
5. Request/Response Transformation: Modifies requests and responses on-the-fly, such as compressing data or filtering content.
6. Encryption: Can encrypt data sent between clients and the proxy, adding a layer of security for the traffic.


## A reverse proxy 
## A reverse proxy is a server that sits in front of one or more web servers and acts as an intermediary between the web servers and the internet. When a client makes a request, it is sent to the reverse proxy, which then forwards the request to the appropriate web server. After receiving the response from the web server, the reverse proxy sends that response back to the client.

## A reverse proxy is primarily used for:
1. SSL Termination: Manages SSL encryption and decryption, offloading this resource-intensive process from backend servers, which allows them to focus on handling requests more efficiently.

2. Load Balancing: Distributes incoming traffic across multiple web servers to optimize resource use and enhance performance.

3. Security: Protects backend servers by concealing their identities and serving as a barrier against direct access, thereby enhancing the overall security posture of the network.




## Difference between Forward and Reverse Proxy Based on features:
 	# Forward Proxy 	                                                                      #Reverse Proxy
Purpose 	  -     1.Provides anonymity and caching to clients 	            | 1. Improves server performance, load balancing, and security
Location	  -     2. Between the client and the internet 	                    | 2. Between the internet and server
Visibility	  -     3. he client is aware of the proxy                          | 3. The server is not aware of the proxy
Configuration - 	4. The client must be configured to use proxy 	            | 4. Server must be configured to use proxy use
Use cases 	  -     5.Bypassing content filters, accessing restricted content 	| 5. Load balancing, caching, SSL/TLS offloading, web application firewall
Examples 	  -     6. Squid, Proxy, Tor                                        | 6. Nginx, Apache, HAProxy



## what is different between yum and dnf ?

#### Yum  (Yellowdog Updater, Modified):
1. It is Used in older versions of CentOS and RHEL
2. yum is an older package manager for RPM-based Linux distributions
3. Slower, especially with large repositories.
4. Higher memory consumption.


### dnf (Dandified Yum)
1. dnf is its modern successor, offering improved performance and features.
2. Default package manager in Fedora and newer versions of CentOS/RHEL.
3. Faster due to a more efficient dependency resolver.
4. Lower memory usage.


#______________________________________#

#  What is Redis and cache

### Redis: 
    -  Redis is an open-source, in-memory data structure store that is often used as a database, cache, and message broker. It supports various data structures such as strings,      hashes, lists, sets, and more.
    -  Redis is known for its high performance and flexibility, making it suitable for applications that require quick data access.

### Cache:
        - A cache is a temporary storage area that holds frequently accessed data to speed up data retrieval. Caching reduces the time it takes to access data from a slower storage layer (like a database) by storing copies of data closer to where it's needed. 
        - Caches can be implemented in various ways, including in-memory storage or disk-based storage.

### Relationship
Redis is commonly used as a caching layer in applications due to its fast access speeds. By caching data in Redis, applications can quickly retrieve information without needing to query a slower database, thus improving performance and scalability.

