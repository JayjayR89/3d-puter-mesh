# Add Key-Value Store to Your App: A Free Alternative to DynamoDB
[Tutorials](https://developer.puter.com/tutorials/)
------------------------

This tutorial will show you how to use Puter.js to add a key-value store to your web application, providing a free alternative to Amazon DynamoDB. With Puter.js, you can easily store and retrieve data without worrying about setting up a backend or managing a database.

Getting Started
---------------

You can use Puter.js without any API keys or sign-ups. To start using Puter.js for key-value store operations, include the following script tag in your HTML file, either in the `<head>` or `<body>` section:

```
<script src="https://js.puter.com/v2/"></script>

```


All set! You can now start using Puter.js for key-value store operations without any additional setup.

Example 1Basic Key-Value Operations
-----------------------------------

Let's start with the basic operations: setting a value, getting a value, and deleting a value.

```
<html>
<body>
    <script src="https://js.puter.com/v2/"></script>
    <script>
        (async () => {
            // Set a value
            await puter.kv.set('user_name', 'Alice');
            puter.print('Value set<br>');

            // Get a value
            const name = await puter.kv.get('user_name');
            puter.print('Retrieved name:', name, '<br>');

            // Delete a value
            await puter.kv.del('user_name');
            puter.print('Value deleted<br>');

            // Try to get the deleted value
            const deletedName = await puter.kv.get('user_name');
            puter.print('Deleted name:', deletedName, '<br>'); // Will be null
        })();
    </script>
</body>
</html>

```


The example above demonstrates how to use Puter.js to perform basic key-value operations. You can set a value with [`puter.kv.set()`](https://docs.puter.com/KV/set/), retrieve a value with [`puter.kv.get()`](https://docs.puter.com/KV/get/), and delete a value with [`puter.kv.del()`](https://docs.puter.com/KV/del/).

Example 2Create a Simple User Profile Manager
---------------------------------------------

Now, let's create a more practical example: a user profile manager that stores and retrieves user information.

```
<html>
<body>
    <h1>User Profile Manager</h1>
    <form id="profile-form">
        <input type="text" id="username" placeholder="Username" required>
        <input type="email" id="email" placeholder="Email" required>
        <input type="number" id="age" placeholder="Age" required>
        <button type="submit">Save Profile</button>
    </form>
    <button id="load-profile">Load Profile</button>
    <div id="profile-display"></div>

    <script src="https://js.puter.com/v2/"></script>
    <script>
        const form = document.getElementById('profile-form');
        const loadButton = document.getElementById('load-profile');
        const display = document.getElementById('profile-display');

        form.addEventListener('submit', async (e) => {
            e.preventDefault();
            const username = document.getElementById('username').value;
            const email = document.getElementById('email').value;
            const age = document.getElementById('age').value;

            const profile = { email, age };
            await puter.kv.set(`user:${username}`, JSON.stringify(profile));
            alert('Profile saved!');
        });

        loadButton.addEventListener('click', async () => {
            const username = document.getElementById('username').value;
            const profileJson = await puter.kv.get(`user:${username}`);
            
            if (profileJson) {
                const profile = JSON.parse(profileJson);
                display.innerHTML = `
                    <h2>Profile for ${username}</h2>
                    <p>Email: ${profile.email}</p>
                    <p>Age: ${profile.age}</p>
                `;
            } else {
                display.innerHTML = '<p>Profile not found</p>';
            }
        });
    </script>
</body>
</html>

```


Example 3Working with Multiple Keys
-----------------------------------

Puter.js also allows you to work with multiple keys at once. Let's create an example that demonstrates listing keys and batch operations.

```
<html>
<body>
    <h1>Product Inventory</h1>
    <form id="add-product">
        <input type="text" id="product-name" placeholder="Product Name" required>
        <input type="number" id="product-price" placeholder="Price" required>
        <button type="submit">Add Product</button>
    </form>
    <button id="list-products">List Products</button>
    <button id="clear-inventory">Clear Inventory</button>
    <div id="product-list"></div>

    <script src="https://js.puter.com/v2/"></script>
    <script>
        const addForm = document.getElementById('add-product');
        const listButton = document.getElementById('list-products');
        const clearButton = document.getElementById('clear-inventory');
        const productList = document.getElementById('product-list');

        addForm.addEventListener('submit', async (e) => {
            e.preventDefault();
            const name = document.getElementById('product-name').value;
            const price = document.getElementById('product-price').value;

            await puter.kv.set(`product:${name}`, price);
            alert('Product added!');
        });

        listButton.addEventListener('click', async () => {
            const products = await puter.kv.list('product:*', true);
            productList.innerHTML = '<h2>Products:</h2>';
            products.forEach(product => {
                productList.innerHTML += `<p>${product.key.split(':')
[1]}: ${product.value}</p>`;
            });
        });

        clearButton.addEventListener('click', async () => {
            const products = await puter.kv.list('product:*');
            for (const key of products) {
                await puter.kv.del(key);
            }
            alert('Inventory cleared!');
            productList.innerHTML = '';
        });
    </script>
</body>
</html>

```


This example demonstrates how to use the [`list`](https://docs.puter.com/KV/list/) method to retrieve multiple keys matching a pattern, and how to perform batch operations by iterating over the results.

Example 4Atomic Operations
--------------------------

Puter.js also supports atomic increment and decrement operations, which are useful for counters or any numeric values that need to be updated concurrently.

```
<html>
<body>
    <h1>Visit Counter</h1>
    <p>This page has been visited <span id="visit-count">0</span> times.</p>
    <button id="reset-count">Reset Count</button>

    <script src="https://js.puter.com/v2/"></script>
    <script>
        const countDisplay = document.getElementById('visit-count');
        const resetButton = document.getElementById('reset-count');

        async function updateVisitCount() {
            const count = await puter.kv.incr('visit_count');
            countDisplay.textContent = count;
        }

        resetButton.addEventListener('click', async () => {
            await puter.kv.set('visit_count', '0');
            countDisplay.textContent = '0';
        });

        updateVisitCount();
    </script>
</body>
</html>

```


This example uses the [`incr`](https://docs.puter.com/KV/incr/) method to atomically increment a counter, ensuring accurate counts even with concurrent updates. That's it!

You now have a free alternative to DynamoDB using Puter.js. This allows you to add key-value store capabilities to your web applications without worrying about setting up a backend or managing a database.