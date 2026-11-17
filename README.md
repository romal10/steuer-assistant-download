# Steuer-Assistant – Download

A **local-first** assistant for your German tax documents. It sorts your receipts and payslips into a tax folder on **your own computer**, asks about deductions step by step, estimates your refund and prepares a report for your Steuerberater.

* Your documents never leave your computer.
* It **never** logs in to ELSTER, stores a certificate or sends anything to a Finanzamt. You submit yourself.
* Languages: Deutsch · English · Polski · العربية · فارسی (Dari)

> The figures are an indicative estimate, not tax advice or a tax assessment.

## Screenshots

*Fictional demo data only. Your real documents never leave your computer.*

| Guided start | Work, home office, commute |
|---|---|
| ![Start](screenshots/01-start.jpg) | ![Work](screenshots/02-work.jpg) |
| **What is still missing** | **Estimated refund** |
| ![Documents](screenshots/03-documents.jpg) | ![Result](screenshots/04-result.jpg) |

## How it works

1. **Pick the tax year** – with the filing deadline.
2. **About you** – drop a Finanzamt letter; names, Steuernummer and tax office are read automatically (on your computer).
3. **Work** – job, on site / hybrid / home office, home and work address. The commute distance and days are calculated (optional online distance lookup only after you agree).
4. **Income and family** – salary, freelance income, children, church tax.
5. **Documents** – put everything into one folder. It is sorted, costs and income are separated, and you see what is missing.
6. **Result** – your estimated refund with a step-by-step calculation, a report for your Steuerberater and an ELSTER guide.

Nothing to provide? One click calculates every standard deduction automatically. Nothing is invented – more real receipts can raise the estimate.

Privacy: the app listens on `127.0.0.1` only, has no telemetry and never logs in to ELSTER. Tax years 2025 and later (estimates for 2025 and 2026 so far).

## Download

**Website:** https://romal10.github.io/steuer-assistant-download/

Pick your system (direct download):

