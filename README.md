# Postbox Services - Email Deliverability & Security Tools (MCP server)

[![Postbox Services MCP connector](https://glama.ai/mcp/connectors/com.postboxservices/postbox-tools/badges/score.svg)](https://glama.ai/mcp/connectors/com.postboxservices/postbox-tools)

A free, open-access [MCP](https://modelcontextprotocol.io/) server that lets AI assistants run **real email deliverability and security checks** - live DNS, real blacklist queries, actual SMTP analysis - instead of guessing from training data.

**Server URL:**

```
https://mcp.postboxservices.com/mcp
```

- Transport: Streamable HTTP - Authentication: none (open access, fair-use limits)
- Official registry: [`com.postboxservices/postbox-tools`](https://registry.modelcontextprotocol.io/v0/servers?search=postbox)
- Setup guides with screenshots (claude.ai, Claude Desktop, Claude Code, ChatGPT, Grok, Cursor): **https://postboxservices.com/mcp/**
- MCP Server Card: https://mcp.postboxservices.com/.well-known/mcp.json
- See it in action: [8 real examples from ChatGPT, Claude and Grok, with screenshots](https://postboxservices.com/blogs/post/email-deliverability-checks-from-your-ai/)

## The 8 tools

| Tool | What it does |
|---|---|
| `check_blacklist` | Domain or IP against 24 DNS blacklists (Spamhaus ZEN, Barracuda, SpamCop and more) |
| `check_spoofability` | Spoofing / BEC exposure grade (A-F) from public DNS: SPF, DMARC policy strength, live lookalike domains |
| `trace_redirect` | Follows a URL through every redirect hop to its real destination, with phishing flags |
| `create_mailtest` | Two-step email spam test, step 1: mints a disposable address - you send a real email to it |
| `get_mailtest_result` | Two-step test, step 2: the /10 score, per-category breakdown and action plan |
| `analyze_eml` | Analyzes a raw .eml file (headers + content) when you cannot send a live email |
| `get_domain_age` | Registration date and age of a domain |
| `whois_lookup` | Registrar, created/expires dates, nameservers, DNSSEC, status flags |

## Try these prompts

- "Is acme.com on any email blacklists?"
- "Could someone send phishing emails pretending to be acme.com? Grade it."
- "Where does this shortened link actually go: https://bit.ly/xyz"
- "Run a spam test for my newsletter setup"

Each of these, and four more, is walked through with a screenshot in [8 real examples](https://postboxservices.com/blogs/post/email-deliverability-checks-from-your-ai/): blacklist check, spoofing grade, redirect trace, full spam test, bounce diagnosis, domain age and WHOIS.

## Quick install

**Claude Code**

```
claude mcp add --transport http postbox-tools https://mcp.postboxservices.com/mcp
```

**claude.ai / Claude Desktop:** Settings -> Connectors -> Add custom connector -> paste the URL (No sign-in).

**Cursor** (`~/.cursor/mcp.json`):

```json
{ "mcpServers": { "postbox-tools": { "url": "https://mcp.postboxservices.com/mcp" } } }
```

**ChatGPT (web):** Plugins -> Add MCP server -> **Create MCP App** -> paste the URL, set Authentication to **No authentication** (it defaults to OAuth). Name it `postbox_tools` in your prompt for reliable invocation.

**Grok:** Settings -> Connectors -> Custom Connector -> paste the URL.

Full walkthroughs with screenshots: https://postboxservices.com/mcp/

## Data handling

- Email files (`analyze_eml`) are processed in memory and never stored.
- Test reports live 30 days at a private link, then are permanently deleted.
- Domain/IP/URL results are cached up to 24 hours, keyed only by the input.
- Logs hold request metadata (IP, tool, timestamps), never message content.
- No accounts, no API keys, no stored conversations. URL tracing is SSRF-hardened and runs on isolated infrastructure.

## About

Built and run by [Postbox Consultancy Services](https://postboxservices.com/) - an email deliverability consultancy. The server is a thin wrapper over the same engines that power our [free web tools](https://postboxservices.com/tools). Fair-use limits protect the free service; for legitimate bulk needs, [talk to us](https://postboxservices.com/contact).
