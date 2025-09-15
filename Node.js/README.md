### **Node.js: 20 Theoretical & Conceptual Questions**

**1. Q: What is Node.js? Is it a framework or a language?**
*   **A:** Node.js is neither a framework nor a language. It is a **JavaScript runtime environment** built on Google's V8 JavaScript engine. It allows developers to run JavaScript code on the server-side, outside of a web browser.

**2. Q: Explain the key architectural concepts of Node.js: single-threaded, event-driven, and non-blocking I/O.**
*   **A:**
    *   **Single-Threaded:** Node.js operates on a single main thread for executing JavaScript code. This means it doesn't create a new thread for every request, which saves memory.
    *   **Event-Driven:** Node.js uses an event loop. When an asynchronous operation (like a database query) is initiated, it registers a callback function and continues executing other code. When the operation completes, an event is placed in the event queue, and the event loop executes the corresponding callback.
    *   **Non-Blocking I/O:** This is the core of Node.js's performance. Instead of waiting for a long-running I/O operation (like reading a file) to complete, Node.js offloads the operation to the system's kernel (via libuv). The main thread is free to handle other requests. This model makes Node.js highly efficient for I/O-bound applications.

**3. Q: What is the Event Loop?**
*   **A:** The event loop is the mechanism that allows Node.js to perform non-blocking I/O operations despite being single-threaded. It's an infinite loop that constantly checks for and processes events from an event queue. When the main call stack is empty, the event loop picks up events (like a completed file read or an incoming HTTP request) and pushes their associated callback functions onto the stack for execution.

**4. Q: What is "callback hell" and how can it be avoided?**
*   **A:** "Callback hell" (or the pyramid of doom) describes a situation where multiple nested callbacks make the code hard to read, maintain, and debug. It can be avoided by using modern asynchronous patterns:
    *   **Promises:** Objects that represent the eventual completion (or failure) of an asynchronous operation. They can be chained together with `.then()` and have a `.catch()` for error handling.
    *   **Async/Await:** Syntactic sugar built on top of Promises. It allows you to write asynchronous code that looks and behaves like synchronous code, making it much more readable and easier to reason about.

**5. Q: What is the difference between CommonJS (`require`) and ES Modules (`import`/`export`)?**
*   **A:** These are two different module systems for JavaScript.
    *   **CommonJS (CJS):** The original module system in Node.js. It uses `require()` to import modules and `module.exports` to export them. It is synchronous.
    *   **ES Modules (ESM):** The official standard for JavaScript modules. It uses `import` and `export` statements. It is asynchronous and has features like static analysis and tree-shaking. Modern Node.js versions support both.

**6. Q: What is the purpose of `package.json`?**
*   **A:** `package.json` is the manifest file for a Node.js project. It contains essential metadata, including:
    *   Project name, version, and description.
    *   The project's dependencies (`dependencies`) and development dependencies (`devDependencies`).
    *   Scripts for automating tasks (`scripts`), such as `npm start`.
    *   The entry point of the application (`main`).

**7. Q: What is the difference between `dependencies` and `devDependencies`?**
*   **A:**
    *   `dependencies`: Packages required for the application to run in production (e.g., `express`, `pg`). They are installed when someone runs `npm install`.
    *   `devDependencies`: Packages only needed for development and testing (e.g., `nodemon`, `jest`, `eslint`). They are installed by running `npm install` in the project root but are skipped when using the `--production` flag.

**8. Q: What are Streams in Node.js? Explain the four types.**
*   **A:** Streams are objects that let you read data from a source or write data to a destination in a continuous fashion. They are highly memory-efficient for handling large amounts of data. The four types are:
    *   **Readable:** Streams from which data can be read (e.g., `fs.createReadStream`).
    *   **Writable:** Streams to which data can be written (e.g., `fs.createWriteStream`).
    *   **Duplex:** Streams that are both readable and writable (e.g., a network socket).
    *   **Transform:** Duplex streams that can modify or transform the data as it is written and read (e.g., a zlib compression stream).

