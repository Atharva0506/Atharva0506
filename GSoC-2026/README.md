<p align="center">
  <img src="assets/chainvoice-banner.png" alt="Chainvoice: private invoicing, on-chain" width="100%">
</p>

<h1 align="center">Google Summer of Code 2026: Final Report</h1>

<p align="center">
  <b>Chainvoice: Private On-Chain Invoicing with ThruBox Encrypted Relay</b>
</p>

<p align="center">
  <a href="https://github.com/StabilityNexus/Chainvoice/releases/tag/v2.0.0"><img alt="Chainvoice v2.0.0" src="https://img.shields.io/badge/Chainvoice-v2.0.0-22c55e"></a>
  <a href="https://github.com/AOSSIE-Org/ThruBox-Server/releases/tag/v1.0.0"><img alt="ThruBox Server v1.0.0" src="https://img.shields.io/badge/ThruBox_Server-v1.0.0-00ADD8?logo=go&logoColor=white"></a>
  <a href="https://www.npmjs.com/package/@aossie-org/thrubox-client"><img alt="npm thrubox-client" src="https://img.shields.io/npm/v/@aossie-org/thrubox-client?label=%40aossie-org%2Fthrubox-client&logo=npm"></a>
  <a href="https://www.npmjs.com/package/@aossie-org/idb-backup"><img alt="npm idb-backup" src="https://img.shields.io/npm/v/@aossie-org/idb-backup?label=%40aossie-org%2Fidb-backup&logo=npm"></a>
</p>

---

## 👤 Project details

