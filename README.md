# Bloomio Intent Knowledge for Claude

`bloomio-intent-knowledge` is a passive Claude Skill that teaches Claude how to interpret and apply Bloomio's `BrowseIntent` profile property.

It provides canonical signal semantics and overridable lifecycle-marketing playbooks. It contains no connector, executable code, credentials, customer data, scoring formula, or permission to inspect or change Klaviyo—or any other external system. Users connect and authorize the Klaviyo MCP separately.

## Install in Claude

1. Download `bloomio-intent-knowledge-claude-v0.1.0.zip` from the latest GitHub release.
2. In Claude, open **Customize > Skills**.
3. Select **+ > Create skill > Upload a skill**.
4. Upload the ZIP and enable the skill.
5. Configure and authorize the Klaviyo MCP separately if you want Claude to work with a Klaviyo account.

## How it works with Klaviyo

Claude decides when the skill is relevant, reads its canonical guidance, and combines that context with information or actions available through the separately installed Klaviyo MCP.

The Bloomio skill interprets and advises. The Klaviyo MCP reads or changes Klaviyo only when the user's request and Klaviyo's own controls allow it. Installing this skill does not install Klaviyo access, grant permissions, or cause actions by itself.

## First test

Start with a read-only request:

> Confirm whether you can read a custom profile property named `BrowseIntent`. Do not change anything. Report the distinct values you can observe, including missing or unexpected values, and interpret them using Bloomio Intent Knowledge.

Then test a recommendation:

> Recommend one campaign hypothesis for profiles whose `BrowseIntent` is `High`. Separate observed facts, canonical Bloomio meaning, and your recommendation. Do not make any Klaviyo changes.

See [PUBLISHING.md](PUBLISHING.md) for the complete test matrix and release process.

## Repository structure

```text
bloomio-intent-knowledge/
├── skills/
│   └── bloomio-intent-knowledge/
│       ├── SKILL.md
│       └── references/
│           ├── activation-playbooks.md
│           └── signal-contract.md
├── tests/
├── CHANGELOG.md
├── LICENSE
├── PUBLISHING.md
└── README.md
```

The files under `skills/bloomio-intent-knowledge/` are the canonical knowledge source. The downloadable ZIP contains only that skill folder.

## Validate locally

From this repository:

```bash
python3 -m unittest discover -s tests -p 'test_*.py'
```

If `skills-ref` is installed:

```bash
skills-ref validate skills/bloomio-intent-knowledge
```

## Support boundaries

- This repository covers Bloomio Browse Intent only.
- It does not cover Bloomio agents, automatic campaigns, or deprecated intent scoring.
- It does not bundle or operate the Klaviyo MCP.
- It is currently distributed and documented for Claude only.

## Sources

- [Bloomio whitepaper](https://bloomio.ai/whitepaper/browsing-intent-practical-shopper-intent-signal-ecommerce-phil-roselli-july-2026.pdf)
- [Bloomio AI activation guide](https://bloomio.ai/blog/how-to-use-bloomio-in-claude-and-composer)
- [Agent Skills specification](https://agentskills.io/specification)
- [Claude custom skills documentation](https://support.claude.com/en/articles/12512198-how-to-create-custom-skills)

## License

MIT. See [LICENSE](LICENSE).
