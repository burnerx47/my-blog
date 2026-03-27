# My Personal Security Researcher Toolbox

In the world of smart contract auditing and blockchain security, having a well-organized and efficient toolkit is essential. The right tools can significantly speed up your auditing process and help uncover potential vulnerabilities that might otherwise go unnoticed.

Here's a rundown of my personal toolkit, organized by category, that I find invaluable in my work.

---

## Base Development Setup

Having a solid base setup is crucial as it ensures a smooth workflow during the auditing process.

- **macOS (Unix-like systems)** — Many auditor tools are UNIX-compatible, which makes Linux-like systems an easy choice for installation.
- **VS Code** — Stands out due to its extensive range of plugins compared to other IDEs.
- **Notion** — A fantastic task management tool that helps in organizing thoughts and tasks effectively.

---

## VS Code Extensions

Visual Studio Code extensions enhance the functionality of VS Code, providing additional tools and features for smart contract development and auditing.

| Extension | Description |
|---|---|
| **Solidity Language & Themes** | Syntax highlighter that detects state transitions and showcases potential vulnerabilities like unchecked returns. |
| **Solidity Metrics** | Created by @ConsensysAudits — shows contract dependencies, SLOC, and displays stats in charts. |
| **Solidity Visual Developer** | Generates UML and Graphviz charts for smart contracts to understand function flows and intercommunication. |
| **Test Explorer UI** | Visualizes smart contract test coverage directly in code. |
| **Tools for Solidity** | Enhances navigation with Go to Type Definition, Go to Implementation, and Find References. |
| **Ethereum Security Bundle** | Bundles Solidity language syntax, Yul, and inline bookmarks — super useful for the audit process. |
| **ETHover** | Hover over Ethereum addresses to download their bytecode and more. |
| **Foundry Test Explorer** | Visual UI for running Foundry tests in VS Code. |
| **Even Better TOML** | Since Foundry reads config from `.toml` files, this extension is essential. |
| **GitHub Copilot** | AI pair programmer powered by OpenAI. |
| **GitHub Linker** | Right-click on a file or code line to copy a direct GitHub link — very useful for writing audit reports. |
| **Solidity Debugger** | Run and debug Solidity transactions right in VS Code. |

---

## AI Tools

AI tools offer a layer of automation and intelligence that can be invaluable in code analysis and smart contract auditing.

- **[OpenAI Chat](https://chat.openai.com)** — General AI tool for various purposes including code analysis and documentation review.
- **[Etherscan Code Reader](https://etherscan.io)** — GPT-3 integrated in Etherscan to help analyze smart contracts.
- **[AuditWizard](https://auditwizard.io)** — Similar to Etherscan Code Reader for analyzing smart contract code.

---

## Code-Specific Tools

Code-specific tools aid in auditing and analyzing smart contracts in detail — from static analysis to formal verification.

- **[RareSkills CLI Tools](https://www.rareskills.io)** — A collection of CLI tools covering: Static Analysis, Mutation Testing, Fuzzing & Invariant Testing, Formal Verification & Symbolic Execution, and Visualization.
- **[4naly3er](https://github.com/Picodes/4naly3er)** — Gas usage analysis and optimization.
- **[sol2uml](https://github.com/naddison36/sol2uml)** — CLI tool to create UML diagrams from Solidity code.
- **[pyrometer](https://github.com/nascentxyz/pyrometer)** — Examines function inputs and the range of possible input values.
- **[solhint](https://protofire.github.io/solhint/)** — Solidity linter to enforce coding style and best practices.
- **[slitherin](https://github.com/pessimistic-io/slitherin)** — An enhanced version of Slither with more vulnerability detection methods.
- **Contract Diff Comparison Tool** — Useful for comparing contract versions.
- **[dethcode](https://github.com/dethcrypto/dethcode)** — Inspect deployed contracts in a browser-based VS Code.

---

## Transaction Debugging Tools

These tools are crucial for tracing and debugging transactions on the blockchain.

- **[Tenderly Dashboard](https://tenderly.co)** — Full transaction simulation and monitoring.
- **[Openchain Trace](https://openchain.xyz/trace)** — Transaction trace explorer.
- **[Phalcon Explorer](https://phalcon.blocksec.com)** — Advanced transaction explorer.
- **[EthTx Info](https://ethtx.info)** — Detailed transaction info and decoded calls.
- **[MetaSleuth](https://metasleuth.io)** — Inspect transaction flow, track fund movements, and avoid scams.

---

## Contract Decoder Tools

Decoding tools are essential for understanding contract data, especially when dealing with complex or minified code.

- **Online ABI Decoder**
- **Unverified ABI Code Getter**
- **Calldata Decoder**
- **[ByteGraph](https://bytegraph.xyz)** — View any contract as a graph of opcodes.
- **Online Bytecode Decompiler**
- **[Sourcify Playground](https://playground.sourcify.dev)** — Retrieve contract metadata.

---

## Contract Storage Readers

Understanding how data is stored and accessed is crucial in auditing smart contracts for potential vulnerabilities.

- **Contract Reader**
- **EVM Storage**

---

## Signature Databases

Signature databases are useful for identifying common patterns and signatures in smart contracts.

- **[4byte Directory](https://www.4byte.directory)** — Function signature database.
- **[Etherface](https://www.etherface.io)** — Another signature lookup tool.
- **[Openchain Signatures](https://openchain.xyz/signatures)** — Signature database.
- **[CyberChef](https://gchq.github.io/CyberChef/)** — Create a hash from any input.

---

## Miscellaneous Tools

Miscellaneous tools that provide various functionalities useful in different auditing scenarios.

- **[TokenSniffer](https://tokensniffer.com)** — Detect fraud tokens.
- **[EVM Codes](https://www.evm.codes)** — Solidity opcodes with usage examples.
- **[Revoke Cash](https://revoke.cash)** — Revoke your own token approvals.
- **[Full Precision Calculator](https://www.wolframalpha.com)** — Useful when auditing protocols with tokens and checking correct math operations.

---

## And This Is Not All...

There's also a great resource — **Swiss Knife** — with tools like epoch-converter, tx explorer, ETH/hex converters, and transaction caller.

**[Remix](https://remix.ethereum.org)** — An online Solidity IDE to develop and run Solidity code in a browser, and debug transactions even on the bytecode level. Comes with many useful code plugins.

**[Etherscan](https://etherscan.io)** houses converter tools, DEX/token tracker tools, and contract AI explorer tools — all found under the **More** item in the top menu.

For those hungry for more tools, check out this list of **90+ tools**.

---

## In Conclusion

...these tools are designed to **accelerate your smart contract research** and aid in uncovering more bugs, ensuring a robust and secure smart contract environment.

**Happy coding and auditing, folks! :-)**