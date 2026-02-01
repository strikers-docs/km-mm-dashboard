# KM MM Bot Optimizer

A real-time dashboard that analyzes **Markets by Kinetiq (KM)** pairs on Hyperliquid and recommends optimal **Tread.fi Market Maker bot** settings for maximum PNL.

![Dashboard Preview](preview.png)

## Features

- 📊 **Real-time market data** from Hyperliquid's public API
- 🎯 **MM-friendliness scores** (0-100) for each KM pair
- ⚙️ **Recommended Tread.fi settings** (Mode, Spread, Grid, Bias, Stop Loss, Leverage)
- 🔄 **Auto-refresh** every 60 seconds
- 🎨 **Clean dark theme** optimized for trading

## How It Works

### Scoring Algorithm

Each market is scored on:

| Factor | Weight | What's Good |
|--------|--------|-------------|
| **Volume** | 25 pts | Higher = more taker flow to capture |
| **Spread** | 25 pts | 5-30 bps optimal (profit opportunity) |
| **Open Interest** | 15 pts | $100K-$10M (liquid but not overcrowded) |
| **Funding Rate** | 10 pts | Near neutral (no directional pressure) |
| **Premium** | 5 pts | Close to fair value |

### Recommended Settings

Based on the score and market conditions:

| Score | Mode | Spread | Grid | Leverage | Stop Loss |
|-------|------|--------|------|----------|-----------|
| 70+ | Aggressive | +1 to +2 | ON | 5x | 3% |
| 50-69 | Normal | +3 to +4 | ON | 3x | 5% |
| <50 | Normal | +5 | OFF | 2x | 3% |

## Setup

### Option 1: GitHub Pages (Recommended)

1. Fork this repository
2. Go to **Settings** → **Pages**
3. Set source to **main branch** / **root**
4. Access at `https://yourusername.github.io/km-mm-dashboard`

### Option 2: Local

Just open `index.html` in your browser. No server needed!

## Configuration

Edit these values in the `<script>` section of `index.html`:

```javascript
const CONFIG = {
    HYPERLIQUID_API: 'https://api.hyperliquid.xyz/info',
    KM_DEX_NAME: 'KM',           // Markets by Kinetiq dex identifier
    REFRESH_INTERVAL: 60000,      // Refresh every 60 seconds
};
```

## API Reference

This dashboard uses Hyperliquid's **public** info API (no authentication needed):

- `perpDexs` - List all HIP-3 dexes
- `metaAndAssetCtxs` - Market metadata and real-time context (price, volume, OI, funding)

For HIP-3 markets, assets are prefixed with the dex name: `KM:AAPL`, `KM:SPX`, etc.

## Troubleshooting

### "Failed to fetch KM markets"

1. Check if KM dex is live on Hyperliquid
2. Open browser console (F12) to see the actual API response
3. The dex name might be different - check `perpDexs` response

### Markets not loading

- CORS issues shouldn't occur (Hyperliquid API allows cross-origin)
- Check your internet connection
- Try refreshing the page

## Disclaimer

⚠️ **This is not financial advice.** 

- Market making carries significant risk
- Past performance doesn't guarantee future results
- Always DYOR and use proper risk management
- The recommended settings are algorithmic suggestions, not guarantees

## Links

- [Tread.fi](https://tread.fi) - MM Bot Platform
- [Markets by Kinetiq](https://kinetiq.xyz) - KM Exchange
- [Hyperliquid](https://hyperliquid.xyz) - L1 Exchange
- [Hyperliquid API Docs](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api)

## Contributing

PRs welcome! Ideas for improvement:
- Historical PNL tracking
- Backtesting settings
- Alert notifications (Telegram/Discord)
- More sophisticated scoring models

## License

MIT
