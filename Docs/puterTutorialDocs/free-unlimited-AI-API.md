# Free, Unlimited AI API
[Tutorials](https://developer.puter.com/tutorials/)
------------------------

This tutorial will show you how to incorporate any major AI capabilities in your website or app for free, without any API keys, backend setup, or usage restrictions. With a single line of code, you can leverage the power of OpenAI models, Anthropic's Claude, Google's Gemini, Meta's Llama, and more than 400 other leading AI models directly from your frontend code.

Puter is the pioneer of the ["User Pays" model](https://docs.puter.com/user-pays-model/), which allows developers to incorporate AI capabilities into their websites and applications while users cover their own usage costs. This revolutionary approach eliminates the need for developers to manage API keys, worry about billing, or maintain server infrastructure, making advanced AI accessible to everyone.

Getting Started
---------------

[Puter.js](https://developer.puter.com/) is completely serverless and works without any API keys or sign-ups. To start using Puter.js, simply include the following script tag in your HTML file:

```
<script src="https://js.puter.com/v2/"></script>

```


That's it! You're now ready to use Puter.js for free access to all major AI models in your website or app. No API keys, backend setup, or server-side code required.

### OpenAI Models

To integrate AI models into your website or app, use the [`puter.ai.chat()`](https://docs.puter.com/AI/chat/) function and specify the model name in the `model` parameter. Here's an example of how to use the OpenAI's GPT-4.1 Nano model:

```
puter.ai.chat("What are the benefits of exercise?", { model: "gpt-4.1-nano" })
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
        puter.ai.chat("What are the benefits of exercise?", { model: "gpt-4.1-nano" })
            .then(response => {
                puter.print(response);
            });
    </script>
</body>
</html>

```


As you can see, the experience is completely serverless and doesn't require any API keys or backend setup.

### Claude Models

Puter.js is not limited to OpenAI models. You can use any major AI model by specifying the model name in the `model` parameter. Here's an example of how to use the Claude Sonnet 4 model:

```
<html>
<body>
    <script src="https://js.puter.com/v2/"></script>
    <script>
        // Claude Sonnet 4
        puter.ai.chat(
            "Write a creative short story about a time traveler",
            { model: "claude-sonnet-4" }
        ).then(response => {
            puter.print(response.message.content[0].text);
        });
    </script>
</body>
</html>

```


### Google Gemini Models

Leverage Google's Gemini models for various AI tasks:

```
<html>
<body>
    <script src="https://js.puter.com/v2/"></script>
    <script>
        puter.ai.chat(
            "Create a meal plan for a healthy week",
            { model: "google/gemini-2.5-flash" }
        ).then(response => {
            puter.print(response.message.content);
        });
    </script>
</body>
</html>

```


### Other Models

From open-source to commercial, Puter supports more than 400 AI models. You can use any of them by specifying the model name in the `model` parameter. The full list of models is available [here](https://puter.com/puterai/chat/models).

Advanced Features
-----------------

### Streaming Responses

For better user experience with longer content, use streaming to display responses in real-time:

```
<html>
<body>
    <div id="streamOutput"></div>
    <script src="https://js.puter.com/v2/"></script>
    <script>
        async function streamExample() {
            const outputDiv = document.getElementById('streamOutput');
            outputDiv.innerHTML = '<h2>AI Streaming Response Demo</h2>';
            
            // Stream from GPT-4.1 Nano
            const response = await puter.ai.chat(
                "Write a detailed essay about the future of renewable energy",
                { model: "gpt-4.1-nano", stream: true }
            );
            
            // Print the response in real-time
            for await (const part of response) {
                if (part?.text) {
                    outputDiv.innerHTML += part.text;
                }
            }
        }

        streamExample();
    </script>
</body>
</html>

```


### Image Analysis

You are not limited to text generation. You can also analyze images using AI. In the example below, we're using GPT-4.1 Nano to analyze an image and then ask follow-up questions. All you have to do is pass the image URL to the `puter.ai.chat()` function:

```
<html>
<body>
    <h1>AI Image Analysis</h1>
    <input type="text" id="imageUrl" placeholder="Enter image URL..." style="width: 400px; padding: 5px;">
    <button onclick="analyzeImage()">Analyze Image</button>
    <div id="analysis"></div>

    <script src="https://js.puter.com/v2/"></script>
    <script>
        async function analyzeImage() {
            const imageUrl = document.getElementById('imageUrl').value;
            if (!imageUrl) return;

            const analysisDiv = document.getElementById('analysis');
            analysisDiv.innerHTML = '<p>Analyzing image...</p>';

            // Display the image
            analysisDiv.innerHTML = `<img src="${imageUrl}" style="max-width: 400px; margin: 10px 0;"><br>`;
            
            // Get AI analysis
            const response = await puter.ai.chat(
                "Describe this image in detail. What objects, people, or scenes do you see?",
                imageUrl
            );
            
            analysisDiv.innerHTML += `<h3>Analysis:</h3><p>${response}</p>`;
        }

        // Example with default image
        window.onload = () => {
            document.getElementById('imageUrl').value = 'https://assets.puter.site/doge.jpeg';
        };
    </script>
</body>
</html>

```


Function Calling (a.k.a. "Tool Calling" or "Agentic AI")
--------------------------------------------------------

Function calling allows AI models to call functions in your application, enabling them to perform actions, access real-time data, and interact with external systems. This transforms static AI responses into dynamic, interactive experiences.

With Puter.js, you can define functions that the AI can call, and the AI will intelligently decide when and how to use them based on the user's request. This is perfect for creating chatbots, virtual assistants, and interactive applications.

Here's a simple example showing how to create a weather assistant that can fetch weather data:

```
<html>
<body>
    <input type="text" id="userInput" placeholder="Ask about the weather..." style="width: 400px; padding: 10px; margin: 10px 0;">
    <button onclick="askWeather()">Ask</button>
    <div id="response" style="margin-top: 20px; padding: 15px; background: #f8f9fa; border-radius: 5px;"></div>

    <script src="https://js.puter.com/v2/"></script>
    <script>
        // Mock weather function - in a real app, this would call a weather API
        function getWeather(location) {
            const weatherData = {
                'Paris': { temp: '22°C', condition: 'Partly Cloudy', humidity: '65%' },
                'London': { temp: '18°C', condition: 'Rainy', humidity: '80%' },
                'New York': { temp: '25°C', condition: 'Sunny', humidity: '45%' },
                'Tokyo': { temp: '28°C', condition: 'Clear', humidity: '70%' }
            };
            
            const weather = weatherData[location] || { temp: '20°C', condition: 'Unknown', humidity: '50%' };
            return JSON.stringify(weather);
        }

        // Define the functions available to the AI
        const tools = [{
            type: "function",
            function: {
                name: "get_weather",
                description: "Get current weather information for a specific location",
                parameters: {
                    type: "object",
                    properties: {
                        location: {
                            type: "string",
                            description: "City name (e.g., Paris, London, New York)"
                        }
                    },
                    required: ["location"],
                    additionalProperties: false
                },
                strict: true
            }
        }];

        async function askWeather() {
            const userInput = document.getElementById('userInput').value;
            const responseDiv = document.getElementById('response');
            
            if (!userInput) return;
            
            responseDiv.innerHTML = 'Processing...';
            
            try {
                // First, get the AI's response with potential function calls
                const completion = await puter.ai.chat(userInput, { tools });
                
                // Check if the AI wants to call a function
                if (completion.message.tool_calls && completion.message.tool_calls.length > 0) {
                    const toolCall = completion.message.tool_calls[0];
                    
                    if (toolCall.function.name === 'get_weather') {
                        // Parse the arguments and call our weather function
                        const args = JSON.parse(toolCall.function.arguments);
                        const weatherResult = getWeather(args.location);
                        
                        // Send the function result back to the AI for a natural response
                        const finalResponse = await puter.ai.chat([
                            { role: "user", content: userInput },
                            completion.message,
                            { 
                                role: "tool",
                                tool_call_id: toolCall.id,
                                content: weatherResult
                            }
                        ]);
                        
                        responseDiv.innerHTML = `<strong>Weather Assistant:</strong><br>${finalResponse}`;
                    }
                } else {
                    // No function call needed, just show the response
                    responseDiv.innerHTML = `<strong>Assistant:</strong><br>${completion}`;
                }
            } catch (error) {
                responseDiv.innerHTML = `<strong>Error:</strong> ${error.message}`;
            }
        }
    </script>
</body>
</html>

```


  

* * *

That's it! You now have access to all major AI models through a single, simple interface. With Puter.js, you can build powerful AI applications without worrying about API keys, rate limits, or backend infrastructure. The future of AI development is serverless, and it's available to you right now - completely free.

Related Resources
-----------------

*   [Puter.js Documentation](https://docs.puter.com/)
*   [Free, Unlimited OpenAI API](https://developer.puter.com/tutorials/free-unlimited-openai-api)
*   [Free, Unlimited Claude API](https://developer.puter.com/tutorials/free-unlimited-claude-35-sonnet-api)
*   [Free, Unlimited OpenRouter API](https://developer.puter.com/tutorials/free-unlimited-openrouter-api)
*   [Free, Unlimited DeepSeek API](https://developer.puter.com/tutorials/free-unlimited-deepseek-api)
*   [Free, Unlimited Text-to-Speech API](https://developer.puter.com/tutorials/free-unlimited-text-to-speech-api)