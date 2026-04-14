most of the DJ script failed. after testing, hermes showed 6 out of 7 dependecy failures on installation. hermes then provided 6 individual prompts for making sure each dependency is installed before context filled. /reset or /new context after each prompt.



SECTION 1: Create DJ Skill Directory
   ------------------------------------
   Task: Create the DJ skill directory structure at /home/master/.hermes/skills/dj/
   Files needed:
   - DJ-Skill.md (main skill documentation)
   - dj.py (main DJ playback script)
   - config.md (configuration file)
   - matrix_handler.py (Matrix chat integration)
   - tts_helper.py (TTS helper for pirate voice)
   - intents.json (DJ command intents)
   - dialogs.json (conversation dialogs)
   - extensions.json (skill extensions)
   - player.py (audio player controls)
   - library.py (music library management)

   Requirements:
   - Create directory: mkdir -p ~/.hermes/skills/dj/
   - All files should be Python 3 compatible
   - Use UTF-8 encoding
   - Set appropriate permissions (644 for files, 755 for directory)

   SECTION 2: Install Python Dependencies
   ---------------------------------------
   Task: Install required Python packages for the DJ skill
   Packages needed:
   - pydub (for audio manipulation)

   Installation commands:
   - pip3 install pydub
   - pip3 install ffmpeg-python (optional, for advanced features)
   - pip3 install mutagen (for metadata reading)

   Verification:
   - python3 -c "import pydub; print(pydub.__version__)"

 SECTION 3: Configure DJ Settings
   --------------------------------
   Task: Create and configure the DJ configuration file (config.md)
   Configuration variables needed:
   - DJ_VOLUME (default: 0.8)
   - DJ_VOLUME_MIN (default: 0.3)
   - DJ_VOLUME_MAX (default: 1.0)
   - DJ_SAMPLE_RATE (default: 44100)
   - DJ_CHANNELS (default: 1 or 2)

   Additional settings:
   - DJ_MATRIX_ROOM (Matrix room for chat)
   - DJ_STATUS_INTERVAL (status update frequency in seconds)
   - DJ_AUTO_RESTART (boolean for auto-restart on crash)

   SECTION 4: Implement Main DJ Script (dj.py)
   --------------------------------------------
   Task: Create the main DJ playback script at ~/.hermes/skills/dj/dj.py
   Key features needed:
   - Continuous DJ loop with smart playlist rotation
   - Audio playback using pydub/ffmpeg
   - Volume control with fade in/out
   - Playlist management (random, queue-based)
   - Error handling for audio files
   - Logging to console and files

   Functions to implement:
   - init(): Initialize DJ subsystem
   - load_playlist(): Load music files from library
   - play_track(): Play single track with volume control
   - next_track(): Move to next track
   - stop(): Stop playback gracefully
   - status(): Get current status


SECTION 5: Implement Matrix Handler (matrix_handler.py)
   --------------------------------------------------------
   Task: Create Matrix chat integration at ~/.hermes/skills/dj/matrix_handler.py
   Features needed:
   - Listen for Matrix chat messages
   - Parse DJ commands (e.g., "arrr, play some rock", "next song")
   - Respond with pirate-themed DJ announcements
   - Handle voice commands via TTS
   - Integrate with main DJ script

   Command patterns to recognize:
   - "play [genre/type]"
   - "next" / "skip"
   - "pause" / "resume"
   - "volume up/down"
   - "stop"
   - "status"
   - "shuffle on/off"

   SECTION 6: Implement TTS Helper (tts_helper.py)
   -----------------------------------------------
   Task: Create TTS helper for pirate voice announcements at ~/.hermes/skills/dj/tts_helper.py
   Features needed:
   - Pirate-themed voice modulation (lower pitch, deeper tone)
   - Text-to-speech using existing TTS system
   - Announce track changes, volume adjustments
   - Handle shout-outs and requests
   - Cache audio for repeated announcements

   Voice characteristics:
   - Base pitch: -10% to -20%
   - Speed: 1.0x normal
   - Add pirate phrases: "arrr", "aye", "me hearties", "shiver me timbers"



Post-Installation Verification Commands
   ---------------------------------------
   After all sections complete, run these checks. (if they fail, remember that and create a prompt for each failure to be fixed in it's own context (make sure to put the necessary context prior to the prompt to keep agent on course):

   1. Directory exists:
      ls -la ~/.hermes/skills/dj/

   2. All files present:
      wc -l ~/.hermes/skills/dj/*.py ~/.hermes/skills/dj/*.md

   3. Python syntax check:
      python3 -m py_compile ~/.hermes/skills/dj/dj.py
      python3 -m py_compile ~/.hermes/skills/dj/matrix_handler.py
      python3 -m py_compile ~/.hermes/skills/dj/tts_helper.py

   4. Import test:
      cd ~/.hermes/skills/dj && python3 -c "import dj; import pydub; print('OK')"

   5. Load skill in Hermes:
      hermes skill load DJ-Skill.md

   6. Start DJ (test):
      hermes skill run DJ-Skill.md --test

/new
Alpha Test
load any music file from the library. set output volume to 50%. let track play for 15 seconds and end test.
