# Free, Unlimited Auth API
[Tutorials](https://developer.puter.com/tutorials/)
------------------------

This tutorial will show you how to implement user authentication in your web applications using Puter.js, completely free and without any API keys or usage restrictions. Using Puter.js, you can add secure user authentication to your applications without managing servers, databases, or authentication providers.

Getting Started
---------------

Puter.js works without any API keys or sign-ups. To start using Puter.js, include the following script tag in your HTML file, either in the `<head>` or `<body>` section:

```
<script src="https://js.puter.com/v2/"></script>

```


You're now ready to use Puter.js for free authentication capabilities. No API keys or sign-ups are required.

Example 1Basic Authentication Flow
----------------------------------

Here's a simple example showing how to implement a sign-in button and handle authentication:

```
<html>
<body>
    <script src="https://js.puter.com/v2/"></script>
    <button id="sign-in">Sign in</button>
    <div id="user-info"></div>

    <script>
        // Get the sign in button
        const signInButton = document.getElementById('sign-in');
        const userInfoDiv = document.getElementById('user-info');

        // Add click event listener to the sign in button
        signInButton.addEventListener('click', async () => {
            try {
                // Attempt to sign in
                await puter.auth.signIn();
                
                // Get user information after successful sign in
                const user = await puter.auth.getUser();
                userInfoDiv.innerHTML = `Welcome, ${user.username}!`;
                
                // Hide the sign in button
                signInButton.style.display = 'none';
            } catch (error) {
                console.error('Sign in failed:', error);
            }
        });
    </script>
</body>
</html>

```


Example 2Check Authentication Status
------------------------------------

You can check if a user is already signed in using the [`isSignedIn()`](https://docs.puter.com/Auth/isSignedIn/) method:

```
<html>
<body>
    <script src="https://js.puter.com/v2/"></script>
    <div id="status"></div>
    <button id="sign-in" style="display: none;">Sign in</button>
    <button id="sign-out" style="display: none;">Sign out</button>

    <script>
        const statusDiv = document.getElementById('status');
        const signInButton = document.getElementById('sign-in');
        const signOutButton = document.getElementById('sign-out');

        // Function to update UI based on auth state
        async function updateAuthUI() {
            if (puter.auth.isSignedIn()) {
                const user = await puter.auth.getUser();
                statusDiv.textContent = `Signed in as: ${user.username}`;
                signInButton.style.display = 'none';
                signOutButton.style.display = 'block';
            } else {
                statusDiv.textContent = 'Not signed in';
                signInButton.style.display = 'block';
                signOutButton.style.display = 'none';
            }
        }

        // Set up event listeners
        signInButton.addEventListener('click', async () => {
            await puter.auth.signIn();
            updateAuthUI();
        });

        signOutButton.addEventListener('click', () => {
            puter.auth.signOut();
            updateAuthUI();
        });

        // Check initial auth state
        updateAuthUI();
    </script>
</body>
</html>

```


Example 3Protected Content
--------------------------

Here's how to create a simple application with protected content that's only visible to authenticated users:

```
<html>
<body>
    <script src="https://js.puter.com/v2/"></script>
    <div id="public-content">
        <h1>Welcome to Our App</h1>
        <p>Please sign in to view protected content.</p>
        <button id="sign-in">Sign in</button>
    </div>

    <div id="protected-content" style="display: none;">
        <h1>Protected Content</h1>
        <p>Welcome to the protected area of our application!</p>
        <button id="sign-out">Sign out</button>
    </div>

    <script>
        const publicContent = document.getElementById('public-content');
        const protectedContent = document.getElementById('protected-content');
        const signInButton = document.getElementById('sign-in');
        const signOutButton = document.getElementById('sign-out');

        async function updateUI() {
            if (puter.auth.isSignedIn()) {
                publicContent.style.display = 'none';
                protectedContent.style.display = 'block';
            } else {
                publicContent.style.display = 'block';
                protectedContent.style.display = 'none';
            }
        }

        signInButton.addEventListener('click', async () => {
            await puter.auth.signIn();
            updateUI();
        });

        signOutButton.addEventListener('click', () => {
            puter.auth.signOut();
            updateUI();
        });

        // Check initial auth state
        updateUI();
    </script>
</body>
</html>

```


Example 4Combining Auth with Cloud Storage
------------------------------------------

Here's an example that combines authentication with cloud storage to create a simple personal notes application:

```
<html>
<body>
    <script src="https://js.puter.com/v2/"></script>
    <div id="auth-container">
        <button id="sign-in">Sign in to access your notes</button>
    </div>

    <div id="notes-container" style="display: none;">
        <h2>My Notes</h2>
        <textarea id="note-content" rows="10" cols="50"></textarea>
        <br>
        <button id="save-note">Save Note</button>
        <button id="sign-out">Sign out</button>
    </div>

    <script>
        const authContainer = document.getElementById('auth-container');
        const notesContainer = document.getElementById('notes-container');
        const noteContent = document.getElementById('note-content');
        const saveNoteButton = document.getElementById('save-note');
        const signInButton = document.getElementById('sign-in');
        const signOutButton = document.getElementById('sign-out');

        async function loadNote() {
            try {
                const blob = await puter.fs.read('my-note.txt');
                const text = await blob.text();
                noteContent.value = text;
            } catch (error) {
                // File doesn't exist yet, that's okay
                noteContent.value = '';
            }
        }

        async function saveNote() {
            await puter.fs.write('my-note.txt', noteContent.value);
            alert('Note saved!');
        }

        async function updateUI() {
            if (puter.auth.isSignedIn()) {
                authContainer.style.display = 'none';
                notesContainer.style.display = 'block';
                await loadNote();
            } else {
                authContainer.style.display = 'block';
                notesContainer.style.display = 'none';
            }
        }

        signInButton.addEventListener('click', async () => {
            await puter.auth.signIn();
            updateUI();
        });

        signOutButton.addEventListener('click', () => {
            puter.auth.signOut();
            updateUI();
        });

        saveNoteButton.addEventListener('click', saveNote);

        // Check initial auth state
        updateUI();
    </script>
</body>
</html>

```


That's it! You now have a free and unlimited authentication system using Puter.js. This allows you to add secure user authentication to your web applications without managing servers or worrying about usage limits.

Best Practices
--------------

When implementing authentication in your web applications with Puter.js, always verify the authentication status before displaying protected content. This can be done using the [`isSignedIn()`](https://docs.puter.com/Auth/isSignedIn/) method at key points in your application flow.

Your application should handle authentication errors gracefully and provide clear feedback to users when authentication fails. It's crucial to update your UI immediately after any authentication state changes to maintain a consistent user experience.

Consider building on top of the authentication system by combining it with other Puter.js features. For example, you might use cloud storage to save user preferences or leverage the AI capabilities to provide personalized experiences for authenticated users.

Related
-------

*   [Free, Unlimited OpenAI API](https://developer.puter.com/tutorials/free-unlimited-openai-api)
*   [Free, Unlimited Claude API](https://developer.puter.com/tutorials/free-unlimited-claude-35-sonnet-api)
*   [Free, Unlimited OpenRouter API](https://developer.puter.com/tutorials/free-unlimited-openrouter-api)
*   [Free, Unlimited Text-to-Speech API](https://developer.puter.com/tutorials/free-unlimited-text-to-speech-api)