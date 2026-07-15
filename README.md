# vetaskill

**Vet a Skill: a Claude Skill that statically audits other people's Skills before you install them. It reads them as untrusted data, analyses full contents, and returns a detailed security verdict.** 

---

## Why this exists

A Claude Skill is executable instruction. When you enable one, Claude follows it automatically with whatever you have connected: files, email, memory, MCP servers. That makes every third-party Skill a supply-chain dependency.

Malicious Skills can steal your confidential data, run code, watch your conversations, hijack agents, poison memory, reframe outputs, and more.

The risks: Snyk's February 2026 audit of [3,984 public Skills](https://snyk.io/blog/toxicskills-malicious-ai-agent-skills-clawhub/) found more than a third carried a security flaw and 76 were confirmed malicious (credential theft, data exfiltration), with 40+ near-identical malicious Skills traced to a single account. Two academic scans agree: one of [nearly 100,000 Skills](https://arxiv.org/abs/2602.06547) confirmed 157 malicious, another across [three marketplaces](https://arxiv.org/abs/2606.23416) confirmed 131, 63% of them disguised as ordinary tools. The entry bar on some registries is a markdown file and a week-old account.

Scanners help, but share two blind spots:

1. **Bundled test files.** Major scanners skip the "test" fixtures a Skill ships with, which is [where a payload may hide](https://venturebeat.com/security/anthropic-skill-scanners-passed-every-check-malicious-code-test-file).
2. **Off-file instructions.** When a Skill tells the agent to fetch a URL and follow it ("read the docs and continue", "install from here"), that page is unread Skill content with the same authority, and it never ships in the bundle a scanner reads. It can change after a clean scan, or sit on a lookalike domain. A one-off scan is a static snapshot that cannot protect you from a link that changes hands later ([demonstrated here](https://www.air.security/blog-posts/the-story-of-skills)).

Experts agree: run only Skills you built yourself or got from unambiguously secure sources, read every bundled file, and never trust skills that point to external links for instructions.

More details in the article: [Love free Skill bundles? Hackers love them too.](https://aisafelens.substack.com/p/love-free-skill-bundles-hackers-love)

## What vetaskill does

Given a `SKILL.md`, a skill folder, or a zip, it reads every file - scripts and test fixtures included - as untrusted data and reports what the Skill could do if trusted. It:

- never runs, sources, fetches, or installs anything under review, and holds no web-fetch or install permission itself;
- extracts zips read-only into quarantine, never into a skills directory;
- flags exfiltration and network callbacks, code execution and droppers, file and credential access, persistence and memory writes, concealment and encoded blobs, off-file or load-bearing links and lookalike domains, and any tool permission the stated job does not justify;
- returns a verdict - SAFE TO TRY, REVIEW NEEDED, or DO NOT INSTALL - decided by fixed rules rather than overall impression, with the file and line quoted for every finding.

Recommendation only - the install decision stays a deliberate human step.

This skill underwent an adversarial red-team review by Anthropic's **Fable**.

## How to use it

This is a working reference implementation. Because this repo exists to make you audit strangers' Skills, hold this one to the same standard:

1. **Read the content first.** It is one file. It asks for four read-only tools (`Bash`, `Read`, `Grep`, `Glob`), no web-fetch, no install permission - by design.
2. Copy the `vetaskill/` folder into your skills directory (for example `~/.claude/skills/vetaskill/`), or point your agent to the link of this repo and ask it to build the skill.
3. Invoke vetaskill before you install any third-party Skill and point your agent at the full skill bundle (text, folder, or zip).

## Licence

MIT. See [`LICENSE`](LICENSE).
