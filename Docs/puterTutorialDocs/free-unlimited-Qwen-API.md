# Free, Unlimited Qwen API
[Tutorials](https://developer.puter.com/tutorials/)
------------------------

This tutorial will show you how to use Puter.js to access all Qwen family models—from general chat to instruction‑tuned, vision and code models—completely free, without any API keys or usage restrictions.

Puter is the pioneer of the ["User Pays" model](https://docs.puter.com/user-pays-model/), which allows developers to incorporate AI capabilities into their applications while each user will cover their own usage costs. This model enables developers to access advanced AI capabilities for free, without any API keys or server-side setup.

Getting Started
---------------

You can use puter.js without any API keys or sign-ups. To start using Puter.js, include the following script tag in your HTML file, either in the `<head>` or `<body>` section:

```
<script src="https://js.puter.com/v2/"></script>

```


Nothing else is required to start using Puter.js for free access to Qwen models and capabilities.

Example 1Use QwQ-32B for conversational AI
------------------------------------------

To generate text using QwQ-32B, use the [`puter.ai.chat()`](https://docs.puter.com/AI/chat/) function:

```
puter.ai.chat("Tell me a fun trivia fact about space.", { model: "qwen/qwq-32b" })
    .then(response => {
        puter.print(response);
    });

```


Full code example:

```
<html>
<body>
    <script src="https://js.puter.com/v2/"></script>
    <script>
        puter.ai.chat("Tell me a fun trivia fact about space.", { model: "qwen/qwq-32b" })
            .then(response => {
                puter.print(response);
            });
    </script>
</body>
</html>

```


Example 2Write code with qwen3-coder
------------------------------------

To write code using qwen3-coder, use the [`puter.ai.chat()`](https://docs.puter.com/AI/chat/) function:

```
puter.ai.chat(
    "Write a simple JavaScript function that calculates the sum of two numbers.",
    { model: "qwen/qwen3-coder" }
)
.then(response => {
    puter.print(response);
});

```


Full code example:

```
<html>
<body>
    <script src="https://js.puter.com/v2/"></script>
    <script>
        puter.ai.chat(
            "Write a simple JavaScript function that calculates the sum of two numbers.",
            { model: "qwen/qwen3-coder" }
        )
        .then(response => {
            puter.print(response, {code: true});
        });
    </script>
</body>
</html>

```


Example 3Stream responses for longer queries
--------------------------------------------

For longer responses, use streaming to get results in real-time:

```
async function streamResponse() {
    const response = await puter.ai.chat(
        "Explain quantum computing in detail", 
        { model: "qwen/qwen3-235b-a22b", stream: true }
    );
    
    for await (const part of response) {
        puter.print(part?.text);
    }
}

streamResponse();

```


Full code example:

```
<html>
<body>
    <script src="https://js.puter.com/v2/"></script>
    <script>
        async function streamResponse() {
            const response = await puter.ai.chat(
                "Explain quantum computing in detail", 
                { model: "qwen/qwen3-235b-a22b", stream: true }
            );
            
            for await (const part of response) {
                puter.print(part?.text);
            }
        }

        streamResponse();
    </script>
</body>
</html>

```


List of supported models
------------------------

The following Qwen models are supported by Puter.js:

```
qwen/qwen-2-72b-instruct
qwen/qwen-2.5-72b-instruct
qwen/qwen-2.5-72b-instruct:free
qwen/qwen-2.5-7b-instruct
qwen/qwen-2.5-coder-32b-instruct
qwen/qwen-2.5-coder-32b-instruct:free
qwen/qwen-2.5-vl-7b-instruct
qwen/qwen-max
qwen/qwen-plus
qwen/qwen-turbo
qwen/qwen-vl-max
qwen/qwen-vl-plus
qwen/qwen2.5-vl-32b-instruct
qwen/qwen2.5-vl-32b-instruct:free
qwen/qwen2.5-vl-72b-instruct
qwen/qwen2.5-vl-72b-instruct:free
qwen/qwen3-14b
qwen/qwen3-14b:free
qwen/qwen3-235b-a22b
qwen/qwen3-235b-a22b-07-25
qwen/qwen3-235b-a22b-07-25:free
qwen/qwen3-235b-a22b:free
qwen/qwen3-30b-a3b
qwen/qwen3-30b-a3b:free
qwen/qwen3-32b
qwen/qwen3-4b:free
qwen/qwen3-8b
qwen/qwen3-8b:free
qwen/qwen3-coder
qwen/qwq-32b
qwen/qwq-32b-preview
qwen/qwq-32b:free

```


That's it! You now have a free alternative to the Qwen API using Puter.js. This allows you to access QwQ-32B, Qwen2-VL, Qwen2.5-Coder, and many other Qwen model capabilities without needing an API key or a backend. True serverless AI!

Related Resources
-----------------

*   [Free, Unlimited AI API](https://developer.puter.com/tutorials/free-unlimited-ai-api)
*   [Free, Unlimited OpenAI API](https://developer.puter.com/tutorials/free-unlimited-openai-api)
*   [Free, Unlimited Claude API](https://developer.puter.com/tutorials/free-unlimited-claude-35-sonnet-api)
*   [Free, Unlimited Mistral API](https://developer.puter.com/tutorials/free-unlimited-mistral-api)
*   [Free, Unlimited OpenRouter API](https://developer.puter.com/tutorials/free-unlimited-openrouter-api)
*   [Free, Unlimited DeepSeek API](https://developer.puter.com/tutorials/free-unlimited-deepseek-api)
*   [Free, Unlimited Grok API](https://developer.puter.com/tutorials/free-unlimited-grok-api)