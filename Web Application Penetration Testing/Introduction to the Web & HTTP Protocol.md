# Web Applications

## Introduction to Web App Security Testing

### Introduction to Web Application Security

**What are Web Applications?**

- Web applications are software programs that run ob web servers and are accessible over the internet thorugh web browsers.
- They are designed to provide interactive and dynamic functionality to users, allowing them to perform various tasks, access information, and interact with data online.
- Web applications have become an integral part of modern internet usage, and they power a wide range of online services and activities.
- Examples of web applications include:
  - Social media platforms
  - Online email services
  - E-commerce websites
  - Cloud-based productivity tools
 
---

### Web Application Security Testing

- Web application security testing is the process of evaluating and assessing the security aspects of web applications to identify vulnerabilities, weaknesses, and potential security risks.
- It involves conducting various tests and assessments to ensure that web applications are resistant to security threats and can effectively protect sensitive data and functionalities from unathorized access or malicious activities.
- The primary goal of web application security testing is to uncover security flaws before they are exploited by attackers.
- By identifying and addressing vulnerabilities, organizations can enhance the overall security posture of their web applications, reduce the risk of data breaches and unauthorized access, and protect their users and sensitive information.

---

#### Web Application Security Testing Types

- Web application security testing typically involves a combination of automated scanning tools and manual testing conducted on web applications include:
  - **Vulnerability Scanning:** Using automated tools to scan the web application for known vulnerabilities, such as SQL injection, Cross-Site Scripting (XSS), insecure configurations, and outdated software versions.
  - **Penetration Testing:** Simulating real-world attacks to assess the application's defenses and identify potential security weaknesses. This involves ethical hacking to gain insights into how an attacker might exploit vulnerabilities.
  - **Code Review and Static Analysis:** Manual examination of the application's source code to identify coding flaws, security misconfigurations, and potential security risks.
  - **Authentication and Authorization Testing:** Evaluating the effectiveness of authentication mechanisms and access control features to ensure that only authorized users have appropriate access levels.
  - **Input Validation and Output Encoding Testing:** Assessing how the application handles user inputs to prevent common security vulnerabilities like XSS and SQL injection.
  - **Session Management Testing:** Verifying how the application manages user sessions and related tokens to prvent session-related attacks.
  - **API Security Testing:** Assessing the security of APIs (Application Programming Interfaces) used by the web application for data exchange and integration with other systems.

---

#### Web Application Penetration Testing

- Web application pentesting, is a subset of web application security testing that spesifically invovles attempting to exploit identified vulnerabilities.
- It is a simulated attack on the web application conducted by skilled security professionals known as pentesters, bug bounty hunters or ethical hackers.
- The process involves a systematic and controlled approach to assess the applicaiton's security by attempting to exploit known vulnerabilities.

---

#### Web App Pentesting vs Web App Security Testing

- Key differences between web app security testing and web app pentesting:
  **Scope:** Web application security testing covers a broader range of assessments, including static and dynamic analysis, when web application pentesting focuses on actively exploiting vulnerabilities.
  **Objective:** The primary goal of security testing is to identify weaknesses, whereas pentesting aims to validate vulnerabilities and assess the organization's ability to detect and respond to attacks.
  **Methodology:** Security testing includes both manual and automated techniques, while pentesting is predominantly a manual process, involving the use of various tools and techniques for exploitaiton.
  **Exploitation:** Security testing does not involve exploitation of vulnerabilities, while pentesting does, albeit in a controller and authorized manner.


