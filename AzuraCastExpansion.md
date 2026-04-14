Prompt 1:
"We are building an expansion for DJ Squawk, a Linux-based personal radio agent. The goal is to allow DJ Squawk to play music through the local sound card and simultaneously stream that same audio to a remote AzuraCast server.

Your current task: Implement the persistence layer.

Create a skill manage_creds that handles the DJ JSON config

It must store: stream_host, stream_port, mount_point, and source_password.

Implement SET, GET, and UPDATE functions.

Ensure the file has restricted permissions (chmod 600).

This config will be used in the next phase to power the streaming services. Confirm when the storage skill is ready for the credentials."
