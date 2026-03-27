# Centrifuge Project Audit on Code4rena

One month ago, I embarked on an audit of the **Centrifuge codebase** to delve into the intricacies of its protocol. This exploration was further enriched by my thorough review of backstage reports from Code4rena, which provided a nuanced understanding of various aspects of the code and its functionality.

Additionally, the insights gleaned from reading the public report were invaluable in forming a well-rounded perspective. As I delved deeper, several thoughts and security considerations surfaced regarding the protocol. The exercise revealed a few areas of concern which, from my standpoint, require attention to bolster the protocol's robustness and ensure its smooth operation.

The nuanced understanding of different sources allowed me to identify potential issues and security risks, each from a unique angle. The juxtaposition of the Centrifuge code logic against the observations from Code4rena reports highlighted the importance of continuous scrutiny and the need for a robust security framework.

---

## My Security Considerations About the Protocol

### Asset Management

- **Asset Price Assumption in `InvestmentManager`** — The contract assumes asset prices will always be positive, potentially leading to inaccurate value representation in the Liquidity Pool when dealing with real-world assets that might have negative values.

- **Price Convertors Check** — Check the outcome from price convertors to ensure values will not be zero.

- **Currency Decimals Discrepancy** — Currency has different decimals on different chains.

### Access Control & Ownership

- **Ownership Transfer Mechanism** — The `Root.sol` contract lacks a mechanism for transferring ownership.

- **Unrestricted Access to `executeScheduledRely()`** — Anyone can call `executeScheduledRely()` and execute the Rely.

- **Prevent Admin from Denying Themselves** — There is no guard preventing an admin from removing their own access.

- **Arbitrary Minting in Tranche Contract** — The `Tranche` contract allows any investor with a valid ERC1404 membership to mint an arbitrary amount of tokens using `TrancheToken.mint()`.

### Cross-Chain & Signatures

- **Risk of Reuse of Signatures in Case of Forks** — No chain ID is specified, which creates a risk of signature replay on forks.

- **Reorg Attack Prevention** — Always use `CREATE2` with a salt (including `msg.sender`) when creating internal contracts to defend against reorg attacks.

- **Gateway Contract Vulnerability** — The `Gateway` contract has a vulnerability where "stuck" cross-chain transactions can be replayed at a later time, potentially causing harm to the system.

- **Implement Token Recovery Mechanism** — Allow recovery of burned tokens on the source chain if the destination chain message isn't processed within a specified time frame (e.g., 24 hours).

### Token & Approval Handling

- **Payable Functions in `Router.sol`** — Axelar's gateway lacks payable functions, preventing users from passing value during contract interactions. Check the `payable` modifier in functions that have `call`.

- **Modify `transferIn` Function** — Recommended to modify it to only allow `msg.sender` as the `source` address.

- **Permit Modification** — Use `safePermit` instead of `permit` to handle weird ERC-20 tokens.

- **Max Allowance Setting** — Setting allowance to max is really dangerous.

- **Allowance Reset** — Approve allowance to `0` first before setting a new amount.

- **Token Parameter in `approve` Function** — The first parameter is `TOKEN` — verify order.

- **Token Decrease Check** — Check how many tokens users can decrease according to their balance.

- **`permit` Function Check** — Some tokens like BNB do not have a `permit` function.

- **Support ERC-20 Tokens with Blocklists** — Should be restricted.

### Liquidity & Tranche Logic

- **Tranche Token Issue** — Problem with 1 tranche token per many stablecoin pools: deposit USDC in 1 pool → get tranche token → redeem in USDT pool → not enough USDT tokens.

- **Liquidity Pool Removal Check** — Add a check in `removeLiquidityPool` to ensure there are no pending redemptions before removing a liquidity pool.

- **Slippage Protection** — Add slippage protection when doing swaps.

- **Order Expiration** — Orders should have expiration timestamps.

- **Non-zero Delay Period** — Delay period cannot be `0`.

- **Tranche Token Decimal Creation** — Creating a tranche token with 18+ decimals can cause problems in the system.

- **Different Epoch Withdrawal Problems** — Different prices across epochs can cause withdrawal discrepancies.

### Code Quality & Standards

- **Variable Shadowing** — Variable shadowing observed — should be resolved.

- **Logic Combination** — Check that `addTranche` + `deployTranche` logic can be combined correctly.

- **Sensitive Data Exposure** — Exclude sensitive data from event parameters to enhance user privacy.

- **Rounding Standards** — Always check rounding up/down and match with the ERC-4626 standard.

- **Enum Usage in File Pattern** — Use enums in the `File` pattern instead of string computation.

- **Token Retrieval Mechanism** — If a user mistakenly sends tokens to escrow, there should be a mechanism to withdraw them.

- **State Dependency Check** — Before removing some states, check dependencies between this state and others.

- **Low-level Call Validation** — When doing low-level arbitrary calls, validate the encoded selector.

- **Protocol Instance Removal** — If instances are added to the protocol, there should be an ability to remove them.

- **Modifier Consistency** — `virtual` and `override` modifiers should be consistent.

- **Missing `Success_code` Function** — There is no `Success_code` function in the `erc1404` interface.

- **Minimum Deposit Setting** — Set a minimum deposit, as smaller transactions can cost much more in fees.

- **Follow Axelar Docs** — Ensure implementation aligns with Axelar's official documentation.

### Natspec / Logic Bug

> **⚠️ Redemption Limits Logic Bug** — The Natspec comments indicate that when a redemption order is fulfilled during epoch execution, the redemption limits (`maxRedeem` and `maxWithdraw`) should be **increased**. However, the current code logic is **reducing** the redemption limits instead of increasing them.

- **Removing an investor from the member list in the Restriction Manager should lock their tokens.**