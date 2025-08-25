# Getting Started with Puter.js
[Tutorials](https://developer.puter.com/tutorials/)
------------------------

Puter.js adds serverless auth, cloud, and AI features directly to your frontend code. From cloud storage and database to OpenAI and Claude APIs, Puter.js has you covered. Sound amazing? well it gets even better, Puter.js is also 100% free for apps and [open-source](https://github.com/heyputer/puter/)!

Puter is the pioneer of the ["User Pays" model](https://docs.puter.com/user-pays-model/), which allows developers to incorporate AI capabilities into their applications while users cover their own usage costs. This innovative approach eliminates the need for developers to manage API keys or worry about billing, making advanced AI accessible to everyone.

This tutorial will guide you through the process of setting up and using Puter.js in your project to access its powerful features. Let's get started!

Installation
------------

To begin using Puter.js, simply add it to your HTML file using the following script tag either in the `<head>` or `<body>` of your HTML file:

```
<script src="https://js.puter.com/v2/"></script>

```


That's it! You're now ready to start using Puter.js in your web application. No need to install any dependencies or set up a server. No API keys or configuration required.

Example 1Add GPT-4o to your web application
-------------------------------------------

Once you've added the Puter.js script to your web application, a global `puter` object will be available for you to use. This object contains all of the functionality provided by Puter.js. For example, to use GPT-4o mini, you can call the puter.ai.chat function:

```
<html>
<body>
    <script src="https://js.puter.com/v2/"></script>
    <script>
        puter.ai.chat(`Why did the chicken cross the road?`).then(puter.print);
    </script>
</body>
</html>

```


In this example, we're using the [`puter.ai.chat`](https://docs.puter.com/AI/chat/) function to generate text with GPT-4o. The generated text is then printed to the console using the [`puter.print`](https://docs.puter.com/Utils/print/) function. You can replace the input text with any prompt you'd like to generate text for.

Example 2Add cloud storage to your web application
--------------------------------------------------

Let's try another example, this time using cloud storage to write and read a file:

```
<html>
<body>
    <script src="https://js.puter.com/v2/"></script>
    <script>
        async function fileDemo() {
            // Write a file
            await puter.fs.write('hello.txt', 'Hello, Puter!');
            puter.print('File written successfully<br>');

            // Read the file
            const fileContent = await puter.fs.read('hello.txt');
            puter.print('File content: ', await fileContent.text(), '<br>');
        }

        fileDemo();
    </script>
</body>
</html>

```


In this example, we're using the [`puter.fs.write`](https://docs.puter.com/FS/write/) function to write a file to the cloud storage. We then use the [`puter.fs.read`](https://docs.puter.com/FS/read/) function to read the file and print its content to the console. You can replace the file name and content with your own data.

Example 3Cloud Key-Value Store
------------------------------

Let's use Puter.js to store and retrieve data from the cloud key-value store. In this example, we'll save a user preference to the cloud and then retrieve it:

```
<html>
<body>
    <script src="https://js.puter.com/v2/"></script>
    <script>
        async function kvDemo() {
            // Set a value
            await puter.kv.set('user_preference', 'dark_mode');
            puter.print('Preference saved<br>');

            // Get the value
            const preference = await puter.kv.get('user_preference');
            puter.print('User preference:', preference, '<br>');
        }

        kvDemo();
    </script>
</body>
</html>

```


In this example, we're using the [`puter.kv.set`](https://docs.puter.com/KV/set/) function to save a user preference to the cloud key-value store. We then use the [`puter.kv.get`](https://docs.puter.com/KV/get/) function to retrieve the preference and print it to the console. You can replace the key and value with your own data.

Example 4Authentication
-----------------------

Puter.js handles authentication automatically. When your code tries to access any cloud services, the user will be prompted to sign in with their Puter.com account if they haven't already. You can build your app as if the user is already signed in, and Puter.js will handle the authentication process for you when needed.

If you want to explicitly check if a user is signed in or trigger the sign-in process, you can use the following methods:

```
<html>
<body>
    <script src="https://js.puter.com/v2/"></script>
    <script>
        async function authDemo() {
            // Check if user is signed in
            const isSignedIn = puter.auth.isSignedIn();
            puter.print('Is user signed in? ', isSignedIn, '<br>');

            if (!isSignedIn) {
                // Trigger sign-in process
                await puter.auth.signIn();
                puter.print('User signed in successfully<br>');
            }

            // Get user info
            const user = await puter.auth.getUser();
            puter.print('User info:', JSON.stringify(user));
        }

        authDemo();
    </script>
</body>
</html>

```


This is all you need to use GPT-4o mini in your app. No backend code, no configuration, and no API keys. Just include the Puter.js script, and you're ready to start.

Puter.js offers many more features, including [hosting static websites](https://docs.puter.com/playground/?example=hosting-create), [generating images with DALL-E 3](https://docs.puter.com/playground/?example=ai-txt2img), and more. Explore the [Puter.js documentation](https://docs.puter.com/) to discover all the possibilities and start building powerful, serverless web applications with ease! Remember, Puter.js is designed to be simple and straightforward, allowing you to focus on building your application without worrying about backend infrastructure or complex setups. Happy coding!

Related
-------

*   [Free, Unlimited OpenAI API](https://developer.puter.com/tutorials/free-unlimited-openai-api)
*   [Free, Unlimited Claude API](https://developer.puter.com/tutorials/free-unlimited-claude-35-sonnet-api)
*   [Free, Unlimited OpenRouter API](https://developer.puter.com/tutorials/free-unlimited-openrouter-api)
*   [Free, Unlimited Text-to-Speech API](https://developer.puter.com/tutorials/free-unlimited-text-to-speech-api)