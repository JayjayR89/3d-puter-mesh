# Serverless AI, Forever Free for Developers
[Tutorials](https://developer.puter.com/tutorials/)
------------------------

This tutorial will show you how to add powerful AI capabilities to your web applications using Puter.js, completely free and without any API keys or usage restrictions. Using Puter.js, you can leverage multiple AI models including GPT-4o, Claude 3.5 Sonnet, and Llama for various tasks like text generation, analysis, and more.

Puter offers a simple way to add AI to your applications through its ["User Pays" model](https://docs.puter.com/user-pays-model/). Instead of developers managing API keys and billing, users pay for their own AI usage. This straightforward approach makes it easy for developers to add AI features without the usual complexity and costs.

Getting Started
---------------

Puter.js works without any API keys or sign-ups. To start using Puter.js, include the following script tag in your HTML file, either in the `<head>` or `<body>` section:

```
<script src="https://js.puter.com/v2/"></script>

```


You're now ready to use Puter.js for free AI capabilities. No API keys or sign-ups are required.

Example 1Basic Text Generation with GPT-4o
------------------------------------------

Here's a simple example showing how to generate text using GPT-4o:

```
<html>
<body>
    <script src="https://js.puter.com/v2/"></script>
    <script>
        puter.ai.chat("Explain quantum computing in simple terms").then(response => {
            document.write(response);
        });
    </script>
</body>
</html>

```


This example demonstrates the most basic usage of the AI capabilities. The `puter.ai.chat()` function sends your prompt to the GPT-4o model and returns the response. By default, Puter.js uses GPT-4o mini, which is optimized for speed and efficiency.

Example 2Using Claude 3.5 Sonnet for Complex Tasks
--------------------------------------------------

Claude 3.5 Sonnet is particularly good at complex reasoning and detailed analysis:

```
<html>
<body>
    <script src="https://js.puter.com/v2/"></script>
    <script>
        puter.ai.chat("Analyze the potential impact of quantum computing on cryptography", {
            model: 'claude-3-5-sonnet'
        }).then(response => {
            document.write(response);
        });
    </script>
</body>
</html>

```


This example shows how to specify a different model using the options parameter. Claude 3.5 Sonnet is well-suited for tasks requiring deep analysis or technical understanding.

Example 3Streaming Responses with Llama
---------------------------------------

For longer responses, you can use streaming to get results in real-time:

```
<html>
<body>
    <script src="https://js.puter.com/v2/"></script>
    <script>
        async function streamResponse() {
            const response = await puter.ai.chat(
                "Write a detailed analysis of renewable energy sources", 
                {
                    model: 'meta-llama/Meta-Llama-3.1-70B-Instruct-Turbo',
                    stream: true
                }
            );
            
            for await (const part of response) {
                document.write(part?.text);
            }
        }

        streamResponse();
    </script>
</body>
</html>

```


This example demonstrates streaming with Llama, which is particularly useful for longer responses. The streaming approach provides a better user experience by showing the response as it's generated rather than waiting for the complete response.

Example 4Vision Capabilities
----------------------------

You can also analyze images using GPT-4 Vision:

```
<html>
<body>
    <script src="https://js.puter.com/v2/"></script>
    <img src="https://assets.puter.site/doge.jpeg" id="image">
    <script>
        puter.ai.chat(
            "What do you see in this image?",
            "https://assets.puter.site/doge.jpeg"
        ).then(response => {
            document.write(response);
        });
    </script>
</body>
</html>

```


This example shows how to use GPT-4 Vision capabilities to analyze images. You can pass an image URL as the second parameter to have the AI analyze its contents.

Best Practices
--------------

When implementing AI in your web applications with Puter.js:

1.  Choose the appropriate model for your use case:
    
    *   GPT-4o mini: Best for quick, general-purpose responses
    *   Claude 3.5 Sonnet: Ideal for complex analysis and technical tasks
    *   Llama: Good for general tasks with different model sizes available
    *   GPT-4o: Best for vision-related tasks
2.  Use streaming for longer responses to improve user experience
    
3.  Handle errors gracefully and provide feedback to users when the AI is processing
    
4.  Consider rate limiting your requests to ensure fair usage
    

Related
-------

*   [Free, Unlimited OpenAI API](https://developer.puter.com/tutorials/free-unlimited-openai-api)
*   [Free, Unlimited Claude API](https://developer.puter.com/tutorials/free-unlimited-claude-35-sonnet-api)
*   [Free, Unlimited Text-to-Speech API](https://developer.puter.com/tutorials/free-unlimited-text-to-speech-api)
*   [Free, Unlimited OCR API](https://developer.puter.com/tutorials/free-unlimited-ocr-api)