# vetaskill - operator guide (Claude Code version)

This file is for the human.
The accompanying `SKILL.md` is for Claude in Claude Code.

## What vetaskill is

A static review that reads an untrusted, third-party skill and returns a verdict: SAFE TO
TRY, REVIEW NEEDED, or DO NOT INSTALL, with line-level evidence. It reads the file as data,
never runs it, and never installs or enables anything. It is a gate, not a guarantee.

This is the Claude Code version of vetaskill, for the disk-side install that Claude Code reads from local folders on your computer. The [chat version](../chat/) of vetaskill is the safer default, because a chat sandbox reaches none of your real files while it reads the third-party skill, whereas Claude Code runs with real access to your files. The chat version of vetaskill explains why chat is safer, and the top-level README (link) makes the full case for vetting third-party skills at all. Using the chat version of vetaskill does cover third party skills for Cowork/Claude Code use.  Use this Claude Code version of vetaskill only when you specifically want the third-party skill read in the same environment it will later run in.

## The safest posture

1. Run vetaskill on every third-party skill before you use it, and prefer the chat version of vetaskill for the scan itself.
2. If possible, do not install the third-party skill even if it is safe. Ask Claude to build your own instead, using the information from the verdict to build it safely.

## The workflow

1. **Read the content of vetaskill's `SKILL.md` first.** As a habit, read skill files before you use them. It asks only for read-only tools (`Bash`, `Read`, `Grep`, `Glob`, or equivalent read-only tools), no web-fetch and no install permission, by design.
2. **Install vetaskill.** Copy `claude-code/SKILL.md` into a folder named `vetaskill` inside your skills directory, so it lands at `~/.claude/skills/vetaskill/SKILL.md`. (A Claude Code skill is a folder named for the skill, holding a `SKILL.md`.)
3. **Run vetaskill before you install any third-party skill.** Ask Claude to point vetaskill at the full third-party skill bundle (a folder or a zip). If it is a zip, do not unpack it.
4. **Verdict saying REVIEW NEEDED** means: a human decision is required before anything proceeds, not a soft pass.
5. **Verdict saying SAFE TO TRY, consider rebuilding instead** means: if the job is simple enough to reproduce, ask Claude to build a clean version from the described behaviour rather than installing the stranger's file. That removes the supply-chain risk entirely. The rebuild must be re-derived from what the skill should do, never copied line for line from the untrusted file, or you inherit any hidden payload.
6. **Read the third-party skill yourself as well.** Once the verdict is in and is not DO NOT INSTALL, read the skill's files yourself before installing. The security check catches mechanical tells; your own read catches anything that may simply smell wrong.
7. **Only then decide whether and where to install.** This is your decision, made per surface, and it is separate from the verdict.

## Red-team

vetaskill was adversarially red-teamed with Anthropic's Fable model.

## Licence

MIT. See [`LICENSE`](../LICENSE).
