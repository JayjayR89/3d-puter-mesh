# Free, Unlimited Mistral API
[Tutorials](https://developer.puter.com/tutorials/)
------------------------

This tutorial will show you how to use Puter.js to access Mistral's powerful AI models for free, without any API keys or usage restrictions. Using Puter.js, you can leverage models like Mistral Large, Mistral Medium, Mistral Small, and Codestral for various tasks including text generation, code completion, and complex reasoning without worrying about usage limits or costs.

Puter is the pioneer of the ["User Pays" model](https://docs.puter.com/user-pays-model/), which allows developers to incorporate AI capabilities into their applications while users cover their own usage costs. This model enables developers to access advanced AI capabilities for free, without any API keys or server-side setup.

Getting Started
---------------

Puter.js works without any API keys or sign-ups. To start using Puter.js, include the following script tag in your HTML file, either in the `<head>` or `<body>` section:

```
<script src="https://js.puter.com/v2/"></script>

```


You're now ready to use Puter.js for free access to Mistral capabilities. No API keys or sign-ups are required.

Example 1Basic Text Generation with Mistral Large
-------------------------------------------------

To generate text using Mistral Large, use the [`puter.ai.chat()`](https://docs.puter.com/AI/chat/) function with your preferred model:

```
<html>
<body>
    <script src="https://js.puter.com/v2/"></script>
    <script>
        puter.ai.chat("Explain the concept of machine learning to a beginner", {
            model: 'mistral-large-latest'
        }).then(response => {
            puter.print(response.message.content);
        });
    </script>
</body>
</html>

```


Example 2Code Generation with Codestral
---------------------------------------

Codestral is Mistral's specialized model for code generation. Here's how to use it:

```
<html>
<body>
    <script src="https://js.puter.com/v2/"></script>
    <script>
        puter.ai.chat(
            "Write a Python function that calculates the Fibonacci sequence up to n terms", 
            {model: 'codestral-latest'}
        ).then(response => {
            puter.print(response.message.content, {code: true});
        });
    </script>
</body>
</html>

```


Example 3Streaming Responses for Longer Content
-----------------------------------------------

For longer responses, use streaming to get results in real-time:

```
<html>
<body>
    <script src="https://js.puter.com/v2/"></script>
    <script>
        (async () => {
            const response = await puter.ai.chat(
                "Write a comprehensive guide on sustainable living practices", 
                {
                    model: 'mistral-large-latest',
                    stream: true
                }
            );
            
            for await (const part of response) {
                if (part?.text) {
                    puter.print(part.text);
                }
            }
        })();
    </script>
</body>
</html>

```


Example 4Using Different Mistral Models
---------------------------------------

Mistral offers various models optimized for different use cases. Here's how to use them:

```
<html>
<body>
    <script src="https://js.puter.com/v2/"></script>
    <script>
        // Mistral Large - Best for complex tasks
        puter.ai.chat(
            "Analyze the economic implications of renewable energy adoption",
            { model: "mistral-large-latest" }
        ).then(response => {
            puter.print("<h2>Mistral Large Response:</h2>");
            puter.print(response.message.content);
        });

        // Mistral Medium - Balanced performance
        puter.ai.chat(
            "Summarize the key points of climate change",
            { model: "mistral-medium-latest" }
        ).then(response => {
            puter.print("<h2>Mistral Medium Response:</h2>");
            puter.print(response.message.content);
        });

        // Mistral Small - Fast and efficient
        puter.ai.chat(
            "What are the benefits of regular exercise?",
            { model: "mistral-small-latest" }
        ).then(response => {
            puter.print("<h2>Mistral Small Response:</h2>");
            puter.print(response.message.content);
        });

        // Mistral Nemo - Lightweight model
        puter.ai.chat(
            "Explain photosynthesis in simple terms",
            { model: "open-mistral-nemo" }
        ).then(response => {
            puter.print("<h2>Mistral Nemo Response:</h2>");
            puter.print(response.message.content);
        });
    </script>
</body>
</html>

```


Example 5Comparing Mistral Models
---------------------------------

Here's an example that compares responses from different Mistral models for the same prompt:

```
<html>
<body>
    <h1>Mistral Model Comparison</h1>
    <input type="text" id="prompt" style="width: 100%; padding: 10px; margin-bottom: 20px;" 
        placeholder="Enter a prompt to compare models..." 
        value="Explain the concept of artificial intelligence">
    <button onclick="compareModels()" style="padding: 10px 20px; background: #FF7000; color: white; border: none; border-radius: 4px; cursor: pointer;">
        Compare Models
    </button>
    <div id="results" style="margin-top: 20px;"></div>

    <script src="https://js.puter.com/v2/"></script>
    <script>
        async function compareModels() {
            const prompt = document.getElementById('prompt').value;
            const resultsDiv = document.getElementById('results');
            
            const models = [
                { name: 'mistral-large-latest', label: 'Mistral Large' },
                { name: 'mistral-medium-latest', label: 'Mistral Medium' },
                { name: 'mistral-small-latest', label: 'Mistral Small' },
                { name: 'open-mistral-nemo', label: 'Mistral Nemo' }
            ];
            
            resultsDiv.innerHTML = '<p>Generating responses...</p>';
            
            let html = '';
            for (const model of models) {
                html += `<div style="margin-bottom: 30px; padding: 15px; border: 1px solid #ddd; border-radius: 8px;">`;
                html += `<h3 style="color: #FF7000;">${model.label}</h3>`;
                
                try {
                    const response = await puter.ai.chat(prompt, { model: model.name });
                    html += `<p>${response.message.content}</p>`;
                } catch (error) {
                    html += `<p style="color: red;">Error: ${error.message}</p>`;
                }
                
                html += '</div>';
                resultsDiv.innerHTML = html;
            }
        }
    </script>
</body>
</html>

```


Available Mistral Models
------------------------

Puter.js provides access to the following Mistral models:

```
mistral-large-latest
mistral-medium-latest
mistral-small-latest
open-mistral-nemo
codestral-latest

```


That's it! You now have free, unlimited access to Mistral's powerful AI models using Puter.js. This allows you to leverage advanced language understanding, generation, and coding capabilities without worrying about API keys or usage limits.

Related
-------

*   [Free, Unlimited OpenAI API](https://developer.puter.com/tutorials/free-unlimited-openai-api)
*   [Free, Unlimited Claude API](https://developer.puter.com/tutorials/free-unlimited-claude-35-sonnet-api)
*   [Free, Unlimited Gemini API](https://developer.puter.com/tutorials/free-gemini-api)
*   [Free, Unlimited DeepSeek API](https://developer.puter.com/tutorials/free-unlimited-deepseek-api)
*   [Free, Unlimited Llama API](https://developer.puter.com/tutorials/free-unlimited-llama-api)
*   [Free, Unlimited Text-to-Speech API](https://developer.puter.com/tutorials/free-unlimited-text-to-speech-api)