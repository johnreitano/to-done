# To-Done

## Description

To-Done is a to do application with basic features for its free plan and more advanced features for its paid plan.

## Basic Features (Free Plan)

- each item has these fields: title (required), description, deadline, assignee
- Description allows rich text
- Show items as list vs show items as cards
- Share items with others via links with opengraph info

## Advanced Features (Paid Plan)

- Allows lists of items to be shared with another account
- Sends reminders
- AI assistance for creating items


## Tech Stack

- Next.js
- Supabase
- Stripe
- Radix UI
- Open AI SDK

## Demo

Install agent-os 
```bash
clear && cd ~ && rm -rf ~/agent-os
curl -sSL https://raw.githubusercontent.com/johnreitano/agent-os/main/scripts/base-install.sh 
```

Install agent-os in project
```bash
~/agent-os/scripts/project-install.sh \
    --claude-code-commands true \
    --standards-as-claude-code-skills true \
    --agent-os-commands true \
```
