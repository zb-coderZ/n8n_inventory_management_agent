# Inventory Management Agent (n8n)

An AI-powered inventory management assistant built with n8n, Google Sheets, and Google Gemini. Interact via chat to check stock, list low-stock items, add new products, and update stock levels — with confirmation before any write action.

## Overview

This workflow turns a Google Sheet into a conversational inventory system. A user chats with an AI Agent (Gemini) that reads/writes inventory data through a set of Google Sheets tools, handles product names case-insensitively, and always confirms before making changes.

## Architecture

```
n8n Chat Trigger
      │
      ▼
Google Gemini AI Agent
      │
      ├── Tool: Get Stock Level
      ├── Tool: List Low Stock
      ├── Tool: Add New Product
      └── Tool: Update Stock
      │
      ▼
Google Sheets (Inventory_DB)
```

## Components

| Component | Role |
|---|---|
| **n8n Chat Trigger** | Entry point for user messages |
| **Google Gemini (AI Agent)** | Understands intent, decides which tool to call, drafts responses |
| **Inventory_DB (Google Sheets)** | Single source of truth for stock data |
| **Get Stock Level** | Returns current quantity for a given product |
| **List Low Stock** | Returns all products below their reorder threshold |
| **Add New Product** | Adds a new row/product to the sheet |
| **Update Stock** | Updates quantity for an existing product |

## Features

- **Conversational interface** — no forms, just chat
- **Case-insensitive product matching** — "iphone case" matches "iPhone Case"
- **Confirmation-before-update** — the agent confirms details with the user before writing changes to the sheet (prevents accidental edits)
- **Low-stock alerts** — ask the agent to list items below threshold at any time

## Setup

1. **Google Sheets** — Create an `Inventory_DB` sheet with columns for product name, quantity, and reorder threshold (adjust to your schema).
2. **Credentials** — Connect your Google Sheets OAuth credential and Google Gemini API credential in n8n.
3. **Import the workflow** — Import the `.json` workflow file into your n8n instance.
4. **Configure the four tool nodes** — Point each Google Sheets tool node to your `Inventory_DB` sheet and correct tab.
5. **Activate** — Publish/activate the workflow and open the Chat Trigger URL to start using it.

## Usage Examples

- "What's the stock level for iPhone Case?"
- "Show me all low stock items"
- "Add a new product: Wireless Mouse, 50 units, reorder at 10"
- "Update stock for Wireless Mouse to 35"

## Known Limitations / Roadmap

- **WhatsApp integration** — Attempted via a local Docker tunnel but blocked by Meta verification issues. Planned to be added later via n8n Cloud for direct WhatsApp access.
- Currently accessible only through the n8n chat interface (not yet multi-channel).

## Tech Stack

- n8n (workflow automation)
- Google Gemini (LLM / AI Agent)
- Google Sheets (data store)

## Author

Built by **Zohaib Zulfiqar** 