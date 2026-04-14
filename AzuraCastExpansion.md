Prompt 1:
"We are building an expansion for DJ Squawk, a Linux-based personal radio agent. The system must use the official AzuraCast Docker installation.

Create the directory /var/azuracast, download the docker.sh installer from the official repo, and run the install command.

Configure the AzuraCast instance to accept an external Base Source connection, which our FFmpeg bridge will use to feed the audio from the local sound card."

Prompt 1:
"We are expanding the DJ Squawk Linux home server agent. The goal is to take the audio currently playing through the physical sound card and simultaneously broadcast it via a self-hosted AzuraCast instance running on this same machine.

Your current task:

Install AzuraCast: Use the official Docker-based installation method. Create /var/azuracast, fetch the docker.sh setup script, and run the automated installation.

Credential Management: Create a skill manage_creds that handles a persistent JSON config at ~/.dj_squawk_config.

This skill must store the local connection details for the AzuraCast 'Source' (e.g., localhost, the streamer port, mount point, and source password).

Implement SET, GET, and UPDATE functions for these credentials.

Note: AzuraCast will run in Docker, but our audio bridge will run on the host to access the sound card. Confirm once the Docker containers are spinning and the credential skill is ready."

Prompt 3:
"Continuing the DJ Squawk expansion (Local Audio + AzuraCast Stream). We have the credentials stored; now we need to implement the 'Radio Station' behavior.

Your current task: Create the streaming control skills.

Skill azura_start:

Retrieve credentials via manage_creds.

Use FFmpeg to capture the live audio from the sound card's 'monitor' (PulseAudio/PipeWire) or ALSA loopback.

Stream this audio to the remote AzuraCast mount point while ensuring the local speakers keep playing.

Run this as a background process and log the PID.

Skill azura_stop:

Locate and terminate only the FFmpeg process associated with the stream.

Provide a status check to confirm if the stream is currently 'On Air' or 'Offline'."
