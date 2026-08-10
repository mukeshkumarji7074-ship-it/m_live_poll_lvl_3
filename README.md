# LivePoll

LivePoll is a mini end-to-end Stellar + Soroban dApp: a multi-wallet polling app backed by a deployed Soroban smart contract on Stellar Testnet, with real-time contract event sync, transaction progress feedback, basic caching, and a small automated test suite.

## Level 3 Submission Checklist (fill before submitting)

- Live demo link: https://m-live-poll-lvl-3.vercel.app/
- Demo video (1 minute) link: https://drive.google.com/file/d/1phrH84HC_0vvVmI6U5weEliVH8AkrQ6W/view?usp=sharing Test output screenshot (3+ passing tests): ✅ (see below)
- Public GitHub repo link: https://github.com/mukeshkumarji7074-ship-it/m_live_poll_lvl_3.git
- 3+ meaningful commits for Level 3: ✅


## Submission Overview

This project demonstrates:

- Multi-wallet integration with `StellarWalletsKit`
- Smart contract deployment on Stellar Testnet
- Contract reads and writes from the frontend
- Real-time event polling and state synchronization
- Visible transaction lifecycle feedback
- Wallet error handling for missing wallet, rejected request, and insufficient balance
- Loading states and progress indicators during reads/writes
- Basic caching of recently loaded poll data in `localStorage`
- Automated tests for core helper logic

## Key Features

- Connect with supported Stellar wallets including Freighter, xBull, Albedo, Rabet, Lobstr, Hana, Hot Wallet, and Klever
- Create, vote on, close, and delete polls through frontend contract calls
- Browse contract data in read-only mode even without a connected wallet
- See transaction phases in the UI: `preparing`, `awaiting-signature`, `pending`, `success`, and `error`
- Refresh poll state automatically from recent on-chain contract events

## Screenshots

🏠 Home Page
      ![Screenshot 2026-08-10 124613.png](screenshot/Screenshot%202026-08-10%20124613.png)
📝 Create Poll
      ![Screenshot 2026-08-10 124622.png](screenshot/Screenshot%202026-08-10%20124622.png)
🗳️ Voting
    ![Screenshot 2026-08-10 131012.png](screenshot/Screenshot%202026-08-10%20131012.png)
✅ CI/CD
    ![Screenshot 2026-08-10 131740.png](screenshot/Screenshot%202026-08-10%20131740.png)

## Mobile responsive screenshots

Below is a mobile view screenshot demonstrating the responsive layout on narrow screens. Replace the placeholder with a real phone-sized screenshot captured from the dev tools or a device.

![WhatsApp Image 2026-08-10 at 1.19.12 PM.jpeg](screenshot/WhatsApp%20Image%202026-08-10%20at%201.19.12%20PM.jpeg)


## Deployed Contract

- Network: `Stellar Testnet`
- Contract address: `CDPYFRUN6ZRKUIKZR45AMWF7SYPQJL4WRJIBJI2SR3DWRMMANTXXRMD2`
- Contract explorer: https://stellar.expert/explorer/testnet/contract/CDPYFRUN6ZRKUIKZR45AMWF7SYPQJL4WRJIBJI2SR3DWRMMANTXXRMD2

## Verifiable Contract Call

- Deploy tx hash: `5b24ed87e38545845d60b0df87f68e1ac324880da94ed31e7bbfc11a4bafbdd7`
- Stellar Expert link: https://stellar.expert/explorer/testnet/tx/5b24ed87e38545845d60b0df87f68e1ac324880da94ed31e7bbfc11a4bafbdd7
- Sample `create_poll` tx hash: `71ee88b4549ffcdf0663f160fe8e3483876f42a21df00641f739ae09193920e6`
- Stellar Expert link: https://stellar.expert/explorer/testnet/tx/71ee88b4549ffcdf0663f160fe8e3483876f42a21df00641f739ae09193920e6

## Live Demo

https://online-live-poll.vercel.app/

## Setup

Run all commands from the `live-poll` project directory.

1. Install dependencies:

```bash
npm install
```

2. Build the Soroban contract:

```bash
npm run contract:build
```

3. Sync the compiled contract WASM into the frontend (used to load the contract spec/ABI at runtime):

```bash
npm run wasm:sync
```

4. Optionally create a local env file:

```powershell
Copy-Item .env.example .env.local
```

5. Start the frontend:

```bash
npm run dev
```

6. Build for production:

```bash
npm run build
```

## Tests

Run the automated tests:

```bash
npm test
```

For submission, include a screenshot of the terminal output showing **3+ tests passing**.

## Environment Variables

```env
VITE_STELLAR_RPC_URL=https://soroban-testnet.stellar.org
VITE_STELLAR_NETWORK_PASSPHRASE=Test SDF Network ; September 2015
VITE_STELLAR_CONTRACT_ID=CDPYFRUN6ZRKUIKZR45AMWF7SYPQJL4WRJIBJI2SR3DWRMMANTXXRMD2
VITE_STELLAR_READ_ACCOUNT=
VITE_STELLAR_EXPLORER_URL=https://stellar.expert/explorer/testnet
VITE_POLL_CONTRACT_WASM_URL=/contracts/poll_contract.wasm
```

## Testnet Notes

- A connected wallet must be funded on Stellar Testnet before it can send contract transactions
- If a wallet has not been created on Testnet yet, fund it with Friendbot first and then retry
- The app can still read poll data without a funded wallet by using a temporary read account

## Scripts

- `npm run dev` starts the frontend
- `npm run build` creates a production build
- `npm run lint` runs ESLint
- `npm test` runs the Node.js test suite
- `npm run contract:build` builds the Soroban contract
- `npm run wasm:sync` copies the compiled WASM into `public/contracts/` for the frontend to load the contract spec
- `npm run contract:deploy` uploads and deploys the contract to testnet

## Deploy (Vercel / Netlify)

This is a standard Vite build.

- Node.js: use Node `^20.19.0` or `>=22.12.0` (required by Vite 8)
- Build command: `npm run build`
- Output directory: `dist`
- Set the env vars from the section above (at minimum `VITE_STELLAR_CONTRACT_ID` if you deploy a new contract)

## Demo Video (1 minute)

https://drive.google.com/file/d/1SRK_eF2qJyIfuN-KMlgzCpeacAeYJ23t/view?usp=sharing

Walkthrough:

1. Open the deployed site and show the “Read from contract” panel updating.
2. Connect a wallet (Freighter or any supported wallet).
3. Create a poll (show “awaiting-signature” → “pending” → “success”).
4. Vote on the poll and show the event feed / vote count updating.
5. Open the contract/tx on Stellar Expert via the links in the UI.

## Project Structure

- `src/` contains the React frontend
- `src/lib/stellar.js` contains wallet, RPC, contract, and event helpers
- `src/lib/pollCache.js` contains the basic poll cache helpers
- `src/lib/pollLogic.js` contains pure helper functions used by the UI
- `poll_contract/` contains the Soroban contract
- `scripts/` contains deployment helpers
- `tests/` contains the automated test suite

## Additional Docs

- Frontend guide: [FRONTEND.md](./FRONTEND.md)
- Contract guide: [poll_contract/README.md](./poll_contract/README.md)

## Submission Notes

- GitHub repository: `https://github.com/Sagar522290/livepoll.git`
- The project includes multiple meaningful commits in git history
- The contract is deployed on testnet and called from the frontend
- Real-time event integration and visible transaction status are implemented
- Before final submission, update the checklist at the top with your live demo link, demo video link, and test screenshot
