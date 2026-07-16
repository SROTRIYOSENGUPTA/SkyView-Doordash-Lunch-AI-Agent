---
name: lunch-order
description: Collect group lunch orders and place them on DoorDash via browser automation. Use when the user says "collect lunch orders", "order lunch", "place our lunch order", "lunch order from Teams", or any variation of group lunch ordering from DoorDash.
---

# Lunch Order

Delegate this entire task to the **lunch-order-agent** subagent (via the Agent tool). Pass along everything the user provided: the orders (pasted text or a pointer to a Teams chat), the restaurant, and the DoorDash Group Order link (`https://drd.sh/cart/...`) if given.

The agent handles the full workflow itself:

1. Collects orders from Microsoft Teams chat (or parses pasted text)
2. Presents the parsed order table for user confirmation
3. Opens the DoorDash Group Order link in Chrome and builds the cart via its pure-JavaScript protocol
4. Presents the cart summary and **stops for explicit user confirmation before any checkout step**

Do not drive the browser yourself from this skill — the agent definition contains the validated DoorDash automation protocol (scroll pacing, lazy-load handling, batching, error recovery) and must be the one doing it.

If the `lunch-order-agent` agent type is not available, tell the user to install `lunch-order-agent.md` into `~/.claude/agents/` and restart Claude Code.

## Hard rules (apply even if the agent is unavailable)

- Never click "Place Order" or submit payment. Cart building only; checkout is always done by the user.
- Never enter payment details, addresses, or credentials.
- If DoorDash shows a login wall or CAPTCHA, pause and ask the user to resolve it in the browser.
