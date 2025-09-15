### **Web/HTTP Standards: 20 Theoretical & Conceptual Questions**

**1. Q: What is HTTP and what is its fundamental purpose?**
*   **A:** HTTP (Hypertext Transfer Protocol) is the application-layer protocol that forms the foundation of data communication for the World Wide Web. Its fundamental purpose is to define a standard way for a **client** (like a web browser) to request resources from a **server** and for the server to respond with those resources.

**2. Q: What does it mean for HTTP to be a "stateless" protocol?**
*   **A:** "Stateless" means that the server does not keep any memory or state about past requests from a client. Each request from a client is treated as a completely independent transaction. If state is needed (like for a user login session), it must be managed externally, typically using cookies or tokens sent with each request.

**3. Q: What are the main components of an HTTP request?**
*   **A:** An HTTP request consists of three main parts:
    1.  **Request Line:** Contains the HTTP method (e.g., `GET`), the request URI (the path to the resource, e.g., `/users/123`), and the HTTP version (e.g., `HTTP/1.1`).
    2.  **Headers:** Key-value pairs that provide additional information about the request, such as the `Host`, `User-Agent`, and `Accept` content types.
    3.  **Body (Optional):** Contains the data being sent to the server, used with methods like `POST` and `PUT`.

**4. Q: What are the main components of an HTTP response?**
*   **A:** An HTTP response consists of three main parts:
    1.  **Status Line:** Contains the HTTP version, a status code (e.g., `200`), and a status text (e.g., `OK`).
    2.  **Headers:** Key-value pairs that provide information about the response, such as `Content-Type`, `Content-Length`, and caching directives.
    3.  **Body (Optional):** Contains the actual resource being sent back to the client (e.g., HTML, JSON, an image).

**5. Q: What is the purpose of HTTP methods? Name the most common ones.**
*   **A:** HTTP methods (or verbs) define the desired **action** to be performed on a specified resource. The most common methods are:
    *   **GET:** Retrieve a resource.
    *   **POST:** Submit a new entity to a resource, often causing a change in state or side effects on the server.
    *   **PUT:** Replace an existing resource with a new representation.
    *   **DELETE:** Delete a specified resource.
    *   **PATCH:** Apply partial modifications to a resource.
    *   **OPTIONS:** Describe the communication options for the target resource.
    *   **HEAD:** Same as `GET` but without the response body; used to check resource metadata.

**6. Q: What is the difference between `GET` and `POST`?**
*   **A:**
    *   `GET`: Used for requesting data. Data is sent in the URL's query string. `GET` requests should be idempotent and are cacheable. They have a length limit and are not secure for sensitive data.
    *   `POST`: Used for submitting data to be processed. Data is sent in the request body. `POST` requests are not idempotent (running it twice may create two resources), are not cached, have no data size limit, and are used for sensitive information.

**7. Q: What does it mean for an HTTP method to be "idempotent"?**
*   **A:** An HTTP method is idempotent if making the same request multiple times produces the **same result** as making it once. `GET`, `PUT`, `DELETE`, and `HEAD` are idempotent. `POST` is not idempotent because calling it multiple times will likely create multiple resources.

**8. Q: What does it mean for an HTTP method to be "safe"?**
*   **A:** A method is "safe" if it is a read-only operation that does not change the state of the resource on the server. `GET` and `HEAD` are safe methods.

**9. Q: Explain the five categories of HTTP status codes.**
*   **A:**
    *   **1xx (Informational):** The request was received, and the process is continuing. (Rarely seen).
    *   **2xx (Success):** The request was successfully received, understood, and accepted. (e.g., `200 OK`, `201 Created`).
    *   **3xx (Redirection):** Further action needs to be taken by the client to complete the request. (e.g., `301 Moved Permanently`, `302 Found`).
    *   **4xx (Client Error):** The request contains bad syntax or cannot be fulfilled. (e.g., `400 Bad Request`, `401 Unauthorized`, `404 Not Found`).
    *   **5xx (Server Error):** The server failed to fulfill an apparently valid request. (e.g., `500 Internal Server Error`, `503 Service Unavailable`).

