# Answers.md

# Module 1 – Internet Fundamentals

---

## 1.1 History of the Internet

### 1.

ARPANET was the world's first large-scale packet-switched computer network. It was launched in 1969 and became the foundation of the modern Internet.

---

### 2.

ARPANET was created to enable reliable communication, resource sharing, and collaboration between research institutions while ensuring communication could continue even if part of the network failed.

---

### 3.

ARPANET was funded by **ARPA (Advanced Research Projects Agency)**, a research organization under the U.S. Department of Defense.

---

### 4.

ARPANET solved problems such as unreliable communication, expensive standalone computers, lack of resource sharing, and difficulty exchanging information between research institutions.

---

### 5.

The first message attempted over ARPANET was **"LOGIN"**, but the receiving computer crashed after receiving only **"LO"**, making "LO" the first Internet message.

---

### 6.

ARPANET gradually expanded by connecting more universities and organizations. As common protocols like TCP/IP were adopted, independent networks could communicate, eventually forming today's Internet.

---

### 7.

Common protocols provide standardized communication rules so devices built by different manufacturers and running different operating systems can communicate successfully.

---

### 8.

Early computers were isolated machines with no common networking infrastructure or communication standards, making direct communication impossible.

---

### 9.

During the Cold War, communication needed to continue even if part of the network was destroyed or failed, making reliability a critical design goal.

---

### 10.

Packet switching uses network resources efficiently, allows packets to travel through multiple routes, and continues working even when some network paths fail.

---

### 11.

Using multiple communication paths increases fault tolerance. If one path fails, packets can be routed through another path without stopping communication.

---

### 12.

Packet Switching divides data into small packets that travel independently across the network and are reassembled at the destination.

---

### 13.

Circuit Switching establishes one dedicated communication path between two devices that remains reserved until communication ends.

---

### 14.

| Packet Switching             | Circuit Switching                     |
| ---------------------------- | ------------------------------------- |
| Data is divided into packets | Dedicated communication path          |
| Efficient resource usage     | Resources remain reserved             |
| Can reroute packets          | Communication stops if the path fails |
| Used by the Internet         | Used in traditional telephone systems |

---

### 15.

Traditional telephone calls are a good example of Circuit Switching because a dedicated connection is maintained throughout the call.

---

### 16.

Web browsing, email, file downloads, and video streaming are examples of Packet Switching because data is transmitted as packets.

---

## 1.2 What is the Internet?

### 17.

The Internet is a global system of interconnected computer networks that communicate using standardized protocols, primarily TCP/IP.

---

### 18.

It is called a **Network of Networks** because it connects millions of independent networks into one global communication system.

---

### 19.

A network is a collection of connected devices that can communicate and share resources with each other.

---

### 20.

Distributed communication means there is no single central computer controlling the Internet. Many independent devices and networks work together to exchange data.

---

### 21.

Global infrastructure refers to the physical and networking components that make the Internet possible, including routers, fiber optic cables, data centers, ISPs, and undersea cables.

---

### 22.

A Local Area Network (LAN) is a network that connects devices within a limited geographical area such as a home, school, or office.

---

### 23.

A centralized network would be difficult to manage, less scalable, and vulnerable to a single point of failure. Distributed networks are more reliable and scalable.

---

### 24.

If one route or device fails, distributed communication allows data to travel through alternative routes, keeping communication active.

---

### 25.

Fiber optic cables transmit data using light, providing extremely high speed, low latency, and large bandwidth over long distances.

---

### 26.

Internet Service Providers (ISPs) connect local networks to the global Internet, allowing users to communicate with devices outside their own network.

---

### 27.

| Internet                      | Local Area Network                             |
| ----------------------------- | ---------------------------------------------- |
| Global network                | Small private network                          |
| Connects millions of networks | Connects nearby devices                        |
| No single owner               | Usually owned by one organization or household |
| Worldwide communication       | Limited geographical area                      |

---

### 28.

| Internet                                       | World Wide Web                  |
| ---------------------------------------------- | ------------------------------- |
| Physical and logical networking infrastructure | Service running on the Internet |
| Includes routers, cables, protocols            | Includes websites and webpages  |
| Supports many services                         | One of many Internet services   |

