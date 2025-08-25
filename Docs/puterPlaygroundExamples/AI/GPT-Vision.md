<html>
<body>
    <script src="https://js.puter.com/v2/"></script>
    <img src="https://assets.puter.site/doge.jpeg" style="display:block;">
    <script>
        // Loading ...
        puter.print(`Loading...`);

        // Chat with GPT-4 Vision
        puter.ai.chat(
            `What do you see?`, 
            `https://assets.puter.site/doge.jpeg`)
        .then(puter.print);
    </script>
</body>
</html>