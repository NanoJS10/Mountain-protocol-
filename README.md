# Fake USDM Token — Mountain Protocol Impersonation

**Case:** NanoJS-PhishFactory01
**Chain:** Ethereum Mainnet
**Date:** June 24, 2026
**Investigator:** NanoJS Investigations

---

Someone deployed a fake USDM token on Ethereum, named it `MountainProtocolUSDM` in verified source code, and listed it on Uniswap V2 within minutes. The deployer wallet was funded by an Etherscan-confirmed phishing address that has been mass-funding attack wallets across Ethereum for 52 days.

This is not an isolated deployment. It is part of a coordinated phishing factory operation.

---

##  Fake Contract Address

```
0x4A9E3f6240521a4d3F10c94F4Ea1e7e76a7f578f
```

Do not buy, trade, or approve this contract. It is not Mountain Protocol USDM.

---

## The Addresses

| Role | Address |
|---|---|
| Fake USDM Contract | `0x4A9E3f6240521a4d3F10c94F4Ea1e7e76a7f578f` |
| Deployer | `0xAE9D50E345248AaB42ceFc28cEFC21749B58b8F8` |
| Phishing Funder | `0xC32020965Ed7Fc48eCf894328260A5F25D815702` |
| Root Controller | `0xcA7ECe5E43eF44De8e430629a5b535eca48e251B` |

---

## What Happened

On June 24, 2026 at 14:47 UTC, a fresh wallet  created hours earlier deployed a contract named `MountainProtocolUSDM` on Ethereum. The contract was verified on Etherscan using standard OpenZeppelin ERC-20 code, giving it a veneer of legitimacy. Within one minute of deployment, the deployer added Uniswap V2 liquidity and began interacting with the contract.

By 19:01 UTC the same day, the deployer returned 4.99 ETH back to the wallet that funded them. Total operation time: approximately 4 hours.

Tracing the funding chain reveals this is part of a larger phishing network. The deployer was funded by `0xC32020965...`, a wallet Etherscan has tagged `Fake_Phishing4164534` with 10,914 transactions. That wallet itself was funded 52 days ago by a root controller address.

On June 25, 2026, the phishing funder distributed ETH to 14+ wallets simultaneously in a single block standardized amounts of approximately 0.10 ETH each, scripted and automated. The MountainProtocolUSDM deployer is one node in that network.

---

## The Funding Chain

```
0xcA7ECe5E43eF44De8e430629a5b535eca48e251B
  [Root Controller — funded the operation 52 days ago]
        │
        ▼
0xC32020965Ed7Fc48eCf894328260A5F25D815702
  [Phishing Funder — Etherscan: Fake_Phishing4164534]
  [10,914 transactions | 52 days active]
  [Block 25396360: distributed ETH to 14+ wallets simultaneously]
        │
        ▼
0xAE9D50E345248AaB42ceFc28cEFC21749B58b8F8
  [Deployer — wallet age: 0.0 hours at deployment]
  [Received 2.73175639 ETH]
        │
        ├──► Block 25388167: Deployed MountainProtocolUSDM
        ├──► Block 25388169: Uniswap V2 liquidity added (1.1 ETH)
        ├──► Block 25388170: CRYOI listed on Uniswap V2
        └──► Block 25389427: 4.99 ETH returned to funder
```

---

## Contract Analysis

The contract source code is verified on Etherscan. Contract name in source: **MountainProtocolUSDM**.

It is a standard OpenZeppelin ERC-20 implementation no backdoors, no drain functions, no flash loan logic. The Etherscan token tracker shows it as `ERC-20: Cryoix (CRYOI)`.

The attack is not technical. It is social engineering. The name `MountainProtocolUSDM` is designed to deceive users searching for Mountain Protocol's real USDM stablecoin into purchasing a worthless token.

Key contract details:
Compiler: Solidity 0.8.30, EVM Cancun
Optimizer: 200 runs
Base: OpenZeppelin ERC-20 v5.5.0
Deployer interaction within 0 hours of wallet creation

---

## Phishing Network — Co-funded Wallets

The following wallets were funded by the same phishing funder in block 25396360 on June 25, 2026. All funded within the same block — automated, not manual.