---

### 29.

The World Wide Web is one application that uses the Internet. Other services such as email, FTP, video calls, and cloud storage also use the same Internet infrastructure.

---

### 30.

The request travels from the laptop to the home router, then to the ISP, through multiple networks and routers, until it reaches Google's servers.

---

### 31.

The ISP connects your local network to the Internet and forwards your requests toward their destination.

---

## 1.3 How Computers Communicate

### 32.

Computers communicate by exchanging structured data over a network using standardized communication protocols.

---

### 33.

A message is a piece of information sent from one computer to another.

---

### 34.

Data transmission is the process of moving data from one device to another through networking technologies such as Wi-Fi, Ethernet, or fiber optic cables.

---

### 35.

A sender is the device or application that initiates communication by transmitting data to another device.

---

### 36.

A receiver is the device or application that accepts and processes incoming data sent by another device.

---

### 37.

Standardization means that all devices follow the same communication rules and protocols, allowing systems built by different companies to communicate successfully.

---

### 38.

Without communication rules, computers would not know how to interpret incoming data, where messages begin or end, or how to respond correctly.

---

### 39.

Standardization ensures interoperability. It allows different operating systems, programming languages, devices, and networks to communicate using common protocols.

---

### 40.

Data is divided into packets to improve efficiency, reliability, and fault tolerance. Packets can travel independently and be reassembled at the destination.

---

### 41.

When you open YouTube, your browser creates a request, sends it through the Internet to YouTube's servers, receives the response, and displays the webpage or app interface.

---

### 42.

A login request is created by the client, transmitted through the network to the server, validated by the backend, checked against the database, and the server returns a success or failure response.

---

### 43.

Without common communication standards, devices from different companies would use incompatible formats and protocols, making communication impossible.

---

## 1.4 Protocols

### 44.

A protocol is a standardized set of rules that defines how computers communicate over a network.

---

### 45.

Protocols exist to ensure that devices exchange data in a structured, reliable, and understandable way regardless of their hardware or software differences.

---

### 46.

A protocol stack is a collection of networking protocols organized into layers, where each layer performs a specific responsibility during communication.

---

### 47.

The Application Layer provides services directly to applications. Protocols such as HTTP, HTTPS, FTP, SMTP, and DNS operate at this layer.

---

### 48.

The Transport Layer manages communication between devices by handling reliability, packet ordering, error detection, and data delivery. TCP and UDP belong to this layer.

---

### 49.

The Internet Layer is responsible for logical addressing and routing packets between different networks using IP.

---

### 50.

The Network Access Layer handles the actual transmission of data over physical or wireless communication media such as Ethernet and Wi-Fi.

---

### 51.

HTTP (HyperText Transfer Protocol) is used to transfer webpages and API requests between clients and servers.

---

### 52.

HTTPS (HyperText Transfer Protocol Secure) is the secure version of HTTP. It encrypts communication using TLS to protect transmitted data.

---

### 53.

TCP (Transmission Control Protocol) provides reliable, ordered, and error-checked communication between devices.

---

### 54.

UDP (User Datagram Protocol) provides fast communication with minimal overhead but does not guarantee packet delivery or ordering.

---

### 55.

DNS (Domain Name System) translates human-readable domain names into IP addresses so computers can locate servers.

---

### 56.

FTP (File Transfer Protocol) is used to transfer files between computers over a network.

---

### 57.

SMTP (Simple Mail Transfer Protocol) is used to send emails between mail servers.

---

### 58.

| HTTP                                     | HTTPS                             |
| ---------------------------------------- | --------------------------------- |
| Data is sent in plain text               | Data is encrypted                 |
| Less secure                              | More secure                       |
| Uses HTTP only                           | Uses HTTP with TLS                |
| Suitable for non-sensitive communication | Suitable for secure communication |

---

### 59.

