# Twitch Stream Status — Corsair iCUE Widget

A live Twitch stream status widget for the **Corsair Xeneon Edge** touchscreen display, built for the iCUE Widget platform. Displays real-time stream info — live status, stream title, category, viewer count, and uptime — pulled directly from the Twitch API.

---

## Features

- 🔴 **Live / Offline / Loading** status indicator with animated dot
- 📺 **Stream title** with automatic 2-line wrapping for long titles
- 🎮 **Category** currently being streamed
- 👥 **Viewer count** with formatted number display
- ⏱️ **Stream uptime** with animated progress ring (fills over 6 hours)
- 🕐 **Live clock** updated every second
- 🔄 **Auto-refresh** on a configurable interval (minimum 30 seconds)
- 🎨 **Fully themeable** — accent color, text color, and background color all configurable from iCUE
- 📐 **Three responsive layouts** for all Xeneon Edge configurations:
  - **Small** — 840 × 344 px
  - **Medium** — 1680 × 344 px
  - **Large** — 1680 × 688 px

---

## Screenshots

> _Add screenshots of your widget here_

| Small (840×344) | Medium (1680×344) | Large (1680×688) |
|---|---|---|
| _(screenshot)_ | _(screenshot)_ | _(screenshot)_ |

---

## Requirements

- [Corsair iCUE](https://www.corsair.com/icue) (with Widget support)
- A **Corsair Xeneon Edge** display (or any iCUE-compatible widget surface)
- A free [Twitch Developer Application](https://dev.twitch.tv/console/apps) for API credentials

---

## Setup

### 1. Create a Twitch Application

1. Go to [https://dev.twitch.tv/console/apps](https://dev.twitch.tv/console/apps) and log in
2. Click **Register Your Application**
3. Fill in any name (e.g. `My iCUE Widget`)
4. Set the **OAuth Redirect URL** to `http://localhost`
5. Set **Category** to `Other`
6. Click **Create**
7. Click **Manage** on your new app, then click **New Secret**
8. Copy your **Client ID** and **Client Secret** — you'll need both

### 2. Install the Widget

1. Download or clone this repository
2. Open **iCUE** and navigate to the Xeneon Edge widget panel
3. Add a new widget and select the `index.html` file from this project
4. In the widget settings panel, fill in:
   - **Twitch Client ID** — from step 1
   - **Twitch Client Secret** — from step 1
   - **Channel Name** — the Twitch username to monitor (e.g. `giantwaffle`)
   - **Refresh Interval** — how often to poll in seconds (minimum 30, default 60)

### 3. Customize Appearance (optional)

In the iCUE widget settings under **Appearance**:

| Setting | Default | Description |
|---|---|---|
| Accent Color | `#9146FF` (Twitch purple) | Viewer count, uptime ring, live dot |
| Text Color | `#FFFFFF` | Channel name and value text |
| Background Color | `#0A0A0F` | Widget background |

---

## File Structure

```
├── index.html        # Main widget file
└── resources/
    └── icon.svg      # Widget icon (shown in iCUE)
```

---

## How It Works

The widget uses the [Twitch Helix API](https://dev.twitch.tv/docs/api/) with the **Client Credentials** OAuth flow — no user login required.

On each refresh cycle it:
1. Requests a short-lived app access token from `id.twitch.tv/oauth2/token`
2. Queries `api.twitch.tv/helix/streams` for the configured channel
3. Updates all display elements — or shows an OFFLINE state if the stream is down

All API calls happen client-side inside the iCUE browser context. Your credentials are stored only in iCUE's widget settings and are never transmitted anywhere except to Twitch's own endpoints.

---

## Responsive Layouts

The widget automatically detects its container size and switches layout:

| Size | Dimensions | Layout |
|---|---|---|
| Small | 840 × 344 | Left panel (channel + status) + Right panel (info grid + uptime ring) |
| Medium | 1680 × 344 | Left panel + Center panel (stacked info) + Right panel (large uptime ring) |
| Large | 1680 × 688 | All three panels at full scale with larger typography |

---

## Troubleshooting

**Widget shows "Enter your Client ID and Client Secret"**
→ Open the iCUE widget settings panel and fill in all three required fields (Client ID, Client Secret, Channel Name).

**Widget shows ERROR**
→ Double-check your Client ID and Client Secret are correct and that your Twitch app is active. The error message displayed is the raw API response to help diagnose the issue.

**Widget shows OFFLINE but the stream is live**
→ Check that the Channel Name matches the Twitch username exactly (not case-sensitive, but must be the login name, not display name).

**Viewer count or uptime not updating**
→ The widget refreshes on the interval you set. Decrease the Refresh Interval in settings for more frequent updates (minimum 30 seconds to avoid Twitch API rate limits).

---

## License

MIT — free to use, modify, and share.

---

## Acknowledgements

- [Twitch API](https://dev.twitch.tv/docs/api/) for stream data
- [Corsair iCUE Widget SDK](https://developer.corsair.com) for the widget platform
