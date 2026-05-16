A comprehensive, production-grade guide for installing, configuring, and troubleshooting the OpenClaw AI agent framework natively on Windows using a local Ollama inference server and a Telegram Bot interface.

This guide details the complete workflow, including every terminal command used, interactive setup menu options, known Windows-specific bugs, and a step-by-step resolution process.

---

## 📋 Table of Contents
1. [Step 1: Install and Run Local Inference (Ollama)](#-step-1-install-and-run-local-inference-ollama)
2. [Step 2: Create a Telegram Bot from Scratch](#-step-2-create-a-telegram-bot-from-scratch)
3. [Step 3: Open an Administrator Shell and Prepare Files](#-step-3-open-an-administrator-shell-and-prepare-files)
4. [Step 4: The Interactive Wizard (`openclaw onboard`)](#-step-4-the-interactive-wizard-openclaw-onboard)
5. [Step 5: The Headless JSON Bypass (Fixing Connection Errors)](#-step-5-the-headless-json-bypass-fixing-connection-errors)
6. [Step 6: Configure the Messaging Channel](#-step-6-configure-the-messaging-channel)
7. [Step 7: Launch and Device Pairing](#-step-7-launch-and-device-pairing)
8. [ Why Standard Setup Often Fails on Windows](#-why-standard-setup-often-fails-on-windows)
9. [ Complete Purge & Uninstallation](#-complete-purge--uninstallation)

---

##  Step 1: Install and Run Local Inference (Ollama)

Before launching the agent runtime, you must establish an offline local LLM framework to handle training, reasoning, and system parsing securely on your own hardware.

1. Go to the official [Ollama Download Page](https://ollama.com) and download the native Windows installer.
2. Run the installer package and ensure the Ollama application initializes inside your Windows System Tray.
3. Open a Windows terminal and pull the optimized lightweight model weights:
   ```cmd
   ollama pull llama3.2



4. **Verify Localhost Availability:** Open your browser and go to `http://127.0.0.1:11434`. The screen must read **"Ollama is running"**.



##  Step 2: Create a Telegram Bot from Scratch

OpenClaw requires a communication medium to receive requests and return responses. Follow these steps to build your custom gateway interface:

1. Open your Telegram client, click the search bar, and locate the official account: **`@BotFather`** (Look for the blue verification badge).
2. Click **Start** or type the following initialization command:
```text
/newbot

```


3. **Set a Display Name:** When prompted, enter a friendly name for your assistant (e.g., `My Local Agent`).
4. **Set a Username:** Choose a completely unique tag for your bot. **It must end in `_bot**` (e.g., `my_custom_openclaw_bot`).
5. **Save the API Token:** BotFather will provide an HTTP API Token string that looks like this:
```text
7182938475:AAH_ExampleTokenStringXyZ12345

```


*Copy this string to your clipboard. Keep it hidden—anyone with access to this token can control your bot.*

---

##  Step 3: Open an Administrator Shell and Prepare Files

To perform software-wide installations, you must work out of an elevated shell environment.

1. Open your Windows Start Menu, type **PowerShell**.
2. Right-click on **Windows PowerShell** and select **Run as administrator**.
3. Run the clean core framework engine installer globally using the Node Package Manager (`npm`):
```powershell
npm install -g openclaw@latest --force

```

##  Step 4: The Interactive Wizard (`openclaw onboard`)

The application provides an automated user configuration assistant. Run the following command to initialize it:

```powershell
openclaw onboard

```

### Navigating the Interactive Prompt Tree:

1. **Security Disclaimer:** Use your **Left Arrow Key** to highlight **`Yes`** and press **Enter**.
2. **Setup Mode:** Choose **`Manual setup`** (or `QuickStart`) and press **Enter**.
3. **What do you want to set up?:** Select **`Local gateway (this machine)`** and press **Enter**.
4. **Gateway Defaults:** Press **Enter** to accept the default port (`18789`), bind address (`127.0.0.1`), and auth settings.
5. **Model/Auth Provider:** Scroll down with your arrow keys, select **`More...`**, press **Enter**, locate **`Ollama (Cloud and local open models)`**, and press **Enter**.
6. **Ollama Mode:** Choose **`Local only`** and press **Enter**.

---

##  Step 5: The Headless JSON Bypass (Fixing Connection Errors)

> ⚠️ **Critical Interactive Loop Error:** On native Windows systems, the interactive menu contains a parsing bug. During the `Ollama base URL` phase, it appends input strings incorrectly, saving a broken, corrupted localhost target into persistent system configurations (e.g., `http://127.0.0.1:11434llama3.2`). This triggers an endless loop error stating: *"Ollama could not be reached"*.

To fix this connection issue permanently, bypass the interactive prompt by formatting the raw configuration text directly:

1. Terminate the locked onboarding session by pressing **`Ctrl + C`** inside your PowerShell terminal.
2. Force-open the backend system configuration file using native Windows Notepad:
```powershell
notepad "$env:USERPROFILE\.openclaw\openclaw.json"

```


3. If Notepad alerts you that the file does not exist, click **Yes** to generate it.
4. Wipe anything inside the document and paste this structurally clean, verified JSON blueprint:

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

5. Press **`Ctrl + S`** to save your changes, and close the Notepad window.

---

##  Step 6: Configure the Messaging Channel

Now that your local machine's endpoint address (`127.0.0.1:11434`) is structurally sound, bind the Telegram bot gateway:

1. Execute the dedicated channel interface config command in PowerShell:
```powershell
openclaw configure --section channels

```


2. Highlight **Telegram** using your keyboard arrow keys and press **Enter**.
3. Carefully paste your unique HTTP API Token generated in **Step 2** from `@BotFather`.
4. Confirm, save your settings, and return to the main shell workspace prompt.

---

##  Step 7: Launch and Device Pairing

Initialize the core background processing environment:

```powershell
openclaw start

```

* **Pairing Your Chat Room:** Upon a clean launch, the PowerShell terminal will display a distinct **Pairing Code**.
* Navigate back to Telegram, open your newly created custom bot channel, hit the **Start** button, paste the Pairing Code directly into the chat box, and send it. Your account is now bound as the secure administrator of your local agent.

---

## 🔍 Why Standard Setup Often Fails on Windows

If your environment froze, locked up, or crashed prior to following this guide, it is due to documented operating system compatibility quirks inside the tool layout:

1. **PowerShell QuickEdit Thread Freezes:**
By default, Windows PowerShell runs with **QuickEdit Mode** enabled. If you accidentally click your mouse anywhere inside the blue terminal area while text is processing, Windows halts the active script thread to let you select text. This causes the onboarding tool to freeze indefinitely until you press the **`Esc`** key on your keyboard to release the lock.
2. **Interactive String Splicing Bugs:**
The parameter verification parser inside `openclaw onboard` incorrectly flattens nested inputs on Windows, smashing base URLs and model names together into junk strings that break system routing.
3. **Invalid Parameter Signatures:**
Overwriting configurations directly inline using command parameters (e.g., `openclaw configure model.base_url http://...`) can trigger argument exceptions (`Too many arguments for this command`) on specific PowerShell versions due to string literal evaluation mismatches.

---

## 🧼 Complete Purge & Uninstallation

If you ever need to completely remove every trace of this environment from your hardware, execute these commands sequentially inside an Administrator PowerShell window to ensure a clean sweep:

```powershell
# 1. Force terminate any active background application or agent worker processes
Get-Process -Name "openclaw*" -ErrorAction SilentlyContinue | Stop-Process -Force

# 2. Erase the persistent Windows Scheduled Task background service
schtasks /Delete /F /TN "OpenClaw Gateway"

# 3. Cleanly uninstall the global npm module binaries from your environment
npm uninstall -g openclaw

# 4. Recursively force-delete hidden app directories, databases, and cached configs
Remove-Item -Recurse -Force "$env:USERPROFILE\.openclaw" -ErrorAction SilentlyContinue

```

### Uninstall Verification Check

To prove your machine is completely clean of the environment, search for the binary entry point:

```powershell
openclaw

```

*Expected Pure Output:* `The term 'openclaw' is not recognized as the name of a cmdlet, function, script file, or operable program...`

```

```