| TCP                        | UDP                             |
| -------------------------- | ------------------------------- |
| Reliable communication     | Fast communication              |
| Guarantees delivery        | Does not guarantee delivery     |
| Packets arrive in order    | Packets may arrive out of order |
| Used for websites and APIs | Used for streaming and gaming   |

---

### 60.

| FTP                                  | SMTP                   |
| ------------------------------------ | ---------------------- |
| Transfers files                      | Sends emails           |
| Used for uploading/downloading files | Used for mail delivery |
| File communication                   | Email communication    |

---

### 61.

HTTPS encrypts communication using TLS, protecting sensitive information such as passwords and personal data from being intercepted.

---

### 62.

Websites use TCP because webpages and API responses must arrive completely, correctly, and in the proper order.

---

### 63.

Online games prefer UDP because speed and low latency are more important than retransmitting every lost packet.

---

### 64.

Humans remember domain names more easily than IP addresses. DNS translates domain names into IP addresses so computers can locate servers.

---

### 65.

When you type `google.com`, the browser asks DNS for Google's IP address, establishes a TCP connection, performs a TLS handshake (for HTTPS), sends an HTTP request, receives the response, and renders the webpage.

---

# Module 2 – Client–Server Architecture

## 2.1 What is a Client?

### 66.

A client is a device or software application that initiates communication by requesting resources or services from a server.

---

### 67.

A client collects user input, creates requests, sends them to servers, receives responses, and presents the results to the user.

---

### 68.

Yes. A Python script can send HTTP requests to APIs, making it a client.

---

### 69.

Yes. One backend service can request data or functionality from another backend service, acting as a client.

---

### 70.

Yes. IoT devices such as smart watches, sensors, and smart home devices send data to servers and therefore act as clients.

---

### 71.

The client initiates communication because it is the component that needs a resource or service. The server waits until a client requests something.

---

### 72.

A browser is considered a client because it creates HTTP requests, sends them to servers, receives responses, and displays the results to users.

---

### 73.

Yes. A device or application can act as both a client and a server depending on the interaction. For example, a FastAPI application acts as a server to a browser but may act as a client when calling another API.

---

## 2.2 What is a Server?

### 74.

A server is a computer or software application that listens for incoming requests, processes them, and returns responses to clients.

---

### 75.

A server listens for requests, receives them, executes business logic, communicates with databases or external services, and sends responses back to clients.

---

### 76.

The listening state is the condition in which a server waits for incoming client requests while keeping a network port open.

---

### 77.

A server spends most of its time waiting because it only performs work when a client sends a request.

---

### 78.

After receiving a request, the server analyzes it, performs validation and business logic, interacts with the database if required, generates a response, and sends it back to the client.

---

### 79.

A server's primary role is to provide services, not request them. Therefore, it waits for clients to initiate communication.

---

### 80.

A server is designed to accept and process requests from many different clients, allowing multiple users to access the same application simultaneously.

---

## 2.3 Client–Server Communication

### 81.

A request is a message sent by a client asking a server to perform an action or provide a resource.

---

### 82.

A response is the server's reply to a client's request, containing the requested data, a status message, or an error.

---

### 83.

Stateless communication means each request is independent. The server does not automatically remember information from previous requests.

---

### 84.

A request may contain an HTTP method, URL, headers, query parameters, cookies, and an optional request body.

---

### 85.

A response may contain data (HTML, JSON, images, files), response headers, HTTP status codes, and error messages.

---

### 86.

The client sends login credentials to the server. The server validates the credentials, checks the database, generates an authentication token if successful, and returns a response to the client.

---

### 87.

The browser sends a search request to Google's servers. Google processes the query, finds matching results, creates a response, and the browser displays the search results.

---

### 88.

HTTP is called stateless because each request is processed independently, without automatically remembering previous interactions.

---

### 89.

Applications remember users by using technologies such as cookies, sessions, or authentication tokens, while the underlying HTTP protocol remains stateless.

---

# Module 3 – Backend Engineering

## 3.1 Where Does Backend Fit?

### 90.

The backend sits between the frontend and the database. It receives client requests, processes business logic, communicates with databases or external services, and returns responses.

---

### 91.

