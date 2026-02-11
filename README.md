# Sipal dTelecom Bot v1.0

> **Sipal Airdrop Community** — dTelecom Daily Check-In & Auto Tweet Bot

## Features

- **Daily Check-In** — Automatic daily check-in on rewards.dtelecom.org (+5 pts/day)
- **Auto Post Tweet** — Generates unique tweets about dTelecom and submits to platform (+15 pts/day)
- **Dashboard UI** — Live terminal dashboard with account table + scrollable execution logs
- **Multi-Account** — Run multiple Solana wallets simultaneously with staggered scheduling
- **Stealth Mode** — Fingerprint persistence, cookie management, dummy traffic, human-like delays
- **Proxy Support** — HTTP/HTTPS/SOCKS5 proxy per account
- **Auto Retry** — Exponential backoff with automatic session refresh on 401/403
- **Referral System** — Automatic referral registration for community growth
- **Integrity Protection** — Anti-tamper system prevents unauthorized code modifications
- **Flat Structure** — Single `index.js` file, no config.json needed

## Important

This bot requires registration via the official Sipal Airdrop referral link:

**https://rewards.dtelecom.org/reward?referral_code=B7AU3KRG**

The referral is automatically applied when you run the bot for the first time.

> **WARNING:** Do NOT modify `index.js` — the built-in integrity protection system
> will detect any changes and the bot will refuse to run. If you encounter issues,
> re-download the original from the official repository.

## Setup

### 1. Install Dependencies

```bash
npm install
```

### 2. Configure Accounts

Copy the template and fill in your credentials:

```bash
cp accounts_tmp.json accounts.json
```

Edit `accounts.json`:

```json
[
  {
    "privateKey": "YOUR_SOLANA_PRIVATE_KEY_BASE58",
    "proxy": "http://user:pass@host:port",
    "AppKey": "YOUR_TWITTER_APP_KEY",
    "AppKeySecret": "YOUR_TWITTER_APP_KEY_SECRET",
    "AccessToken": "YOUR_TWITTER_ACCESS_TOKEN",
    "AccessTokenSecret": "YOUR_TWITTER_ACCESS_TOKEN_SECRET"
  }
]
```

| Field | Required | Description |
|-------|----------|-------------|
| `privateKey` | ✅ | Solana wallet private key (base58 format, 64-byte keypair) |
| `proxy` | ❌ | HTTP/SOCKS5 proxy URL |
| `AppKey` | ❌ | Twitter API app key (for auto tweet) |
| `AppKeySecret` | ❌ | Twitter API app secret |
| `AccessToken` | ❌ | Twitter OAuth access token |
| `AccessTokenSecret` | ❌ | Twitter OAuth access secret |
| `isReferrer` | ❌ | Set `true` ONLY for source/referrer accounts (skip auto-referral) |

### 3. Run

```bash
npm start
```

## Dashboard

The bot displays a live terminal dashboard with:

- **Banner** — Sipal Airdrop branding
- **Account Table** — Status, points, check-in/tweet status, last/next run times
- **Execution Logs** — Scrollable log of recent actions (last 20 entries)

## Scheduling

- Each account runs independently on a **22–26 hour randomized cycle**
- Accounts start with a **15-second stagger delay** between each other
- **Daily reset watcher** monitors UTC 00:00 for task resets

## Security Notes

- `accounts.json` is in `.gitignore` — never commit your private keys
- Sessions are stored in `tokens.json` (auto-generated, also gitignored)
- Device fingerprints persist in `device_fingerprints.json` (auto-generated)
- All configuration is inline in `index.js` — no external config files
- **Integrity Protection** — The bot verifies its own source code hash at startup
  and periodically during runtime. Any modification (even a single character) will
  cause the bot to exit with a runtime error.
- **Referral Protection** — The referral code is XOR-encrypted and verified via
  multiple SHA-256/MD5 checkpoints. Changing the referral code requires updating
  4+ cryptographic constants simultaneously, plus the file integrity hash.

## File Structure

```
├── index.js           # Main bot (all logic, config, UI)
├── accounts.json      # Your credentials (gitignored)
├── accounts_tmp.json  # Empty template for setup
├── package.json       # Dependencies
├── .gitignore         # Security exclusions
├── LICENSE            # MIT License
└── README.md          # This file
```

## Author

**Sipal Airdrop Community**

## License

MIT