| | |
|---|---|
| **Contributor** | Atharva Girish Naik · [@Atharva0506](https://github.com/Atharva0506) |
| **Organization** | [AOSSIE](https://aossie.org) · [Stability Nexus](https://stability.nexus) |
| **Mentors** | Bruno Woltzenlogel Paleo ([@Zahnentferner](https://github.com/Zahnentferner)) · Yogesh Agrawal ([@yogesh0509](https://github.com/yogesh0509)) · Karan Kumar Kumawat ([@kumawatkaran523](https://github.com/kumawatkaran523)) · Aditya Bhattad ([@adityabhattad2021](https://github.com/adityabhattad2021)) · Aditya Gupta |
| **Repositories** | [StabilityNexus/Chainvoice](https://github.com/StabilityNexus/Chainvoice) · [AOSSIE-Org/ThruBox-Server](https://github.com/AOSSIE-Org/ThruBox-Server) · [AOSSIE-Org/ThruBox-Client](https://github.com/AOSSIE-Org/ThruBox-Client) · [AOSSIE-Org/IndexedDB-Import-Export](https://github.com/AOSSIE-Org/IndexedDB-Import-Export) |
| **Project size** | Large (350 hours, 22 weeks) · May 26 – Nov 2, 2026 |
| **Project page** | [chainvoice.stability.nexus](https://chainvoice.stability.nexus) |
| **Demo video** | [▶️ Watch the demo](https://drive.google.com/file/d/122KQXxjb4ltC-8FrBgoR3bErSzOM7dU9/view?usp=sharing) |

## 📑 Contents

1. [Abstract](#-abstract)
2. [Deliverables](#-deliverables)
3. [How it works](#️-how-it-works)
4. [Timeline: Lit → Waku → ThruBox](#️-timeline-lit--waku--thrubox)
5. [Work done](#️-work-done)
6. [Deployments](#-deployments)
7. [Challenges and lessons](#-challenges-and-lessons)
8. [Future work](#-future-work)
9. [Acknowledgements](#-acknowledgements)

## 📝 Abstract

Chainvoice's privacy layer was broken: Lit Protocol was defunct, so invoice creation and rendering failed for real users. This project rebuilt Chainvoice's privacy architecture end to end and shipped **Chainvoice v2.0.0**.

Invoice details are now encrypted in the browser with **ECIES (secp256k1 + AES-256-GCM)**. Only a 32-byte hash goes on-chain, and recipients check every invoice against that hash. When Waku's rate limiting blocked invoice delivery, I built **ThruBox**, a self-hostable encrypted mailbox relay with a Go server and a TypeScript SDK. I also built **idb-backup**, a reusable IndexedDB backup library that Chainvoice uses for local storage.

All four projects are released. The two libraries are published on npm and the relay's Docker image is on GHCR.

## 📦 Deliverables

| Project | What it is | Release | Published on |
|---|---|---|---|
| [**Chainvoice**](https://github.com/StabilityNexus/Chainvoice) | Private on-chain invoicing dApp (React + Solidity) | [v2.0.0](https://github.com/StabilityNexus/Chainvoice/releases/tag/v2.0.0) | 🌐 Web: [chainvoice.stability.nexus](https://chainvoice.stability.nexus) |
| [**ThruBox-Server**](https://github.com/AOSSIE-Org/ThruBox-Server) 🆕 | Encrypted mailbox relay (Go + SQLite) | [v1.0.0](https://github.com/AOSSIE-Org/ThruBox-Server/releases/tag/v1.0.0) | 🐳 GHCR: [`ghcr.io/aossie-org/thrubox-server`](https://github.com/AOSSIE-Org/ThruBox-Server/pkgs/container/thrubox-server) |
| [**ThruBox-Client**](https://github.com/AOSSIE-Org/ThruBox-Client) 🆕 | TypeScript SDK for ThruBox | [v1.1.0](https://github.com/AOSSIE-Org/ThruBox-Client/releases/tag/v1.1.0) | 📦 npm: [`@aossie-org/thrubox-client`](https://www.npmjs.com/package/@aossie-org/thrubox-client) |
| [**IndexedDB-Import-Export**](https://github.com/AOSSIE-Org/IndexedDB-Import-Export) 🆕 | IndexedDB backup and restore library | [v1.1.0](https://github.com/AOSSIE-Org/IndexedDB-Import-Export/releases/tag/v1.1.0) | 📦 npm: [`@aossie-org/idb-backup`](https://www.npmjs.com/package/@aossie-org/idb-backup) |

<sub>🆕 Repository created during GSoC 2026.</sub>

### 📊 By the numbers

| | Chainvoice | ThruBox-Server | ThruBox-Client | IndexedDB-Import-Export | **Total** |
|---|:-:|:-:|:-:|:-:|:-:|
| **Merged PRs** | 63 | 23 | 23 | 22 | **131** |
| **PRs reviewed** | 32 | 18 | 8 | 9 | **67** |

- I also reviewed **19** PRs in WalletLink, StablePay and Fate.
- npm downloads since May 2026: **1,017** for `@aossie-org/idb-backup` and **416** for `@aossie-org/thrubox-client`.

### 🧰 Technologies

**Frontend:** React, Vite, Wagmi, Viem, WalletLink, IndexedDB<br>
**Smart contracts:** Solidity, Foundry, Slither<br>
**Relay:** Go, SQLite, Docker<br>
**SDK and libraries:** TypeScript, Vitest<br>
**Cryptography:** ECIES (secp256k1 + AES-256-GCM)<br>
**CI/CD:** GitHub Actions, Cloudflare Pages, npm Trusted Publishing (OIDC), GHCR

## ⚙️ How it works

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://github.com/user-attachments/assets/1037bf05-5e00-40ca-b8a2-140415652741">
  <img alt="Chainvoice system architecture" src="https://github.com/user-attachments/assets/a2fc6c12-1552-4e42-9b31-6de6af1001c9">
</picture>

1. The sender's browser encrypts the invoice details for the recipient's public key (ECIES).
2. The contract stores only the parties, amount, token and a `bytes32` hash of the details.
3. The encrypted payload goes to the recipient's ThruBox mailbox.
4. The recipient decrypts it, checks it against the on-chain hash and pays in the native coin or any ERC-20 token.

<details>
<summary><b>Sending an invoice</b></summary>
<br>
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://github.com/user-attachments/assets/447f8f28-2dd5-45de-8f2b-3ea3a822af00">
  <img alt="Sending an invoice" src="https://github.com/user-attachments/assets/7aa67cbb-a9e2-4aeb-a8ef-7fbf01361f0c">
</picture>
</details>

<details>
<summary><b>Receiving and paying an invoice</b></summary>
<br>
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://github.com/user-attachments/assets/369b3d1a-709f-440e-a8e0-ca0cf2f43f5e">
  <img alt="Receiving and paying an invoice" src="https://github.com/user-attachments/assets/6a74e29b-2495-4aa4-b301-7add80273a84">
</picture>
</details>

## 🗓️ Timeline: Lit → Waku → ThruBox

| Weeks | What happened |
|:-:|---|
| **1–2** | Built `IndexedDB-Import-Export` as a standalone library instead of code embedded in Chainvoice, so other AOSSIE projects can reuse it. Published it as `@aossie-org/idb-backup`. Built PR preview environments to speed up mentor reviews. |
| **3–5** | Removed Lit Protocol. Added ECIES encryption and an on-chain key registry, and cut on-chain invoice storage to a 32-byte hash. Invoice delivery went over Waku. |
| **6** | Waku started rate-limiting LightPush requests, which blocked the frontend. I opened a support ticket with the Waku team. |
| **7** | Since the rate limiting couldn't be fixed in time, we pivoted to a custom relay and designed **ThruBox**: one Go binary with embedded SQLite, no broker and no P2P network. |
| **8–12** | Built the ThruBox server and SDK, published them to npm and GHCR, and wired ThruBox into Chainvoice. Before the midterm, added repository docs across all four repos. |
| **13–17** | Product work: share and import invoices by link or QR code, sender-details onboarding, a new dashboard layout, one-command Docker setup, and a Terms of Use modal. |
| **18–22** | Security review and launch: contract hardening, a QA audit, fixes for all five launch blockers, WalletLink, testnet deployments, and the v1.0.0 / v1.1.0 / v2.0.0 releases. |

## 🛠️ Work done

### 1. Chainvoice v2.0.0

#### 🔒 Privacy

| PR | Change |
|---|---|
| [#171](https://github.com/StabilityNexus/Chainvoice/pull/171) | Removed Lit Protocol and all its code |
| [#169](https://github.com/StabilityNexus/Chainvoice/pull/169) | On-chain public-key registry and `invoiceDataHash` validation |
| [#195](https://github.com/StabilityNexus/Chainvoice/pull/195) | Invoice payloads go over the ThruBox relay instead of being stored on-chain |
| [#197](https://github.com/StabilityNexus/Chainvoice/pull/197) | Key registration is a step in the invoice flow |
| [#238](https://github.com/StabilityNexus/Chainvoice/pull/238) | Key derivation bound to the site's origin and wallet address, so lookalike sites can't derive keys |
| [#247](https://github.com/StabilityNexus/Chainvoice/pull/247), [#317](https://github.com/StabilityNexus/Chainvoice/pull/317) | Invoices are shown and paid from verified on-chain values, never from the payload |

#### ✨ Features

| PR | Change |
|---|---|
| [#209](https://github.com/StabilityNexus/Chainvoice/pull/209) | Share an invoice by link, QR code or `.cvinv` file, and import it before connecting a wallet |
| [#175](https://github.com/StabilityNexus/Chainvoice/pull/175), [#284](https://github.com/StabilityNexus/Chainvoice/pull/284), [#297](https://github.com/StabilityNexus/Chainvoice/pull/297) | Batch invoicing: up to 50 invoices per transaction (15 on Sepolia, to fit its gas limit) |
| [#138](https://github.com/StabilityNexus/Chainvoice/pull/138), [#249](https://github.com/StabilityNexus/Chainvoice/pull/249) | Export to JSON, CSV and PDF |
| [#157](https://github.com/StabilityNexus/Chainvoice/pull/157) | Product catalog import and invoice autofill |
| [#183](https://github.com/StabilityNexus/Chainvoice/pull/183), [#204](https://github.com/StabilityNexus/Chainvoice/pull/204), [#205](https://github.com/StabilityNexus/Chainvoice/pull/205) | Settings page, first-run onboarding and a compact dashboard |
| [#185](https://github.com/StabilityNexus/Chainvoice/pull/185) | Local invoice storage in IndexedDB |
| [#272](https://github.com/StabilityNexus/Chainvoice/pull/272) | Replaced RainbowKit/WalletConnect with WalletLink, Stability Nexus's own wallet connector |
| [#178](https://github.com/StabilityNexus/Chainvoice/pull/178), [#179](https://github.com/StabilityNexus/Chainvoice/pull/179) | Input validation, with tests |

#### 🛡️ Smart contract and security

| PR | Change |
|---|---|
| [#228](https://github.com/StabilityNexus/Chainvoice/pull/228) | SafeERC20 and a check of the amount the issuer actually receives, so USDT-style and fee-on-transfer tokens are safe |
| [#295](https://github.com/StabilityNexus/Chainvoice/pull/295) | Fee roles renamed to `dev`, `devFee` and `devFeeReceiver` |
| [#242](https://github.com/StabilityNexus/Chainvoice/pull/242), [#245](https://github.com/StabilityNexus/Chainvoice/pull/245) | Slither static analysis in CI and reentrancy-guard tests |
| [#307](https://github.com/StabilityNexus/Chainvoice/pull/307), [#319](https://github.com/StabilityNexus/Chainvoice/pull/319) | The relay rejects malformed payloads and never silently replaces a key. The client waits out the relay's rate limit instead of dropping invoices |
| [#320](https://github.com/StabilityNexus/Chainvoice/pull/320), [#225](https://github.com/StabilityNexus/Chainvoice/pull/225) | Pay and cancel can no longer overlap. Batch amounts are summed as BigInt |
| [#332](https://github.com/StabilityNexus/Chainvoice/pull/332), [#335](https://github.com/StabilityNexus/Chainvoice/pull/335) | Fixes from the peer audit before the mainnet deployment |

#### 🚀 Infrastructure

| PR | Change |
|---|---|
| [#166](https://github.com/StabilityNexus/Chainvoice/pull/166), [#211](https://github.com/StabilityNexus/Chainvoice/pull/211), [#309](https://github.com/StabilityNexus/Chainvoice/pull/309) | PR preview environments, moved off the production origin to Cloudflare Pages |
| [#180](https://github.com/StabilityNexus/Chainvoice/pull/180), [#229](https://github.com/StabilityNexus/Chainvoice/pull/229), [#288](https://github.com/StabilityNexus/Chainvoice/pull/288) | Frontend and contract CI, lint enforcement, a build-size report and drafted release notes |
| [#218](https://github.com/StabilityNexus/Chainvoice/pull/218) | One-command Docker setup for the frontend and a ThruBox relay |
| [#250](https://github.com/StabilityNexus/Chainvoice/pull/250)–[#255](https://github.com/StabilityNexus/Chainvoice/pull/255) | SEO, social cards and lazy loading, which cut the JS bundle by 38% |
| [#315](https://github.com/StabilityNexus/Chainvoice/pull/315) | A working Ethereum Classic network config and Mordor/Amoy testnets |

### 2. ThruBox-Server v1.0.0 🆕

A small, self-hostable relay that works as a dumb encrypted mailbox. It stores and forwards opaque blobs and never sees plaintext.

| PR | Change |
|---|---|
| [#5](https://github.com/AOSSIE-Org/ThruBox-Server/pull/5)–[#8](https://github.com/AOSSIE-Org/ThruBox-Server/pull/8) | Config system, SQLite store, HTTP handlers and a server with graceful shutdown |
| [#9](https://github.com/AOSSIE-Org/ThruBox-Server/pull/9), [#18](https://github.com/AOSSIE-Org/ThruBox-Server/pull/18) | Docker support, and multi-arch images on GHCR with provenance and an SBOM |
| [#34](https://github.com/AOSSIE-Org/ThruBox-Server/pull/34)–[#36](https://github.com/AOSSIE-Org/ThruBox-Server/pull/36) | `PORT` variable, configurable config path and CORS for browser clients |
| [#67](https://github.com/AOSSIE-Org/ThruBox-Server/pull/67) | Per-mailbox cursors, content-derived message IDs, and a fix for a rate-limit bypass via spoofed `X-Forwarded-For` |
| [#70](https://github.com/AOSSIE-Org/ThruBox-Server/pull/70) | Removed an unauthenticated delete endpoint |

### 3. ThruBox-Client v1.1.0 🆕

| PR | Change |
|---|---|
| [#5](https://github.com/AOSSIE-Org/ThruBox-Client/pull/5), [#8](https://github.com/AOSSIE-Org/ThruBox-Client/pull/8) | TypeScript SDK (`send`, `receive`, `poll`) with unit tests |
| [#28](https://github.com/AOSSIE-Org/ThruBox-Client/pull/28) | npm publishing via OIDC Trusted Publishing, with provenance |
| [#63](https://github.com/AOSSIE-Org/ThruBox-Client/pull/63) | Cursor-based polling. The cursor only moves forward after the callback succeeds, so a failed save is retried instead of lost |
| [#65](https://github.com/AOSSIE-Org/ThruBox-Client/pull/65), [#66](https://github.com/AOSSIE-Org/ThruBox-Client/pull/66) | Removed `delete()` and released 1.1.0 |

### 4. IndexedDB-Import-Export v1.1.0 🆕

| PR | Change |
|---|---|
| [#11](https://github.com/AOSSIE-Org/IndexedDB-Import-Export/pull/11), [#12](https://github.com/AOSSIE-Org/IndexedDB-Import-Export/pull/12) | Exporter with `Uint8Array` serialization, and an importer with overwrite and merge strategies |
| [#29](https://github.com/AOSSIE-Org/IndexedDB-Import-Export/pull/29) | Exporter, importer and round-trip tests |
| [#31](https://github.com/AOSSIE-Org/IndexedDB-Import-Export/pull/31), [#63](https://github.com/AOSSIE-Org/IndexedDB-Import-Export/pull/63), [#98](https://github.com/AOSSIE-Org/IndexedDB-Import-Export/pull/98) | Automated npm release pipeline |
| [#73](https://github.com/AOSSIE-Org/IndexedDB-Import-Export/pull/73) | Selective restore with `storeNames` |

### 5. Across the organization

- Rolled out security-review and remediation tooling to all four repos ([Chainvoice #221](https://github.com/StabilityNexus/Chainvoice/pull/221), [ThruBox-Server #49](https://github.com/AOSSIE-Org/ThruBox-Server/pull/49), [ThruBox-Client #44](https://github.com/AOSSIE-Org/ThruBox-Client/pull/44), [IndexedDB #94](https://github.com/AOSSIE-Org/IndexedDB-Import-Export/pull/94)).
- Set up npm publishing CI for [WalletLink](https://github.com/StabilityNexus/WalletLink/pull/8) and [SocialShareButton](https://github.com/AOSSIE-Org/SocialShareButton/pull/156).
- Added repository guidelines, `AGENTS.md` and maintainer docs to all four repos.

## 🌐 Deployments

| Network | Chain ID | `Chainvoice.sol` |
|---|:-:|---|
| Ethereum Classic (mainnet) | 61 | _TODO: address_ |
| Base (mainnet) | 8453 | _TODO: address_ |
| Ethereum Sepolia | 11155111 | [`0xff10Cda5…136363a`](https://sepolia.etherscan.io/address/0xff10Cda545E10656C2DcBEAB6C9eC375E136363a) |
| Ethereum Classic Mordor | 63 | [`0xeF6669DD…C2120d2`](https://etc-mordor.blockscout.com/address/0xeF6669DDEd0078A8Cfdd758A40D194b1cC2120d2) |

## 💡 Challenges and lessons

- **Don't let an external dependency block you.** Waku's rate limiting stopped frontend work for weeks. Building ThruBox was more work up front, but it gave the project a relay we control, can test and can self-host.
- **Make things reusable.** Building `idb-backup` and ThruBox as standalone libraries instead of code embedded in Chainvoice means other projects can use them. Both are published with automated, provenance-signed releases.
- **Review speed matters.** PRs waiting on review for weeks were the biggest slowdown. PR preview environments and smaller PRs helped mentors review faster.
- **Audit before launch.** A full QA and security audit before the release found five launch blockers, including a payload that could crash a recipient's page and key derivation that wasn't bound to the origin. All five were fixed before release.

## 🔭 Future work

- Grow ThruBox into a general-purpose relay for other AOSSIE and Stability Nexus apps, for example as the transport for WalletLink mobile.
- Push notifications for new invoices, and running ThruBox on several relays for redundancy.
- Add more EVM chains as Chainvoice is deployed to them.

## 🙏 Acknowledgements

Thank you to my mentors [@Zahnentferner](https://github.com/Zahnentferner), [@yogesh0509](https://github.com/yogesh0509), [@kumawatkaran523](https://github.com/kumawatkaran523), [@adityabhattad2021](https://github.com/adityabhattad2021) and Aditya Gupta for their reviews, guidance and patience, especially during the Waku → ThruBox pivot. Thanks also to the AOSSIE and Stability Nexus community, and to every contributor whose PRs went into Chainvoice v2.0.0.