The frontend is the part of an application that users interact with directly. It displays information, accepts user input, and communicates with the backend.

---

### 92.

The backend is the server-side part of an application responsible for processing requests, executing business logic, accessing databases, and generating responses.

---

### 93.

A database is a system that stores and manages persistent application data such as users, products, orders, and messages.

---

### 94.

Infrastructure refers to the hardware and software environment that allows applications to run, including servers, operating systems, networking, storage, and cloud services.

---

### 95.

A web server receives HTTP/HTTPS requests, serves static content, manages HTTPS, and forwards dynamic requests to an application server.

---

### 96.

An application server runs the backend application, executes business logic, communicates with databases, and generates responses.

---

### 97.

| Frontend                   | Backend            |
| -------------------------- | ------------------ |
| User Interface             | Business Logic     |
| Runs in the browser or app | Runs on the server |
| Sends requests             | Processes requests |
| Displays data              | Generates data     |

---

### 98.

| Web Server             | Application Server      |
| ---------------------- | ----------------------- |
| Receives HTTP requests | Runs backend code       |
| Serves static files    | Executes business logic |
| Handles HTTPS          | Accesses databases      |
| Example: Nginx         | Example: Uvicorn        |

---

### 99.

Allowing the frontend to access the database directly would expose sensitive data, bypass business rules, and create serious security risks. The backend acts as a secure intermediary.

---

### 100.

Separating the frontend, backend, and database improves security, maintainability, scalability, testing, and code organization.

---

## 3.2 Responsibilities of Backend

### 101.

Business logic is the collection of rules that determine how an application behaves and how requests should be processed.

---

### 102.

Authentication is the process of verifying a user's identity by checking credentials such as usernames, passwords, or authentication tokens.

---

### 103.

Authorization determines what actions an authenticated user is permitted to perform within the application.

---

### 104.

Validation checks whether incoming data is complete, correctly formatted, and satisfies the application's rules before processing it.

---

### 105.

The backend communicates with the database to create, read, update, and delete application data while enforcing business rules.

---

### 106.

An API response is the data returned by the backend after processing a request. It may contain JSON, HTML, files, images, status information, or error messages.

---

### 107.

Error handling allows the backend to detect problems, prevent application crashes, return meaningful error messages, and improve reliability and debugging.

---

### 108.

| Authentication         | Authorization                   |
| ---------------------- | ------------------------------- |
| Verifies identity      | Verifies permissions            |
| Answers "Who are you?" | Answers "What can you do?"      |
| Happens first          | Happens after authentication    |
| Example: Login         | Example: Delete User permission |

---

### 109.

When a user clicks **"Buy Now"**, the backend authenticates the user, validates the request, checks inventory, calculates the total price, processes payment, stores the order in the database, and returns a confirmation response.

---

### 110.

For a login request, the backend receives the credentials, validates them, checks the database, verifies the password, generates an authentication token if successful, and sends the response back to the client.

---

### 111.

Validation prevents invalid or malicious data from entering the system, improves data quality, enhances security, and reduces unexpected application errors.

---

## 3.3 What Backend Does NOT Do

### 112.

No. DNS resolution happens before the request reaches the backend. It is handled by the browser, operating system, and DNS infrastructure.

---

### 113.

No. TCP connections are established by the operating system and networking stack before the backend application begins processing the request.

---

### 114.

Usually no. TLS handshakes are commonly handled by web servers, reverse proxies, or load balancers before requests are forwarded to the backend.

---

### 115.

No. The backend generates content such as HTML or JSON, but the browser is responsible for rendering webpages on the user's screen.

---

### 116.

No. Internet routing is performed by routers, ISPs, and networking infrastructure, not by backend applications.

---

### 117.

Browser rendering depends on the client's rendering engine. The backend only provides data—it does not control how browsers display that data.

---

### 118.

DNS is part of the Internet's networking infrastructure. Its responsibility is translating domain names into IP addresses before communication with the backend begins.

---

### 119.

Web servers and reverse proxies are optimized for managing HTTPS certificates and encrypted communication, allowing backend applications to focus on business logic.

---

