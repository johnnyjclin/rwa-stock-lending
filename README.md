# RWA Stock Lending — Contract Integration Experiments

This is the `compound-test` branch of a hackathon proof of concept. It preserves earlier lending-contract experiments and their application adapters. Switch to `main` for the current application overview.

**Use synthetic data, disposable test wallets and sandbox/testnet services only. This branch is not a production financial service or an audited lending protocol.**

## Integration focus

My contribution is the application integration layer: connecting the React interface, Next.js backend, MongoDB records and existing contract interfaces. ERC-3643 / OnchainID and lending-contract implementations were developed by other contributors or upstream projects.

This branch explores:

- Wallet connection and application state.
- Brokerage sandbox account data and tokenized-asset workflows.
- Calls to identity registries, claim issuers and token contracts.
- Lending interfaces for collateral supply, withdrawal, borrowing and repayment.
- Test-contract and price-oracle configuration.

The Solidity contracts here are experimental artifacts, not an official Compound deployment. Compatibility depends on the exact contract ABI, network, token units and deployment configuration.

## Repository guide

- [`src/app`](src/app): application pages, server actions and API routes.
- [`src/lib`](src/lib): brokerage, identity and lending adapters plus database access.
- [`contracts`](contracts): earlier lending and oracle experiments.
- [`scripts`](scripts): experimental setup helpers; review them before use.

The stack combines Next.js, React, TypeScript, MongoDB, Ethers and Solidity tooling. Historical contract notes, addresses and deployment scripts are reference material, not maintained production configuration.

## Local exploration

Use Node.js 22 LTS, npm, a local MongoDB instance and a test-only browser wallet. Copy `.env.example` to `.env.local`, then supply your own sandbox credentials and compatible testnet contracts. The application selects the `rwa_lending` database.

```sh
npm ci
npm run dev -- --hostname 127.0.0.1
```

The blank configuration does not provision external services or contracts. Some legacy package scripts reference files that are not present; this branch is not a complete deployment kit. Do not run deployment or transaction scripts against accounts holding real assets.

## Boundaries

Wallet-address checks and application identity records are not a complete authentication or KYC/AML system. Minting a demonstration token does not prove real-asset ownership, reservation or settlement. Public deployment would require separate authorization, verification, dependency, privacy and recovery work, plus contract review.

## Configuration safety

Keep credentials and authenticated URLs in `.env.local`. `NEXT_PUBLIC_*` settings are exposed to the browser and must contain public configuration only. Never commit personal data, private keys or live service credentials.

Install [Gitleaks](https://github.com/gitleaks/gitleaks) 8.25+ and enable the local check in each clone:

```sh
git config core.hooksPath .githooks
gitleaks git --log-opts="--all --full-history" --redact=100 --ignore-gitleaks-allow
```

The hook blocks staged local environment files and scans staged changes. After the history cleanup, use a fresh clone instead of merging or pushing old history. Inspect unpublished work before reapplying it; copies in other clones or forks are not erased by a rewrite.

## Attribution

- [ERC-3643 / tokenized-stock contracts](https://github.com/RonShih/Tokenized-Stock)
- [Hackathon lending contracts](https://github.com/herochen11/comet_rwa_hackathon)
- [OnchainID](https://github.com/onchain-id/solidity)

See [LICENSE](LICENSE). Referenced projects retain their own licenses and attribution requirements.
