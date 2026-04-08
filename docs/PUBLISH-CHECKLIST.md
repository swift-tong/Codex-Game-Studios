# Publish Checklist

Use this checklist before publishing Codex Game Studios as a public repository.

## Repository Surface

- [ ] `README.md` reflects the final repository name and positioning
- [ ] `AGENTS.md` is the active root instruction file
- [ ] `.agents/` is complete and committed
- [ ] Nested `AGENTS.md` files exist where needed
- [ ] `legacy/` is either intentionally kept or intentionally removed

## Public Docs

- [ ] `CONTRIBUTING.md` is up to date
- [ ] `CHANGELOG.md` includes the release being published
- [ ] `UPGRADING.md` matches the Codex-first structure
- [ ] `docs/GITHUB-METADATA.md` has the final repo description and topics
- [ ] `docs/releases/v1.0.0-codex.md` matches the release summary you want to publish

## GitHub Setup

- [ ] Repository description is set
- [ ] Topics are set
- [ ] Social preview image is added if desired
- [ ] `CODEOWNERS` is correct
- [ ] Issue templates and PR template match the contribution flow you want

## Cleanup

- [ ] Remove local-only or editor-only files you do not want tracked
- [ ] Review `git status` for accidental changes
- [ ] Confirm no active docs still point to obsolete paths
- [ ] Decide whether archived Claude-era material should stay public

## Release

- [ ] Create the initial commit history you want to publish
- [ ] Tag the first public release
- [ ] Copy release notes from `docs/releases/v1.0.0-codex.md`
