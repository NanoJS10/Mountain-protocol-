
# Fake USDM Token — Mountain Protocol Wind-Down Exploitation

**Case:** NanoJS-PhishFactory01
**Chain:** Ethereum Mainnet
**Date:** June 24, 2026
**Investigator:** NanoJS Investigations

---

Mountain Protocol announced the wind-down of USDM following its acquisition by Anchorage Digital. Phase 3 begins August 22, 2026 at which point all USDM redemptions move exclusively to a Uniswap pool on Ethereum.

On June 24, 2026 during the wind-down period, someone deployed a fake USDM token on Ethereum, named it `MountainProtocolUSDM` in verified source code, and listed it on Uniswap V2 within minutes. The deployer was funded by an Etherscan-confirmed phishing address with 10,914 transactions.

The timing is not accidental. This fake token is positioned to intercept users searching for USDM on Uniswap during and after the Phase 3 transition.

---

## Fake Contract Address

```
0x4A9E3f6240521a4d3F10c94F4Ea1e7e76a7f578f
```

Do not buy, trade, or approve this contract. It is not Mountain Protocol USDM.

---

## Why the Timing Matters

Mountain Protocol's wind-down is structured in three phases:

Phase 1 (May 12 — June 11): Minting disabled. Rewards still active.
Phase 2 (June 12 — July 11): Reward rate set to 0%.
Phase 3 (August 22 onwards): USDM reserves move to a Uniswap pool. All redemptions happen on Uniswap directly.

This fake token was deployed on June 24 — deep in Phase 2, six weeks before Phase 3 begins. When Phase 3 launches and users go to Uniswap to redeem real USDM, they may encounter this fake token instead.

Users who are unfamiliar with Uniswap — specifically those redeeming USDM for the first time — are the target. The name `MountainProtocolUSDM` in verified source code is designed to appear in search results and token lists alongside the real redemption pool.

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

On June 24, 2026 at 14:47 UTC, a wallet created hours earlier deployed a contract named `MountainProtocolUSDM` on Ethereum. The contract was verified on Etherscan using standard OpenZeppelin ERC-20 code. Within one minute of deployment, Uniswap V2 liquidity was added. By 19:01 UTC the same day, the deployer returned 4.99 ETH back to the wallet that funded them.

Total operation window: approximately 4 hours.

Tracing the funding chain shows this is part of a coordinated phishing network. The deployer was funded by `0xC32020965...` — tagged `Fake_Phishing4164534` by Etherscan — with 10,914 transactions active across 52 days. That wallet was itself funded by a root controller address 52 days ago.

On June 25, 2026, the phishing funder distributed ETH to 14+ wallets simultaneously in a single block. Standardized amounts. Automated. The MountainProtocolUSDM deployer is one node in a larger network of attack wallets.

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

It is a standard OpenZeppelin ERC-20 implementation. No backdoors. No drain functions. No flash loan logic. The attack is not technical, it is social engineering timed to the wind-down.

Mountain Protocol's Phase 3 instructs all users to redeem USDM via Uniswap. Users who search for USDM on Uniswap may find this fake token before finding the real redemption pool. Users unfamiliar with verifying contract addresses are the primary target.

Key contract details:
Compiler: Solidity 0.8.30, EVM Cancun
Optimizer: 200 runs
Base: OpenZeppelin ERC-20 v5.5.0
Deployer wallet age at deployment: 0.0 hours

---

## Phishing Network — Co-funded Wallets

The following wallets were funded by the same phishing funder in block 25396360 on June 25, 2026. All funded in the same block — automated, not manual. Each should be monitored for additional fake token deployments.

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

---

## Disclosure

Private notification sent to @MountainUSDM and @AnchorageDigital on June 26, 2026.
Follow-up warning sent same day — 24-hour acknowledgement deadline given.
No response received.

This repository is the public disclosure.

Phase 3 begins August 22, 2026. Users will be redeeming on Uniswap. This fake token must be flagged before that date.

---

## Evidence

| File | Description |
|---|---|
| `evidence/screenshots/etherscan_deployer_wallet.jpg` | Deployer wallet — 9 txns, contract creation, Uniswap activity |
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

# DISCLOSURE.md

# Responsible Disclosure

**Case:** NanoJS-PhishFactory01
**Investigator:** NanoJS Investigations

## Context

