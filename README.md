This README provides a step-by-step guide on how to set up and run your Boys vs Girls TikTok Interactive Tower Game.
👦 Boys vs Girls: TikTok Interactive Tower 👧
This is a real-time interactive game where your TikTok Live viewers control the outcome. Viewers can build towers for their team using specific gifts or by typing in the chat.
🚀 Features
Real-time Physics: Towers grow and shrink based on live events.
Gift Integration: Specific gifts trigger massive "Fire" or "Sabotage" events.
Chat Control: Typing "B" or "G" adds points to the respective teams.
Automated Rounds: The game detects a winner, shows a celebration, and resets for the next round automatically.
Animated Environment: Includes a dynamic sky, aurora effects, and shooting stars.
🛠️ Prerequisites
Before starting, ensure you have the following installed:
Node.js (Version 20 or higher recommended): Download here
A TikTok Account: You must be able to go LIVE to use the real-time connection.
📥 Installation
Create a Project Folder:
Create a folder on your computer (e.g., tiktok-game) and place the three provided files inside:
index.html
server.js
package.json
Install Dependencies:
Open your terminal (Command Prompt, PowerShell, or Terminal) in that folder and run:
code
Bash
npm install
This will install tiktok-live-connector (to talk to TikTok) and ws (to talk to your browser).
🎮 How to Run the Game
Step 1: Start the Bridge Server
The server acts as a "bridge" between TikTok and your web browser. In your terminal, run:
code
Bash
node server.js
You should see a message: ⚡ Boys vs Girls bridge ready on ws://localhost:8080. Keep this window open while playing.
Step 2: Open the Game UI
Simply double-click the index.html file to open it in any modern web browser (Chrome or Edge recommended).
Step 3: Connect to your TikTok Live
Go LIVE on TikTok (using TikTok Live Studio or OBS).
In the game (on your browser), look at the right panel under "TIKTOK USERNAME".
Enter your username (without the @).
Click ▶ GO LIVE.
If successful, the status dot will turn Green and the "LIVE" pill will start pulsing.
🕹️ Gameplay Mechanics
Action	Result	Points
Gift: Fire (ID: 5583)	Adds blocks to Boys	+2 Blocks
Gift: Rose (ID: 5655)	Adds blocks to Girls	+2 Blocks
Gift: Rosa (ID: 8913)	Sabotages Girls tower	-5 Blocks
Gift: Necklace (ID: 9947)	Sabotages Boys tower	-5 Blocks
Chat: "B" or "Boys"	Adds height to Boys	+0.5 Blocks
Chat: "G" or "Girls"	Adds height to Girls	+0.5 Blocks
Win Condition: The first team to reach 200 blocks wins the round!
📺 How to Stream it on TikTok
To show this game to your viewers, use TikTok Live Studio or OBS:
Add a new "Window Capture" source.
Select your browser window showing the game.
(Optional) Hold Alt and drag the edges to crop out the "Right Panel" (the connection settings) so viewers only see the game and the leaderboard.
Interact with your chat and encourage them to "Type B or G to build!"
⚙️ Customization
Changing the Goal
Open index.html and change the GOAL constant at the top of the <script> section:
code
JavaScript
const GOAL = 500; // Change from 200 to 500
Changing Gift IDs
If you want to use different gifts (e.g., a "Tiny Diny" instead of a "Fire"), you need to find the Gift ID and update it in both server.js and index.html.
Find the ID in the server.js console log when someone sends a gift.
Update the constants at the top of both files to match the new ID.
❓ Troubleshooting
"Bridge not found": Make sure you ran node server.js in your terminal and that it is still running.
Not connecting to TikTok: Ensure you are actually LIVE. TikTok's API usually prevents connecting to accounts that are offline.
Blocks not appearing: Check the terminal window where server.js is running. If gifts are appearing there but not in the game, refresh the index.html page.
