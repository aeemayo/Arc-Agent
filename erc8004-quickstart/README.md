# ERC-8004 Quickstart

A hands-on walkthrough for registering an AI agent on the Arc testnet using the [ERC-8004](https://eips.ethereum.org/EIPS/eip-8004) standard. One script, eight steps — you'll go from zero to a fully registered, reputation-scored, and validated agent identity.

## What it does

The script (`index.ts`) runs through the full ERC-8004 lifecycle:

1. **Creates two wallets** via Circle's Developer-Controlled Wallets — one acts as the agent owner, the other as a validator.
2. **Registers an agent identity** on the Identity Registry, minting an on-chain NFT that represents your agent.
3. **Retrieves the agent ID** by reading the `Transfer` event logs from the registry.
4. **Records reputation** — the validator wallet submits a feedback score (e.g. `95` for a `successful_trade` tag) to the Reputation Registry.
5. **Verifies reputation** by checking the emitted feedback events.
6. **Requests validation** — the owner asks the validator for a KYC-style verification.
7. **Responds to validation** — the validator approves the request (score `100` = passed).
8. **Checks validation status** on-chain to confirm everything went through.

All transactions are sent via Circle's API and confirmed on Arc Testnet. You can follow along on the [Arc Testnet Explorer](https://testnet.arcscan.app).

## On-chain contracts

| Contract             | Address                                      |
| -------------------- | -------------------------------------------- |
| Identity Registry    | `0x8004A818BFB912233c491871b3d84c89A494BD9e`  |
| Reputation Registry  | `0x8004B663056A597Dffe9eCcC1965A193B7388713`  |
| Validation Registry  | `0x8004Cb1BF31DAf7788923b405b754f57acEB4272`  |

## Prerequisites

- **Node.js** v18+
- A **Circle Developer** account — you'll need an API key and entity secret. Grab them from the [Circle Console](https://console.circle.com).

## Setup

1. **Clone & install**

   ```bash
   git clone <your-repo-url>
   cd erc8004-quickstart
   npm install
   ```

2. **Configure your `.env`**

   ```env
   CIRCLE_API_KEY=your_circle_api_key
   CIRCLE_ENTITY_SECRET=your_entity_secret
   METADATA_URI=https://your-metadata-url.example
   ```

   `METADATA_URI` points to your agent's metadata JSON (see `agent-metadata.json` for the format). You can host it on IPFS, Arweave, or any public URL.

3. **Run it**

   ```bash
   npx tsx index.ts
   ```

   Sit back — the script will walk through each step, printing progress and explorer links as it goes.

## Agent metadata

The file `agent-metadata.json` is a sample of what your agent's on-chain metadata looks like:

```json
{
  "name": "DAO Governance Agent v1.0",
  "description": "Autonomous agent for participating in DAO governance...",
  "image": "https://...",
  "agent_type": "governance",
  "capabilities": ["proposal_analysis", "sentiment_aggregation", "automated_voting"],
  "version": "1.0.0"
}
```

Upload this to IPFS (or wherever you prefer) and set the resulting URL as `METADATA_URI` in your `.env`.

## Tech stack

- **[Circle Developer-Controlled Wallets SDK](https://developers.circle.com)** — wallet creation & transaction signing
- **[viem](https://viem.sh)** — reading on-chain state and parsing event logs
- **TypeScript** + **tsx** — zero-config TS execution

## License

ISC
