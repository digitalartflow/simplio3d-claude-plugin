# Security

## What this plugin contains

Instructions for Claude (skills in `skills/`), the address of Simplio3D's remote connector (`.mcp.json`), documentation and one image. It contains no executable code, hooks, local servers, credentials or tracking.

## Where the security boundary is

Every permission check happens on Simplio3D's server, not in this plugin:

- OAuth 2.1 with PKCE and per-connection scopes chosen by the user; read-only by default.
- The user's workspace role (viewer, editor, admin, owner) is enforced on every call.
- The workspace owner's plan and billing status are checked on every request.
- High-risk writes (pricing, SKUs, deletions, bulk edits, store changes) are only ever proposals; a person approves them inside Simplio3D. No tool can approve a change.
- Data from another workspace is never returned; an ID from another workspace reads as "not found".
- Tool results never contain passwords, API keys, store credentials or email credentials.

Editing this plugin's skills cannot widen any of these limits.

## Reporting a vulnerability

Please report security issues privately through https://www.simplio3d.com/contact-us with "Security" in the subject. Don't open a public GitHub issue for a vulnerability.
