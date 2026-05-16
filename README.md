# OpenClaw Native Windows Setup Guide: Local Ollama & Telegram Bot Integration

A complete, end-to-end installation and deployment guide for setting up the OpenClaw personal AI agent runtime natively on Windows using a 100% local Ollama inference engine and a private Telegram Bot interface.

This guide provides a manual, headless bypass for common Windows PowerShell onboarding freezes, parameter errors, and installer menu caching bugs.


##  Step 1: Install and Run Your Local LLM (Ollama)

OpenClaw requires an inference backbone. To protect your data privacy, we will run our models entirely offline on your local GPU/CPU hardware.

1. Download the native Windows installer from the official [Ollama Download Page](https://ollama.com).
2. Execute the setup file and let the Ollama daemon initialize in your Windows system tray.
3. Open a standard terminal window (Command Prompt or PowerShell) and pull the recommended lightweight model weight family:
   ```cmd
   ollama pull llama3.2


4. Verify your local server is running by opening your browser and visiting: `http://127.0.0.1:11434`. It should output: `"Ollama is running"`. Keep this terminal running or let the tray application manage it.


##  Step 2: Create a Dedicated Telegram Bot from Scratch

OpenClaw operates as a background service that chats with you through standard messaging platforms. Follow these steps to provision a completely private bot gateway:

1. Open your Telegram app and type **`@BotFather`** into the search bar. Ensure it has the official blue verification checkmark.
2. Click **Start** or send the command:text/newbot



3. **Choose a Display Name:** Type any descriptive name you want for your AI assistant (e.g., `My Local Agent`).
4. **Choose a Username:** Type a unique username that **must** end in `_bot` or `Bot` (e.g., `clawnative_assistant_bot`).
5. **Secure Your Token:** BotFather will immediately generate an HTTP API Token. It will look similar to this:
```text
7182938475:AAH_ExampleTokenStringXyZ12345

```


*Copy this token to your clipboard. Do not share this token or upload it publicly to GitHub.*

---

##  Step 3: Clean Global Engine Installation

1. Click on your Windows Start Menu, search for **PowerShell**.
2. **Right-click** on *Windows PowerShell* and choose **Run as Administrator**.
3. Execute the global installer command to fetch the latest stable framework build and overwrite any partial dependency errors:
```powershell
npm install -g openclaw@latest --force

```



---

##  Step 4: The Headless Configuration Bypass (Crucial)

> ⚠️ **Critical Bug Alert:** Running the interactive menu `openclaw onboard` natively on Windows contains an architecture bug that strings together character inputs, accidentally hardcoding broken, un-editable loop addresses like `http://127.0.0.1:11434llama3.2` into the persistent files. Bypassing the onboarding script via this manual file configuration is highly recommended.

1. In your Administrator PowerShell window, run this command to generate and open the framework configuration file directly in Windows Notepad:
```powershell
notepad "$env:USERPROFILE\.openclaw\openclaw.json"

```


2. If Notepad prompts you to create a new file because it does not exist yet, select **Yes**.
3. Copy and paste this structurally clean, verified JSON schema directly into the blank window:

```json
{
  "model": {
    "provider": "ollama",
    "name": "ollama/llama3.2",
    "base_url": "[http://127.0.0.1:11434](http://127.0.0.1:11434)"
  },
  "gateway": {
    "mode": "local",
    "port": 18789,
    "bind": "loopback",
    "auth": "token",
    "tailscale": "off"
  }
}

```

4. Press **`Ctrl + S`** to save the changes, then close the Notepad window.

---

## 🔌 Step 5: Link the Telegram Channel Workspace

Now that the core model engine configurations are cleanly mapped, bind your messaging channel pathway:

1. Return to your blue PowerShell window and call the explicit configurations channel daemon:
```powershell
openclaw configure --section channels

```


2. Choose **Telegram** from the rendered interactive terminal checklist.
3. Paste the unique **HTTP API Token** you generated in **Step 2** from `@BotFather`.
4. Save your workspace parameters and exit back to the main prompt.

---

## 🏁 Step 6: Initialize and Pair the Agent Session

Launch the background runtime engine:

```powershell
openclaw start

```

* **Authentication Code:** On the very first boot, the terminal console will generate a distinct **Pairing Code**.
* Open Telegram, navigate to your custom bot username, press the **Start** button, and copy-paste that terminal pairing code straight into the chat window to authorize your device session.

---

IF YOU WANT TO UNINSTALL OPENCLAW FOLLOW THIS 

## Total Clean Purge and Uninstallation

To completely wipe every trace of OpenClaw, its database files, local configuration folders, and automated system services from your system, run these lines sequentially in an Administrator PowerShell window:

```powershell
# 1. Force kill any stuck active background application threads
Get-Process -Name "openclaw*" -ErrorAction SilentlyContinue | Stop-Process -Force

# 2. Delete the automated Windows Scheduled Task service
schtasks /Delete /F /TN "OpenClaw Gateway"

# 3. Uninstall the global npm package executable binaries
npm uninstall -g openclaw

# 4. Recursively wipe the hidden configurations directory
Remove-Item -Recurse -Force "$env:USERPROFILE\.openclaw" -ErrorAction SilentlyContinue

```

### Verification

Confirm that your machine is 100% clean by checking the binary command path:

```powershell
openclaw

```

*Expected Clean Output:* `The term 'openclaw' is not recognized as the name of a cmdlet...`

```

```
