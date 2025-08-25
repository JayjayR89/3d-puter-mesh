# Free, Unlimited OCR API
[Tutorials](https://developer.puter.com/tutorials/)
------------------------

Need to extract text from images in your web application? Whether you're building a document scanner, digitizing receipts and business cards, or converting handwritten notes to text, this tutorial shows you how to implement OCR (Optical Character Recognition) using Puter.js. Best of all, it's completely free with no usage restrictions - no API keys or backend required.

Getting Started
---------------

Add Puter.js to your project with a single line:

```
<script src="https://js.puter.com/v2/"></script>

```


That's it - you're ready to start extracting text from images.

Example 1Basic Image to Text
----------------------------

Here's a simple example that extracts text from an image URL:

```
<html>
<body>
    <script src="https://js.puter.com/v2/"></script>
    
    <div>
        <h3>Image to Text Converter</h3>
        <input type="text" id="image-url" placeholder="Enter image URL" 
               value="https://cdn.handwrytten.com/www/2020/02/home-hero-photo2%402x.png">
        <button onclick="extractText()">Extract Text</button>
        <div id="result" style="margin-top: 20px; white-space: pre-wrap;"></div>
    </div>

    <script>
        async function extractText() {
            const imageUrl = document.getElementById('image-url').value;
            const resultDiv = document.getElementById('result');
            
            resultDiv.textContent = 'Processing image...';
            
            try {
                const text = await puter.ai.img2txt(imageUrl);
                resultDiv.textContent = text || 'No text found in image';
            } catch (error) {
                resultDiv.textContent = 'Error: ' + error.message;
            }
        }
    </script>
</body>
</html>

```


This basic example demonstrates how to extract text from an image URL. Simply input the URL of an image containing text, and Puter.js will process it and return any text it finds.

Example 2File Upload OCR
------------------------

Here's how to handle OCR for uploaded image files:

```
<html>
<body>
    <script src="https://js.puter.com/v2/"></script>
    
    <div>
        <h3>OCR File Upload</h3>
        <input type="file" id="image-input" accept="image/*">
        <button onclick="processImage()">Process Image</button>
        
        <div style="margin-top: 20px;">
            <h4>Preview:</h4>
            <img id="preview" style="max-width: 500px; display: none;">
        </div>
        
        <div style="margin-top: 20px;">
            <h4>Extracted Text:</h4>
            <div id="result" style="white-space: pre-wrap;"></div>
        </div>
    </div>

    <script>
        const imageInput = document.getElementById('image-input');
        const preview = document.getElementById('preview');
        const result = document.getElementById('result');

        imageInput.addEventListener('change', function(e) {
            const file = e.target.files[0];
            if (file) {
                // Show image preview
                preview.src = URL.createObjectURL(file);
                preview.style.display = 'block';
                result.textContent = ''; // Clear previous result
            }
        });

    async function processImage() {
        const file = imageInput.files[0];
        if (!file) {
            alert('Please select an image first');
            return;
        }

        result.textContent = 'Processing image...';
        
        try {
            // Convert file to data URL
            const dataUrl = await new Promise((resolve) => {
                const reader = new FileReader();
                reader.onload = () => resolve(reader.result);
                reader.readAsDataURL(file);
            });
            
            // Now pass the data URL to img2txt
            const text = await puter.ai.img2txt(dataUrl);
            result.textContent = text || 'No text found in image';
        } catch (error) {
            result.textContent = 'Error: ' + error.message;
        }
    }   
    </script>
</body>
</html>

```


This example shows how to handle file uploads for OCR. It includes an image preview feature and processes local image files directly. The OCR function works with File objects just as easily as with URLs.

Example 3Batch OCR Processing
-----------------------------

Here's an example that processes multiple images and saves the results:

```
<html>
<body>
    <script src="https://js.puter.com/v2/"></script>
    
    <div>
        <h3>Batch OCR Processing</h3>
        <input type="file" id="image-input" accept="image/*" multiple>
        <button onclick="processBatch()">Process All Images</button>
        
        <div id="progress"></div>
        
        <div style="margin-top: 20px;">
            <h4>Results:</h4>
            <div id="results"></div>
        </div>
        
        <button onclick="saveResults()" id="save-button" style="display: none;">
            Save Results
        </button>
    </div>

    <script>
        let processedResults = [];

        // Convert File to data URL
        function fileToDataURL(file) {
            return new Promise((resolve) => {
                const reader = new FileReader();
                reader.onload = () => resolve(reader.result);
                reader.readAsDataURL(file);
            });
        }

        async function processBatch() {
            const files = document.getElementById('image-input').files;
            if (files.length === 0) {
                alert('Please select some images first');
                return;
            }

            const progress = document.getElementById('progress');
            const results = document.getElementById('results');
            results.innerHTML = '';
            processedResults = [];

            for (let i = 0; i < files.length; i++) {
                const file = files[i];
                progress.textContent = `Processing image ${i + 1} of ${files.length}...`;

                try {
                    // Convert to data URL first
                    const dataUrl = await fileToDataURL(file);
                    const text = await puter.ai.img2txt(dataUrl);
                    
                    // Store result
                    processedResults.push({
                        filename: file.name,
                        text: text,
                        timestamp: new Date().toISOString()
                    });

                    // Display result
                    results.innerHTML += `
                        <div style="margin-bottom: 20px;">
                            <strong>${file.name}</strong>
                            <pre>${text || 'No text found'}</pre>
                        </div>
                    `;
                } catch (error) {
                    results.innerHTML += `
                        <div style="margin-bottom: 20px; color: red;">
                            <strong>${file.name}</strong>: Error - ${error.message}
                        </div>
                    `;
                }
            }

            progress.textContent = 'All images processed!';
            document.getElementById('save-button').style.display = 'block';
        }

        async function saveResults() {
            try {
                const resultsText = processedResults.map(result => 
                    `File: ${result.filename}\nTimestamp: ${result.timestamp}\n\n${result.text}\n\n---\n\n`
                ).join('');

                await puter.fs.write('ocr-results.txt', resultsText);
                alert('Results saved to ocr-results.txt');
            } catch (error) {
                alert('Error saving results: ' + error.message);
            }
        }
    </script>
</body>
</html>

```


This advanced example demonstrates batch processing of multiple images. It includes several useful features:

*   Multiple file selection and processing
*   Progress tracking
*   Organized display of results
*   Saving results to a file in your Puter cloud storage
*   Error handling for individual files

Implementation Tips
-------------------

1.  Always validate input images before processing
2.  Show progress indicators for longer operations
3.  Handle errors gracefully and provide user feedback
4.  Consider image size limits and processing time
5.  Save or export results for later use
6.  Preview images when possible to ensure correct file selection

Related
-------

*   [Free, Unlimited OpenAI API](https://developer.puter.com/tutorials/free-unlimited-openai-api)
*   [Free, Unlimited Auth API](https://developer.puter.com/tutorials/free-unlimited-auth-api)
*   [Free, Unlimited Text-to-Speech API](https://developer.puter.com/tutorials/free-unlimited-text-to-speech-api)
*   [Free, Unlimited Claude API](https://developer.puter.com/tutorials/free-unlimited-claude-35-sonnet-api)