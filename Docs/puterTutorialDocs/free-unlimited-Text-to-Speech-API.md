# Free, Unlimited Text-to-Speech API
[Tutorials](https://developer.puter.com/tutorials/)
------------------------

This tutorial will show you how to use Puter.js to access text-to-speech capabilities similar to Amazon Polly for free, without any API keys or usage restrictions. Using Puter.js, you can convert text to speech for a wide range of applications without worrying about usage limits or costs.

Getting Started
---------------

Using puter.js does not require any API keys or sign-ups. You can start using Puter.js by including the following script tag in your HTML file, either in the `<head>` or `<body>` section:

```
<script src="https://js.puter.com/v2/"></script>

```


That's all you need to start using Puter.js for free text-to-speech conversion! No API keys or sign-ups required.

Example 1Use Puter.js for text-to-speech conversion
---------------------------------------------------

To convert text to speech using Puter.js, use the [`puter.ai.txt2speech()`](https://docs.puter.com/AI/chat/) function:

```
puter.ai.txt2speech("Hello, world! This is text-to-speech using Puter.js.")
    .then((audio) => {
        audio.play();
    });

```


Here's a complete example with a text input and a button to trigger the text-to-speech conversion:

```
<html>
<body>
    <textarea id="text-input" rows="4" cols="50">Hello, world! This is text-to-speech using Puter.js.</textarea>
    <br>
    <button id="speak-button">Speak</button>

    <script src="https://js.puter.com/v2/"></script>
    <script>
        document.getElementById('speak-button').addEventListener('click', () => {
            const text = document.getElementById('text-input').value;
            puter.ai.txt2speech(text)
                .then((audio) => {
                    audio.play();
                })
                .catch((error) => {
                    console.error('Error:', error);
                });
        });
    </script>
</body>
</html>

```


Example 2Customize the voice
----------------------------

Puter.js supports multiple languages and voices. You can specify the language when calling the [`txt2speech`](https://docs.puter.com/AI/txt2speech/) function:

```
puter.ai.txt2speech("Bonjour, le monde!", "fr-FR")
    .then((audio) => {
        audio.play();
    });

```


Here's an example that allows users to select different languages:

```
<html>
<body>
    <textarea id="text-input" rows="4" cols="50">Hello, world!</textarea>
    <br>
    <select id="language-select">
        <option value="en-US">English (US)</option>
        <option value="fr-FR">French</option>
        <option value="de-DE">German</option>
        <option value="es-ES">Spanish</option>
        <option value="it-IT">Italian</option>
    </select>
    <button id="speak-button">Speak</button>

    <script src="https://js.puter.com/v2/"></script>
    <script>
        document.getElementById('speak-button').addEventListener('click', () => {
            const text = document.getElementById('text-input').value;
            const language = document.getElementById('language-select').value;
            puter.ai.txt2speech(text, language)
                .then((audio) => {
                    audio.play();
                })
                .catch((error) => {
                    console.error('Error:', error);
                });
        });
    </script>
</body>
</html>

```


Example 3Choose different speech engines
----------------------------------------

Puter.js offers three different speech synthesis engines, each with unique characteristics:

*   **Standard**: The default engine that provides good quality speech synthesis
*   **Neural**: Offers higher quality, more natural-sounding speech
*   **Generative**: Uses advanced AI to create the most human-like speech

You can specify the engine using the options parameter:

```
puter.ai.txt2speech("Hello, world!", {
    voice: "Joanna",
    engine: "neural",
    language: "en-US"
})
.then((audio) => {
    audio.play();
});

```


Here's an interactive example that lets you compare all three engines:

```
<html>
<head>
    <style>
        body { font-family: Arial, sans-serif; max-width: 600px; margin: 0 auto; padding: 20px; }
        textarea { width: 100%; height: 80px; margin: 10px 0; }
        button { margin: 5px; padding: 10px 15px; cursor: pointer; }
        .standard { background-color: #e3f2fd; }
        .neural { background-color: #f3e5f5; }
        .generative { background-color: #e8f5e8; }
        .status { margin: 10px 0; padding: 5px; font-size: 14px; }
    </style>
</head>
<body>
    <script src="https://js.puter.com/v2/"></script>
    
    <h1>Text-to-Speech Engine Comparison</h1>
    
    <textarea id="text-input" placeholder="Enter text to convert to speech...">Hello world! This is a test of the text-to-speech engines. Notice the difference in quality between standard, neural, and generative engines.</textarea>
    
    <div>
        <button class="standard" onclick="playAudio('standard')">Standard Engine</button>
        <button class="neural" onclick="playAudio('neural')">Neural Engine</button>
        <button class="generative" onclick="playAudio('generative')">Generative Engine</button>
    </div>
    
    <div id="status" class="status"></div>

    <script>
        const textInput = document.getElementById('text-input');
        const statusDiv = document.getElementById('status');
        
        async function playAudio(engine) {
            const text = textInput.value.trim();
            
            if (!text) {
                statusDiv.textContent = 'Please enter some text first!';
                return;
            }
            
            if (text.length > 3000) {
                statusDiv.textContent = 'Text must be less than 3000 characters!';
                return;
            }
            
            statusDiv.textContent = `Converting with ${engine} engine...`;
            
            try {
                const audio = await puter.ai.txt2speech(text, {
                    voice: "Joanna",
                    engine: engine,
                    language: "en-US"
                });
                
                statusDiv.textContent = `Playing ${engine} audio`;
                audio.play();
            } catch (error) {
                statusDiv.textContent = `Error: ${error.message}`;
            }
        }
    </script>
</body>
</html>

```


That's it! You now have a comprehensive understanding of how to use Puter.js as a free alternative to the Amazon Polly API. With support for multiple languages, voices, and engines, you can create rich text-to-speech experiences without worrying about API keys or usage limits.

Additional Features
-------------------

Puter.js offers many more features, including cloud storage, hosting static websites, and AI-powered image generation. Explore the [Puter.js documentation](https://docs.puter.com/) to discover all the possibilities and start building powerful, serverless web applications with ease!

Related
-------

*   [Free, Unlimited OpenAI API](https://developer.puter.com/tutorials/free-unlimited-openai-api)
*   [Free, Unlimited Claude API](https://developer.puter.com/tutorials/free-unlimited-claude-35-sonnet-api)
*   [Free, Unlimited OCR API](https://developer.puter.com/tutorials/free-unlimited-ocr-api)