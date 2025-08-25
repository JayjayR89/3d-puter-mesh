# Free, Unlimited Claude API
[Tutorials](https://developer.puter.com/tutorials/)
------------------------

This tutorial will show you how to use Puter.js to access Claude's advanced AI capabilities (both Claude Sonnet 4 and Claude Opus 4) for free, without any API keys, backend, or servers. Using Puter.js, you can generate text with Claude for a wide range of tasks, from creative writing to code generation and function calling without worrying about usage limits or costs.

Puter is the pioneer of the ["User Pays" model](https://docs.puter.com/user-pays-model/), which allows developers to incorporate AI capabilities into their applications while users cover their own usage costs. This model enables developers to access advanced AI capabilities for free, without any API keys or server-side setup.

Getting Started
---------------

Puter.js works without any API keys or sign-ups. To start using Puter.js, include the following script tag in your HTML file, either in the `<head>` or `<body>` section:

```
<script src="https://js.puter.com/v2/"></script>

```


You're now ready to use Puter.js for free access to Claude capabilities. No API keys or sign-ups are required.

Example 1Basic Text Generation with Claude Sonnet 4
---------------------------------------------------

To generate text using Claude, use the [`puter.ai.chat()`](https://docs.puter.com/AI/chat/) function with your preferred model. Here's a full code example using Claude Sonnet 4:

```
<html>
<body>
    <script src="https://js.puter.com/v2/"></script>
    <script>
        puter.ai.chat("Explain quantum computing in simple terms", {model: 'claude-sonnet-4'})
            .then(response => {
                puter.print(response.message.content[0].text);
            });
    </script>
</body>
</html>

```


Example 2Streaming Responses for Longer Queries
-----------------------------------------------

For longer responses, use streaming to get results in real-time:

```
async function streamClaudeResponse(model = 'claude-sonnet-4') {
    const response = await puter.ai.chat(
        "Write a detailed essay on the impact of artificial intelligence on society", 
        {model: model, stream: true}
    );
    
    for await (const part of response) {
        puter.print(part?.text);
    }
}

// Use Claude Sonnet 4 (default)
streamClaudeResponse();

```


Here's the full code example with streaming:

```
<html>
<body>
    <script src="https://js.puter.com/v2/"></script>
    <script>
        (async () => {
            const response = await puter.ai.chat(
                "Write a detailed essay on the impact of artificial intelligence on society", 
                {model: 'claude-opus-4', stream: true}
            );
            
            for await (const part of response) {
                puter.print(part?.text);
            }
        })();
    </script>
</body>
</html>

```


Example 3Using different Claude models
--------------------------------------

You can specify different Claude models using the `model` parameter, for example `claude-sonnet-4` or `claude-opus-4`:

```
// Using claude-sonnet-4 model
puter.ai.chat(
    "Write a short poem about coding",
    { model: "claude-sonnet-4" }
).then(response => {
    puter.print(response);
});

// Using claude-opus-4 model
puter.ai.chat(
    "Write a short poem about coding",
    { model: "claude-opus-4" }
).then(response => {
    puter.print(response);
});

```


Full code example:

```
<html>
<body>
    <script src="https://js.puter.com/v2/"></script>
    <script>
        // Using claude-sonnet-4 model
        puter.ai.chat(
            "Write a short poem about coding",
            { model: "claude-sonnet-4" }
        ).then(response => {
            puter.print("<h2>Using claude-sonnet-4 model</h2>");
            puter.print(response);
        });

        // Using claude-opus-4 model
        puter.ai.chat(
            "Write a short poem about coding",
            { model: "claude-opus-4" }
        ).then(response => {
            puter.print("<h2>Using claude-opus-4 model</h2>");
            puter.print(response);
        });
    </script>
</body>
</html>

```


Available Models
----------------

The following Claude models are available via Puter.js:

```
claude-sonnet-4
claude-opus-4
claude-3-7-sonnet
claude-3-7-opus

```


That's it! You now have free, unlimited access to Claude capabilities using Puter.js. This allows you to leverage Claude's advanced language understanding and generation abilities without worrying about API keys or usage limits.

Related
-------

*   [Free, Unlimited OpenAI API](https://developer.puter.com/tutorials/free-unlimited-openai-api)
*   [Free, Unlimited Gemini API](https://developer.puter.com/tutorials/free-gemini-api)
*   [Free, Unlimited OpenRouter API](https://developer.puter.com/tutorials/free-unlimited-openrouter-api)
*   [Free, Unlimited DeepSeek API](https://developer.puter.com/tutorials/free-unlimited-deepseek-api)
*   [Free, Unlimited Llama API](https://developer.puter.com/tutorials/free-unlimited-llama-api)
*   [Free, Unlimited Mistral API](https://developer.puter.com/tutorials/free-unlimited-mistral-api)
*   [Free, Unlimited Text-to-Speech API](https://developer.puter.com/tutorials/free-unlimited-text-to-speech-api)