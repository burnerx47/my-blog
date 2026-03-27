# Leveraging ChatGPT for Auditing Solidity Smart Contracts

In the realm of blockchain development, auditing smart contracts is a crucial step to ensure the security and efficiency of decentralized applications. Solidity, as a prominent smart contract language for the Ethereum blockchain, demands meticulous auditing to mitigate any potential vulnerabilities or bugs.

The introduction of **ChatGPT** as an assistive tool in this endeavor has been a game changer. This post delves into how ChatGPT can significantly streamline the auditing process of Solidity smart contracts.

---

## 1. Exhaustive Vulnerability Assessment Prompt

A primary step in auditing is to identify all existing issues and vulnerabilities within a smart contract. A useful prompt for ChatGPT in this context:

```
Provide an exhaustive list of all issues and vulnerabilities inside the following smart contract.
Be detailed in the issue descriptions and describe the actors involved.
Include one exploit scenario in each vulnerability.

Output as a valid markdown table with the following columns:
- description
- action
- severity
- actors
- scenario
- type
- line

'type' can be: 'usability', 'vulnerability', 'optimization', or 'suggestion'
'actors' is a list of the involved actors
'severity' can be: 'low 🧊', 'medium', or 'high 🔥'
'line' is the line number of the issue

Ensure that all fields of the table are filled out.
```

---

## 2. Reporting Template

When participating in auditing contests like **Code4rena**, it's essential to have a structured report. Here's a useful template for reporting findings:

```markdown
# Title

## Impact
<Detailed description of the impact of this finding.>

## Proof of Concept
<Provide direct links to all referenced code in GitHub.
Add screenshots, logs, or any other relevant proof that illustrates the concept.>

## Tools Used
Manual review

## Recommended Mitigation Steps
<steps…>
```

> **Tip:** Save this template in your ChatGPT conversation at the start of each audit session so it remembers the format when generating findings.

---

## 3. Smart Contract Reconnaissance with ChatGPT

A thorough understanding of the smart contract's architecture and functionalities is pivotal before diving into the auditing process. You can ask ChatGPT to remember the following strategies:

### Basic Strategy

Ask ChatGPT to analyze the contract through these lenses:

- Who are the **actors** of the system?
- What is the **value** of the system?
- What **actions** does the system have?
- What **constraints** are in the system?
- What are potential **ways to break** the system?
- What are potential **data ranges** for the contract state?
- What **allowances** does the system have?

### Architecture Strategy

Explore the deeper design of the protocol:

- Economic incentives
- Roles
- Design decisions
- Expected use cases
- Failure modes
- Integrations
- Adversarial scenarios

### Constraints and Flow Strategy

- Describe state changes in every function based on constraints
- Provide information on Solidity patterns and DeFi patterns used
- Create flows showing the order of function execution, crucial points, and weakest parts

### Axioms Strategy

- Write **positive and negative axioms** based on the system information

### QA and Optimization Strategy

- List optimizations and code changes to improve the quality of code *(with code snippets)*

> **💡 Tip:** Visual representation of data often provides a clearer understanding of the system's workings. When working with ChatGPT, request visualizations of output — for instance, state modifications in **ASCII symbol diagrams**. Although not all visualizations may be meaningful, some can provide invaluable insights into the smart contract's operations.

---

## 4. Finding Vulnerabilities

In essence, while **ChatGPT may not replace a human auditor**, it significantly augments the auditing process, providing a clearer understanding of:

- Protocol state transitions
- Constraints and invariants
- Interoperability between contracts

The tool is especially powerful for grasping **protocol state transitions and constraints**. Although writing Proof of Concepts (PoCs) is not its forte, it's highly useful for **elucidating documentation**.

### Pro Tip: Feed Context First

Before auditing, feeding ChatGPT with relevant protocol documentation can enhance its contextual understanding, making the auditing process more insightful and less prone to oversight.

It's as simple as saying:

> *"This is the documentation to provide better context for `<protocol_name>` which I am auditing"* — then paste the document.

---

## Conclusion

ChatGPT emerges as a potent ally for auditors, providing a structured and insightful approach to auditing Solidity smart contracts. Its ability to:

- Streamline the **reconnaissance phase**
- Elucidate **complex documentation**
- Assist in drafting **structured reports**

...makes it an indispensable tool in an auditor's toolkit.

The blockchain space continues to evolve, and with tools like ChatGPT, the stride toward more secure and efficient smart contract deployments becomes a tangible reality.

> Remember: **a well-audited smart contract is the bedrock of a secure, reliable decentralized application.**