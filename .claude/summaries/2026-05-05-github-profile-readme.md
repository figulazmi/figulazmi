---
id: 2026-05-05-github-profile-readme-stable-activity-ho-001
date: 2026-05-05
source: claude-code-cli
collection: knowledge_v2_keyfacts
project: homelab
chunk_type: feature
topic: GitHub Profile README Stable Activity Homelab Stack
tags: [homelab, vm-b1, github-profile, readme, developer-branding, implemented]
related: []
session_type: ops-documentation
environment: homelab
git_branch: main
status: implemented
chunk_source: design
---

## CHUNK 1: GitHub Profile README Stable Activity Homelab Stack
<!-- rag_chunk_meta chunk_type=feature tags=[homelab, vm-b1, github-profile, readme, developer-branding, implemented] -->

## CHUNK 1: GitHub Profile README Stable Activity and Homelab Stack

### Context

The figulazmi GitHub profile README is used for personal branding toward recruiters and technical visitors. The session improved reliability and better exposed the user's .NET enterprise work plus homelab AI tooling.

### Problem

External GitHub Stats widgets often failed to render. The unstable widgets included github-readme-stats, a streak stats service, and a visit counter. The profile also needed to show the user's server tools without making the README noisy.

### Solution

Removed external stats cards and the visit counter from README.md. Replaced them with a native Activity note that points visitors to GitHub's built-in contribution graph below the README. Added Focus Areas and a Homelab Runtime Stack table under Personal Projects. The table uses three columns: Tool, Role, Link. It lists Multica, OpenClaw, Hermes Agent, 9router, n8n, Portainer, Proxmox, rag-gateway-mini, and Uptime Kuma.

### Target Files

- README.md

### Interfaces

```markdown
## 📈 Activity

GitHub contribution graph is available natively on my profile page below this README.

Most of my professional work is in private enterprise repositories, so public activity represents only part of my development output.
```

### Contract

- Do not depend on external GitHub stats image services for activity.
- Keep homelab tools scannable with a Tool, Role, Link markdown table.
- Keep the private enterprise repository note visible in the Activity section.

### Verification

```bash
rtk read README.md
rtk git diff README.md
```

### Key Facts

- GitHub native contribution graph is preferred because it is built into the profile page.
- External stats widgets were removed to avoid rate limit, cold start, and uptime problems.
- The Homelab Runtime Stack table is the accepted format for server tools.
- Duplicate OpenClaw entries from the original list were deduplicated.
- The accepted changes were committed and pushed to origin/main with commit message "Update profile README with homelab tooling".

### Caveats

Do not reintroduce external GitHub stats widgets unless the user explicitly prioritizes visual metrics over rendering reliability.

## CHUNK 2: GitHub Profile README Keep Original Structure
<!-- rag_chunk_meta chunk_type=decision tags=[homelab, vm-b1, github-profile, readme, design-decision, developer-branding, implemented] -->

## CHUNK 2: GitHub Profile README Keep Original Structure

### Context

After the stable README improvements were accepted, a larger redesign was explored locally. The experiment used a more curated profile style with a stronger hero, About, What I Build, Selected Experience, and Featured Work sections.

### Problem

The larger redesign changed the tone and structure too far from the user's preferred profile style. The user judged the previous README version to be better and asked to undo the redesign.

### Solution

Restored README.md back to the previously accepted version. The final profile keeps the original structure: Work Experience, Personal Projects, Homelab Runtime Stack table, Tech Stack, Focus Areas, and Activity. This established a clear preference for incremental profile improvements over broad narrative restructuring.

### Key Facts

- The large narrative redesign was attempted locally only and was not committed or pushed.
- The user explicitly preferred the earlier README layout.
- The final accepted profile is the simpler, direct, scannable structure.
- For this profile, direct recruiter scanning is preferred over a cinematic storytelling layout.
- Future redesign experiments should remain local until reviewed.

### Code / Commands

```bash
rtk git checkout -- README.md
```

### Caveats

When proposing future profile redesigns, use reversible local edits and ask for review before any commit or push.

## CHUNK 3: OpenClaw Phase 7 origin hardening procedure and verification
<!-- rag_chunk_meta chunk_type=runbook tags=[homelab, vm-b1, openclaw, security, docker, hardening] -->

### Context
OpenClaw dashboard gateway on VM B1 at 192.168.18.199:18789, running inside Docker container `openclaw`. Runtime config is persisted in Docker volume at `/home/node/.openclaw/openclaw.json`. Previous config had wildcard `*` in allowedOrigins and `dangerouslyAllowHostHeaderOriginFallback=true`.

### Problem
Origin policy was permissive (break-glass posture from initial restore). Phase 7 required removing wildcard origins and disabling host-header fallback while preserving LAN, Tailscale, and HTTPS dashboard access. Risk RISK-OPENCLAW-ORIGIN-2026-05-02 was open and blocking security posture improvement.

