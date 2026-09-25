# Brieflee "New Video" workflow — Vertex node update checklist

Workflow: **New Video** (n8n ID `PrSV0egnYf941dPx`)

Scope: just the URL swap (Gemini 2.0 → 2.5) and adding `generationConfig` with `maxOutputTokens: 32768`. **Not** the full draft-prompt body swap — that's for another day.

## Nodes

| # | n8n node | What it's for | URL changed | Token added | Pairs with prompt file |
|---|----------|---------------|:-----------:|:-----------:|------------------------|
| 1 | Vetex AI | Standard text brief review | ☐ | ☐ | `brieflee-brief-vertex-ai` |
| 2 | Vetex AI1 | No-brief review (creator submitted without one) | ☐ | ☐ | `no-brief-vertex-ai-1` |
| 3 | Vetex AI2 | Swipe link review (URL reference) | ☐ | ☐ | `swipe-link-vetex-ai-2` |
| 4 | Vetex AI3 | Swipe file review (uploaded reference video) | ☐ | ☐ | `swipe-file-vetex-ai-3` |
| 5 | Vetex AI4 | PDF brief review | ☐ | ☐ | `pdf-brief-vertex-ai-4` |
| 6 | Vetex AI5 | Revision review (vs original + brief) | ☐ | ☐ | `revision-vertex-ai-5` |

## Two minimal in-place edits per node

### Edit 1 — URL

`gemini-2.0-flash-001` → `gemini-2.5-flash`

The full URL becomes:
`https://us-central1-aiplatform.googleapis.com/v1/projects/overploy-video-storage/locations/us-central1/publishers/google/models/gemini-2.5-flash:generateContent`

### Edit 2 — Body

Inside the existing `generationConfig` block, change one number:

`"max_output_tokens": 8192` → `"max_output_tokens": 32768`

That's it. No new block, no schema changes. The existing block already has temperature/top_p/top_k; leave those alone.

## Later (separate day)

When you're ready to test, swap each prompt body for its matching `-DRAFT-v2` file (audit in `vertex-prompts-audit.md`). Those drafts already include the `generationConfig` block above, so the body-replace is one paste per node.
