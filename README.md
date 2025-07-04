# Webhook Receiver (Webhook Repo)

This repository contains the Flask backend which acts as a webhook receiver for GitHub repository events. It stores `push` and `pull_request` events into a MongoDB database and serves them to the frontend UI.

## Technologies Used

- Python + Flask
- MongoDB (Cloud Atlas)
- Flask-CORS
- Cloudflare Tunnel
- React (frontend)

## Features

- Listens to GitHub webhook events: `push`, `pull_request` (only `opened` events)
- Stores event data in MongoDB
- Provides `/events` API endpoint to fetch latest events
- React frontend fetches and displays events every 15 seconds

## MongoDB Schema

Each event document contains:

```json
{
  "author": "Travis",
  "event_type": "push", // or "pull_request"
  "from_branch": "dev", // only for pull_request
  "to_branch": "main",
  "timestamp": "UTC datetime"
}

## Note on Cloudflare Tunnel**

⚠️ This project uses a temporary Cloudflare tunnel for exposing the local Flask server.

Every time the Cloudflare tunnel is restarted, a new URL is generated. If you test the project yourself:

- Update the Webhook URL in GitHub settings (for Action Repo)
- Update the frontend fetch URL in `EventFeed.jsx`

For a permanent solution, a named Cloudflare tunnel should be used with a Cloudflare account. But as per assignment instructions, this temporary URL setup is acceptable for testing purposes.

