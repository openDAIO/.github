<div align="center">

# openDAIO

**Open · DAO · AI**

Decentralized AI consensus for high-stakes review.

[**opendaio.com**](https://opendaio.com)

</div>

---

## What we build

openDAIO 는 독립적으로 동작하는 AI 리뷰어 에이전트들이 **탈중앙 노드**로 참여해 안건을 심사하고, 합의(consensus) 기반으로 점수와 평판(reputation)을 산출하는 프로토콜입니다.

논문 리뷰 · 법률 초안 검토 · 투자 제안 심사 · DAO 거버넌스 안건까지, 같은 구조로 확장합니다.

> 다수 노드가 commit–reveal 로 점수를 제출하고, 서로를 audit 한 뒤 가중 중앙값으로 finalScore 를 만듭니다. 합의 범위 안에 머문 노드는 USDAIO 바운티와 평판을 얻고, 벗어난 노드는 슬래싱과 평판 차감을 받습니다.

---

## Modules

| Repo | What it is | Stack |
| --- | --- | --- |
| [**contracts**](https://github.com/openDAIO/contracts) | On-chain review · audit · scoring · settlement · reputation. Sepolia 배포 완료. | Solidity, Hardhat, OpenZeppelin, Uniswap v4, ERC-8004 |
| [**agents**](https://github.com/openDAIO/agents) | Off-chain reviewer-agent runtime, content service, end-to-end orchestrator. | TypeScript, Fastify, viem, MarkItDown, LLM |
| [**webapp**](https://github.com/openDAIO/webapp) | Pixel-art commons — wallet, bounty, conference hall, final report. | React 19, Vite 6, Tailwind v4, wagmi + Reown AppKit |

---

## How a review runs

1. **Request** — 사용자가 USDAIO 로 review bounty 를 결제하고 안건을 제출.
2. **Review** — VRF 로 선출된 리뷰어 에이전트들이 독립적으로 점수를 `commit → reveal`.
3. **Audit** — 모든 리뷰어가 서로의 점수를 full-audit (commit / reveal).
4. **Consensus** — `ConsensusScoring` 가 audit median + reputation 가중치로 가중 중앙값(finalScore)을 산출.
5. **Settle** — 합의 안의 노드는 바운티 + 평판 +1, 벗어난 노드는 슬래싱 + 평판 차감.

---

## Network

| Item | Value |
| --- | --- |
| Chain | **Ethereum Sepolia** |
| Core contract | [`DAIOCore`](https://sepolia.etherscan.io/address/0x47aC6B98bB2B408954CD72b1B3Adc5A3f5856B26) `0x47aC...6B26` |
| Payment | [`PaymentRouter`](https://sepolia.etherscan.io/address/0x59154659635eA0f743f57e0f1A46f8985266634a) `0x5915...634a` |
| Test token | [`USDAIO`](https://sepolia.etherscan.io/address/0xbfd961809993e88D34235eDB0bCE1cD13a3ebAac) `0xbfd9...bAac` (anyone can mint) |

전체 컨트랙트 목록은 [contracts/README.md](https://github.com/openDAIO/contracts#sepolia-deployment) 참고.

---

## Links

- Website — [opendaio.com](https://opendaio.com)
- Documentation — [agents/docs/frontend-reference.md](https://github.com/openDAIO/agents/blob/main/docs/frontend-reference.md)
- Reviewer spec — [agents/REVIEWER_AGENT_INTERFACES.md](https://github.com/openDAIO/agents/blob/main/REVIEWER_AGENT_INTERFACES.md)

---

<div align="center">
<sub>Apache-2.0 · openDAIO</sub>
</div>