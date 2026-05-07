# EUrouter Key Limit Checker

A simple, secure, and modern single-page web application to monitor your [EUrouter](https://www.eurouter.ai/) API keys, usages, and limits directly from your browser. 

## Features

- **Direct API Fetch:** Connects directly to the EUrouter API (`https://api.eurouter.ai/api/v1/keys`). No middleman. No keys stored on the client or third-party servers.
- **Modern UI:** Responsive, glassmorphic design that scales beautifully on desktop and mobile.
- **Detailed Metrics:** Tracks active/disabled statuses, total limit, remaining balance, and usage history (daily, weekly, monthly, and total) formatted in EUR.
- **Reset Schedules:** See exactly when your API limits reset.
- **Zero Configuration Build:** This project is a single `index.html` file that relies entirely on vanilla HTML, CSS, and JS. 

## Setup & Local Development

Due to typical browser CORS policies regarding the `file://` protocol, you must run this page over a local web server (e.g. `localhost`).

1. Clone or download this repository.
2. Open a terminal in the folder containing `index.html`.
3. Start a simple HTTP server. For example, using Python 3:
   ```bash
   python3 -m http.server 8080
   ```
4. Open your browser and navigate to: `http://localhost:8080/`

## Deployment (GitHub Pages)

Because this repository contains a purely static HTML file with no build steps, you can directly host it using **GitHub Pages**. 
Just push the repository to GitHub, go to your repository **Settings > Pages**, and set the source to deploy from the `main` branch.

## Terminal Usage (CLI Alternative)

If you just want to grab key stats securely via the command line using `curl` and `jq`:

```bash
curl -s -X GET "https://api.eurouter.ai/api/v1/keys" \
  -H "Authorization: Bearer YOUR_API_KEY_HERE" \
  | jq '.data[] | {name: .name, status: (if .disabled then "Disabled" else "Active" end), limit: .limit, remaining: .limit_remaining, reset: .limit_reset, usage_daily: .usage_daily}'
```
