---
id: publish-kit-pii-verification
title: Verify PII scrub completeness before opening publish-kit PR
scope: command
trigger: /publish-kit, publish-kit, template sync
enforcement: hard
created: 2026-04-02
source: pr-review
---

## Rule

After running the scrub pass in `/publish-kit` and before opening the PR:

1. **Run verification grep** against ALL denylist terms from `scrub-denylist.yaml`:
   ```bash
   grep -riE "$(paste -sd'|' <(yq '.terms[]' scrub-denylist.yaml))" template/ .claude/CLAUDE.md --include='*.md' --include='*.yaml'
   ```
   This must return **0 results**. If any match, fix before proceeding.

2. **Check scrub-denylist.yaml completeness** — every person name, product name, and account ID referenced in HQ must have an entry. Run the denylist patterns against `template/` as a second pass.

3. **Scan knowledge files separately** — knowledge files in `template/knowledge/` are frequently missed by the scrub because they contain documentation examples (code blocks, tables, file paths) where names appear in non-obvious contexts. Grep knowledge files with `-rn` to catch table cells, code comments, and YAML values.

4. **Account IDs are numeric** — they won't match word-based scrub patterns. Explicitly check for any numeric IDs that match known social media account IDs from company settings.

5. **Linter interaction** — the pre-commit linter does partial scrubbing that can conflict with manual edits. After any linter runs, re-verify account IDs and placeholder consistency (linter may revert `{account-id}` back to the raw number, or turn `{product}` into the real name).

## Rationale

Early releases passed through publish-kit with PII instances: person names in knowledge files, product names in policy rationales, account IDs in policies + worker templates. This gate prevents PII from reaching the public repo.
