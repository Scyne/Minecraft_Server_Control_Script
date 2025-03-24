# Minecraft Server Control Script

This script provides an easy way to manage a Minecraft server using `tmux`. It supports starting, stopping, restarting, checking the status, and accessing the server console. Follow the steps below to configure and use this script for your own Minecraft server.

---

## Features
- Start, stop, restart, and monitor your Minecraft server.
- Access the server console via `tmux`.
- Query player count and server status using `mcstatus`.

---

## Requirements
1. **tmux**: A terminal multiplexer that allows you to run processes in the background.
2. **Python `mcstatus` module**: Used to query server status and player count.
3. **A localy Hosted Java Minecraft Server**: This script supports any standard or modded server `.jar` file (e.g., `paper.jar`, `server.jar`).

---

## Installation Instructions

### Step 1: Install Required Packages
#### Install `tmux`
Run the following command to install `tmux`:
```bash
sudo apt update && sudo apt install tmux -y
```
#### Install Python and `pip`
If Python is not installed, install it using:
```bash
sudo apt install python3 python3-pip -y
```
#### Install `mcstatus`
To install `mcstatus`, use:
```bash
pip install mcstatus
```
If you encounter issues installing `mcstatus`, first install `pipx` (a Python package manager) and then use it to install `mcstatus`:
```bash
python3 -m pip install –user pipx
python3 -m pipx ensurepath
pipx install mcstatus
```
### Step 2: Save the Script
1. Copy the script provided above into a file named `serv`.
2. Save it in `/usr/local/bin/`:
```bash
sudo nano /usr/local/bin/serv
```
Paste the script into the editor, save (`Ctrl+O`), and exit (`Ctrl+X`).

3. Make the script executable:
```bash
sudo chmod +x /usr/local/bin/serv
```
### Step 3: Configure Your Minecraft Server Directory
1. Open the script for editing:
```bash
sudo nano /usr/local/bin/serv
```
2. Modify the following variables at the top of the script:
- **`MINECRAFT_DIR`**: Set this to your Minecraft server's directory (e.g., `/home/username/minecraft_server`).
- **`SERVER_JAR`**: Set this to your Minecraft server `.jar` file name (e.g., `paper.jar`).

Example:
```bash
MINECRAFT_DIR=”/home/username/minecraft_server”
SERVER_JAR=“paper.jar”
```

3. Do **not** remove `$SERVER_JAR nogui` from the start command (`START_COMMAND`). The `nogui` argument disables the graphical user interface for the server, which is critical for running it efficiently on a headless machine.

4. Save your changes (`Ctrl+O`, then `Ctrl+X`).

---

## Usage Instructions

### Available Commands
You can use this script with the following commands:

| Command             | Description                                                                 |
|---------------------|-----------------------------------------------------------------------------|
| `serv start`        | Starts the Minecraft server in a background tmux session.                  |
| `serv stop`         | Stops the Minecraft server gracefully by sending a "stop" command.         |
| `serv restart`      | Restarts the Minecraft server by stopping it and starting it again.        |
| `serv console`      | Attaches to the tmux session to view or interact with the server console. Exit the console without killing your server by pressing `ctrl+B` and then `D`.  |
| `serv status`       | Displays server status, uptime, memory usage, and player count.            |


---

## Troubleshooting

### Permissions Issues
If you encounter permissions errors when starting or stopping the server, ensure that your Minecraft directory is owned by your user:
```bash
sudo chown -R $USER:$USER /path/to/minecraft_server/
```

### Server Not Starting Properly
Ensure that `$SERVER_JAR nogui` is included in the start command (`START_COMMAND`). The `nogui` argument is necessary for running a headless server.

---

## Notes

- The script uses a tmux socket (`/tmp/minecraft-tmux`) to manage sessions securely.
- To detach from a tmux session without stopping the server, press `Ctrl+B`, then `D`.
- For additional functionality like querying player count, ensure that `mcstatus` is installed.

---

## Uninstallation

To remove this script from your system:
1. Delete `/usr/local/bin/serv`:
```bash
sudo rm /usr/local/bin/serv
```
2. Optionally uninstall tmux and mcstatus if no longer needed:
```bash
sudo apt remove tmux -y && pip uninstall mcstatus -y
```

---

>>>Enjoy managing your Minecraft server with ease! I built this over a few days because I'm super lazy and cheap and just wanted to use a low cost VPS to host my friends only server. Thought that this might be useful to alot of people and save yah from the insecurity of using rcon. Feel free to fork if you need any special features but please no commercial use without contacting me. Private use is ok with credit. if you wanna throw me a tip, I'd appreciate that [(Cashapp $scyne)](https://cash.app/$scyne) but it's not needed. Hope this helps!
