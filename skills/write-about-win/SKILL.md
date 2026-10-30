---
name: write-about-win
description: Turn a recent win or achievement into a draft Entry post. Use when the owner shares good news, a project launch, or a milestone they want to write about.
---

# Write About a Win

Help the owner capture wins and achievements as Entry drafts.

## When to use

- The owner shares a project launch, milestone, or achievement
- They mention wanting to write about recent work
- They say something like "I should post about this"
- They want to document a win for their profile

## Instructions

Entry is draft-and-approve: you draft, the owner edits and publishes in Entry. Nothing goes live until they say so.

### Step 1: Gather context

If needed, use `get_entry_profile` to understand the owner's work and voice. Use `list_drafts` with `state: "published"` to see their past posts and match their style.

### Step 2: Create the draft

Use `create_draft` with:

- `title` - Clear, specific title
- `body` - The full post content in markdown
- `state` - Always `"working"` for a new draft
- Optionally `tags` - Relevant topic tags

Keep it concise and authentic. Match the owner's voice from their profile and past posts. Use markdown for formatting.

### Step 3: Refine if needed

If the owner wants changes, use `get_draft` to read the current version (including its `revision`), then `update_draft` with the revision and the updated `body` (send the complete updated text, not just the changed part).

### Step 4: Request publication

When the draft is ready, use `request_publication` with the draft ID and its current revision. Tell the owner the publication request is waiting in Entry, where they can review and publish it.

## Example

"I have created a draft post about your project launch. It is saved in your Entry writing studio. When you are ready, I can send it for your approval to publish."

## Remember

- New drafts start as `state: "working"` (private)
- Read the draft with `get_draft` before updating it
- Always pass the current `revision` when calling `update_draft`
- Use `request_publication` to ask the owner to publish
- The owner reviews and publishes in Entry, not in chat
- Nothing goes live without their approval
