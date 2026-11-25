# n8n Discord Notifier

A small n8n workflow that sends a message to a Discord channel through a webhook. It's a simple starting point for Discord alerts and reminders built with n8n.

## How it works

```
Schedule Trigger     HTTP Request  ->  Discord
(timer)              (webhook URL)     (sends "Hello From N8n!")
```

1. **Schedule Trigger** is the timer that starts the workflow.
2. **HTTP Request** calls your Discord webhook URL.
3. **Discord** node posts the message "Hello From N8n!" to your channel using webhook authentication.

Change the text in the Discord node to send your own message.

## What you need

- [n8n](https://docs.n8n.io/hosting/) running (this project uses a self-hosted n8n in Docker)
- A Discord server where you can create a webhook (you need the Manage Webhooks permission)

## Setup

### 1. Create a Discord webhook

1. In Discord, open your server, then **Server Settings** (or the channel's settings) and go to **Integrations**.
2. Click **Webhooks**, then **New Webhook**.
3. Choose the channel it should post to, then click **Copy Webhook URL**.

Treat this URL like a password. Anyone who has it can post to your channel.

### 2. Import the workflow

1. Open n8n (usually `http://localhost:5678`) and create a new workflow.
2. Click the three dots menu, then **Import from File**.
3. Choose `workflows/discord-project-workflow.json`.

The workflow file has no webhook URL or logins in it, so you add your own next.

### 3. Add your webhook

- **HTTP Request:** replace `YOUR_DISCORD_WEBHOOK_URL` with the webhook URL you copied.
- **Discord:** create a new **Discord Webhook** credential, paste the same webhook URL into it, and select it in the node.

### 4. Run it

1. Click **Execute workflow**. The message should show up in your Discord channel.
2. To send on a schedule, connect the **Schedule Trigger** output to the **HTTP Request** node, set how often it should run, and publish the workflow.

## Troubleshooting

- **Nothing arrives in Discord:** check that the webhook URL is correct in both the HTTP Request node and the Discord credential, and that the webhook wasn't deleted in Discord.
- **Node shows a warning:** the Discord node needs its credential selected (step 3).
- **Schedule never runs:** the Schedule Trigger has to be connected to the first node (step 4).

## Notes

- Never commit your real webhook URL to GitHub. Keep it only inside your own n8n. If it ever gets exposed, delete the webhook in Discord and create a new one.
