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

Use `propose_profile_update` with the Entry ID and only the fields that should change. You can update:

- `name` - Full name
- `headline` - Short professional headline
- `bio` - Longer bio (markdown supported)
- `location` - City, region, or remote
- `availability` - Current availability status
- `links` - Array of URLs (personal site, social profiles, etc.)

Keep within Entry's field limits (check the tool schema). Be concise and professional.

### Step 3: Guide approval

Tell the owner the proposal is waiting in Entry under Settings → Integrations. They review exactly what would change and approve or reject it. Do not claim it is published until they confirm.

## Example

"I see your headline is currently 'Designer at ACME'. I have proposed updating it to 'Senior Product Designer at ACME' to reflect your promotion. Check Entry under Settings → Integrations to approve the change."

## Remember

- Always read the current profile first with `get_entry_profile`
- Only propose fields that need to change
- The owner approves in Entry, not in chat
- Nothing goes live without their approval