| Wallet | ETH Received |
|---|---|
| `0x4307E357...036E19B35` | 2.64921818 ETH |
| `0x0C83309c...e60a41299` | 0.09770955 ETH |
| `0x10a40f65...dF4Cd2341` | 0.10027824 ETH |
| `0x78963806...e1684804A` | 0.10028143 ETH |
| `0x10859417...c5AFb491c` | 0.10028008 ETH |
| `0x374E3c8f...147Cc683F` | 0.10027906 ETH |
| `0x95E95bEE...185fF1F23` | 0.10027934 ETH |
| `0x69DF6769...46535a48F` | 0.10028180 ETH |
| `0x544475D2...814c9383F` | 0.10027884 ETH |
| `0xfEb56e67...55006B19f` | 0.10027864 ETH |
| `0xf9B3e0B4...F0A3783Fc` | 0.10028122 ETH |
| `0x43bD9734...942E2792e` | 0.10027818 ETH |
| `0x80dF6974...74F52cf13` | 0.10027793 ETH |
| `0xA9ab7482...373d2A5D4` | 0.08187381 ETH |

Each of these wallets should be treated as a potential additional attack wallet from the same network.

---

## Disclosure

Private notification sent to @MountainUSDM and @AnchorageDigital on June 26, 2026.
Follow-up warning sent same day 24-hour acknowledgement deadline given.
No response received.

This repository is the public disclosure.

---

## Evidence

| File | Description |
|---|---|
| `evidence/screenshots/etherscan_deployer_wallet.jpg` | Deployer wallet 9 txns, contract creation, Uniswap activity |
| `evidence/screenshots/etherscan_fake_contract.jpg` | Fake contract — MountainProtocolUSDM, Cryoix tracker |
| `evidence/screenshots/etherscan_phishing_funder.jpg` | Phishing funder — Fake_Phishing4164534 tag, 10,914 txns |
| `evidence/screenshots/metasleuth_fanout.jpg` | MetaSleuth fund flow — hub-and-spoke to 14+ wallets |
| `evidence/addresses.md` | All addresses |
| `evidence/timeline.md` | Full on-chain timeline |
| `evidence/contract_analysis.md` | Contract breakdown |
| `reports/NanoJS-PhishFactory01_Threat_Report.docx` | Full forensic report |

---

## Contact

NanoJS Investigations
nanojs@proton.me
x.com/NanoJS10
github.com/NanoJS10


---
---

# Responsible Disclosure

**Case:** NanoJS-PhishFactory01
**Investigator:** NanoJS Investigations

## Notification Attempts

| Date | Method | Recipient | Outcome |
|---|---|---|---|
| 2026-06-26 | X DM | @MountainUSDM | No response |
| 2026-06-26 | X DM | @AnchorageDigital | No response |
| 2026-06-26 | X DM follow-up | Both | No response |
| 2026-06-26 | Email | Mountain Protocol | No response |

A 24-hour private disclosure window was given before this repository was made public. No acknowledgement was received within that window.

This disclosure follows standard responsible disclosure protocol. The goal is to protect users of Mountain Protocol — not to cause reputational damage.

**Contact:** nanojs@proton.me | x.com/NanoJS10 | github.com/NanoJS10


---
---
 evidence/addresses

# Addresses — NanoJS-PhishFactory01

## Core Addresses

| Role | Address |
|---|---|
| Fake Contract | `0x4A9E3f6240521a4d3F10c94F4Ea1e7e76a7f578f` |
| Deployer | `0xAE9D50E345248AaB42ceFc28cEFC21749B58b8F8` |
| Phishing Funder | `0xC32020965Ed7Fc48eCf894328260A5F25D815702` |
| Root Controller | `0xcA7ECe5E43eF44De8e430629a5b535eca48e251B` |

## Etherscan

https://etherscan.io/address/0x4A9E3f6240521a4d3F10c94F4Ea1e7e76a7f578f
https://etherscan.io/address/0xAE9D50E345248AaB42ceFc28cEFC21749B58b8F8
https://etherscan.io/address/0xC32020965Ed7Fc48eCf894328260A5F25D815702
https://etherscan.io/address/0xcA7ECe5E43eF44De8e430629a5b535eca48e251B

## MetaSleuth

https://metasleuth.io/result/eth/0xC32020965Ed7Fc48eCf894328260A5F25D815702

## Sibling Wallets Funded in Block 25396360

All funded by `0xC32020965...` in the same block on June 25, 2026.
Each should be monitored for additional fake token deployments.

