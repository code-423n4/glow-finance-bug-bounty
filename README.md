# Welcome to your bounty repo

This file contains information around how to set-up your README.md and prepare for our collaboration.

**Bug Bounties use two repos**:

- a bug bounty repo (this one), which is used for scoping your bug bounty and for providing information to wardens
- a submissions repo, where issues are submitted

Ultimately, when we launch the bug bounty, this repo will be made public and will contain links to the in-scope files to be reviewed and all the information needed for bounty participants.

**Action item for sponsors:**

- [ ] Modify the contents of this README.md file. Describe how your code is supposed to work with links to any relevent documentation and any other criteria/details that the C4 Wardens should keep in mind when reviewing.

# Concrete Bug Bounty

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

Rewards will be further capped at 10% of direct funds at risk at the time of reporting the bug. Funds at risk defined as funds at risk of being stolen to an EOA not controlled by the protocol or permanently locked and unrecoverable due to smart contract failure caused by griefing. Calculated based on a snapshot at report timestamp;.

*Note: Actual reward amounts are determined at Blueprint Finance’s sole discretion. Factors influencing payout include report quality, completeness, and severity/exploitability.*

**Other Terms**

By submitting a report, you grant Blueprint Finance the rights necessary to investigate, mitigate, and disclose the vulnerability. Reward decisions and eligibility are at the sole discretion of Blueprint Finance. The terms, conditions, and scope of this Program may be revised at any time. Participants are responsible for reviewing the latest version before submitting a report.

## Background on Concrete

### What Is Concrete?

[⚡️ **Project**: Add a short overview of the project here.]

### How Does It Work?

[⚡️ **Project**: Add a high-level technical overview of the project here]

### Further Technical Resources & Links

[⚡️ **Project**: Please fill out the following information] 

- **Concrete Docs**: Our system documentation, subject to change: https://docs.concrete.xyz/Overview/welcome
- **Concrete Whitepaper**: [Link]()
- **Concrete Website**: https://concrete.xyz/
- **Twitter**: https://x.com/ConcreteXYZ
- **Discord** https://discord.com/invite/concretexyz

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

Bug reports covering previously-discovered bugs (listed below) are not eligible for a reward within this program. This includes known issues that the project is aware of but has consciously decided not to “fix”, necessary code changes, or any implemented operational mitigating procedures that can lessen potential risk. Every issue opened in the repo, closed PRs, previous contests and audits are out of scope.

[⚡️**Project:** Please provide any relevant links in a bullet format below:]

### Previous Audits

Any **previously reported** vulnerabilities mentioned in past audit reports are not eligible for a reward.

[⚡️ **Project Name**] previous audits can be found below: [Please insert a link to your previous audits.]

### Specific Types of Issues

**An example of that would be the following:**

- Informational findings.
- Design choices related to protocol. For example, the ability to deploy permissionless pools.
- Issues that are ultimately user errors and can easily be caught in the frontend. For example, transfers to address(0).
- Rounding errors.
- Relatively high gas consumption.

[⚡️**Project:** Please add any specific types of issues that should be considered out-of-scope.]

# Additional Context

### Trusted Roles

[⚡️ **Project**: Please explain your protocol's trusted roles.]

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
