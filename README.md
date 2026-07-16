# vetaskill

**A Claude Skill that statically audits other people's Skills before you install them. It reads an untrusted, third-party Skill as data, analyses its full contents, and returns a security verdict: SAFE TO TRY, REVIEW NEEDED, or DO NOT INSTALL, with line-level evidence. It never runs, installs, or enables the skill under review.**

A Claude Skill is executable instruction. When you enable one, Claude follows it automatically with whatever you have connected: files, email, memory, MCP servers. That makes every third-party Skill a supply-chain dependency, and a stranger's Skill can steal data, run code, hijack the agent, poison memory, or point the agent off to a link that changes hands after a clean scan. vetaskill is the gate you run first.

The full case, with sourced figures and documented attacks, is in the article: [Love free Skill bundles? Hackers love them too.](https://open.substack.com/pub/aisafelens/p/love-free-skill-bundles-hackers-love)

## Two variants, one job

vetaskill comes in two versions because the surface you run it on changes how safe the review is. They do the same static analysis and apply the same verdict rules. They differ in the environment they run in and the tools they use.

- **[`chat/`](chat/) - the safer default.** For Claude chat in claude.ai. Chat's sandbox is isolated and ephemeral, with no access to your local machine, so an untrusted skill has nothing there to reach while it is read as data. Prefer this version for the scan itself whenever you can, even for skills you intend to run in Claude Code. Upload the full third-party skill folder as an attachment and run vetaskill against it.

- **[`claude-code/`](claude-code/) - disk-side install.** For Claude Code, which reads skills from local folders on your computer and runs with real access to your files. Reviewing an untrusted skill here reads it in the same environment it will run in, and that environment has real access. Use this version when that is what you specifically want, and rely on its static-only discipline to keep the read safe.

Each folder holds its own `SKILL.md` and its own `README.md` with the operator detail for that surface. Read the README in the folder you are about to use.

## The safest posture

1. Vet every third-party skill before you use it, and prefer doing it in the chat version (claude.ai, not Cowork or Claude Code).
2. On a passing verdict, consider rebuilding the third party skill yourself, rather than installing. If the job is simple enough to reproduce, ask Claude to build a clean version from the described behaviour. That removes the supply-chain risk entirely. Re-derive it from what the skill should do, never copy the untrusted file line for line, or you inherit any hidden payload.
3. The verdict is a recommendation. The decision to install stays a deliberate human step, made per surface.

## A note on the two storage worlds

Enabling a skill in your chat (claude.ai account) turns it on for chat **and** Cowork, which runs agentically with internet access, and access to your local files. There is no chat-only setting. Claude Code is separate: it reads skills from local disk and does not see skills saved in your chat account. So the two variants here are separate installs, and if you want vetaskill on both surfaces you install each one where it belongs and update both when this repo changes.

## Licence

MIT. See [`LICENSE`](LICENSE).