`0x4307E357...036E19B35` — 2.64921818 ETH
`0x0C83309c...e60a41299` — 0.09770955 ETH
`0x10a40f65...dF4Cd2341` — 0.10027824 ETH
`0x78963806...e1684804A` — 0.10028143 ETH
`0x10859417...c5AFb491c` — 0.10028008 ETH
`0x374E3c8f...147Cc683F` — 0.10027906 ETH
`0x95E95bEE...185fF1F23` — 0.10027934 ETH
`0x69DF6769...46535a48F` — 0.10028180 ETH
`0x544475D2...814c9383F` — 0.10027884 ETH
`0xfEb56e67...55006B19f` — 0.10027864 ETH
`0xf9B3e0B4...F0A3783Fc` — 0.10028122 ETH
`0x43bD9734...942E2792e` — 0.10027818 ETH
`0x80dF6974...74F52cf13` — 0.10027793 ETH
`0xA9ab7482...373d2A5D4` — 0.08187381 ETH


---
---

 Evidence/timeline.md

# Timeline — NanoJS-PhishFactory01

## On-Chain

| Block | UTC | Event |
|---|---|---|
| 25388166 | 2026-06-24 14:47:47 | Deployer received 2.73175639 ETH from phishing funder |
| 25388167 | 2026-06-24 14:47:59 | MountainProtocolUSDM contract deployed |
| 25388168 | 2026-06-24 14:48:11 | Deployer called fake contract |
| 25388169 | 2026-06-24 14:48:23 | Uniswap V2 liquidity added — 1.1 ETH |
| 25388170 | 2026-06-24 14:48:35 | Uniswap V2: CRYOI listed |
| 25388206 | 2026-06-24 14:55:47 | Unknown wallet interacted with fake contract |
| 25388215 | 2026-06-24 14:57:35 | Unknown wallet interacted with fake contract |
| 25388220 | 2026-06-24 14:58:35 | Unknown wallet interacted with fake contract |
| 25388223 | 2026-06-24 14:59:11 | Unknown wallet interacted with fake contract |
| 25389424 | 2026-06-24 19:01:11 | Deployer called Uniswap V2 Router |
| 25389425 | 2026-06-24 19:01:23 | Deployer called Uniswap V2 Router |
| 25389427 | 2026-06-24 19:01:47 | Deployer returned 4.99061708 ETH to phishing funder |
| 25396360 | 2026-06-25 18:13:59 | Phishing funder distributed ETH to 14+ wallets in one block |
| 25397053 | 2026-06-25 20:33:47 | Fake_Phishing4164534 interacted with funder wallet |

## Investigation

| Date | Action |
|---|---|
| 2026-06-24 | Suspicious contract deployment flagged |
| 2026-06-26 | Full investigation completed |
| 2026-06-26 | Contract source confirmed as MountainProtocolUSDM |
| 2026-06-26 | DMs sent to @MountainUSDM and @AnchorageDigital |
| 2026-06-26 | Follow-up warning sent — 24hr deadline |
| 2026-06-26 | Full report emailed to Mountain Protocol |
| 2026-06-27 | No response received — public disclosure |


---
---


# Evidence/contract_analysis.md

# Contract Analysis — NanoJS-PhishFactory01

## Fake Contract

**Address:** `0x4A9E3f6240521a4d3F10c94F4Ea1e7e76a7f578f`
**Name in source code:** MountainProtocolUSDM
**Token tracker:** ERC-20: Cryoix (CRYOI)
**Verified:** Yes Etherscan (Source Code tab confirms name)
**Created:** Block 25388167 — June 24, 2026 14:47:59 UTC
**Creator:** `0xAE9D50E345248AaB42ceFc28cEFC21749B58b8F8`

## Technical Details

| Field | Value |
|---|---|
| Solidity version | 0.8.30 |
| EVM version | Cancun |
| Optimizer | Enabled 200 runs |
| Base contract | OpenZeppelin ERC-20 v5.5.0 |
| Source length | 23,639 characters |

## Functions

Standard ERC-20 only — no custom attack logic:
`name`, `symbol`, `decimals`, `totalSupply`, `balanceOf`, `transfer`,
`transferFrom`, `approve`, `allowance`, `_mint`, `_burn`, `_transfer`

## What Was Not Found

No flash loan calls
No delegatecall or selfdestruct
No onlyOwner backdoor
No blacklist or freeze mechanism
No external protocol calls
No drain functions

## Assessment

This is a social engineering attack, not a technical exploit. The contract is a clean OpenZeppelin ERC-20. The weapon is the name `MountainProtocolUSDM` chosen specifically to impersonate Mountain Protocol's legitimate USDM stablecoin in DEX search results and token lists.

Users who purchase this token believing it to be real USDM will receive a worthless token with no underlying yield or backing.

## Deployer Behaviour

The deployer wallet had zero prior history. It was created, funded, used to deploy this contract and list it on Uniswap, then returned the remaining ETH to the phishing funder all within 4 hours. This is a throwaway deployment wallet, purpose-built for this operation.

