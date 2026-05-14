# Agent Instructions Repository

This repository enables AI coding agents to generate video and image assets through the Arcads external API. Here's what you need to know:

**Initial Setup:**
First-time users should run `./scripts/setup.sh` if `.env` or `MASTER_CONTEXT.md` don't exist.

**Session Workflow:**
1. Review `MASTER_CONTEXT.md` for brand guidelines and cost information
2. Reference the appropriate skill file from `.cursor/skills/` or `.claude/skills/`
3. Help populate any missing fields in `MASTER_CONTEXT.md` and document changes in the changelog
4. Update the changelog with dated entries after significant modifications

**Technical Details:**
- API endpoint: `https://external-api.arcads.ai`
- Authentication uses HTTP Basic auth via `ARCADS_BASIC_AUTH` or `ARCADS_API_KEY`
- Environment variables in `.env` require single quotes due to special characters
- Available skills include the main API reference and a YouTube thumbnail batch workflow
- Verify setup with `./scripts/check-arcads-env.sh`