![image](https://github.com/user-attachments/assets/dcb63e5c-cccb-478e-940a-b6ff72065bb1)

---

### Common Web Application Threats & Risks

- Given the increased adoption of web applications, it comes as no surprise that web apps are constantly exposed to various security threats and risks due to their widespread accessibility and the valuable data they process.
- Understanding these common security threats is crucial for developers, security professionals, and organization to implement effective measures and safeguard their web applications.
- The actual impact and severity of each threat may vary depending on the specific web application and its security measures.
- Web application security requires a proactive and comprehensive approach to mitigate these threats and protect sensitive data and user interactions effectively.

---

#### Threat vs Risk

- **Threat:**
  - A threat refers to any potential source of harm or adverse event that may exploit a vulnerability in a system or organization's security measures.
  - Threats can be human-made, such as cybercriminals, hackers, or insiders with malicious intent, or they can be natural, such as floods, earthquakes, or power outages.
  - In the context of cybersecurity, threats can include various types of attacks, like malware infections, phishing attemps, denial-of-service attacks, and data breaches.

- **Risk:**
  - Risk is the potential for a loss or harm resulting from a threat exploiting a vulnerability in a system or organization.
  - It is a combination of the likelihood or probability of a threat ocurrence and the impact or severity of the resulting adverse event.
  - Risk is often measured in terms of the likelihood of an incident happening and the potential magnitude of its impact.

- In summary, a threat is a potential danger or harmful event, while risk is the probability and potential impact of that event happening.
- Threats can exist, but they may or may not pose a significant risk depending on the vulnerabilities and security measures in place to mitigate them.

---

#### Common Web Application Threats & Risks


![image](https://github.com/user-attachments/assets/be374392-b92a-4670-82bc-41abc3d473af)


![image](https://github.com/user-attachments/assets/99ce0fb5-3097-48e1-9117-9d3510472434)


- These security threats are just some of the many risks that web apps face.
- To address these challenges, organizations should adopt a multi-layered security approach, including secure coding practices, regular security testing, user education on security best practices, and the continous monitoring and updating of web application components and infrastructure.
- Being proactive and staying informed about emerging threats is crucial for maintaining the security and integrity of web applications in a ever-evolving threat landscape.
- From the perspective of a web app pentester, it is important to get a firm grasp of the top/common threats faced by web apps.

---

## Web Application Architecture & Components

### Web Application Architecture

- Web application architecture refers to the structure and organization of components and technologies used to build a web application.
- It defines how different parts of the application interact with each other to deliver its functionality, handle user requests, and manage data.
- A well-designed web application architecture is cruical for ensuring scalability, maintainability, and security.
- Before performing a security assessment on a web application, it is vitally important to know how web applications work with regards to the underlying architecture. This knowledge will provide you with a much better understanding of where and how to identify and exploit potential vulnerabilities or misconfigurations in web applications.

---

#### Client-Server Model

- Web application are typically built on the client-server model. In this architecture, the web application is divided into two main components:
  - **Client:** The client represents the user interface and user interaction with the web application. It is the front-end od the application that users access through their web browsers. The client is responsible for displaying the web pages, handling user input, and sending requests to the server for data or for actions.
  - **Server:** The server represents the back-end of the web application. It processes client requests, executres the application's business logic, communicates with databases and other services, and generates responses to be sent back to the client.


![grafik](https://github.com/user-attachments/assets/7708f0fb-9af0-44c8-8a14-6be07fc39d88)


### Web Application Components


![grafik](https://github.com/user-attachments/assets/aa0fb5fa-baeb-4e44-b2a0-1fe8a1fbfc72)


#### Client-side Processing

- Client-side processing involves executing tasks and computations on the user's device, typically within their web browser.
- The client-side refers to the user's end of the web application, where the web browser and user interface reside.
- Client-side processing has some limitations. It is not suitable for handling sensitive or critical operations, as it can be easily manipulated by users or malicious actors. (Cross-Side Scripting)

- Key characteristics of client-side processing:
  - **User Interaction:** Client-side processing is well-suited for tasks that require immediate user interaction and feedback, as there is no need to send data back and forth to the server.
  - **Responsive User Experience:** Since processing happens locally, client-side operations can provide a smoother and more responsive user experience.
  - **JavaScript:** JavaScript is the primary programming language used for client-side processing. it allows developers to manipulate the web page's content, handle user interactions, and perform validations without involvin the server.
  - **Data Validation:** Client-side validation ensures that user input meets specific criteria before it is sent to the server, reducing the need to make unnecessary server requests.

---

#### Server-side Processing

- Server-side processing involves executing tasks and computations on the web server, which is the remote computer where the web application is hosted.
- The server-side refers to the backend of the web application, where the business logic and data processing take place.

- Key characteristics of server-side processing:
  - **Data Processing:** Server-side processing is ideal for tasks that involve sensitive data handling, complex computations, and interactions with databases or external services.
  - **Security:** Since server-side code is executed on a trusted server, it is more secure than client-side code, which can be manipulated by users or intercepted by attackers.
  - **Server-side Languages:** Programming languages like PHP, Python, Java, Ruby, and others are commonly used for server-side processing.
  - **Data Storage:** Server-side processing enables secure storage and management of sensitive data in databases or other storage systems.

---

#### Communication & Data Flow

- Web applications communicate over the internet using HTTP (Hyptertext Transfer Protocol).
- When a user interacts with the web application by clicking on links or submitting forms, the client sends HTTP requests to the server.
- The server processes these requests, interacts with the database if necessary, performs the required actions, and generates an HTTP response.
- The response is then sent back to the client, which renders the content and presents it to the user.

---

### Web Application Technologies - Part I

#### Client-Side Technologies

- HTML is the markup language used to structure and define the content of web pages. It provides the foundation for creating the layout and structure of the UI.
- CSS is used to define the presentation and styling of web pages. It allows developers to control the colors, fonts, layout, and other visual aspects of the UI.
- JavaScript - JavaScript is a scripting language that enables interactivity in web applications. It is used to create dynamic and responsive UI elements, handle user interactions, and perform client-side validations.
- Cookies and Local Storage - Cookies and local Storage are client-side mechanisms to store small amounts of data on the user's browser. They are often used to store small amounts of data on the user's browser. They are often used for session management and remembering user preferences.

---

#### Server-Side Technologies

- Web Server- The web server is responsible for recieving and responding to HTTP requests from clients (web browsers). It hosts the web application's files, processes requests ,and sends responses back to clients. (Apache2, Nginx, Microsoft IIS etc)
- Application Server - The application server runs the business logic of the web application. It processes user requests, accesses databases, and performs computations to generate dynamic contect that the web server can serve to clients.
- Database Server - The database server stores and manages the web application's data. It stores user information, content, configurations, and other relevant data required for the application's operation. (MySQL, PostgreSQL, MSSQL, Oracle etc.)

---

#### Server-Side Technologies

- Server-side Scripting Languages - Server-side scripting languages (e.g., PHP, Python, Java, Ruby) are used to handle server-side processing. They interact with databases, perform validations, and generate dynmaic content before sending it to the client.

---

#### Communication & Data Flow

- Web applications communicate over the internet using HTTP.
- When a user interacts with the web application by clicking on links or submitting forms, the client sends HTTP requests to the server.
- The server processes these requests to the server.
- The server processes these requests, interacts with the database if necessary, performs the required actions, and generates an HTTP response.
- The response is then sent back to the client, which renders the content and presents it to the user.

---

#### Data Interchange

- Data interchange refers to the process of exchanging data between different computer systems or applications, allowing them to communicate and share information.
- It is a fundamental aspect of modern computing, enabling interoperarability and data sharing between diverse systems, platforms, and technologies.
- Data interchange involves the convesion of data from one format to another, making it compatile with the recieving system.
- This ensures that data can be interpreted and utilized correctly by the recipient, regardless of the differences in their data structures, programming languages, or operating systems.

---

#### Data Interchange Technologies

- APIs (Application Programming Interfaces) - APIs allow different software systems to interact and exchange data. Web applications use APIs to integrate with external services, share data, and provide functionalities to other applications.

---

#### Data Interchange Protocols

- **JSON** - JSON is a lightweight and widely used data interchange format that is easiy for both humans and machines to read and write. It is based on JavaScript syntax and primarly used for transmitting data between a server and a web application as an alternative to XML.
- **XML** - XML is a versatile data interchange format that uses tags to define the structure of the data. It allows users to create their custom tags to define the structure of the data. It allows users to create their custom tags and define complex hierarchical data structures. XML is commonly used for configuration files, web services and data exchange between different systems.
- **REST** - REST is a software architectural style that uses standard HTTP methods (GET, POST, PUT, DELETE) for data interchange. It is widely used for creating web APIs that allow applications to interact and exchange data over the internet.
- SOAP (Simple Object Access Protocol) - SOAP is a protocol for exchanging structured information in the implementation of web services. It uses XML as the data interchange format and provides a standarized method for communication between different systems.

---

#### Security Technologies

- **Authentication and Authorization Mechanisms** - Authentication verifies the identity of users, while authorization controls access to different parts of the web application based on user roles and permissions.
- **Encryption (SSL/TLS)** - SSL (Secure Socket Layer) or TLS (Transport Layer Security) is used to encrypt data transmitted between the client and server, ensuring secure communication and data protection.

---

#### External Technologies

- **Content Delivery Networks (CDNs)** - CDNs are used to distribute static content (e.g., images, CSS files, JavaScript libraries) to multiple servers located worldwide, improving the web application's performance and reliability.
- **Third-Party Libraries and Frameworks:** Web applications often leverage third-party libraries and frameworks to speed up development and access advanced features.

---

### Web Application Architecture


![grafik](https://github.com/user-attachments/assets/cff9ba50-b5b9-48e3-b3c1-a91bdeee492d)


### How Web Pages Are Rendered


![grafik](https://github.com/user-attachments/assets/3208956b-c605-4e41-a79d-5918135e6364)


### How Web Browsers Parse Responses


![grafik](https://github.com/user-attachments/assets/d39c2a00-66fa-4790-8174-8c8e0f3f1ecc)


# HTTP Protocol

## HTTP/S Protocol Fundamentals

### Introduction to HTTP

- HTTP (Hyptertext Transfer Protocol) is a stateless application layer protocol used for the transmission of resources like web application data and runs on top of TCP.
- It was specifically designed for communication between web browsers and web servers.
- HTTP utilizes the typical client-server architecture for communication, whereby the browser is the client, and the web server is the server.
- Resources are uniquely identified with a URL/URI.
- HTTP has 2 versions; HTTP 1.0 & HTTP 1.1.
  - HTTP 1.1 is the most widely used version of HTTP and has several advantage over HTTP 1.0 such as the ability to re-use the same connection and can request for multiple      URI's/Resources.

### HTTP Protocol Basics


![grafik](https://github.com/user-attachments/assets/ca028032-cd51-4009-9709-401da31654ba)


- During HTTP communication, the client and the server exchange messages, typically classified as HTTP requests and responses.
- The client sends requests to the server and gets back responses.


![grafik](https://github.com/user-attachments/assets/57c99574-6ef8-4443-8a0b-8af30065f640)

---

### HTTP Requests

#### HTTP Request Components

**Request Line**
- The request line is the first line of an HTTP request and contains the following three components:
  - **HTTP method/verb (e.g., GET, POST, PUT, DELETE, etc.):** Indicates the type of request being made.
  - **URL (Uniform Resource Locater):** The address of the resource the client wants to access.
  - **HTTP version:** The version of the HTTP protocol being used (e.g., HTTP/1.1).

**Request Headers**
- Headers provide additional information about the request. Common headers include:
  - **User-Agent:** Information about the client making the request (e.g., browser type).
  - **Host:** The hostname of the server.
  - **Accept:** The media types the client can handle in the response (e.g., HTML, JSON).
  - **Authorization:** Credentials for authentication, if required.
  - ** Cookie:** Information stored on the client-side and sent back to the server with each request.

**Request Body**
- Some HTTP methods (like POST or PUT) include a request body where data is sent to the server, typically in JSON or form data format.

---

#### HTTP Request Example

- Lets examine an HTTP request in detail. The following is the data contained in a request that we send when we navigate to www.google.com with a web browser.


![grafik](https://github.com/user-attachments/assets/9ef6cdd7-338b-4551-8fc3-d2cc74148aa7)


#### HTTP Request Headers

- An HTTP request to www.google.com is initiated. What you see here are the headers (HTTP Request Headers) for this request.
- Note that a connection to www.google.com on port 80 is initiated before sending HTTP commands to the webserver.


![grafik](https://github.com/user-attachments/assets/11d22966-6e34-42b4-8f98-d3b728caa15f)


#### HTTP Request Methods

- HTTP request methods (HTTP Verbs) provide a standarized way for clients and servers to communicate and interact with resources on the web. The choice needs to be performed on the resource.
- Get is the default request method usd when you make a request to a web application, in this case we are trying to connect to www.google.com


![grafik](https://github.com/user-attachments/assets/9bfa145a-d3f3-4a78-8f54-f93095ec3196)


### HTTP Request Methods Explained


![grafik](https://github.com/user-attachments/assets/0493ecbd-3c5d-48fe-9e54-3dd3c626ba57)


#### HTTP Request URL/Path

- The address of the resource/URI the client wants to access.
- The home page of a website is always "/". Other pages can be requested, of course, for example: /downloads/index.php.
- Your request always refers to the root folder to specify the requested file (hence the leading "/").


![grafik](https://github.com/user-attachments/assets/23e8dcfb-cc74-45f2-941e-4958792b8612)


#### HTTP Request Protocol

- This is the HTTP protocol version that your browser wants to communicate with (HTTP 1.0/HTTP 1.1).


![grafik](https://github.com/user-attachments/assets/7f10c841-f2fc-409e-8522-333aff3d4651)


#### HTTP Request Host Header

- This is the beginning of HTTP Request Headers. HTTP Headers have the following structure: Header-name:Header-Value.
- The Host header allows a web server to host multiple websites at a single IP address. Our browser is specifying in the Host header which website you are interested in.


![grafik](https://github.com/user-attachments/assets/de6566f9-98e0-4084-a04c-64ad44b618f7)


- After each request, you will find its corresponding value. In this case we want to access the Host www.google.com
- Note: Host value + Path combine to create the full URL you are requesting: the home page of www.google.com/


#### HTTP Request User-Agent Header

- The User-Agent is used to specify and send your browser, browser version, operating system and language to the remote web server.
- All web browsers have their own user-agent identification string. This is how most web sites recognize the type of browser in use.


![grafik](https://github.com/user-attachments/assets/3eec0d01-a3f0-47a5-9ce5-381aca58db2d)


#### HTTP Request Accept Header

- The Accept header is used by your browser to specify which document/file types are expected to be returned from the web server as a result of this request.


![grafik](https://github.com/user-attachments/assets/be8180d9-19e1-4cc0-9f47-c2d35d071a6c)


#### HTTP Request Accept-Encoding Header

- The Accept-Encoding header is similar to Accept, and is used to restrict the content encoding that is acceptable in the response.
- Content encoding is primarly used to allow a document to be compressed or transformed without losing the original format and without the loss of information


![grafik](https://github.com/user-attachments/assets/dd71d493-8f29-471c-b5a4-7e0a272d011e)


#### HTTP Request Connection Header

- When using HTTP 1.1, you can maintain/re-use the connection to the remote web server for an unspecified amount of time using the value "keep-alive".
- This indicates that all requests to the web server will continue to be sent through this connection without initiating a new (TCP) connection every time (as in HTTP 1.0)


![grafik](https://github.com/user-attachments/assets/117a43fe-e184-4b3d-9d17-113225290e56)

---

### HTTP Responses

#### HTTP Response Components

**Response Headers**

- Similar to request headers, response headers provide additional information about the response. Common headers include:
  - Content-Type: The media type of the response content (e.g., text/html, application/json).
  - Content-Length: The size of the response body in bytes.
  - Set-Cookie: Used to set cookies on the client-side for subsequent requests. | Cookie is always set by the web server.
  - Cache-Control: Directives for caching behavior.

**Response Body (Optional)**
- The reponse body contains the acutal content of the response. For example, in the case of an HTML page, the response body will contain the HTML markup.

---

#### HTTP Request & Response Example

- Tow that we know what an HTTP request comprises of, let us inspect HTTP responses.


![grafik](https://github.com/user-attachments/assets/724aff3a-66c1-4013-a4a2-20c0023a955d)


- In response to the HTTP Request, the web server will respond with the requested resource, preceded by a bunch of new HTTP response headers.
- These new response headers from the web server will be used by your web browser to interpret the content contained in the Response content/body of the response.
