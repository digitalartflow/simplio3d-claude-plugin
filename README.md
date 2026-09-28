<img src="assets/simplio3d-icon.png" alt="Simplio3D" width="72" height="72">

# Simplio3D for Claude

Work with your real [Simplio3D](https://www.simplio3d.com) 3D product configurators from Claude. Ask Claude to audit a configurator before it goes live, explain why an option is hidden, calculate what a configuration costs, add a material option, or check whether a project is ready to publish. Claude reads your actual projects through Simplio3D's official connector and follows Simplio3D's own approval rules for anything that touches prices.

This plugin is published by Simplio3D. It packages the Simplio3D connector with skills that teach Claude how to use it well.

## What you can ask

- "Show me my Simplio3D projects."
- "Audit my closet configurator and tell me what's broken."
- "Find broken option references in the shoe configurator."
- "Why is the Leather option hidden when I pick the Standard frame?"
- "Explain how the window configurator is priced."
- "What does the chair cost in Walnut with armrests?"
- "Which priced options are missing SKUs?"
- "Add Oak, Walnut and Black as upholstery options."
- "Only show the Footrest option when the Deluxe frame is selected."
- "Is the jersey configurator ready to publish?"
- "How do I embed a configurator on my Shopify store?"
- "Help me set up a modular shelving configurator."

You don't need to know tool names, project IDs or block IDs. Refer to projects, options and materials by the names you see in Simplio3D.

## Skills

| Skill | What it does |
|---|---|
| Workspace navigation | Finds projects, options, materials and 3D models by name, and explains connection, permission and subscription messages. |
| Configurator audit | Health-checks a project: 3D targets, options, rules, materials, pricing, SKUs and forms, with a plain-language fix for each finding. Explains why an option is hidden. |
| Configurator authoring | Adds and edits option blocks, variants, conditional rules, 3D part visibility, resizing number inputs and modular (snap-together) modules. Always inspects the real model first and never guesses 3D part names. |
| Pricing and CPQ | Explains pricing blocks and formulas, calculates prices with Simplio3D's server engine, finds missing SKUs, and proposes price or SKU changes for your approval. |
| Materials | Finds and reuses library materials, imports curated or free materials, creates new ones and assigns them to the right 3D parts. |
| Publish readiness | Produces a Ready / Ready with warnings / Not ready verdict with a to-do list. It never publishes. |
| Simplio3D help | Answers product questions from the official Simplio3D documentation and links the page it used. |

## Requirements

- A Simplio3D account on any plan (Starter, Pro or Enterprise) or an active 30-day trial.
- Claude on the web, desktop, mobile or Cowork, or Claude Code.

## Connect your account

The plugin uses Simplio3D's remote connector at `https://app.simplio3d.ai/mcp`. Sign-in uses OAuth: you sign in on app.simplio3d.ai, pick a workspace and approve the permissions. The plugin contains no API keys or passwords, and you never paste a token into Claude.

- **Claude (web, desktop, mobile, Cowork):** install the plugin from **Customize → Plugins**, open its **Connectors** tab and connect **Simplio3D**. If you already added the Simplio3D connector from the directory, the plugin uses that same connection.
- **Claude Code:** `claude plugin marketplace add digitalartflow/simplio3d-claude-plugin`, then `claude plugin install simplio3d@simplio3d`. Start a session, run `/mcp`, select **simplio3d** and choose **Authenticate**.

## Permissions

Sign-in asks for **read-only** access by default. You choose on Simplio3D's consent screen whether to also allow changes, one area at a time, and you can revoke or narrow access at any time in Simplio3D → Dashboard → Integrations → AI Connections.

| Area | Read (default) | Write (opt-in) |
|---|---|---|
| Workspace | Account, plan, billing status, seats | None |
| Projects | Projects, settings, 3D structure, health, sharing status | Create, rename, duplicate; project settings; move and rename 3D parts; quote-request status |
| 3D assets | Asset library and model structure | None (uploads stay in the app) |
| Materials | Materials library and categories | Create, import and assign materials |
| Configurator | Option blocks, variants, rules, animations | Create and edit options, variants, rules, modules |
| Pricing | Pricing blocks, formulas, price calculation | Proposes price, SKU and formula changes, each approved by you in Simplio3D |
| Forms | Quote and checkout form fields | Create and edit form fields |
| Quote requests | Opt-in only: customer leads and email activity | None |
| Store | Opt-in only: store connection and product list | Proposes a product link or checkout mode, approved by you in Simplio3D |
| Workflows | Progress of multi-step AI jobs | Start, answer, pause or cancel them |
| Documentation | Official Simplio3D docs | None |

## How changes stay safe

- **Proposals, not surprises.** Price, SKU, deletion, bulk and store changes are never applied by Claude. They become a proposed change you review and approve in Simplio3D (Dashboard → AI Changes). Claude has no tool that can approve one.
- **Claude asks first.** Tools that change or remove existing data are marked so Claude asks before running them.
- **Undo.** Most applied edits can be undone from Dashboard → AI Changes.
- **Checked against your model.** 3D part names are verified against the actual model file, so Claude can't target a part that doesn't exist.
- **Out of reach.** Publishing, connecting a store, emailing customers, uploading files, passwords, API keys and store or email credentials are not available to Claude at all.
- **Your role applies.** A team member with a viewer seat can only read, whatever they approve on the consent screen.

## Data and privacy

What the plugin runs, sends and fetches:

- **Runs:** nothing on your computer. The plugin contains only instructions (skills) and the connector address. It has no scripts, hooks or local servers.
- **Sends:** when Claude uses a Simplio3D tool, the tool name and its arguments (for example a project ID or a new price) go to `app.simplio3d.ai`, which is Simplio3D's own service. Nothing else from your conversation is sent.
- **Fetches:** results from your own Simplio3D workspace. When you ask for free textures, Simplio3D fetches them from public texture libraries (ambientCG, CGBookcase, Pixabay). When you ask about your store, Simplio3D reads your connected Shopify or WooCommerce store.
- **Stored by Simplio3D:** the changes you make, as in the app, and a 30-day log of tool calls (tool name, account, workspace, time and outcome; argument names but not their values).

Details: [privacy and data handling](https://app.simplio3d.ai/docs/mcp/privacy-data-handling) · [Simplio3D privacy policy](https://www.simplio3d.com/privacy-policy).

## Limitations

- Prices from Claude come from Simplio3D's server calculation. It doesn't evaluate every rule the live configurator does, and says so when that matters. The live Preview is the final word.
- File uploads (3D models, images, price catalogues), publishing and store connections happen in the Simplio3D app.
- Modular snap connections are authored when you tell Claude which faces connect; Claude won't infer them from shapes.
- Results reflect saved data. Changes you haven't saved in the editor aren't visible yet.

## Support and documentation

- Connector and tool reference: https://app.simplio3d.ai/docs/mcp
- Tutorials: https://app.simplio3d.ai/docs/tutorials
- Support: https://www.simplio3d.com/contact-us
- Security reports: see [SECURITY.md](SECURITY.md)

## License

MIT. See [LICENSE](LICENSE).
