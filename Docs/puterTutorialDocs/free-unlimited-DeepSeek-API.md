# Free, Unlimited DeepSeek API
[Tutorials](https://developer.puter.com/tutorials/)
------------------------

This tutorial will show you how to use Puter.js to access DeepSeek's powerful language models for free, without any API keys or usage restrictions. Using Puter.js, you can leverage both DeepSeek Chat and DeepSeek Reasoner for various tasks like text generation, analysis, and complex reasoning.

Puter is the pioneer of the ["User Pays" model](https://docs.puter.com/user-pays-model/), which allows developers to incorporate AI capabilities into their applications while users cover their own usage costs. This model enables developers to access advanced AI capabilities for free, without any API keys or server-side setup.

Getting Started
---------------

Puter.js works without any API keys or sign-ups. To start using Puter.js, include the following script tag in your HTML file, either in the `<head>` or `<body>` section:

```
<script src="https://js.puter.com/v2/"></script>

```


You're now ready to use Puter.js for free access to DeepSeek capabilities. No API keys or sign-ups are required.

Example 1Basic Text Generation with DeepSeek Chat (DeepSeek V3.1)
-----------------------------------------------------------------

Here's a simple example showing how to generate text using DeepSeek Chat (DeepSeek V3.1):

```
<html>
<body>
    <script src="https://js.puter.com/v2/"></script>
    <script>
        puter.ai.chat("Explain quantum entanglement in simple terms", {
            model: 'deepseek-chat'
        }).then(response => {
            document.write(response.message.content);
        });
    </script>
</body>
</html>

```


Using the [`puter.ai.chat()`](https://docs.puter.com/AI/chat/) function, you can generate text using DeepSeek Chat.

Example 2Complex Reasoning with DeepSeek Reasoner (DeepSeek R1)
---------------------------------------------------------------

DeepSeek Reasoner (DeepSeek R1) is particularly good at complex problem-solving and step-by-step analysis:

```
<html>
<body>
    <script src="https://js.puter.com/v2/"></script>
    <script>
        puter.ai.chat(
            "What would be the environmental impact of replacing all cars with electric vehicles? Consider both positive and negative effects.", 
            {
                model: 'deepseek-reasoner'
            }
        ).then(response => {
            document.write(response.message.content);
        });
    </script>
</body>
</html>

```


Example 3Streaming Responses
----------------------------

For longer responses, use streaming to get results in real-time:

```
<html>
<body>
    <div id="output"></div>
    <script src="https://js.puter.com/v2/"></script>
    <script>
        async function streamResponse() {
            const outputDiv = document.getElementById('output');
            
            // DeepSeek Chat with streaming
            outputDiv.innerHTML += '<h2>DeepSeek Chat Response:</h2>';
            const chatResponse = await puter.ai.chat(
                "Explain the significance of dark matter in the universe", 
                {
                    model: 'deepseek-chat',
                    stream: true
                }
            );
            
            for await (const part of chatResponse) {
                if (part?.text) {
                    outputDiv.innerHTML += part.text;
                }
            }
            
            // DeepSeek Reasoner with streaming
            outputDiv.innerHTML += '<h2>DeepSeek Reasoner Response:</h2>';
            const reasonerResponse = await puter.ai.chat(
                "Explain the significance of dark matter in the universe", 
                {
                    model: 'deepseek-reasoner',
                    stream: true
                }
            );
            
            for await (const part of reasonerResponse) {
                if (part?.text) {
                    outputDiv.innerHTML += part.text;
                }
            }
        }

        streamResponse();
    </script>
</body>
</html>

```


Example 4Comparing Models
-------------------------

Here's how to compare responses from both DeepSeek models:

```
<html>
<body>
    <script src="https://js.puter.com/v2/"></script>
    <script>
    (async () => {
        // DeepSeek Chat
        const chat_resp = await puter.ai.chat(
            'Solve this puzzle: If you have 9 coins and one is counterfeit (lighter), how can you identify it with just 2 weighings on a balance scale?',
            {model: 'deepseek-chat', stream: true}
        );
        document.write('<h2>DeepSeek Chat Solution:</h2>');
        for await (const part of chat_resp) {
            if (part?.text) {
                document.write(part.text.replaceAll('\n', '<br>'));
            }
        }

        // DeepSeek Reasoner
        const reasoner_resp = await puter.ai.chat(
            'Solve this puzzle: If you have 9 coins and one is counterfeit (lighter), how can you identify it with just 2 weighings on a balance scale?',
            {model: 'deepseek-reasoner', stream: true}
        );
        document.write('<h2>DeepSeek Reasoner Solution:</h2>');
        for await (const part of reasoner_resp) {
            if (part?.text) {
                document.write(part.text.replaceAll('\n', '<br>'));
            }
        }
    })();
    </script>
</body>
</html>

```


Best Practices
--------------

1.  Use streaming for longer responses to provide better user experience
2.  Consider the specific strengths of each model when choosing which to use
3.  Handle errors gracefully and provide feedback during processing
4.  Use appropriate error handling for network issues or API failures
5.  Consider implementing retry logic for failed requests

That's it! You now have free access to DeepSeek's powerful language models using Puter.js. This allows you to add sophisticated AI capabilities to your web applications without worrying about API keys or usage limits.

Related
-------

*   [Free, Unlimited OpenAI API](https://developer.puter.com/tutorials/free-unlimited-openai-api)
*   [Free, Unlimited Claude API](https://developer.puter.com/tutorials/free-unlimited-claude-35-sonnet-api)
*   [Free, Unlimited Gemini API](https://developer.puter.com/tutorials/free-gemini-api)
*   [Free, Unlimited Llama API](https://developer.puter.com/tutorials/free-unlimited-llama-api)
*   [Serverless AI: Forever Free for Developers](https://developer.puter.com/tutorials/serverless-ai-forever-free-for-developers)