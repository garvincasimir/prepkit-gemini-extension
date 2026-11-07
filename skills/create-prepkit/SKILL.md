---
name: create-prepkit
description: Create, validate, suggest, revise, or submit a portable KitML learning package to the learner's PrepKit account. Use when the learner asks Gemini to build a course, study plan, practice kit, or PrepKit, or asks what they should learn next.
---

# Create a PrepKit

Use Gemini's current model access and tools to design the content. PrepKit stores, reviews, presents, tracks, and schedules the finished learning kit. Never send Google credentials, hidden prompts, private reasoning, or unrelated conversation history to PrepKit.

## Workflow

1. Call `get_kitml_contract` and follow the returned schemas, limits, passive-file rules, and consent rules.
2. When the learner provides a PrepKit brief ID, call `get_learning_brief`. Use only that approved brief as PrepKit account context.
3. Establish the goal, current level, time budget, and observable outcome from the conversation or approved brief.
4. Research with Gemini's available tools when accuracy or freshness requires it. Record only opened sources in `provenance.json`.
5. Create `manifest.json`, `kit.prepml.xml`, and `provenance.json`, then package deterministic bytes as `.kitml.zip`.
6. Call `validate_kitml`. Correct every finding and validate again.
7. Call `submit_private_kit` only with a live upload grant created by the learner. Use a stable idempotency key and report the result as waiting for review.
8. Call `get_submission` for status. Only the learner accepts or rejects the package inside PrepKit.

For revisions, preserve `packageId`, increment `revision`, create a new `releaseId`, and set the accepted predecessor hash. For background suggestions, call `suggest_private_kit` with a short topic and reason only. Never create or upload suggestion content before the learner requests it.

Do not include scripts, HTML, SVG, PDF, executable content, secrets, or remote embeds. Do not describe PrepKit as paying for or reselling Gemini usage.

## Text-only authoring without archive tools

When `get_kitml_contract` advertises source-form tools, prefer `validate_kitml_source` for text-only kits. Supply `manifest`, `prepml`, and `provenance` exactly as described by that contract. PrepKit derives the content hashes and ZIP bytes; do not invent base64 or include derived `assets` and `contentHashes` fields in the source manifest. Correct validation findings before calling `submit_private_kit_source` with the same source, learner-created upload grant and stable idempotency key. Submission still waits for learner review. Revisions also require the revision permission and accepted predecessor hash.

Keep the archive workflow for allowed media or an older server without source tools. If the host cannot construct deterministic archive bytes and source tools are unavailable, explain the limitation instead of fabricating a package. These tools package authored content; all inference remains in the chosen host account.
