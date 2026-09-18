# The canonical install block

One install story, one wording. `README.md` must say **this** and nothing else. Change it here first, then propagate.

This is a fork of `mattpocock/skills`. Matt's copy of this file describes **his** install story: an official-marketplace listing and [skills.sh](https://skills.sh/mattpocock/skills). Neither is true of this repo, so this file diverges from upstream permanently. On a sync, keep this version and only read his for changes worth mirroring.

## Claude Code: the plugin

`.claude-plugin/marketplace.json` makes this repo its own single-plugin marketplace. That is the whole install story here: nothing is published, and there is no listing to wait on.

<canonical-block name="claude-code">

From inside a Claude Code session:

```
/plugin marketplace add tooky/skills
/plugin install tooky-skills@tooky
```

This repo is its own single-plugin marketplace, so there is nothing to add first and nothing published anywhere. You get the whole set as a managed bundle; run `/plugin update tooky-skills` when you want the latest.

</canonical-block>

To test an unpushed commit, point the marketplace at the working copy instead:

```
/plugin marketplace add ~/Code/tooky/skills
```

## Working on the skills: link-skills.sh

The plugin is a snapshot copy, so your own edits are invisible until you update it. For authoring, `scripts/link-skills.sh` symlinks every skill into `~/.claude/skills` and `~/.agents/skills` (which also covers Codex and other Agent Skills harnesses), so an edit is live in the next session.

<canonical-block name="link-skills">

```bash
./scripts/link-skills.sh
```

That symlinks every skill into `~/.claude/skills` and `~/.agents/skills`, which also covers Codex and other Agent Skills harnesses. An edit in the repo is live in your next session, with no reinstall step.

</canonical-block>

## The two routes are exclusive

The plugin is a managed, read-only bundle you subscribe to. The symlinks point at a repo you edit. Installing both leaves you with every skill twice: always say "pick one".

## Not the install story

`npx skills@latest add mattpocock/skills` installs **Matt's** set, not this one. `skills.sh/tooky/skills` is not a listing that exists. Neither belongs in this repo's docs.
