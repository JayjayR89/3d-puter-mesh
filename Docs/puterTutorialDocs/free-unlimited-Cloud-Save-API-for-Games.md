# Free, Unlimited Cloud Save API for Games
[Tutorials](https://developer.puter.com/tutorials/)
------------------------

Want to add cloud saves to your game without the hassle of managing servers or databases or paying for proprietary services? With Puter.js, you can save player progress, game states, and more to the cloud for free, without any API keys or usage limits. This tutorial will show you how to use Puter.js to implement a cloud save system for your web games.

Getting Started
---------------

Add Puter.js to your game with a single line:

```
<script src="https://js.puter.com/v2/"></script>

```


That's it - you're ready to start saving game data to the cloud.

Example 1Simple Save/Load System
--------------------------------

Let's start with a basic save/load system for a game:

```
<html>
<body>
    <script src="https://js.puter.com/v2/"></script>
    
    <!-- Simple game UI -->
    <div>
        <h3>Player Stats</h3>
        <p>Gold: <span id="gold">0</span></p>
        <p>Level: <span id="level">1</span></p>
        
        <button onclick="addGold()">Get Gold</button>
        <button onclick="levelUp()">Level Up</button>
        <br><br>
        <button onclick="saveGame()">Save Game</button>
        <button onclick="loadGame()">Load Game</button>
    </div>

    <script>
        // Game state
        let playerData = {
            gold: 0,
            level: 1,
            lastSaved: null
        };

        // Game actions
        function addGold() {
            playerData.gold += 10;
            updateUI();
        }

        function levelUp() {
            playerData.level += 1;
            updateUI();
        }

        function updateUI() {
            document.getElementById('gold').textContent = playerData.gold;
            document.getElementById('level').textContent = playerData.level;
        }

        // Save game data
        async function saveGame() {
            try {
                playerData.lastSaved = new Date().toISOString();
                await puter.kv.set('gameData', JSON.stringify(playerData));
                alert('Game saved!');
            } catch (error) {
                alert('Failed to save: ' + error);
            }
        }

        // Load game data
        async function loadGame() {
            try {
                const saved = await puter.kv.get('gameData');
                if (saved) {
                    playerData = JSON.parse(saved);
                    updateUI();
                    alert('Game loaded!');
                } else {
                    alert('No saved game found');
                }
            } catch (error) {
                alert('Failed to load: ' + error);
            }
        }
    </script>
</body>
</html>

```


This first example demonstrates the basics of saving and loading game data. The code maintains a simple game state with gold and level variables, storing them in Puter's key-value store. When a player clicks "Save Game", their current progress is converted to JSON and stored in the cloud with a timestamp. The "Load Game" button retrieves this data and restores their progress.

Key points about this example:

*   Game state is kept in a single object, making it easy to save and load
*   The `lastSaved` timestamp helps track when the game was last saved
*   Data is stored using [`puter.kv.set()`](https://docs.puter.com/KV/set/) which handles all the cloud storage details
*   JSON is used to convert the game state to a format that can be stored

Example 2Auto-Save System
-------------------------

Here's how to implement an auto-save system that saves after important actions:

```
<html>
<body>
    <script src="https://js.puter.com/v2/"></script>
    
    <div>
        <h3>RPG Character</h3>
        <p>Health: <span id="health">100</span></p>
        <p>Experience: <span id="xp">0</span></p>
        
        <button onclick="gainXP()">Gain XP</button>
        <button onclick="heal()">Heal</button>
        <p id="save-status"></p>
    </div>

    <script>
        let gameState = {
            health: 100,
            xp: 0
        };

        let saveTimeout;
        const SAVE_DELAY = 2000; // Wait 2 seconds after last action

        function updateUI() {
            document.getElementById('health').textContent = gameState.health;
            document.getElementById('xp').textContent = gameState.xp;
        }

        function setSaveStatus(message) {
            document.getElementById('save-status').textContent = message;
        }

        // Schedule an auto-save
        function scheduleAutoSave() {
            clearTimeout(saveTimeout);
            setSaveStatus('Waiting to save...');
            
            saveTimeout = setTimeout(async () => {
                try {
                    await puter.kv.set('autoSave', JSON.stringify(gameState));
                    setSaveStatus('Game saved automatically!');
                } catch (error) {
                    setSaveStatus('Auto-save failed!');
                }
            }, SAVE_DELAY);
        }

        // Game actions
        function gainXP() {
            gameState.xp += 10;
            updateUI();
            scheduleAutoSave();
        }

        function heal() {
            gameState.health = 100;
            updateUI();
            scheduleAutoSave();
        }

        // Load last auto-save when game starts
        async function loadLastGame() {
            try {
                const saved = await puter.kv.get('autoSave');
                if (saved) {
                    gameState = JSON.parse(saved);
                    updateUI();
                    setSaveStatus('Previous game loaded!');
                }
            } catch (error) {
                setSaveStatus('Could not load previous game');
            }
        }

        loadLastGame();
    </script>
</body>
</html>

```


The auto-save system builds on the basic save/load functionality by automatically saving after player actions. Instead of saving immediately after every action, it uses a delay timer to prevent excessive saves. This is particularly useful for games where players make frequent actions.

The auto-save implementation demonstrates several important concepts:

*   Uses a timeout to batch multiple quick actions into a single save
*   Provides visual feedback about the save status
*   Automatically loads the previous game state when starting
*   Saves after meaningful actions rather than at fixed intervals

This approach is ideal for RPGs, adventure games, or any game where losing progress would be frustrating for players.

Example 3Save Multiple Characters
---------------------------------

Here's how to implement multiple character saves:

```
<html>
<body>
    <script src="https://js.puter.com/v2/"></script>
    
    <div>
        <h3>Character Selection</h3>
        <div id="character-list"></div>
        <br>
        <button onclick="createCharacter()">New Character</button>
        
        <div id="active-character" style="display: none">
            <h3>Playing as: <span id="char-name"></span></h3>
            <p>Power: <span id="power">1</span></p>
            <button onclick="increasePower()">Train</button>
            <button onclick="saveCharacter()">Save</button>
        </div>
    </div>

    <script>
        let currentChar = null;

        async function loadCharacters() {
            const charList = document.getElementById('character-list');
            charList.innerHTML = 'Loading characters...';

            try {
                // Get list of all character saves
                const chars = await puter.kv.list('char_*');
                
                if (chars.length === 0) {
                    charList.innerHTML = 'No characters found';
                    return;
                }

                // Create buttons for each character
                charList.innerHTML = chars
                    .map(charKey => {
                        const name = charKey.replace('char_', '');
                        return `
                            <button onclick="loadCharacter('${name}')">
                                Play as ${name}
                            </button>
                            <button onclick="deleteCharacter('${name}')">
                                ❌
                            </button>
                            <br><br>
                        `;
                    })
                    .join('');
            } catch (error) {
                charList.innerHTML = 'Failed to load characters';
            }
        }

        async function createCharacter() {
            const name = prompt('Enter character name:');
            if (!name) return;

            const newChar = {
                name: name,
                power: 1,
                created: Date.now()
            };

            try {
                await puter.kv.set(`char_${name}`, JSON.stringify(newChar));
                loadCharacters();
            } catch (error) {
                alert('Failed to create character');
            }
        }

        async function loadCharacter(name) {
            try {
                const charData = await puter.kv.get(`char_${name}`);
                if (charData) {
                    currentChar = JSON.parse(charData);
                    updateCharacterUI();
                }
            } catch (error) {
                alert('Failed to load character');
            }
        }

        function updateCharacterUI() {
            const activeDiv = document.getElementById('active-character');
            activeDiv.style.display = 'block';
            document.getElementById('char-name').textContent = currentChar.name;
            document.getElementById('power').textContent = currentChar.power;
        }

        async function saveCharacter() {
            if (!currentChar) return;
            
            try {
                await puter.kv.set(`char_${currentChar.name}`, JSON.stringify(currentChar));
                alert('Character saved!');
            } catch (error) {
                alert('Failed to save character');
            }
        }

        function increasePower() {
            if (!currentChar) return;
            currentChar.power++;
            updateCharacterUI();
        }

        async function deleteCharacter(name) {
            if (confirm(`Really delete ${name}?`)) {
                await puter.kv.del(`char_${name}`);
                loadCharacters();
            }
        }

        // Initialize by loading character list
        loadCharacters();
    </script>
</body>
</html>

```


This example shows how to manage multiple save files - in this case, different character saves. It demonstrates a complete character management system where players can create, load, save, and delete different characters. This pattern is common in RPGs and other games where players might want to maintain multiple playthroughs.

The multiple character system showcases several advanced techniques:

*   Uses a prefix ('char\_') to organize related saves in the key-value store
*   Implements a complete UI for character management
*   Demonstrates how to list and delete saves
*   Shows how to handle active character state separately from saved data

This approach can be adapted for other types of multiple save systems, such as save slots or different game worlds.

Quick Implementation Tips
-------------------------

1.  Always check for data validity when loading saves - use try/catch blocks and verify data structure.
2.  Save timestamps with your game data to show players when they last saved.
3.  For large save files (like complete game worlds), use [`puter.fs.write()`](https://docs.puter.com/FS/write/) instead of `puter.kv`.
4.  Implement auto-saves after important game events, not on a timer.
5.  Keep save data small by only storing essential information.

Advanced Features
-----------------

For larger games, consider using these additional features:

```
// Save file versioning
const saveData = {
    version: "1.0",
    player: playerState,
    timestamp: Date.now()
};

// Compress large saves
const compressed = btoa(JSON.stringify(saveData));
await puter.kv.set('gameSave', compressed);

// Multiple save slots
await puter.kv.set(`save_slot_${slotNumber}`, saveData);

```


Related
-------

*   [Free, Unlimited Auth API](https://developer.puter.com/tutorials/free-unlimited-auth-api)
*   [Add a Cloud Key-Value Store to Your App: A Free Alternative to DynamoDB](https://developer.puter.com/tutorials/add-a-cloud-key-value-store-to-your-app-a-free-alternative-to-dynamodb)
*   [Free, Unlimited OpenAI API](https://developer.puter.com/tutorials/free-unlimited-openai-api)
*   [Free, Unlimited Text-to-Speech API](https://developer.puter.com/tutorials/free-unlimited-text-to-speech-api)
*   [Free, Unlimited Claude API](https://developer.puter.com/tutorials/free-unlimited-claude-35-sonnet-api)