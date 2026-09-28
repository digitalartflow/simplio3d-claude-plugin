---
name: simplio3d-help
description: Answer questions about how Simplio3D works using the official Simplio3D documentation. Use when the user asks how to do something in Simplio3D, whether Simplio3D can do something, where a Simplio3D setting or feature is, what a Simplio3D option block, pricing block, workflow, plan or integration does, or asks about the Simplio3D API, SDK or MCP connector.
---

# Simplio3D help from the official documentation

Answer from Simplio3D's published documentation, not from memory. Simplio3D changes often, and a confident answer about a menu or setting that doesn't exist sends the user hunting for nothing.

## Search, then read

1. `search_documentation` with 2–4 distinctive keywords. Every word must appear in a section, so fewer words find more: "conditional logic hide", "shopify checkout", "pricing formula".
   - Nothing found: drop a word or use a synonym and search again.
   - Restrict with `page` when the question is clearly about one area: `tutorials`, `api`, `sdk`, `mcp` or `changelog`.
2. `get_documentation_section` with the result's `url` for the full text when the snippet isn't enough.

These tools only need the "docs" permission and read no workspace data.

## Answer

- Give the answer in plain steps, using the menu names from the documentation.
- Cite the page as a full link: `https://app.simplio3d.ai` followed by the result's `url` (for example `https://app.simplio3d.ai/docs/tutorials/conditional-logic`).
- If the documentation doesn't cover it, say so. Don't fill the gap with a guess. Point the user to Simplio3D support: https://www.simplio3d.com/contact-us
- If the question is about their own project ("how do I hide the armrest in my chair configurator?"), answer from the docs and offer to do it for them (configurator-authoring skill).

## Search terms that work

| Topic | Search for |
|---|---|
| Option blocks | the block's name, such as "select material" or "number input" |
| Conditional logic | "conditional logic hide" |
| Pricing | "pricing formula", "price table" |
| Materials | "creating materials" |
| Modular | "modular snap" |
| Sharing and embedding | "share embed" |
| AR | "augmented reality" |
| Shopify / WooCommerce | "shopify checkout", "woocommerce" |
| Plans and trial | "trial billing" |
| AI workflows and connections | "AI workflows", "AI connections" |
| What's new | any topic with `page: changelog` |
