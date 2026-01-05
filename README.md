# Intuition Trust Skill for Claude

A Claude Skill that integrates [Intuition Protocol's](https://intuition.systems) decentralized knowledge graph, enabling Claude to query Web3 trust and reputation data before making recommendations.

## Overview

This skill allows Claude to:

- Query trust scores for wallets, contracts, and projects
- Verify claims and attestations about entities
- Check relationships between Web3 identities
- Assess credibility before recommending Web3 projects
- Access the Intuition knowledge graph through natural language

## How It Works

When a user asks Claude about a Web3 project, wallet, or contract, Claude can query Intuition's GraphQL API to retrieve:

- **Trust Signal**: Total TRUST tokens staked on an entity
- **Position Count**: Number of unique attestors
- **Claims**: Subject-Predicate-Object statements about the entity
- **Counter-Claims**: Negative attestations or disputes

This data helps Claude provide informed recommendations with verifiable on-chain trust data.

## Structure

```
intuition-trust/
├── SKILL.md                      # Main skill instructions for Claude
├── scripts/
│   └── intuition_query.py        # Python helper for GraphQL queries
└── references/
    └── api_reference.md          # Complete API documentation
```

## Example Usage

User prompt:
```
Is this DeFi protocol safe to use? Check its reputation.
```

Claude queries Intuition and responds:
```
Intuition Trust Check: [Protocol Name]

Trust Signal: 5,420 TRUST staked by 47 attestors
Positive Claims:
  - is-audited-by -> CertiK
  - has-track-record -> 2 years
Concerns:
  - had-incident -> Flash loan exploit (resolved)

Assessment: Moderate confidence. Audited with established track record,
but has history of one resolved security incident.

View full profile: https://portal.intuition.systems/identity/12345
```

## API Endpoints

| Network | Endpoint |
|---------|----------|
| Mainnet | `https://mainnet.intuition.sh/v1/graphql` |
| Testnet | `https://testnet.intuition.sh/v1/graphql` |

## Python Helper

The included Python script provides command-line access to Intuition data:

```bash
# Search for an entity
python intuition_query.py --search "Uniswap"

# Get trust score for an atom
python intuition_query.py --trust-score 12345 --format text

# Check claims about an entity
python intuition_query.py --triples-about 12345

# Query by wallet address
python intuition_query.py --address 0x1234...
```

## Core Concepts

| Term | Description |
|------|-------------|
| **Atom** | Fundamental unit representing any entity (wallet, contract, person, concept) |
| **Triple** | A claim in Subject-Predicate-Object format connecting three Atoms |
| **Signal** | Economic weight (TRUST tokens staked) behind a claim |
| **Position** | A user's stake on an Atom or Triple |

## Trust Score Calculation

```
trust_ratio = vault.total_shares / (vault.total_shares + counter_vault.total_shares)
```

| Score | Interpretation |
|-------|----------------|
| > 0.8 | Strong positive sentiment |
| 0.5 - 0.8 | Mixed or contested |
| < 0.5 | Negative sentiment |

## Links

- [Intuition Protocol](https://intuition.systems)
- [Documentation](https://docs.intuition.systems)
- [Portal Explorer](https://portal.intuition.systems)
- [Anthropic Skills PR](https://github.com/anthropics/skills/pull/211)

## Status

This skill has been submitted as a PR to [Anthropic's official skills repository](https://github.com/anthropics/skills/pull/211).

## License

MIT
