---
title: Akeray Tekeray Bot
emoji: 🏠
colorFrom: blue
colorTo: green
sdk: docker
pinned: false
app_port: 7860
---

# Akeray Tekeray Telegram Bot

This is a Telegram rental bot designed to run on deployment platforms like **Railway** or **Hugging Face Spaces** using Docker, and it connects to a SQLite or PostgreSQL database (e.g., Neon.tech).

## Deployment Instructions

### 1. Setup Database
- **SQLite (Default)**: Automatically used if no external database is provided.
- **PostgreSQL**: Create a project at [neon.tech](https://neon.tech) and get your connection string (e.g., `postgres://user:password@host/dbname?sslmode=require`).

### 2. Configure Environment Variables
Whether deploying to **Railway** or **Hugging Face**, configure the following environment variables (Secrets):
- `BOT_TOKEN`: Your Telegram Bot API token.
- `ADMIN_IDS`: Comma-separated list of your Telegram User IDs.
- `DATABASE_URL`: Your PostgreSQL connection string (optional, defaults to local SQLite).
- `GEMINI_API_KEY`: Your Google AI Studio API key.
- `WEBHOOK_URL`: The URL of your app (e.g., `your-app.up.railway.app` or `https://user-space.hf.space`). 
  - *Note: The bot automatically validates this, prepends `https://`, and uses your `BOT_TOKEN` as a secure webhook path to prevent 502/404 errors.*

### 3. Deploy to Railway (Recommended)
- Connect your GitHub repository to Railway.
- Railway will automatically detect the `Dockerfile` and `PORT`.
- Add the Environment Variables above in the Railway Dashboard.

### 4. Deploy to Hugging Face Space
- Create a new **Space** on Hugging Face.
- Select **Docker** as the SDK.
- Go to **Settings > Variables and secrets** and add your secrets.

## Local Development

To run locally, copy `.env.example` to `.env` and fill in the values (leave `WEBHOOK_URL` empty to run in Polling Mode):

```bash
# Create and activate virtual environment (Windows)
python -m venv .venv
.\.venv\Scripts\activate

# Install requirements
pip install -r requirements.txt

# Run the bot
python main.py
```

### Database Options for Local Dev
**SQLite (default)**:
```env
DB_ENGINE=sqlite
SQLITE_PATH=rental_bot.db
```

**PostgreSQL**:
```env
DB_ENGINE=postgres
DATABASE_URL=postgresql://user:password@host/dbname?sslmode=require
```

## Tech Stack
- **Bot Framework**: `python-telegram-bot` (v20+)
- **Database**: PostgreSQL / SQLite 
- **AI**: Google Gemini (gemini-2.0-flash-exp)
- **Image Processing**: Pillow (Watermarking)
