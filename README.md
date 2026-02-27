# Telegram Search Bot

A Telegram bot that lets users search for posts stored in a Firebase Firestore database and returns a direct link to matching content.

## Features

- `/start` — Welcome message with usage instructions.
- `/search <title>` — Search the Firestore database for a post by title and return its link.

## Tech Stack

| Component | Technology |
|-----------|------------|
| Language | Python 3.11 |
| Bot Framework | [python-telegram-bot](https://github.com/python-telegram-bot/python-telegram-bot) v20.7 |
| Database | [Firebase Firestore](https://firebase.google.com/docs/firestore) via `firebase-admin` v6.5.0 |
| Hosting | [Render](https://render.com) |

## Prerequisites

- Python 3.11+
- A [Telegram Bot Token](https://core.telegram.org/bots/tutorial#obtain-your-bot-token) from [@BotFather](https://t.me/botfather)
- A [Firebase project](https://console.firebase.google.com/) with Firestore enabled
- A Firebase service account key (`firebase-key.json`)

## Setup

### 1. Clone the repository

```bash
git clone https://github.com/IamRishabhJi/Telegram-Search-Bot.git
cd Telegram-Search-Bot
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Add Firebase credentials

Download your Firebase service account key from the Firebase Console and save it as `firebase-key.json` in the project root.

> ⚠️ **Never commit `firebase-key.json` to version control.**

### 4. Set environment variables

```bash
export BOT_TOKEN=your_telegram_bot_token_here
```

### 5. Run the bot

```bash
python main.py
```

## Firestore Data Structure

The bot reads from a Firestore collection named `entries`. Each document should have at least a `title` field:

```
entries/
  <doc_id>/
    title: "Your Post Title"
    ...
```

When a match is found, the bot replies with a link in the format:

```
https://tantravidya.ct.ws/post.html?id=<doc_id>
```

## Usage

| Command | Description |
|---------|-------------|
| `/start` | Display the welcome message |
| `/search <title>` | Search for a post by title |

**Example:**

```
/search meditation techniques
```

The bot will reply with the title and a direct link if a match is found, or a "No matching post found." message otherwise.

## Deployment on Render

This project includes a `.render.yaml` for one-click deployment on [Render](https://render.com).

1. Push the repository to GitHub.
2. Connect the repository to Render.
3. Set the `BOT_TOKEN` environment variable in the Render dashboard.
4. Ensure `firebase-key.json` is available to the service (e.g., via a secret file mount).

## Project Structure

```
.
├── main.py             # Bot entry point
├── requirements.txt    # Python dependencies
├── runtime.txt         # Python version (3.11.9)
├── pyproject.toml      # Project metadata
├── .render.yaml        # Render deployment configuration
└── firebase-key.json   # Firebase credentials (not committed)
```

## License

This project is open source. Feel free to fork and customize it for your own use.