| System | File |
|---|---|
| Windows 10/11 | [Steuer-Assistant-Windows.zip](https://github.com/romal10/steuer-assistant-download/releases/latest/download/Steuer-Assistant-Windows.zip) |
| Mac with Apple chip (M1–M4) | [Steuer-Assistant-Mac-AppleSilicon.zip](https://github.com/romal10/steuer-assistant-download/releases/latest/download/Steuer-Assistant-Mac-AppleSilicon.zip) |
| Mac with Intel chip | [Steuer-Assistant-Mac-Intel.zip](https://github.com/romal10/steuer-assistant-download/releases/latest/download/Steuer-Assistant-Mac-Intel.zip) |

## Installation (first start) – Anleitung

### Windows
1. Download the ZIP, **right-click ▸ Extract all…** (Alle extrahieren).
2. Open the folder `Steuer-Assistant` and double-click **`Steuer-Assistant.exe`**.
3. If Windows shows *"Windows protected your PC"*: click **More info ▸ Run anyway** (the app is not code-signed yet).
4. A black window opens – **keep it open** (it watches for new files). Your browser opens at `http://127.0.0.1:8766`.

### Mac
1. Download the ZIP and double-click it – a folder `Steuer-Assistant` appears. Move it to *Applications* or *Documents*.
2. Open **Terminal**, type `xattr -dr com.apple.quarantine ` (with a space at the end), drag the folder into the window, press **Return**. This removes the "unidentified developer" block (the app is not code-signed yet).
3. Double-click **`Steuer-Assistant`** inside the folder (or drag it into Terminal and press Return).
4. Keep the window open. Your browser opens at `http://127.0.0.1:8766`.

### Local AI (free, works without internet)
The AI that reads your documents runs **on your own computer** through [Ollama](https://ollama.com) – free, no account, no API key, nothing is sent anywhere. Without it the app still sorts files by rules; the AI adds reading of unclear documents and free-form answers.

**Easiest way:** open **Settings ▸ AI** in the app and press **Install for me**, or double-click **`Setup-AI.bat`** (Windows) / **`Setup-AI.command`** (Mac) in the folder `KI-Einrichtung-Setup-AI`. It asks once, installs Ollama and the model, and checks that the model answers.

#### Which model? (free, runs offline)
The default is **`qwen3.5:4b`**. Pick a smaller one for older PCs or a bigger one if you have plenty of memory. Download sizes are approximate (Ollama shows the exact size).

| Your computer | Model (Ollama tag) | Download | Notes |
|---|---|---|---|
| 4 GB RAM or old PC | `llama3.2:1b` | ~1.3 GB | Fast, simple documents only |
| 8 GB RAM | **`qwen3.5:4b`** (default) or `llama3.2:3b` | ~2–3 GB | Good balance, recommended start |
| 16 GB RAM | `qwen2.5:7b` | ~4.7 GB | Better reading of difficult scans |
| 32 GB RAM or more | `qwen2.5:14b` | ~9 GB | Best quality, slower on CPU |

Ollama itself is another ~1.8 GB on Windows (~0.2 GB on Mac). Models are stored in `C:\Users\<you>\.ollama\models` (Windows) or `~/.ollama/models` (Mac). A graphics card is **not** required; without one it is slower but works.

**Use a different model:** install it once, then tell the app which one to use.

* Windows (PowerShell): `ollama pull llama3.2:3b` and, before starting the app, `$env:STEUER_MODEL="llama3.2:3b"`
* Mac (Terminal): `ollama pull llama3.2:3b` and `STEUER_MODEL=llama3.2:3b ./Steuer-Assistant`
* Or choose it later in **Settings ▸ AI engine**. If the chosen model is missing, the app falls back to any installed `qwen`, `gemma` or `llama` model.

**No internet at the target PC?** On any computer with internet run `Make-Offline-Pack`, copy the `offline-pack` folder next to the setup script and run `Setup-AI` again. Other free engines work too: **LM Studio**, **Jan** or llama.cpp (Settings ▸ AI engine ▸ local OpenAI-compatible server). Your own cloud API key is possible but only after you explicitly agree, because documents would then leave your computer.

#### AI does not work on Windows? Quick checks
1. Open PowerShell and run `ollama list` – your model must appear. If `ollama` is not found, restart the PC once or run `Setup-AI.bat` again.
2. Open `http://127.0.0.1:11434` in the browser – it must say *Ollama is running*. If not: start **Ollama** from the Start menu.
3. "Model unavailable" in the app: the model is not downloaded yet (`ollama pull qwen3.5:4b`) or Ollama is stopped. Files stay in the inbox and are retried automatically.
4. Download stops halfway: free ~6 GB of disk space, check the connection and run the setup again – it continues where it stopped.
5. Antivirus or a company PC may block the Ollama installer: use the offline pack or ask your IT.

Optional cloud drive: choose your Google Drive / OneDrive / iCloud / Dropbox folder in setup.

### First-run setup in the app
1. **Click "Get started"** – choose where your tax folder is created (default: *Documents ▸ Steuerverwaltung*).
2. **Enter the people** in your household and choose your **Bundesland** and **Finanzamt** from the dropdowns.
3. **Drop your documents** (payslips, receipts, letters) into the *Inbox* folder or onto the page. The app sorts them.
4. Open **Savings ▸ ▶ Guide me step by step**: for every deduction you get a suggested amount (from your Bundesland, payslips or documents) – press **Use this amount**, **Enter my own amount** or **Not needed**.
5. Open **Report** to print/save the report for your Steuerberater, and **Overview ▸ Guided ELSTER help** when you file.

Updating: download the new ZIP and replace the old folder – your tax folder and settings stay untouched.

## Licence
MIT – see [LICENSE](LICENSE). This repository only contains the ready-to-run program and instructions.
