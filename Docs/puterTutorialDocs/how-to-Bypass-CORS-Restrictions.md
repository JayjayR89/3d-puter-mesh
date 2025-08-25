# How to Bypass CORS Restrictions
[Tutorials](https://developer.puter.com/tutorials/)
------------------------

When building web applications, one of the common challenges developers inevitably face is making unrestricted HTTP requests to external APIs and services from the browser. The browser's built-in [`fetch()`](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) API is powerful, but it comes with significant limitations due to the [Same-Origin Policy](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy) and [CORS (Cross-Origin Resource Sharing)](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/CORS) restrictions. These security measures, while important, can be major roadblocks when you need to access resources from different domains or APIs that don't explicitly allow cross-origin requests.

This tutorial will show you how to use [Puter.js](https://developer.puter.com/)'s networking capabilities to make unrestricted HTTP requests directly from your frontend code, bypassing CORS limitations without needing a proxy server or backend implementation.

Getting Started with Puter.js
-----------------------------

To begin using Puter.js for unrestricted network requests, simply add it to your HTML file using the following script tag:

```
<script src="https://js.puter.com/v2/"></script>

```


That's it! You're now ready to start making CORS-free network requests. No API keys, no configuration, and no backend code required.

Example 1Making a simple request
--------------------------------

Let's start with a simple example. We'll make an HTTP GET request to `https://httpbin.org/get` and print the response to the console.

```
<html>
<body>
    <script src="https://js.puter.com/v2/"></script>
    <script>
        (async () => {
            // Send a GET request to httpbin.org/get
            const response = await puter.net.fetch('https://httpbin.org/get');

            // Get the response body as text
            const data = await response.text();

            // Print the response body as a code block
            puter.print(data, {code: true});
        })();
    </script>
</body>
</html>

```


As you can see, the [`puter.net.fetch()`](https://docs.puter.com/Networking/fetch/) function is a drop-in replacement for the native `fetch()` API. It's a simple function that takes a URL and returns a promise that resolves to a `Response` object.

Example 2Making a CORS-free request to example.com
--------------------------------------------------

In this example, we'll make a CORS-free request to example.com using `puter.net.fetch()` and compare the response to the response from the regular `fetch()` API which would fail due to CORS restrictions.

```
<html>
<body>
    <div id="output"></div>
    <script src="https://js.puter.com/v2/"></script>
    <script>
    (async () => {
        try {
            // (1) Use puter.net.fetch() to make a CORS-free request to example.com
            puter.print(`<h3>puter.net.fetch(): Response from example.com:</h3>`);
            const response = await puter.net.fetch('https://www.example.com/');
            const data = await response.text();
            
            puter.print(data, {code: true});

            // (2) Now try using the regular fetch API which would fail due to CORS restrictions
            puter.print(`<h3>fetch(): Response from example.com:</h3>`);
            const response_regular = await fetch('https://www.example.com/');
            const data_regular = await response_regular.text();

        } catch (error) {
            puter.print(`<p>Error: ${error.message}</p>`);
        }
    })();
    </script>
</body>
</html>

```


Example 3Handling Different HTTP Methods and Headers
----------------------------------------------------

Now let's look at a more complex example that demonstrates how to use different HTTP methods and headers with `puter.net.fetch()`:

```
<html>
<body>
    <div id="controls">
        <button id="get-btn">GET</button>
        <button id="post-btn">POST</button>
        <button id="put-btn">PUT</button>
        <button id="delete-btn">DELETE</button>
    </div>
    <div id="output"></div>
    
    <script src="https://js.puter.com/v2/"></script>
    <script>
        const output = document.getElementById('output');
        
        // GET request
        document.getElementById('get-btn').addEventListener('click', async () => {
            const response = await puter.net.fetch('https://httpbin.org/get');
            const data = await response.json();
            output.innerHTML = `<h3>GET Response:</h3><pre>${JSON.stringify(data, null, 2)}</pre>`;
        });
        
        // POST request
        document.getElementById('post-btn').addEventListener('click', async () => {
            const response = await puter.net.fetch('https://httpbin.org/post', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify({
                    title: 'New Post',
                    body: 'This is a new post created with puter.net.fetch()',
                    userId: 1
                })
            });
            const data = await response.json();
            output.innerHTML = `<h3>POST Response:</h3><pre>${JSON.stringify(data, null, 2)}</pre>`;
        });
        
        // PUT request
        document.getElementById('put-btn').addEventListener('click', async () => {
            const response = await puter.net.fetch('https://httpbin.org/put', {
                method: 'PUT',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify({
                    id: 1,
                    title: 'Updated Post',
                    body: 'This post was updated with puter.net.fetch()',
                    userId: 1
                })
            });
            const data = await response.json();
            output.innerHTML = `<h3>PUT Response:</h3><pre>${JSON.stringify(data, null, 2)}</pre>`;
        });
        
        // DELETE request
        document.getElementById('delete-btn').addEventListener('click', async () => {
            const response = await puter.net.fetch('https://httpbin.org/delete', {
                method: 'DELETE'
            });
            const data = await response.json();
            output.innerHTML = `<h3>DELETE Response:</h3><pre>${JSON.stringify(data, null, 2)}</pre>`;
        });
    </script>
</body>
</html>

```


This example demonstrates how to use different HTTP methods (GET, POST, PUT, DELETE) with `puter.net.fetch()`. The syntax is identical to the native `fetch()` API, making it easy to integrate into existing codebases.

How it works
------------

Our networking stack is built on the WISP protocol, a websocket based proxy protocol built to relay and multiplex UDP and TCP sockets over a single WebSocket stream. The [puter.net.Socket](https://docs.puter.com/Networking/Socket/) api is an interface which allows you to create a TCP stream over a wisp stream in a user friendly way. While `puter.net.fetch` is a secure way to fetch external resources over a wisp stream. Unlike contemporary cors-proxies, with `puter.net.fetch()`, TLS is done client side inside of the puter.js library with the help of [rustls-wasm](https://github.com/rustls/rustls), allowing your connection to be fully secure. Our servers never have access to any HTTPS resource sent through it over the appropriate Puter APIs.

Applications You Can Now Build
------------------------------

The CORS-free `puter.net.fetch()` unlocks a world of possibilities for frontend-only applications that were previously impossible without complex backend infrastructure. You can now build API testing tools like your own Postman-like app that can test any API directly from the browser without CORS issues, or create browser-based web scrapers that can fetch and parse HTML from any website for data extraction. The technology also enables you to build API aggregators that combine data from multiple APIs (even ones without CORS support) into a single unified interface, develop real-time monitoring dashboards that pull data from various services and APIs directly, and create multi-service integrations that connect to multiple third-party services directly from your frontend without having to build proxies for each one.

Puter.js offers many more features beyond networking, including cloud storage, key-value database, and AI capabilities. Explore the [Puter.js documentation](https://docs.puter.com/) to discover all the possibilities and start building powerful, serverless web applications with no backend code required!

Related
-------

*   [Getting Started with Puter.js](https://developer.puter.com/tutorials/getting-started-with-puterjs)
*   [Free, Unlimited OpenAI API](https://developer.puter.com/tutorials/free-unlimited-openai-api)
*   [Add a Cloud Key-Value Store to Your App: A Free Alternative to DynamoDB](https://developer.puter.com/tutorials/add-a-cloud-key-value-store-to-your-app-a-free-alternative-to-dynamodb)
*   [Add Upload to Your Website for Free](https://developer.puter.com/tutorials/add-upload-to-your-website-for-free)