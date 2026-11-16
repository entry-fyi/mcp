---
name: keep-profile-fresh
description: Keep an Entry profile current by reading it, proposing updates, and guiding the owner through approval. Use when the owner wants to refresh their profile or mentions changes to their headline, bio, location, links, or availability.
---

# Keep Profile Fresh

Help the owner keep their Entry profile accurate and current.

## When to use

- The owner mentions updating their profile
- They share new information about their role, location, or work
- They want to refresh their headline or bio
- They mention availability changes

## Instructions

Entry is draft-and-approve: you propose, the owner approves in Entry. Nothing goes live until they say so.

### Step 1: Read first

Use `list_entries` to get the Entry ID, then `get_entry_profile` to read the current profile. This shows the profile as the owner sees it, including unpublished fields.

### Step 2: Propose changes

Use `propose_profile_update` with the `entryId` and a `changes` object holding only the fields that should change, with their new values. You can change:

- `name` - Full name (at most 80 characters)
- `headline` - Short professional headline (at most 120 characters)
- `bio` - Longer bio, as plain text, not Markdown (at most 1,000 characters)
- `location` - Where they are based (at most 80 characters)
- `website` - Their website, as a full web address (at most 200 characters)
- `links` - A list of at most 8 links, each `{ "label": "...", "url": "https://..." }` (label at most 40 characters, address at most 200). The list replaces the current one, so read the current links first and send the whole list you want; an empty list removes them all.
- `availability` - `{ "status": "available" | "limited" | "unavailable", "note": "..." }` (note at most 60 characters), or `null` to clear it

A cleared text field is an empty string. Optionally add a short `note` to the owner saying why. Stay within the limits (the tool schema states them too), and be concise and professional.

### Step 3: Guide approval

Tell the owner the proposal is waiting in Entry: their dashboard shows it, and they approve or reject it in the profile editor, under "From your assistant", where they see exactly what would change. If their profile changes before they decide, the proposal goes stale; propose it again. Do not say it is live until they have approved it.

## Example

"I see your headline is currently 'Designer at ACME'. I have proposed updating it to 'Senior Product Designer at ACME' to reflect your promotion. You can approve it in Entry, in your profile editor under 'From your assistant'."

## Remember

- Always read the current profile first with `get_entry_profile`
- Only propose fields that need to change, but send `links` as the whole list
- The owner approves in Entry, not in chat
- Nothing goes live without their approval