### Solution
Edit `/home/node/.openclaw/openclaw.json` inside the container, replace allowedOrigins with exact list only, set fallback to false, then restart only `openclaw-gateway` service.

Exact approved origins after hardening:
- http://localhost:18789
- http://127.0.0.1:18789
- http://192.168.18.199:18789
- http://100.120.249.99:18789
- https://openclaw.azmi-lab.cloud
- https://openclaw.azmi-lab.cloud:443

Verification commands:
```bash
ssh figulazmi@192.168.18.199 'sudo docker exec openclaw node -e "const fs=require(\"fs\");const c=JSON.parse(fs.readFileSync(\"/home/node/.openclaw/openclaw.json\",\"utf8\"));console.log(JSON.stringify({hasWildcard:c.allowedOrigins.includes(\"*\"),fallback:c.dangerouslyAllowHostHeaderOriginFallback},null,2))"'
ssh figulazmi@192.168.18.199 'curl -s -o /tmp/openclaw-home.html -w "http_code=%{http_code} size=%{size_download}\n" http://192.168.18.199:18789'
ssh figulazmi@192.168.18.199 'sudo docker exec openclaw node dist/index.js infer model run --local --model openai/9routers --prompt "Reply exactly OK" --json'
ssh figulazmi@192.168.18.199 'sudo docker exec openclaw node dist/index.js agent --agent main --local --message "Reply exactly OK" --json'
```

### Key Facts
- Config file path: `/home/node/.openclaw/openclaw.json` inside Docker volume `openclaw-setup_openclaw-config`
- Verified result: `hasWildcard=false`, `fallback=false`, HTTP 200 size 2821, inference OK, agent OK
- Task IDs: SEC-OPENCLAW-ORIGIN-HARDEN DONE, PH7-PLAN-2026-05-05 DONE
- Runbook entry added to `docs/reference/RUNBOOK.md` under "Harden OpenClaw dashboard origins on VM B1"
- Risk RISK-OPENCLAW-ORIGIN-2026-05-02 moved to Resolved in RISK_REGISTER.md on 2026-05-05
- Restart command: `sudo docker compose up -d openclaw-gateway` from `/opt/homelab/ai-stack/openclaw-setup`

## CHUNK 4: rag_capture.py native push and count reporting
<!-- rag_chunk_meta chunk_type=feature tags=[homelab, vm-b1, python, rag, qdrant, reporting, no-wsl] -->

### Context
The rag_capture.py CLI on Windows was invoking bash for push-to-qdrant.sh via a generic subprocess call, which triggered a WSL warning. Collection point counts were also printed twice per file.
### Problem
Two issues: (1) generic ["bash", ...] call caused WSL warning on Windows; (2) before/after count block appeared from both the shell script and the Python layer, duplicating output.
### Solution
Added native helpers: qdrant_collection_count (urllib direct to Qdrant API), extract_collection_from_summary (reads frontmatter collection field), find_bash_executable (resolves Git Bash from known Windows paths before falling back), run_push_script (uses find_bash_executable instead of bare bash), print_push_report (single count summary). Removed duplicate count prints from auto_push and cmd_push_pending pre-report. Changed cmd_merge to auto-clear drafts without prompt after successful push; prompt retained only for interactive push-failure path.
### Target Files
- C:/Users/Clandesitine/scripts/rag-capture-v2/rag_capture.py
### Interfaces
- qdrant_collection_count(config, collection) -> int | None
- extract_collection_from_summary(path, config) -> str
- find_bash_executable() -> str
- run_push_script(path, config) -> CompletedProcess
- print_push_report(path, config, before_count, after_count)
- format_push_command(config, output_path) -> str
### Contract
- Collection name and before/after point delta printed exactly once per file.
- No WSL warning from rag merge or rag push-pending on Windows with Git Bash installed.
- Drafts auto-cleared after successful push; no prompt shown.
- Queue behavior and retry logic in cmd_push_pending unchanged.
### Verification
- py_compile passes with no syntax errors.
- rag merge output shows single count block: Collection, Points before, Points after, Delta.
- No "WSL has no installed distributions" line in output.
- Draft folder cleared automatically after successful push.
### Key Facts
- find_bash_executable resolves C:/Program Files/Git/bin/bash.exe before falling back to bare bash.
- Duplicate counts removed by deleting pre-report print calls in auto_push and cmd_push_pending.
- cmd_merge now branches on pushed return value, not stdin.isatty alone.
- format_push_command returns python executable path on Windows, bash path on non-Windows.

---

## SESSION METADATA

- **Total chunks**: 4
- **Qdrant collection**: knowledge_v2_keyfacts
- **Generated by**: rag_capture.py v2 -- Incremental Capture
- **Author**: Figur Ulul Azmi
- **Date**: 2026-05-05
- **Unresolved items**: (fill manually if needed)