**10. Q: What is the difference between status codes `401 Unauthorized` and `403 Forbidden`?**
*   **A:**
    *   `401 Unauthorized`: The client must authenticate itself to get the requested response. This means the client has not provided credentials or the credentials are invalid. The client can try again with proper authentication.
    *   `403 Forbidden`: The server understands the request, but refuses to authorize it. This means the client's identity is known, but they do not have the necessary permissions to access the resource. Authenticating again will not help.

**11. Q: What are HTTP headers? Provide examples of a request and response header.**
*   **A:** HTTP headers are key-value pairs that pass additional information between the client and the server.
    *   **Request Header Example:** `User-Agent: Mozilla/5.0 ...` (tells the server what browser is being used).
    *   **Response Header Example:** `Content-Type: application/json` (tells the client what kind of data is in the response body).

**12. Q: What is the purpose of the `Content-Type` header?**
*   **A:** The `Content-Type` header indicates the media type of the resource in the body of the message. In a request, it tells the server what kind of data is being sent (e.g., `application/json`). In a response, it tells the client how to interpret the data (e.g., `text/html`, `image/jpeg`).

**13. Q: How does HTTPS work at a high level?**
*   **A:** HTTPS (HTTP Secure) encrypts the HTTP communication using SSL/TLS (Transport Layer Security). The process involves an "SSL handshake" where the client and server use public-key cryptography to agree on a shared secret key. This symmetric key is then used to encrypt all subsequent communication, providing confidentiality, integrity, and authentication.

**14. Q: What are cookies used for?**
*   **A:** Cookies are small pieces of data that a server sends to a client's web browser. The browser stores the cookie and sends it back to the same server with every subsequent request. They are used to maintain state in the stateless HTTP protocol, primarily for session management (user logins), personalization, and tracking.

**15. Q: What is CORS (Cross-Origin Resource Sharing)?**
*   **A:** CORS is a browser security mechanism that controls how a web page in one origin (domain) can request resources from a different origin. By default, browsers block such cross-origin requests. A server must include specific CORS headers (like `Access-Control-Allow-Origin: *`) in its response to explicitly allow a different origin to access its resources.

**16. Q: What is a "preflight request"?**
*   **A:** A preflight request is an `OPTIONS` request that the browser automatically sends for certain "non-simple" cross-origin requests (e.g., those using methods other than `GET`/`POST`, or with custom headers). The server responds to the `OPTIONS` request, indicating whether the actual request is safe to send. This is a security measure to protect servers that may not understand CORS.

**17. Q: What is the difference between HTTP/1.1 and HTTP/2?**
*   **A:** HTTP/2 is a major revision of HTTP that improves performance. Key differences include:
    *   **Multiplexing:** Allows multiple requests and responses to be sent in parallel over a single TCP connection, eliminating the "head-of-line blocking" problem of HTTP/1.1.
    *   **Binary Protocol:** It uses a binary format instead of plain text, which is more efficient to parse.
    *   **Header Compression:** It compresses headers to reduce overhead.
    *   **Server Push:** Allows the server to proactively send resources to the client that it knows will be needed.

**18. Q: What are WebSockets? How are they different from HTTP?**
*   **A:** WebSockets provide a **full-duplex, persistent communication channel** over a single TCP connection. Unlike the request-response model of HTTP, WebSockets allow both the client and server to send data to each other at any time. This is ideal for real-time applications like chat apps, live notifications, and online gaming.

**19. Q: What is a RESTful API?**
*   **A:** A RESTful API is an architectural style for designing APIs that uses HTTP requests to access and use data. It follows a set of constraints:
    *   **Client-Server Architecture:** Separation of concerns.
    *   **Statelessness:** Each request is self-contained.
    *   **Cacheability:** Responses can be cached.
    *   **Uniform Interface:** Uses standard resource identifiers (URIs) and HTTP methods in a consistent way (e.g., `GET /users` to list users).

**20. Q: What is caching, and what is the purpose of the `ETag` header?**
*   **A:** Caching is the process of storing copies of files in a temporary storage location (a cache) so they can be accessed more quickly. The `ETag` (Entity Tag) is a response header that provides a unique identifier for a specific version of a resource. When a client wants to re-request that resource, it sends the `ETag` value in an `If-None-Match` request header. If the resource hasn't changed, the server responds with a `304 Not Modified` status and an empty body, saving bandwidth.