# Module 4 – Journey of a Request

### 120.

A user performs an action, the browser creates an HTTP request, DNS resolves the domain name, TCP establishes a connection, TLS secures it (for HTTPS), the request reaches the web server, then the application server, the backend executes business logic, communicates with the database if needed, creates a response, and sends it back to the browser for rendering.

---

### 121.

DNS converts a human-readable domain name into an IP address so the browser knows where to send the request.

---

### 122.

TCP establishes a reliable connection between the client and server, ensuring packets are delivered correctly and in order.

---

### 123.

TLS encrypts communication between the client and server, protecting sensitive information during transmission.

---

### 124.

The web server receives incoming HTTP/HTTPS requests, handles tasks such as HTTPS termination and static files, and forwards application requests to the application server.

---

### 125.

The application server runs the backend application, passes requests to the backend code, and returns generated responses.

---

### 126.

The backend performs business logic, validation, authentication, authorization, database communication, and response generation.

---

### 127.

The database stores persistent application data and returns requested information to the backend when queried.

---

### 128.

A complete request lifecycle includes: User → Browser → DNS → TCP → TLS → Internet → Web Server → Application Server → Backend → Database → Backend → Response → Browser → Render → User.

---

# Module 5 – Browser Basics

### 129.

A browser is a client application that retrieves resources from servers, renders webpages, executes JavaScript, and allows users to interact with websites.

---

### 130.

A browser accepts user input, creates requests, communicates with servers, receives responses, renders webpages, stores cookies, manages cache, and provides developer tools.

---

### 131.

The Address Bar is where users enter URLs, IP addresses, or search queries to access web resources.

---

### 132.

The Browser Engine coordinates the browser's major components, including networking, rendering, and JavaScript execution.

---

### 133.

The Networking Layer is responsible for sending HTTP requests, receiving responses, managing network communication, and downloading resources.

---

### 134.

Developer Tools (DevTools) are built-in browser utilities used to inspect, debug, and analyze web applications.

---

### 135.

The Network Tab displays every network request and response, allowing developers to inspect URLs, methods, headers, status codes, request bodies, response bodies, and timing information.

---

### 136.

Open the Network Tab, reproduce the problem, inspect whether the request was sent, verify the URL and HTTP method, check the status code, and examine the request and response data to identify the issue.

---

### 137.

After pressing Enter, the browser processes the URL, performs DNS lookup, establishes a connection, sends an HTTP request, receives the response, and renders the webpage.

---

# Module 6 – Development Environment

### 138.

A development environment is the complete setup used to build, run, test, and debug software before deploying it to production.

---

### 139.

Local development means running and testing an application on your own computer instead of on a public server.

---

### 140.

**localhost** is a special hostname that always refers to the computer currently running the application.

---

### 141.

**127.0.0.1** is the loopback IP address that points back to the same computer, serving the same purpose as localhost in most situations.

---

### 142.

A port is a logical communication endpoint that identifies a specific application or service running on a computer.

---

### 143.

| localhost                     | 127.0.0.1                    |
| ----------------------------- | ---------------------------- |
| Hostname                      | IP Address                   |
| Human-readable                | Numeric loopback address     |
| Usually resolves to 127.0.0.1 | Represents the local machine |

---

### 144.

| Development           | Production                            |
| --------------------- | ------------------------------------- |
| Local machine         | Public server                         |
| Used for testing      | Used by real users                    |
| Frequent code changes | Stable, tested code                   |
| Safe to experiment    | Focus on reliability and availability |

---

### 145.

Developers use localhost to build and test applications safely on their own computers without affecting real users or requiring Internet access.

---

### 146.

Ports allow multiple applications to run on the same computer simultaneously by giving each application its own communication endpoint.

---

### 147.

Developers avoid building directly on production servers because mistakes could affect real users. Local development allows safe testing, debugging, and iterative improvements before deployment.

---

# End of Answers.md

Congratulations! 🎉

You now have a complete revision companion covering **Modules 1–6**. Use it alongside **Questions.md** by attempting each question from memory first, then checking these concise answers to reinforce your understanding.
