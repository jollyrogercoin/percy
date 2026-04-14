your context filled up on this last prompt. you may have already set some of this up, so check and if something is setup already, skip it.

You are an expert Python skill developer for the Hermes / Rhasspy-style voice-agent framework. Your task is to build a complete, production-ready, expandable skillset for a new DJ persona named DJ Squawk (the fun, swashbuckling Personal DJ). Create the entire skill inside the folder:
~/.hermes/skills/dj/

This skill must run as a continuous background DJ service for the server dedicated sound card. Percy already supports multiple personas; this skill registers a new one called “DJ Squawk” that can be activated with voice commands such as “switch to pirate DJ”, “arrr, let’s sail the airwaves”, or similar.

Core Persona & Voice Rules (strictly enforced in every spoken line)
Character: Boisterous, playful pirate parrot perched on the shoulder of every listener. Cheeky first mate on the airwaves.
Speech style: Always talk like a pirate — naturally weave in “Arrr!”, “Ahoy!”, “Ye scurvy landlubbers!”, “Shiver me timbers!”, “Avast!”, “Belay that!”, “Me hearties!”, “Yo ho ho!”, etc. Try to include a few new gen alpha language terms in speech patterns (i.e. "peak", "unc", "maxxing", etc).
Tone: Warm, energetic, entertaining, never mean. Make every listener feel like part of the crew.
Voice synthesis: Use the existing TTS tools Percy already has. Force a slightly gravelly, enthusiastic pirate accent on every utterance. Every line must include pirate flair naturally (no dry announcements).

Music & Media Library
All audio lives in ~/.hermes/music/ and any subfolders.
There is a special subfolder ~/.hermes/music/podcasts/ containing podcast episode files (mp3, m4a, etc.).
The DJ must be able to recursively scan the entire music tree, build a library index on startup (and refresh on demand), and intelligently select tracks.

Core DJ Loop (continuous operation)
Pick a song or podcast segment that flows well from the previous track (genre-aware, tempo-aware, mood-aware — get creative with simple heuristics or metadata).
Play the audio directly through the dedicated sound card’s 3.5mm speaker port (use aplay, ffplay, or pydub + ALSA device; auto-detect the correct sound card).

Between tracks, insert a short spoken break (5–15 seconds) using TTS in the pirate voice: Normal radio DJ pattern: “Arrr, that was a barn-burner from the high seas!”, artist/title, fun facts, jokes, etc.
Occasionally read a shout-out (see below).
Occasionally announce a listener request that was just fulfilled.
Occasionally tease the next track.

Every 4–8 songs, randomly decide to play a podcast episode instead of a song (treat it as a “Pirate’s Log” segment). Cycle through episodes fairly so the same one doesn’t repeat too soon. After the episode ends, return to music.

Matrix Integration (required)
Connect to the Matrix home room (use the existing Matrix client Percy already has).
Listen for commands in the format: /request "song title or artist" — queue the request and acknowledge it live in the room with a pirate reply.
Every 3–6 tracks, scan the last 30 minutes of chat history for any messages that look like shout-outs (e.g., “shoutout to @user”, “big ups to the crew”, or any message tagged with the station). Pick one at random and read it on-air in full pirate style: “Ahoy me hearties! We’ve got a shout-out from the scallywag @user who says…”
Keep a simple in-memory queue for requests and a short-term memory of recent shout-outs.

Skill Structure & Expandability (make this future-proof)

Organize the skill exactly like this:

~/.hermes/skills/dj/
├── __init__.py
├── dj.py                  # main continuous DJ loop (runs as a daemon thread)
├── persona.py             # all spoken lines, pirate vocabulary, joke templates
├── library.py             # music/podcast scanner, metadata helper, smart selection
├── player.py              # low-level audio playback on the dedicated sound card
├── matrix_handler.py      # Matrix listener, request queue, shout-out parser
├── tts_helper.py          # wrapper that forces pirate accent on every TTS call
├── config.yaml            # easy-to-edit settings (music path, sound card, persona name, etc.)
├── intents/               # Hermes-style intent files if needed for voice activation
│   └── DJSquawk.intent
├── dialogs/               # example dialog responses
└── extensions/            # empty folder with a README explaining how to add new features

Must-Have Features (implement all of them)
Full library indexing with caching (JSON or SQLite) so it starts instantly.
Smart playlist generation: ability to create temporary “themed sets” (e.g., “high-seas rock”, “tropical reggae”, “pirate shanties”).
Request queue with deduplication and polite rejection if song not found.
Graceful fade/cross-fade between tracks when possible.
Voice-activated controls: “DJ Squawk, drop the next banger”, “request [song]”, “shout out to [name]”, “skip this scurvy tune”, “what’s in the hold?” (list current playlist), etc.
Auto-restart / crash recovery — the DJ must never stop broadcasting.
Logging to ~/.hermes/logs/dj.log with clear timestamps and what was played/spoken.
Hot-reload support for the config.yaml so new music can be dropped in without restarting the whole skill.

Creative Expansions (add these now so the skill is already rich and easy to grow)
“Treasure Chest” — random fun facts or pirate trivia spoken between songs.
“Crew Request Hour” — every X minutes the DJ announces it’s request time and reads several queued requests back-to-back.
“Podcast of the Deep” — special longer segment where an entire podcast episode plays with pirate intro/outro.
Simple web dashboard (optional Flask mini-server on localhost:9999) showing now-playing, recent requests, and a “drop a coin in the hat” fake tip jar (just for fun).
Future-proof hooks: clear functions with docstrings so the user can later add weather reads, news segments, live listener contests, etc.
Ability to switch personas on the fly while still keeping the music playing (so Percy can hand off to other personas and come back).

Technical Constraints & Best Practices
Use only Python 3.10+ standard library + packages already available in the Percy environment (pydub, python-matrix-client, tinytag, mutagen, pyalsaaudio, etc.).
Never block the main Hermes event loop.
All spoken lines must be generated on-the-fly with TTS so the DJ always sounds fresh.
Include comprehensive inline comments and a top-level README.md inside the skill folder explaining every module.
Make every major class/method easily subclassable or overridable for future expansions.

Output the complete folder structure with every file’s full code. When you finish, print “ DJ SKILL FOR DJ SQUAWK IS READY TO BE DEPLOYED” and give the exact one-line command the user should run to activate the new persona.Start building now. Make this the most fun, alive, and expandable DJ skill Percy has ever had. Arrr! Let’s make the airwaves sing!