Mountain Protocol announced the wind-down of USDM with Phase 3 beginning August 22, 2026. All USDM redemptions in Phase 3 move to Uniswap. This fake token was deployed during the wind-down period and is positioned to intercept users redeeming on Uniswap during and after Phase 3.

## Notification Attempts

| Date | Method | Recipient | Outcome |
|---|---|---|---|
| 2026-06-26 | X DM | @MountainUSDM | No response |
| 2026-06-26 | X DM | @AnchorageDigital | No response |
| 2026-06-26 | X DM follow-up | Both | No response |
| 2026-06-26 | Email | Mountain Protocol | No response |

A 24-hour private disclosure window was given before this repository was made public. No acknowledgement was received within that window.

This disclosure is made in good faith to protect USDM holders during the wind-down transition. The August 22 Phase 3 date makes this time-sensitive — users heading to Uniswap to redeem are the primary target of this fake token.

**Contact:** nanojs@proton.me | x.com/NanoJS10 | github.com/NanoJS10


---
---

# Evidence/addresses.md

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

 # Evidence/timeline.md

# Timeline — NanoJS-PhishFactory01

## Mountain Protocol Wind-Down Context

| Date | Event |
|---|---|
| May 12, 2026 | Phase 1 begins — minting disabled, rewards active |
| June 12, 2026 | Phase 2 begins — reward rate set to 0% |
| June 24, 2026 | Fake MountainProtocolUSDM deployed — during Phase 2 |
| July 11, 2026 | Phase 2 ends |
| August 22, 2026 | Phase 3 begins — all USDM redemptions move to Uniswap |

## On-Chain Timeline

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

## Investigation Timeline

| Date | Action |
|---|---|
| 2026-06-24 | Suspicious contract deployment flagged |
| 2026-06-26 | Full investigation completed |
| 2026-06-26 | Contract source confirmed as MountainProtocolUSDM |
| 2026-06-26 | Wind-down context identified — timing assessed as deliberate |
| 2026-06-26 | DMs sent to @MountainUSDM and @AnchorageDigital |
| 2026-06-26 | Follow-up warning sent — 24hr deadline |
| 2026-06-26 | Full report emailed to Mountain Protocol |
| 2026-06-27 | No response received — public disclosure |
| 2026-08-22 | Phase 3 begins — critical date for user exposure |


---
---

 Evidence/contract_analysis.md

# Contract Analysis — NanoJS-PhishFactory01

## Fake Contract

**Address:** `0x4A9E3f6240521a4d3F10c94F4Ea1e7e76a7f578f`
**Name in source code:** MountainProtocolUSDM
**Token tracker:** ERC-20: Cryoix (CRYOI)
**Verified:** Yes — Etherscan
**Created:** Block 25388167  June 24, 2026 14:47:59 UTC
**Creator:** `0xAE9D50E345248AaB42ceFc28cEFC21749B58b8F8`

## Technical Details

| Field | Value |
|---|---|
| Solidity version | 0.8.30 |
| EVM version | Cancun |
| Optimizer | Enabled — 200 runs |
| Base contract | OpenZeppelin ERC-20 v5.5.0 |
| Source length | 23,639 characters |

## Functions

Standard ERC-20 only — no custom attack logic:
name, symbol, decimals, totalSupply, balanceOf, transfer,
transferFrom, approve, allowance, _mint, _burn, _transfer

## What Was Not Found

No flash loan calls
No delegatecall or selfdestruct
No onlyOwner backdoor
No blacklist or freeze mechanism
No external protocol calls
No drain functions

## Assessment

The attack is social engineering timed to Mountain Protocol's wind-down.

Mountain Protocol's Phase 3 (August 22, 2026) moves all USDM redemptions to a Uniswap pool. Users who have never used Uniswap will be searching for USDM there for the first time. A fake token named `MountainProtocolUSDM` appearing in Uniswap search results during that period is not coincidence it is the attack surface.

The contract code is clean. The weapon is the name and the timing.

## Deployer Behaviour

The deployer wallet had zero prior history. Created, funded, used to deploy this contract and list it on Uniswap, then returned the remaining ETH to the phishing funder all within 4 hours. A throwaway wallet purpose-built for this operation.

The deployment date of June 24 — 12 days into Phase 2 and 59 days before Phase 3 gives the fake token time to be indexed by DEX aggregators, token lists, and search results before the bulk of users arrive on Uniswap in August.



