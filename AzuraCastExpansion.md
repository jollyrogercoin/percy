Prompt 1:
"We are building an expansion for DJ Squawk, a Linux-based personal radio agent. The system must use the official AzuraCast Docker installation.

Create the directory /var/azuracast, download the docker.sh installer from the official repo, and run the install command.

Configure the AzuraCast instance to accept an external Base Source connection, which our FFmpeg bridge will use to feed the audio from the local sound card.

When setting up AzuraCast, if there is already a service hosted on the default port, change port to a free port in the 8000 range."



Prompt 2:
"We are expanding the DJ Squawk Linux home server agent. The goal is to take the audio currently playing through the physical sound card and simultaneously broadcast it via a self-hosted AzuraCast instance running on this same machine.

Your current task:

Install AzuraCast: Use the official Docker-based installation method. Create /var/azuracast, fetch the docker.sh setup script, and run the automated installation.

Credential Management: Create a skill manage_creds that handles a persistent JSON config at ~/.dj_squawk_config.

This skill must store the local connection details for the AzuraCast 'Source' (e.g., localhost, the streamer port, mount point, and source password).

Implement SET, GET, and UPDATE functions for these credentials.

Note: AzuraCast will run in Docker, but our audio bridge will run on the host to access the sound card. Confirm once the Docker containers are spinning and the credential skill is ready."



Prompt 3:
"We need to **configure the AzuraCast instance to accept an external Base Source connection**. This is for the FFmpeg bridge to feed audio from the local sound card. Continuing the DJ Squawk expansion (Local Audio + AzuraCast Stream). We have the credentials stored; now we need to implement the 'Radio Station' behavior.

Your current task: Create the streaming control skills.

Skill azura_start:

Retrieve credentials via manage_creds.

Use FFmpeg to capture the live audio from the sound card's 'monitor' (PulseAudio/PipeWire) or ALSA loopback.

Stream this audio to the remote AzuraCast mount point while ensuring the local speakers keep playing.

Run this as a background process and log the PID.

Skill azura_stop:

Locate and terminate only the FFmpeg process associated with the stream.

Provide a status check to confirm if the stream is currently 'On Air' or 'Offline'."



Prompt 4: run pre-flight checks to validate everything is installed and available including the azuracast server. once initial tests are done, report back for next task. don't try to fix anything yet, just report test results



Prompt 5:  set the soundcard volume to 50% and run a 10 second audio test with any one of the music files in your music library.



Prompt 6: Install NeuTTS Air and integrate it as the primary Text-to-Speech (TTS) engine for the DJ Squawk service.

1. Package Install: Create a dedicated virtual environment or use the existing Hermes environment to run:

Bash
pip install "neutts[llama,onnx]"
Model Procurement: Download a high-fidelity GGUF backbone and the NeuCodec decoder from the Neuphonic HuggingFace collection. Store these in ~/.cache/neutts/.

Dependencies: Ensure libopenblas-dev is installed on the host to accelerate the GGUF inference.

2. Skill Creation: generate_dj_voice
Create a Hermes skill that bridges the agent's text output to NeuTTS. It must:

Reference Audio: Use a 5–10 second .wav file (e.g., dj_persona.wav) for instant voice cloning so the DJ has a consistent "radio" personality.

Execution: Run the NeuTTS inference to generate an output file (e.g., /tmp/dj_announcement.wav).

Hardware Routing: Pipe the output directly to the primary sound card using aplay or paplay to mix it with the current music stream.

3. Integration & Logic
Ducking: Ensure that when generate_dj_voice is called, the music volume is momentarily "ducked" (lowered) by 60% before the TTS plays.

Persistance: Save the path to the dj_persona.wav in the ~/.dj_squawk_config file created in previous steps.

4. Verification Step
Execute a "dry run" by having the agent generate and play the phrase:

"This is DJ Squawk, broadcasting live on your home server. NeuTTS is online and sounding smooth."
