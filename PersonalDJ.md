Prompt 1: Foundation & Library Management Goal: Create the project structure, configuration, and the music indexing logic.

Files to generate: config.yaml, init.py, and library.py.

Focus: Recursive scanning of ~/.hermes/music/, handling metadata (artist, title, genre) using tinytag or mutagen, and implementing the SQLite/JSON caching system for instant startup.

Outcome: A functional indexer that can categorize songs and podcasts.



Prompt 2: The Pirate Persona & TTS Wrapper Goal: Define the "soul" of DJ Squawk.

Files to generate: persona.py and tts_helper.py.

Focus: Building the vocabulary dictionary (Pirate + Gen Alpha slang), creating randomized templates for "bridge" talk, and the wrapper that intercepts strings to inject a "gravelly" pirate tone/accent before sending them to the system TTS.

Outcome: A module where you can input play_intro("Artist") and get a full pirate-style spoken string back.



Prompt 3: Audio Playback & The Core Loop
Goal: Handle the actual sound output and the continuous logic.

Files to generate: player.py and dj.py.

Focus: Implementing pyalsaaudio or pydub playback targeting the specific 3.5mm sound card. Building the "Daemon" loop that picks a song, triggers the TTS intro, plays the audio, and handles the 4–8 song podcast rotation logic.

Outcome: A skill that can actually play music in a sequence with "DJ talk" in between.



Prompt 4: Matrix Integration & Request Handling Goal: Connect the DJ to the outside world.

Files to generate: matrix_handler.py.

Focus: Connecting to the Matrix room, regex parsing for /request, logic for scanning chat history for shout-outs, and managing the in-memory request queue (with deduplication).

Outcome: The DJ now "listens" to the chat and can give live shout-outs on-air.



Prompt 5: Voice Intents & Final Assembly Goal: Enable voice control and wrap up the package.

Files to generate: intents/DJSquawk.intent, dialogs/, README.md, and any remaining "Treasure Chest" trivia logic.

Focus: Creating the Hermes/Rhasspy intent files for voice commands (skip, request, status) and ensuring the "persona switching" logic works so Percy can hand off control.

Outcome: The final deployment-ready folder and the activation command.
