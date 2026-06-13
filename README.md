[My Actor](https://apify.com/logiover/my-actor?fpr=data)

# DexScreener Trending Tokens Scraper

Scrape **real-time trending, boosted, and newly listed crypto tokens** from [DexScreener](https://dexscreener.com) — the #1 DEX aggregator across 80+ blockchains. Get live prices, volume, liquidity, market cap, buy/sell transactions, and boost data for Solana, Ethereum, BSC, Base, and more.

## Why This Scraper?

DexScreener's free API has strict rate limits (60 req/min on trending endpoints). This actor handles retries, deduplication, chain filtering, and automatic enrichment — so you get clean, flat JSON ready for your trading bot, spreadsheet, or database.

## 6 Scraping Modes

| Mode | What It Does | Best For |
| --- | --- | --- |
| **Trending** | Hot token categories + their top trading pairs | Catching meme-coin waves early |
| **Top Boosted** | Tokens with the most paid promotions | Spotting heavily promoted new tokens |
| **Latest Boosted** | Most recently promoted tokens | Real-time alpha on new launches |
| **Latest Profiles** | Newly listed token profiles on DexScreener | Discovering brand-new tokens |
| **Search** | Search pairs by keyword (e.g., "PEPE", "AI") | Finding specific tokens or themes |
| **Token Pairs** | Look up pairs by contract address | Monitoring specific tokens |

## Output Fields (32 Fields)

| Field | Description |
| --- | --- |
| mode | Scraping mode used |
| chainId | Blockchain (solana, ethereum, bsc, base...) |
| dexId | DEX name (raydium, uniswap, pancakeswap...) |
| pairAddress | Trading pair contract address |
| baseTokenName | Token name |
| baseTokenSymbol | Token ticker symbol |
| baseTokenAddress | Token contract address |
| quoteTokenName | Quote token (SOL, ETH, USDT...) |
| quoteTokenSymbol | Quote token symbol |
| quoteTokenAddress | Quote token contract |
| priceUsd | Current price in USD |
| priceNative | Price in native chain token |
| volume_m5 | Trading volume last 5 minutes |
| volume_h1 | Trading volume last 1 hour |
| volume_h6 | Trading volume last 6 hours |
| volume_h24 | Trading volume last 24 hours |
| priceChange_m5 | Price change % (5 min) |
| priceChange_h1 | Price change % (1 hour) |
| priceChange_h6 | Price change % (6 hours) |
| priceChange_h24 | Price change % (24 hours) |
| txns_h24_buys | Buy transactions (24h) |
| txns_h24_sells | Sell transactions (24h) |
| liquidityUsd | Liquidity pool size in USD |
| fdv | Fully diluted valuation |
| marketCap | Market capitalization |
| pairCreatedAt | When the pair was created |
| boostsActive | Number of active paid boosts |
| pairUrl | DexScreener pair page URL |
| imageUrl | Token logo image URL |
| websites | Project website URLs |
| socials | Social media (Twitter, Telegram, Discord) |
| scrapedAt | Scraping timestamp (ISO 8601) |

## Input Parameters

| Parameter | Type | Default | Description |
| --- | --- | --- | --- |
| mode | string | trending | Scraping mode (see table above) |
| searchQueries | string[] | [] | Keywords for search mode |
| tokenAddresses | string[] | [] | Contract addresses for tokenPairs mode |
| chainFilter | string |  | Filter: solana, ethereum, bsc, base, arbitrum, polygon, avalanche, optimism, ton, sui, aptos |
| enrichPairData | boolean | true | Fetch full pair details for boosted/profile tokens |
| maxResults | integer | 0 | Limit results (0 = unlimited) |
| proxyConfig | object | Apify Proxy | Proxy settings (datacenter works) |

## Example Inputs

### Catch trending meme-coins on Solana

```
{
    "mode": "trending",
    "chainFilter": "solana",
    "proxyConfig": { "useApifyProxy": true }
}
```

### Find top boosted tokens (paid promotions = hot launches)

```
{
    "mode": "boostedTop",
    "enrichPairData": true,
    "proxyConfig": { "useApifyProxy": true }
}
```

### Search for AI tokens

```
{
    "mode": "search",
    "searchQueries": ["AI", "GPT", "neural"],
    "proxyConfig": { "useApifyProxy": true }
}
```

### Monitor specific token by contract address

```
{
    "mode": "tokenPairs",
    "tokenAddresses": ["So11111111111111111111111111111111111111112"],
    "proxyConfig": { "useApifyProxy": true }
}
```

## Use Cases

- **Meme-Coin Sniper Bots** — Run every 5 minutes to catch new trending tokens before they pump
- **Arbitrage Detection** — Compare prices across DEXes for the same token
- **Portfolio Tracking** — Monitor specific tokens by contract address
- **Market Research** — Analyze which chains and DEXes have the most activity
- **Whale Alerts** — Track tokens with sudden volume spikes
- **Boost Monitoring** — See which tokens are paying for DexScreener promotion (often meme-coins)

## Cost & Performance

- Trending mode: ~50-200 pairs per run, completes in **5-15 seconds**
- Boosted mode: ~50-100 tokens enriched in **10-20 seconds**
- Search mode: ~20-50 pairs per keyword, **under 5 seconds**
- Datacenter proxies = cheapest option
- **$2.00 per 1,000 results** (pay-per-result)
- Schedule every 5 minutes for real-time monitoring

## Supported Blockchains

Solana, Ethereum, BSC (BNB Chain), Base, Arbitrum, Polygon, Avalanche, Optimism, TON, Sui, Aptos, Fantom, Cronos, zkSync, Mantle, Blast, Linea, Scroll, Celo, and 60+ more chains supported by DexScreener.

## Tips

1. **Run on a schedule** — Set up a 5-minute cron to catch trending tokens in real-time
2. **Filter by chain** — Use `chainFilter: "solana"` to focus on Solana meme-coins
3. **Enrich data** — Keep `enrichPairData: true` to get full price/volume/liquidity info
4. **Combine modes** — Run trending + boostedTop together for maximum coverage
5. **Export to webhook** — Send results to your Telegram bot or Discord channel

## FAQ

**Does it need residential proxies?**
No. Datacenter proxies work perfectly. DexScreener API is public.

**How often should I run it?**
For real-time trading: every 5 minutes. For daily analysis: once per day.

**Can I get historical data?**
This scraper returns current/live data. For historical, you'd need to schedule runs and accumulate data over time.

**What's the rate limit?**
DexScreener allows 60 req/min on trending/boost endpoints and 300 req/min on search/pairs. The scraper automatically respects these limits.

**Is this legal?**
This scraper uses DexScreener's public API. Always check their Terms of Service for your specific use case.