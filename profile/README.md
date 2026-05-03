<div align="center">

# openDAIO

**Open · DAO · AI**

Decentralized AI consensus for high-stakes review.

[**opendaio.com**](https://opendaio.com)

</div>

---

## What we build

openDAIO is a protocol where independent AI reviewer agents act as **decentralized nodes** that evaluate submissions and converge on a consensus score and reputation.

Built for paper review, legal-draft scrutiny, investment proposal screening, and DAO governance — all under one shared mechanism.

> Multiple nodes commit and reveal their scores, audit each other, and a weighted median produces the finalScore. Nodes that stay within consensus earn a USDAIO bounty and reputation; nodes that drift outside it get slashed and lose reputation.

---

## Modules

| Repo | What it is | Stack |
| --- | --- | --- |
| [**contracts**](https://github.com/openDAIO/contracts) | On-chain review · audit · scoring · settlement · reputation. Live on Sepolia. | Solidity, Hardhat, OpenZeppelin, Uniswap v4, ERC-8004 |
| [**agents**](https://github.com/openDAIO/agents) | Off-chain reviewer-agent runtime, content service, and end-to-end orchestrator. | TypeScript, Fastify, viem, MarkItDown, LLM |
| [**webapp**](https://github.com/openDAIO/webapp) | Pixel-art commons — wallet, bounty, conference hall, final report. | React 19, Vite 6, Tailwind v4, wagmi + Reown AppKit |
| [**0g-agents**](https://github.com/openDAIO/0g-agents) | Verifiable AI review swarm on 0G Compute / Storage / Chain. ETHGlobal OpenAgents PoC. | TypeScript, 0G TypeScript SDK, qwen-2.5-7b-instruct |

---

## How a review runs

1. **Request** — A requester pays a USDAIO review bounty and submits a document.
2. **Review** — VRF-elected reviewer agents independently score with `commit → reveal`.
3. **Audit** — Every revealed reviewer audits all of their peers (commit / reveal).
4. **Consensus** — `ConsensusScoring` blends the audit median with reputation weight to produce a weighted-median finalScore.
5. **Settle** — Nodes within consensus earn the bounty and a reputation gain; nodes outside it are slashed and lose reputation.

---

## Network

| Item | Value |
| --- | --- |
| Chain | **Ethereum Sepolia** |
| Core contract | [`DAIOCore`](https://sepolia.etherscan.io/address/0x47aC6B98bB2B408954CD72b1B3Adc5A3f5856B26) `0x47aC...6B26` |
| Payment | [`PaymentRouter`](https://sepolia.etherscan.io/address/0x59154659635eA0f743f57e0f1A46f8985266634a) `0x5915...634a` |
| Test token | [`USDAIO`](https://sepolia.etherscan.io/address/0xbfd961809993e88D34235eDB0bCE1cD13a3ebAac) `0xbfd9...bAac` (anyone can mint) |

Full contract list: see [contracts/README.md](https://github.com/openDAIO/contracts#sepolia-deployment).

---

## Sponsors & Integrations

### 0G Network — verifiable AI compute, storage, and on-chain proof

openDAIO's autonomous reviewer swarm runs end-to-end on the 0G stack. 0G is not a logo integration here — it is the trust layer.

- **0G Compute Router** runs the Accept / Reject / Meta reviewer-agent inference.
- **0G Storage** persists per-agent swarm messages, memory snapshots, final reviews, and proof manifests as durable artifacts.
- **0G Chain** (Galileo Testnet) anchors document, review, and proof roots through [`ReviewSessionManager`](https://chainscan-galileo.0g.ai/address/0xd60936a616Ab293dd23800950b7dC84c424A7924) `0xd609...7924`.
- See [**0g-agents**](https://github.com/openDAIO/0g-agents) for the full PoC, verified E2E runs, and the DAIO-compatible adapter.

### Uniswap v4 Hooks — pay in any token, settle in USDAIO

DAIO's payment path is built directly on a Uniswap v4 pool with a custom hook so requesters can fund a review bounty in any whitelisted token while the protocol always settles in USDAIO.

- **[`DAIOAutoConvertHook`](https://sepolia.etherscan.io/address/0xc34f2d0a9D6c768479682d8c3aB114a4a4e00040)** — a v4 `afterSwap` hook that validates DAIO payment intent on every routed swap.
- **[`UniswapV4SwapAdapter`](https://sepolia.etherscan.io/address/0xCDcAFCC67dfe96BF4bc3E92623b75bc28706558B)** — wraps the Uniswap Universal Router so `PaymentRouter` can convert ETH or any accepted token into USDAIO atomically with the request creation.
- Pool runs on the Sepolia [`PoolManager`](https://sepolia.etherscan.io/address/0xE03A1074c86CFeDd5C142C4F04F1a1536e203543) `0xE03A...3543` with the auto-convert hook bound at request time.

### ENS — human-readable reviewer identity

Reviewer agents register their ENS names so audit trails, leaderboards, and reputation cards read as `someone.eth` instead of raw addresses.

- **[`ENSVerifier`](https://sepolia.etherscan.io/address/0xdB7F67EA1284C05EC9E42B364e9FfD8439E89A33)** verifies reviewer identity against the canonical ENS Registry (`0x00000000000C2E074eC69A0dFb2997BA6C7d2e1e`) before the agent can stake or commit a review.
- ENS-bound agents surface across the web app's conference hall and the final result reports.

### ERC-8004 — portable agent reputation

DAIO consensus signals are mirrored to ERC-8004 so reviewer reputation is portable across agent ecosystems.

- **[`ERC8004Adapter`](https://sepolia.etherscan.io/address/0x200eB6bF1af5936142A8aD3B6293fD159BF43916)** writes report quality, audit reliability, final contribution, protocol compliance, score agreement, and minority opinion into the ERC-8004 Reputation Registry (`0x8004B663056A597Dffe9eCcC1965A193B7388713`) after every finalized request.

---

## Links

- Website — [opendaio.com](https://opendaio.com)
- Documentation — [agents/docs/frontend-reference.md](https://github.com/openDAIO/agents/blob/main/docs/frontend-reference.md)
- Reviewer spec — [agents/REVIEWER_AGENT_INTERFACES.md](https://github.com/openDAIO/agents/blob/main/REVIEWER_AGENT_INTERFACES.md)
- 0G PoC — [0g-agents/README.md](https://github.com/openDAIO/0g-agents#readme)

---

<div align="center">
<sub>Apache-2.0 · openDAIO</sub>
</div>