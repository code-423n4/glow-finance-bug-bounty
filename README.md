# Glow V1 Bug Bounty

**Core Smart Contract Code::**

| Risk Score |  Payout |
|------------|---------|
| Critical | Up to $60,000 in USDC |
| High| Up to $20,000 in USDC |

**Web Interface / Frontend:**
| Risk Score |  Payout |
|------------|---------|
| Critical | Up to $10,000 in USDC |
| High| Up to $2,000 in USDC |

Rewards will be further capped at 10% of direct funds at risk at the time of reporting the bug. Funds at risk defined as funds at risk of being stolen to an EOA not controlled by the protocol or permanently locked and unrecoverable due to smart contract failure caused by griefing. Calculated based on a snapshot at report timestamp.

*Note: Actual reward amounts are determined at Blueprint Finance’s sole discretion. Factors influencing payout include report quality, completeness, and severity/exploitability.*

**Other Terms**

By submitting a report, you grant Blueprint Finance the rights necessary to investigate, mitigate, and disclose the vulnerability. Reward decisions and eligibility are at the sole discretion of Blueprint Finance. The terms, conditions, and scope of this Program may be revised at any time. Participants are responsible for reviewing the latest version before submitting a report.

## Background on Glow

### What Is Glow?

Glow is a Solana protocol designed to enable users to leverage positions of various Solana ecosystem programs by using margin.
It consists of a few core programs:

* Glow Margin [`GLoWMgcn3VbyFKiC2FGMgfKxYSyTJS7uKFwKY2CSkq9X`]: The core margin program that allows users to create margin accounts and trade/interact with other programs using leverage.
* Glow Margin Pools [`CWPeEXnSpELj7tSz9W4oQAGGRbavBtdnhY2bWMyPoo1`]: Borrowing and lending pool program, which when integrated with Glow Margin, allows users to deposit and borrow on leverage.
* Glow Airspace [`AmAJeyNxxjNHfhBoCpsNMgWxhukdv3DSu3XpLfJspace`]: A program that allows configuring programs in an isolated namespace, enabling the Glow programs to be used in public or permissioned contexts. E.g. if there is a need to create permissioned pools and restrict users who interact with those pools.
* Glow Metadata [`yT2ut38wC6A6zsGo2aUgy9kkh8EBuNXYvtmo7aUg1oW`]: A program anabling storing arbitrary account structs used for Glow configuration.

### How Does It Work?

#### Margin Pools

Margin pools allow users to deposit (depositors) funds to earn interest yield. Depositors lend to borrowers, who can either deposit collateral and borrow against it (over-collateralised loans), or interact with the margin program below and borrow with leverage (under-collateralised loans).

This follows the typical lending pool design, where borrowers are charged a rate based on pool utlisation, and depositors earn a rate based on the borrowers rate minus protocol fees.

The program is written from the ground up, and is not a fork of the Solana Public Library's Lending program.

#### Margin

The margin program allows users to create margin accounts. Margin accounts allow users to have up to 32 positions in an account, where each position can be:

* A deposit or loan in a margin pool
* A token account balance
* Some other position from an external program

**Adapters**

The margin system works on "adapters", where an adapter is a sufficiently permitted program that the margin program can invoke via Cross-Program Invocation.

An adapter program is registered in the margin program's config, and then margin accounts are allowed to invoke that adapter program.

A good example is Jupiter Swap, where the margin program has registered it as an adapter, allowing swapping on margin. Such a swap typically requires withdrawing/borrowing tokens from Margin Pool A, swapping them and depositing/repaying Margin Pool B.

#### Airspace

The airspace program can be thought of as a configuration and permissioning program. Users get "tickets" to interact with an airspace, allowing them to create margin accounts and interact with Glow resources within an airspace.

There are public airspaces, with the default mainnet being airspace being called "default". The protocol authority/administrator can create private airspaces, which would require an airspace issuer to be enrolled. This issuer would be responsible for assigning and revoking users' tickets in that airspace.

#### Metadata

This program mainly stores token metadata accounts, as well as margin config details. From a security perspective, the main risks with this program would be focused on serialisation and authorisation exploits.

### Further Technical Resources & Links

- **Glow Docs**: Our system documentation, subject to change: https://docs.glowfinance.xyz
- **Glow Whitepaper**: N/A
- **Glow Website**: https://glowfinance.xyz/
- **Twitter**: https://x.com/GlowFinanceXYZ
- **Discord** https://discord.gg/glowfinance

# Scope & Severity Criteria

## Smart Contracts in Scope

**In-Scope Targets:**

