# Smart Contract Security Audit Checklist

When conducting a security audit for Solidity smart contracts, it's essential to cover a wide range of aspects to ensure the code's safety and integrity. Below is a comprehensive checklist of questions and considerations to help guide your security audit process — covering access control, asset flow, control flow, data flow, assumptions, dependencies, and more.

---

## Community Resources

### @0xBeirao Checklist
This guy created another great **ALL-IN-ONE checklist** covering: Code Questions, Access Control, Vaults, ERC20, ERC721, Proxies, Signatures, Locktime for staking, Account Abstraction, AMMs, Lending, MultiChains, Merkle Trees, LayerZero, Chainlink, and Uniswap. [Check this out!](https://github.com/beirao/checklist)

### @Composable_Sec Verification Standard
This company created a **Smart Contract Verification System Standard** with 24 topics about smart contract verification requirements — a valuable resource for anyone looking to secure their smart contracts. [Find it here.](https://composable-security.com/smart-contract-security-verification-standard/)

---

## Common Questions

- [ ] Does the code compile successfully?
- [ ] What Solidity version is being used? Are there potential overflow vulnerabilities?
- [ ] Are there any missing docstrings to explain the purpose of functions and variables?
- [ ] Is there an `Ownable` contract in use? What does it look like?
- [ ] Are state variables properly scoped with visibility modifiers?
- [ ] Are events used for proper logging?
- [ ] Are user-friendly error messages provided?
- [ ] Is the return value from low-level calls checked?
- [ ] Are there any scenarios where the owner can authorize itself, potentially leading to rug-pulling?
- [ ] Who has control over privileged accounts, and what are the mechanisms for control?
- [ ] Is there a single private key controlling the contract, or is a multisig setup used?
- [ ] What governance mechanisms are in place, and is governance fully open or limited?
- [ ] Are there other contracts within the system, and what roles do they play?
- [ ] Is there a timelock mechanism, and can it be bypassed?
- [ ] How are keys stored, and are there backup mechanisms?
- [ ] Who has access to these keys, and are their actions logged and monitored?
- [ ] How and where are keys generated — is it a standard signing process or a custom implementation?
- [ ] Is there adequate documentation?
- [ ] What types of tokens are involved, and are there potential reentrancy issues?
- [ ] What types of tokens are involved, and could transfers fail?
- [ ] What if no ETH is deposited into the contract?
- [ ] Can the recipient of ETH be trusted? Are there potential DoS or reentrancy vulnerabilities?

---

## Code-Specific Questions

> For a detailed code-level checklist, see [this checklist](#) and the [multichain protocol auditing checklist](#).

---

## Access Control Questions

- [ ] Are the powers associated with roles documented?
- [ ] What are the risks if ownership is compromised, and how could it affect different components of the system?
- [ ] What is the purpose and trust assumptions behind the `onlyOwner` pattern?
- [ ] Can the owner manipulate tokens and ETH within the contract?

---

## Oracle Questions

- [ ] What is the level of decentralization in governance, and are there relevant off-chain processes?
- [ ] What happens if the oracle returns a price of zero or an absurd value?
- [ ] How is the oracle's address set, and what is the process behind it?
- [ ] What is the unit of measurement for the price, and what if it is inverted?
- [ ] What type of oracle is used, and is it allowed to read? Are there any issues with units or a price of zero?
- [ ] How many decimal places does the price have?
- [ ] How is the price calculated within the oracle?
- [ ] Can the price be read on-chain without authentication?
- [ ] How is the price updated, and at what frequency? Are there potential delays?
- [ ] What if the oracle cannot update the price?
- [ ] Can the oracle's logic be upgraded, and if so — who has the authority, how, and when?
- [ ] Are there privileged roles within the oracle, and what powers do they hold?
- [ ] Is it possible to manipulate or shut down the oracle? If so, by whom and under what circumstances?
- [ ] Are there fallback oracles in place to provide a safety net?

---

## Governance Questions

- [ ] Does the governance system include vote delegation, minimum quorum requirements, or specialized committees?
- [ ] Is there continuous voting or augmented voting power via token lock?
- [ ] How does off-chain voting for signaling or polling work?
- [ ] Can on-chain actions be initiated through off-chain voting using oracles?
- [ ] Are there time delays associated with sensitive actions?
- [ ] Are emergency actions (e.g., pausing or shutting down) possible via Multisig or other mechanisms?
- [ ] Are legal entities, such as a foundation, providing support for the DAO?
- [ ] Are there tools in place for DAO treasury management and token issuance to cover protocol expenses?
- [ ] Is there incentivized voting or off-chain engagement, such as forum participation?
- [ ] Is there a risk of flash-loans with governance tokens?

---

## Contract Upgradability Questions

- [ ] What pattern of contract upgradability is being used?
- [ ] Does the new implementation respect storage layouts?
- [ ] Is the new implementation correctly initialized?
- [ ] Does the new implementation require specific upgrade logic?
- [ ] Is there a risk of function clashing between the implementation and the proxy?
- [ ] Are there safety checks in place to prevent bricking the upgrade process?
- [ ] What off-chain validations are used throughout the upgrade process?

### Upgradeable Contract Checklist

- [ ] **No constructors** — only `initialize` methods (which has its own checklist)
- [ ] Should have an `initializer` modifier; if it is a base class, use `onlyInitializing`
- [ ] Should call the `__ContractName_init()` methods of inherited upgradeable contracts
- [ ] Shouldn't be reentrant
- [ ] Only inherit from contracts that are also upgrade-safe (e.g., OpenZeppelin's upgradeable contracts)
- [ ] **No initial values in storage field declarations** — this is equivalent to setting it in the constructor (constants are fine)
- [ ] The implementation contract should have a constructor with only `_disableInitializers()` in it
- [ ] Ensure implementation contracts do **not** contain `selfdestruct`; also pay extra attention to `delegatecall` that could end up in `selfdestruct`
- [ ] The order and type of storage variables **cannot be changed** between upgrades
- [ ] If an upgradeable contract is to be inherited, add a **storage gap array** as best practice
- [ ] Consider using **EIP-1967** type storage slots to avoid storage slot clashes

> See also: [Contract Upgradability Checklist from Composable Security](https://composable-security.com)

---

## Economics, Math & DeFi

- [One super useful checklist about Math, DeFi and tokenomics](#) — helps audit DeFi projects
- [3 useful checklists about Collateralized Debt Positions, Liquid Staking Derivatives (LSD) and AMMs](#)
- [DeFi Protocols Rewards checklist](#)

---

## Questions Beyond the Code

- [ ] Is there comprehensive documentation available for the smart contract and its functionality?
- [ ] Has the code been adequately tested, and are there test suites in place?
- [ ] How have other projects implemented similar features, and have best practices been considered?
- [ ] What is the launch plan for the smart contract, and how will it be operated in a production environment?
- [ ] Is there a plan for peer review and third-party security audits?
- [ ] Are monitoring systems and processes in place to detect and respond to potential issues in real time?

---

## Conclusion

These checklists are designed to help ensure that a thorough security audit is conducted for Solidity smart contracts. They cover a wide range of critical aspects to identify and mitigate potential vulnerabilities and risks in the code and its associated systems.

---

A big shoutout to [@0xRajeev](https://twitter.com/0xRajeev), the [@TheSecureum](https://twitter.com/TheSecureum) team, [@pashovkrum](https://twitter.com/pashovkrum), [@OpenZeppelin](https://twitter.com/OpenZeppelin), [@drdr_zz](https://twitter.com/drdr_zz), [@Composable_Sec](https://twitter.com/Composable_Sec), [@tamjid0x01](https://twitter.com/tamjid0x01), [@0xJuancito](https://twitter.com/0xJuancito), [@bytes032](https://twitter.com/bytes032), and [@0xBeirao](https://twitter.com/0xBeirao).

Your knowledge and contributions will undoubtedly help foster a community of more robust and secure smart contract research. **Thanks a lot!**