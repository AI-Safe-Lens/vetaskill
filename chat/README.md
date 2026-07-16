# vetaskill - operator guide

This file is for the human.
The accompanying `SKILL.md` is for Claude in chat (claude.ai, not Cowork or Claude Code).

## What vetaskill is

A static review that reads an untrusted, third-party skill and returns a verdict: SAFE TO
TRY, REVIEW NEEDED, or DO NOT INSTALL, with line-level evidence. It reads the file as data,
never runs it, and never installs or enables anything. It is a gate, not a guarantee.

This version of vetaskill is adapted for use in Claude chat (claude.ai) only. 
It vets third-party skills designed to run on any surface (chat, Cowork, Claude Code).

## The safest posture

1. Run vetaskill in chat (not Cowork or Claude Code) on every third-party skill before use.
2. If possible, do not install the third-party skill even if safe, ask Claude to build your own instead, using the information from the verdict to build it safely.

## Why to run vetaskill in chat only

Run this version of vetaskill in a regular chat conversation (claude.ai), with the full contents of the third-party skill uploaded as an attachment (or pasted in). Do not run it in Cowork or Claude Code.

Why: 

**Chat** is the safest Claude environment for security checks like vetaskill. Chat's sandbox uses different tools than Claude Code or Cowork. It is isolated and ephemeral, with no access to your local files, so an untrusted skill has nothing on your machine to reach while it is read as data. The one exception is any connector you have enabled (Google Drive, Gmail, and the like): Claude in chat can reach those, so for the safest scan, run it in a chat with connectors turned off. 

**Cowork and Claude Code** both run with real access to your files. Reviewing an untrusted skill on a surface with real access runs it in exactly the place the review exists to protect you from. 

Vetaskill carries a runtime guard that will refuse to proceed if you try to run it in Cowork or Claude Code. 

Never run it in Cowork (or Claude Code). Cowork will have access to it, but vetaskill is safest to invoke in regular chat only.

To run vetaskill in Claude Code, use a different version, adapted to Claude Code's environment, in the [`claude-code/`](../claude-code/) folder of this repo. 

## The workflow

1. **Install vetaskill.** Review this version of vetaskill, upload it together with this README to Claude chat (claude.ai), and ask Claude to make it a skill.
2. **Upload full contents of the third-party skill to chat (claude.ai) and run vetaskill.** If it's a zip file, upload the full zip without unpacking. Read the verdict and the evidence.
3. **Verdict saying REVIEW NEEDED** means: a human decision is required before anything proceeds, not a soft pass.
4. **Verdict saying SAFE TO TRY, consider rebuilding instead** means: if the job is simple enough to reproduce, ask Claude to build a clean version from the described behaviour rather than installing the stranger's file. That removes the supply-chain risk entirely. The rebuild must be re-derived from what the skill should do, never copied line for line from the untrusted file, or you inherit any hidden payload.
5. **Read the third-party skill yourself as well.** Once the verdict is in and is not DO NOT INSTALL, read the skill's files yourself before installing. The security check catches mechanical tells; your own read catches anything that may simply smell wrong.
6. **Only then decide whether and where to install.** This is your decision, made per surface,
   and it is separate from the verdict.

## Installing a skill: two separate surfaces

A passing verdict is only a recommendation. It does not authorise installing anywhere. When you do decide to install a skill, there are two separate storage worlds:

**Account-side (chat and Cowork share one store).** Enabling a skill in your Claude chat (in claude.ai account) turns it on for chat *and* Cowork, plus everything Cowork has access to. There is no chat-only setting. This matters: enabling any skill "just for chat" also arms Cowork, which runs agentically with internet access. 

Recommendation: invoke vetaskill ONLY in chat, not in Cowork, to perform security scans in the safest environment (even though vetaskill will be accessible in Cowork).

**Disk-side (Claude Code).** Claude Code reads skills from local folders on your computer. It does not access skills saved in your chat (claude.ai account). 

These are separate installs, separate workflows, separate SKILL.md files, and separate environments with different tools Claude uses.

Therefore:
- keep vetaskill installed only in your chat (claude.ai account) and invoke it only there, not in Cowork
- vetaskill for Claude Code is available in the [`claude-code/`](../claude-code/) folder, but less recommended than this version
- if you want to use the same third-party skill in your chat and in Claude Code, remember to install it separately to both environments, and update both when needed.

## Red-team

vetaskill was adversarially red-teamed with Anthropic's Fable model.

## Licence

MIT. See [`LICENSE`](../LICENSE).