**9. Q: What are Buffers in Node.js?**
*   **A:** A Buffer is Node.js's way of handling binary data. Since JavaScript doesn't have a good built-in way to handle raw binary data, Node.js provides the `Buffer` class, which represents a fixed-size chunk of memory allocated outside the V8 JavaScript engine.

**10. Q: What is the role of the `libuv` library in Node.js?**
*   **A:** `libuv` is a C library that provides the asynchronous, non-blocking I/O capabilities for Node.js. It manages the event loop and a thread pool for offloading operations that cannot be handled asynchronously by the OS kernel (like certain file system operations or DNS lookups).

**11. Q: How does Node.js handle concurrency if it is single-threaded?**
*   **A:** Node.js achieves concurrency using two main mechanisms:
    1.  **The Event Loop:** For I/O-bound tasks, it uses non-blocking APIs. The work is offloaded to the kernel, and the event loop allows the single thread to serve other requests while waiting.
    2.  **Worker Threads:** For CPU-bound tasks (like complex calculations), you can use the `worker_threads` module to spawn separate threads that run in parallel, preventing the main thread from being blocked.

**12. Q: What is the `child_process` module used for?**
*   **A:** The `child_process` module allows you to spawn and interact with separate operating system processes. This is useful for running external commands or scripts (like a Python script) or for creating child processes to leverage multiple CPU cores.

**13. Q: What is the Node.js Event Emitter?**
*   **A:** The `EventEmitter` is a core class in Node.js that facilitates the event-driven architecture. Many built-in objects (like HTTP servers and streams) inherit from it. It allows you to create, fire, and listen for your own custom events (`emitter.on()`, `emitter.emit()`).

**14. Q: How do you handle uncaught exceptions in a Node.js application?**
*   **A:** You can listen for the `uncaughtException` event on the global `process` object: `process.on('uncaughtException', (err) => { ... })`. However, the recommended practice is to treat this as a last resort for logging the error before gracefully shutting down the server. It is not a substitute for proper error handling with `try/catch` blocks and Promise `.catch()` chains.

**15. Q: What is the difference between `process.nextTick()` and `setImmediate()`?**
*   **A:** Both defer the execution of a function until a later point.
    *   `process.nextTick()`: Its callback is executed **immediately** after the current operation completes, before the event loop continues. It runs before any other I/O events or timers.
    *   `setImmediate()`: Its callback is placed in the "check" phase of the event loop and will execute on the next iteration of the loop, after any I/O event callbacks.

**16. Q: What is NPM?**
*   **A:** NPM (Node Package Manager) is the default package manager for Node.js. It is a command-line tool for installing, updating, and managing the packages (libraries and frameworks) your project depends on. It also refers to the online registry where these packages are hosted.

**17. Q: What are global modules in Node.js?**
*   **A:** Global modules are packages that are installed in a single system-wide location so that their commands can be run from any directory. They are typically command-line tools like `nodemon` or `create-react-app`. You install them using the `-g` flag (e.g., `npm install -g nodemon`).

**18. Q: What is the purpose of the `npm ci` command?**
*   **A:** `npm ci` (clean install) is used for installing dependencies in automated environments like continuous integration pipelines. It provides a faster, more reliable installation by deleting the `node_modules` folder and installing the exact package versions specified in the `package-lock.json` file. It does not modify the lock file.

**19. Q: How can you debug a Node.js application?**
*   **A:** Several methods exist:
    *   Using `console.log()` for simple debugging.
    *   Using Node.js's built-in debugger by running `node inspect <file.js>`.
    *   Using the Chrome DevTools for Node by running `node --inspect <file.js>` and connecting via Chrome.
    *   Using the integrated debugger in code editors like VS Code.

**20. Q: What are Worker Threads and when should you use them?**
*   **A:** Worker Threads are a module in Node.js that allows you to run JavaScript code in parallel on separate threads. You should use them for **CPU-intensive** tasks that would otherwise block the main event loop, such as complex mathematical calculations, image processing, or heavy data encryption. They are not suitable for I/O-bound tasks, as Node's native non-blocking I/O is more efficient for that.