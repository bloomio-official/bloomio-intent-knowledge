# Bloomio Intent Knowledge

`bloomio-intent-knowledge` is a passive Agent Skill that teaches compatible AI assistants how to interpret and apply Bloomio's `BrowseIntent` profile property.

It provides canonical signal semantics and overridable lifecycle-marketing playbooks. It contains no connector, executable code, credentials, customer data, scoring formula, or permission to inspect or change Klaviyo—or any other external system. Users connect and authorize those capabilities separately.

## What is in this repository

```text
bloomio-intent-knowledge/
├── plugin.json
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

The files under `skills/bloomio-intent-knowledge/` are the single canonical knowledge source. Release packaging does not maintain a second copy.

## Install in Claude

1. Download `bloomio-intent-knowledge-claude-v0.1.0.zip` from the GitHub release.
2. In Claude, open **Customize > Skills**.
3. Select **+ > Create skill > Upload a skill**.
4. Upload the ZIP and enable the skill.
5. Configure and authorize the Klaviyo MCP separately if you want Claude to work with a Klaviyo account.

## Install in ChatGPT

The intended non-technical route is the public ChatGPT Plugins Directory after Bloomio's plugin is reviewed and listed. The directory is available on ChatGPT web across plans, including Free, although OpenAI says installation and use can still vary by account, rollout, region, and included capabilities.

After publication:

1. Open **Plugins** in ChatGPT web.
2. Find **Bloomio Intent Knowledge**.
3. Select **Install plugin** when available.
4. Enable it with an `@` mention or through **+ > More**, when those controls appear.
5. Connect the published Klaviyo app separately if it is available for the user's plan and account.

Free ChatGPT web does not provide a supported way to upload this GitHub ZIP as a privately installed plugin. The ZIP is a source, review, and submission artifact; public directory publication is what creates the simple consumer installation experience.

## How it works with Klaviyo

The host assistant decides when the skill is relevant, reads its canonical guidance, and combines that context with information or actions available through separately installed tools. This skill interprets and advises; the Klaviyo MCP reads or changes Klaviyo only when the user's request and that connector's own controls allow it.

Installing this skill does not install Klaviyo access, grant permissions, or cause actions by itself.

## First test

Use this read-only prompt:

> Confirm whether you can read a custom profile property named `BrowseIntent`. Do not change anything. Report the distinct values you can observe, including missing or unexpected values, and interpret them using Bloomio Intent Knowledge.

Then test a recommendation:

> Recommend one campaign hypothesis for profiles whose `BrowseIntent` is `High`. Separate observed facts, canonical Bloomio meaning, and your recommendation. Do not make any Klaviyo changes.

See [PUBLISHING.md](PUBLISHING.md) for the complete test matrix and release process.

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
- Free ChatGPT users must use the published Klaviyo app when available; they cannot add a custom MCP server themselves.
- Direct installation of third-party skills in Klaviyo Composer is not claimed. The reference content can still inform prompts used there.

## Sources

- [Bloomio whitepaper](https://bloomio.ai/whitepaper/browsing-intent-practical-shopper-intent-signal-ecommerce-phil-roselli-july-2026.pdf)
- [Bloomio AI activation guide](https://bloomio.ai/blog/how-to-use-bloomio-in-claude-and-composer)
- [Agent Skills specification](https://agentskills.io/specification)
- [Claude custom skills documentation](https://support.claude.com/en/articles/12512198-how-to-create-custom-skills)
- [OpenAI skill-building documentation](https://learn.chatgpt.com/docs/build-skills)
- [OpenAI plugin-building documentation](https://learn.chatgpt.com/docs/build-plugins)

## License

MIT. See [LICENSE](LICENSE).
