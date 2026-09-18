# This repo is a fork

`tooky/skills` is a fork of [`mattpocock/skills`](https://github.com/mattpocock/skills). Matt's set is the foundation; this repo tracks it, adds skills of its own, and offers changes back where they are generally useful.

The rule that governs everything below: **merge conflicts come only from editing files Matt also edits.** New files are free. So keep the divergence small, concentrated, and deliberate.

## Branches

| Branch | Role |
| --- | --- |
| `main` | Ours. Matt's work merges in; the packaging rebrand and our own skills live here. |
| `upstream-main` | A pure mirror of `upstream/main`. Never commit to it; only fast-forward it. It exists so `git diff upstream-main main` is readable and so GitHub can show comparisons. |
| topic branches off `upstream/main` | One per change destined for Matt. Carries none of our branding. |

Merge, never rebase. Rebasing replays our divergence on every sync and re-fights the same conflicts; merging records each resolution once. `git config rerere.enabled true` is set so git replays those resolutions automatically.

## Syncing from Matt

Roughly monthly, matching his churn.

```bash
git fetch upstream
git log --oneline main..upstream/main          # what's new
git diff main...upstream/main --stat           # where it landed
git switch main && git merge upstream/main     # resolve, commit
git branch -f upstream-main upstream/main && git push -f origin upstream-main
./scripts/link-skills.sh                       # only if skills were added or renamed
```

Expect occasional small conflicts in `README.md`, `CLAUDE.md`, and `.claude-plugin/plugin.json`. In `plugin.json`, keep our `name`/`description`/`author`/`homepage`/`repository` and take his `skills` array. In `README.md`, keep our header and installation section and take everything below it.

## Proposing a change back to Matt

Author it off **his** main, so the pull request carries no rebranding:

```bash
git fetch upstream
git switch -c fix/<thing> upstream/main
# make the change; follow his CLAUDE.md conventions; add a changeset
git push -u origin fix/<thing>
gh pr create --repo mattpocock/skills --base main --head tooky:fix/<thing>
git switch main && git merge fix/<thing>       # take it into our fork straight away
```

That last merge is the point of the shape. We get the improvement immediately, and when Matt merges the pull request the next `git merge upstream/main` sees the same commit and does nothing. A change offered back stops being divergence.

For something already committed on `main` that we later decide to offer back, `git cherry-pick` it onto a branch off `upstream/main` instead.

Note that `gh` resolves to `mattpocock/skills` by default in this fork, so pass `--repo tooky/skills` for anything meant for our own repo.

## What diverges on purpose

Only the packaging layer:

- `.claude-plugin/plugin.json`
- `.claude-plugin/marketplace.json`
- `package.json`
- `README.md` (header and installation section only)
- `.agents/install-block.md`
- `CLAUDE.md` (one added pointer to this file)
- this file

`git diff main...upstream-main --stat` should list exactly those. Anything else is unintended divergence, and is either a change to offer back to Matt or a mistake.

Matt's skill names stay as they are. Renaming `ask-matt` or `setup-matt-pocock-skills` would spread divergence into `plugin.json`, both bucket `README.md`s, `docs/`, `CLAUDE.md`, and a dozen cross-references, and would turn every upstream edit to those files into a conflict. Not worth it.

## Where a new skill goes

Bucket by destination, not by topic.

- **Meant for Matt too**: put it in `engineering/` or `productivity/`, author it on a branch off `upstream/main`, and follow his conventions in full (bucket `README.md`, top-level `README.md`, `plugin.json`, a `docs/` page, a changeset, `ask-matt` routing). The shared-file edits it needs stop being divergence once he merges them.
- **Ours alone**: give it its own bucket, for example `skills/product-management/`. Purely additive, so no conflict surface. It gets a bucket `README.md` listing its skills, and an entry in `.claude-plugin/plugin.json` so the plugin ships it.

Our own buckets get **no** `docs/` page. The `docs/` tree feeds `aihero.dev/skills-<name>`, which is Matt's publishing pipeline, not ours. Leave it untouched so it merges cleanly forever.

`scripts/link-skills.sh` finds skills by locating `SKILL.md`, so a new bucket needs no change to the script. It still skips `deprecated/` and `misc/`.

`ask-matt` is deliberately left alone. It is the router for Matt's set, and it changes often upstream. Revisit routing once there are enough of our own skills to need it.

## Matt's release machinery

`.changeset/`, `.changeset/config.json`, and `.github/workflows/release.yml` are Matt's. Leave all of them untouched: deleting a file upstream keeps editing produces a modify/delete conflict on every sync, for no gain.

GitHub disables Actions workflows on a fork by default, so `release.yml` is inert here and there is nothing to switch off. If Actions are ever enabled on this repo, disable the Release workflow then (`gh workflow disable Release --repo tooky/skills`), or it will open "chore: version skills" pull requests on every push to `main`.

Write a changeset only for a change destined upstream, since that is his convention and his release runs on them. Fork-only changes get none.
