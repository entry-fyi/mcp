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

Use `create_draft` with the `entryId` from `list_entries` and:

- `title` - Clear, specific title
- `body` - The full post content, in Entry's Markdown (below)
- Optionally `dek` - One line under the title
- Optionally `topics` - Up to 3 topics

A new draft is always private (`working`); there is no state to set. Keep it concise and authentic, and match the owner's voice from their profile and past posts.

The body is Entry's own Markdown: `## ` headings (one level), `- ` and `1. ` lists, `> ` quotes, `*italic*`, `**bold**`, `` `code` ``, `[links](https://…)`, `[^1]` notes and fenced code blocks. Anything else (images, tables, `###`) shows as plain text. When the win involved a prompt the owner wants to share, put it in a **prompt block**, a fenced block whose language is `prompt`; Entry shows it labelled, wrapped and with a Copy button for readers:

````markdown
```prompt
Summarise this week's customer calls and list the three requests that came up most.
```
````

### Step 3: Refine if needed

If the owner wants changes, use `get_draft` to read the current version (including its `revision`), then `update_draft` with the revision and the updated `body` (send the complete updated text, not just the changed part).

### Step 4: Request publication

When the draft is ready, use `request_publication` with the draft ID and its current revision. Tell the owner the publication request is waiting in Entry, where they can review and publish it.

## Example

"I have created a draft post about your project launch. It is saved in your Entry writing studio. When you are ready, I can send it for your approval to publish."

## Remember

- New drafts are always private until the owner publishes them
- Read the draft with `get_draft` before updating it
- Always pass the current `revision` when calling `update_draft`
- Use `request_publication` to ask the owner to publish
- The owner reviews and publishes in Entry, not in chat
- Nothing goes live without their approval
