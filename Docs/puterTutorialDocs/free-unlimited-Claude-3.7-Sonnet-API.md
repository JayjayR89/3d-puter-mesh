# Free, Unlimited Claude 3.7 Sonnet API
[Tutorials](https://developer.puter.com/tutorials/)
------------------------

This tutorial will show you how to use Puter.js to access [Claude 3.7 Sonnet](https://developer.puter.com/encyclopedia/claude-3-7-sonnet/) capabilities for free, without any API keys or usage restrictions. Using Puter.js, you can generate text with Claude 3.7 Sonnet for a wide range of tasks, from creative writing to code generation and more without worrying about usage limits or costs.

Puter is the pioneer of the ["User Pays" model](https://docs.puter.com/user-pays-model/), which allows developers to incorporate AI capabilities into their applications while users cover their own usage costs. This model enables developers to access advanced AI capabilities for free, without any API keys or server-side setup.

Getting Started
---------------

Puter.js works without any API keys or server-side setup. To start using Puter.js, include the following script tag in your HTML file, either in the `<head>` or `<body>` section:

```
<script src="https://js.puter.com/v2/"></script>

```


You're now ready to use Puter.js for free access to Claude 3.7 Sonnet capabilities. No API keys or sign-ups are required.

Example 1Use Claude 3.7 Sonnet for text generation
--------------------------------------------------

To generate text using Claude 3.7 Sonnet, use the [`puter.ai.chat()`](https://docs.puter.com/AI/chat/) function with the 'claude-3-7-sonnet' model:

```
puter.ai.chat("Explain quantum computing in simple terms", {model: 'claude-3-7-sonnet'})
    .then(response => {
        puter.print(response.message.content[0].text);
    });

```


Here's the full code example:

```
<html>
<body>
    <script src="https://js.puter.com/v2/"></script>
    <script>
        puter.ai.chat("Explain quantum computing in simple terms", {model: 'claude-3-7-sonnet'})
            .then(response => {
                puter.print(response.message.content[0].text);
            });
    </script>
</body>
</html>

```


Example 2Stream responses for longer queries
--------------------------------------------

For longer responses, use streaming to get results in real-time:

```
async function streamClaudeResponse() {
    const response = await puter.ai.chat(
        "Write a detailed essay on the impact of artificial intelligence on society", 
        {model: 'claude-3-7-sonnet', stream: true}
    );
    
    for await (const part of response) {
        puter.print(part?.text);
    }
}

streamClaudeResponse();

```


Here's the full code example:

```
<html>
<body>
    <script src="https://js.puter.com/v2/"></script>
    <script>
        async function streamClaudeResponse() {
            const response = await puter.ai.chat(
                "Write a detailed essay on the impact of artificial intelligence on society", 
                {model: 'claude-3-7-sonnet', stream: true}
            );
            
            for await (const part of response) {
                puter.print(part?.text);
            }
        }

        streamClaudeResponse();
    </script>
</body>
</html>

```


That's it! You now have free, unlimited access to Claude 3.7 Sonnet capabilities using Puter.js. This allows you to leverage Claude's advanced language understanding and generation abilities without worrying about API keys or usage limits.

Related
-------

*   [Free, Unlimited OpenAI API](https://developer.puter.com/tutorials/free-unlimited-openai-api)
*   [Free, Unlimited OpenRouter API](https://developer.puter.com/tutorials/free-unlimited-openrouter-api)
*   [Free, Unlimited Llama API](https://developer.puter.com/tutorials/free-unlimited-llama-api)
*   [Free, Unlimited Claude API](https://developer.puter.com/tutorials/free-unlimited-claude-35-sonnet-api)
*   [Free, Unlimited DeepSeek API](https://developer.puter.com/tutorials/free-unlimited-deepseek-api)
*   [Free, Unlimited Gemini API](https://developer.puter.com/tutorials/free-gemini-api)
*   [Free, Unlimited Text-to-Speech API](https://developer.puter.com/tutorials/free-unlimited-text-to-speech-api)