- **Core Contracts:**
    - https://github.com/Blueprint-Finance/glow-v1
        - [Airspace](https://github.com/Blueprint-Finance/glow-v1-public/tree/main/programs/airspace)
        - [Metadata](https://github.com/Blueprint-Finance/glow-v1-public/tree/main/programs/metadata)
        - [Margin](https://github.com/Blueprint-Finance/glow-v1-public/tree/main/programs/margin)
        - [Margin Pool](https://github.com/Blueprint-Finance/glow-v1-public/tree/main/programs/margin-pool)
- **Web Interface / Application:**
    - https://app.glowfinance.xyz/

If you discover a vulnerability in any component not explicitly listed but which poses a risk to user funds, user data, or system integrity, you may submit it for consideration. Our team will review such submissions on a case-by-case basis.

## Out-of-Scope Targets:

- Certain types of instructions that:
    - Require administrator access to call (e.g. configuring smart contracts if the exploits would be from intentional malice), and;
    - Would result in loss of user funds, such as transferring a user’s position from one margin account to another.
- Glow Test Service program (`test7JXXboKpc8hGTadvoXcFWN4xgnHLGANU92JKrwA`) - it does not get deployed to mainnet
- [Lookup Table Registry](https://github.com/Blueprint-Finance/lookup-table-registry) program (`LooKUpVskBihZovMhwhEqCER8jwLFHhF4QMZA5axZnJ`)
- Glow Liquid Restaking Program (`LRtc6q4AhSr3k9dSLXpTRoAP1hBrgbQSiFkuQpuHaq3`)
- Environments:
    - Devnet is excluded, code deployed on devnet often includes test instructions that are unpermissioned and do not get deployed to mainnet. Devnet code can also include incomplete features being developed.
- Code quality issues that do not result in an exploit, non-exhaustive examples below:
    - Unused code or logic if it does not result in an exploit. There were features that were stripped out over time.
    - Inefficient compute unit/gas utilisation.
- Features  that are flagged as for testing or devnet only (see Rust feature flags)
- Glow liquidator related issues if they do not result in a liquidator stealing user funds

## **Severity and Rewards**

### **High likelihood**

A finding with high likelihood is defined as a vulnerability purely exploitable by code without social engineering or privileged access, where

1. the attacker has control over creating the requisite circumstances; *and*
2. requisite circumstances not under control of the attacker can be reasonably expected to occur and can be predicted or anticipated by the attacker using publicly available information.

Exploit complexity, sophistication, and expertise are not considered factors in determining likelihood.

### **Critical severity**

A **Critical severity finding** is a high impact issue which has a high likelihood of being exploited, where the impact could result in:

- Manipulation of governance voting result deviating from voted outcome and resulting in a direct change from intended effect of original results
- Direct theft of any user funds, whether at-rest or in-motion, other than unclaimed yield
- Direct theft of any user NFTs, whether at-rest or in-motion, other than unclaimed royalties
- Permanent freezing of funds
- Permanent freezing of NFTs
- Unauthorized minting of NFTs
- Predictable or manipulable RNG that results in abuse of the principal or NFT
- Unintended alteration of what the NFT represents (e.g. token URI, payload, artistic content)
- Protocol insolvency

### **High severity**

A **High severity finding** is a high impact issue with any likelihood which results in:

- Theft of unclaimed yield
- Theft of unclaimed royalties
- Permanent freezing of unclaimed yield
- Permanent freezing of unclaimed royalties
- Temporary freezing of funds
- Temporary freezing NFTs

### Known Issues

Bug reports covering previously-discovered bugs are not eligible for a reward within this program. This includes known issues that the project is aware of but has consciously decided not to “fix”, necessary code changes, or any implemented operational mitigating procedures that can lessen potential risk. Every issue opened in the repo, closed PRs, previous contests and audits are out of scope.

### Previous Audits

Any **previously reported** vulnerabilities mentioned in past audit reports are not eligible for a reward.

Glow previous audits can be found below: https://docs.glowfinance.xyz/audits/.

### Specific Types of Issues

**An example of that would be the following:**

- Informational findings.
- Design choices related to protocol. For example, the ability to deploy permissionless pools.
- Issues that are ultimately user errors and can easily be caught in the frontend. For example, transfers to address(0).
- Rounding errors.
- Relatively high gas consumption.
- Transactions that can only be executed by privileged authorities (e.g. transferring of deposits).

# Additional Context

### Trusted Roles

* Airspace governor: the protocol has a hardcoded authority that is an airspace governor. This is a multisig and all configuration changes go through it.

### **Prohibited Actions**

- **No Unauthorized Testing on Production Environments:**
    
    Do not test vulnerabilities on mainnet or public testnet deployments without prior authorization. Use local test environments or private test setups.
    
- **No Public Disclosure Without Consent:**
    
    Do not publicly disclose details of any vulnerability before it has been addressed and you have received written permission to disclose.
    
- **No Exploitation or Data Exfiltration:**
    
    Do not exploit the vulnerability beyond the minimum steps necessary to demonstrate the issue. Do not access private data, engage in social engineering, or disrupt service.

### **Disclosure Requirements**

The vulnerability must not be disclosed publicly or to any other person, entity or email address before Blueprint Finance has been notified, has fixed the issue, and has granted permission for public disclosure. In addition, disclosure must be made within 24 hours following discovery of the vulnerability.

 Include:

- A clear description of the vulnerability and its impact.
- Proof of concept.
- Conditions under which the issue occurs.
- Potential implications if exploited.

### **Eligibility**

To be eligible for a reward, you must:

- Be the first to report a previously unknown, non-public vulnerability that is not previously known by the Blueprint Finance team and is within the scope of this program.
- Provide sufficient information to reproduce and fix the issue.
- Not have exploited the vulnerability in a malicious manner.
- Not have disclosed the vulnerability to third parties prior to receiving permission.
- Comply with all Program rules and applicable laws.
- Provide all KYC and other documents as requested
- Not be one of our current or former employees, or a vendor or contractor who has been involved in the development of the code of the bug in question.
- You must also be of legal age in your jurisdiction at the time of submitting the request and not reside in a country under sanctions or restrictions, as required by applicable laws.

### Miscellaneous
Individuals currently or formerly employed by Blueprint Finance and their family members, or who contributed to the development of the affected code, are ineligible for bounties.
