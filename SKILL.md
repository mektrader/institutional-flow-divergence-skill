How to Use

Connect your agent to CoinMarketcap AI Agent Hub
Call this Skill with current market data
Receive a ready-to-backtest or ready-to-execute strategy

Backtesting
Backtesting scripts and results are available in the /backtest folder.
Limitations & Disclaimer
This Skill is for educational and hackathon purposes. Trading involves substantial risk of loss. Always do your own research. NFA.
Author
Built by @mektrader_ for BNB Hack: AI Trading Agent Edition (June 2026)

# institutional-flow-divergence-skill

**Track 2 – BNB Hack: AI Trading Agent Edition**  
CMC Skill that generates institutional-grade, backtestable trading strategies by detecting smart money vs retail divergences.

## Overview

This Skill analyzes divergences between on-chain flows, Fear & Greed Index, derivatives data, and retail sentiment to generate structured trading strategies with built-in risk management. It is designed to be consumed by AI agents through the CoinMarketCap AI Agent Hub (MCP / x402).

## Strategy Logic

The Skill identifies high-conviction setups when there is clear divergence between:
- Smart money behavior (on-chain flows, whale activity, exchange netflow)
- Retail sentiment (Fear & Greed Index + social/KOL sentiment)
- Derivatives market structure (funding rates and open interest, when available)

When divergence is confirmed, the Skill outputs a complete strategy specification including bias, conviction level, dynamic position sizing, scaled take-profits, and stop-loss.

## Input Schema

The Skill expects the following market context (can be provided by the agent or fetched via CMC data):

- `fear_greed_index`: number (0-100)
- `onchain_netflow`: string (positive/negative + magnitude)
- `whale_activity`: string (high/medium/low)
- `funding_rate`: number (optional)
- `social_sentiment`: string (bullish/bearish/neutral)
- `market_regime`: string (trending/sideways/high_volatility)

## Output Schema

The Skill returns a structured JSON-like object:

```json
{
  "bias": "Long" | "Short" | "Neutral",
  "conviction": 1-10,
  "position_size_pct": number,
  "entry_zone": string,
  "take_profits": [number, number, number],
  "stop_loss": number,
  "timeframe": string,
  "rationale": string,
  "risk_notes": string
}
