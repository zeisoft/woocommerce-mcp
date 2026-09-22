<div align="center">

<img src="assets/cover.png" alt="WooCommerce through HeyMetra's MCP server" width="100%">

# WooCommerce &times; HeyMetra

**Orders, products and the store's own sales figures, from your own server.**

Your orders live in WooCommerce. What you spent to win them lives in your ad accounts. One question, both answers.

[![MCP Registry](https://img.shields.io/badge/MCP_Registry-com.heymetra%2Fheymetra-1f6feb)](https://registry.modelcontextprotocol.io/v0/servers/com.heymetra%2Fheymetra/versions)
[![Transport](https://img.shields.io/badge/transport-Streamable_HTTP-444)](https://modelcontextprotocol.io/)
[![Auth](https://img.shields.io/badge/auth-OAuth_2.1-444)](https://heymetra.com/security/)
[![Connector page](https://img.shields.io/badge/heymetra.com-woocommerce-1f6feb)](https://heymetra.com/connectors/woocommerce/)

```
https://mcp.heymetra.com/mcp
```

</div>

---

## Ask it things like

> How many orders did the store take this week?

> Which products sold most last month?

> Which products are out of stock or still unpublished?

> How do net sales this month compare with last month?

No dashboard, no export, no query language. You ask in the assistant you already use and the answer comes back with the account it came from.

## Connect WooCommerce

**1. Open the REST API screen in WordPress**

Sign in to the store's WordPress admin and go to WooCommerce → Settings → Advanced → REST API. The screen lists the keys the store has already issued, and has an Add key button.

> It is under WooCommerce, not under the WordPress Settings menu — WordPress has an unrelated Settings of its own, and there is no REST API tab in it.

**2. Add a key whose permission is Read**

Choose Add key, give it a description you will recognise later, pick a user who can see orders, and set Permissions to Read. Then Generate API key.

> Read is not only a precaution: it is what makes the store itself refuse a change, so nothing an assistant does can edit a product, a price or an order even if it tried. The key inherits the chosen user's rights, so a user who cannot see orders produces a key that cannot either.

**3. Copy the consumer key and the consumer secret**

Both appear once, on the screen that follows Generate. The consumer key starts with ck_ and the secret with cs_, so they cannot be confused with one another.

> Leaving that screen loses the secret for good — WordPress does not show it again, and the only remedy is to revoke the key and issue another.

**4. Paste the secret into HeyMetra**

Choose WooCommerce on the Connections screen and paste the consumer secret. It goes to the vault and is never shown again, here or anywhere else.

**5. Enter the store address exactly as the store answers**

https:// and the host, nothing after it. If the store answers at www.yourstore.com, type the www.; if it answers without it, leave it out. Saving checks the address and the key against the store immediately.

> HeyMetra does not follow a redirect from the address you give it — following one would let a store send us to an address nobody checked — so the wrong half of a www. pair fails rather than quietly working.

**6. Add HeyMetra to the assistant you use**

Claude, ChatGPT, Cursor or Codex — HeyMetra gives you the address and the key to paste. The orders, products and sales tools appear in that assistant once it connects.

## Then add HeyMetra to your assistant

Add HeyMetra once and it is there in every conversation. The address is the same everywhere:

```
https://mcp.heymetra.com/mcp
```

### One command

```bash
npx add-mcp https://mcp.heymetra.com/mcp
```

[`add-mcp`](https://www.npmjs.com/package/add-mcp) is a third-party installer that writes the configuration for Claude Code, Codex, Cursor, Antigravity, VS Code and seventeen other agents. It infers the name from the address, so the server lands as `heymetra`. Run against this endpoint before it was written here.

### Or by hand

<details>
<summary><b>Claude</b> — Settings → Customize → Connectors → Add custom connector</summary>

Paste the address above into Settings → Customize → Connectors → Add custom connector.

_On Team and Enterprise plans only an owner can add it, under Organization settings._

Full walkthrough: [heymetra.com/mcp/claude/](https://heymetra.com/mcp/claude/)
</details>

<details>
<summary><b>ChatGPT</b> — Settings → Security and login → Developer mode, then chatgpt.com/plugins</summary>

Paste the address above into Settings → Security and login → Developer mode, then chatgpt.com/plugins.

_The endpoint has to include its /mcp path here._

Full walkthrough: [heymetra.com/mcp/chatgpt/](https://heymetra.com/mcp/chatgpt/)
</details>

<details>
<summary><b>Grok</b> — grok.com/connectors → New Connector → Custom</summary>

Paste the address above into grok.com/connectors → New Connector → Custom.

_XAI calls this “bring your own MCP”._

Full walkthrough: [heymetra.com/mcp/grok/](https://heymetra.com/mcp/grok/)
</details>

<details>
<summary><b>Perplexity</b> — Settings → Connectors → Custom connector → Remote</summary>

Paste the address above into Settings → Connectors → Custom connector → Remote.

_Perplexity documents it as a Pro, Max and Enterprise feature._

Full walkthrough: [heymetra.com/mcp/perplexity/](https://heymetra.com/mcp/perplexity/)
</details>

<details>
<summary><b>Claude Code</b> — claude mcp add --transport http</summary>

```bash
claude mcp add --transport http heymetra https://mcp.heymetra.com/mcp
```

_Or a .mcp.json in the project root; /mcp inside a session shows what connected._

Full walkthrough: [heymetra.com/mcp/claude-code/](https://heymetra.com/mcp/claude-code/)
</details>

<details>
<summary><b>Codex</b> — ~/.codex/config.toml</summary>

```toml
[mcp_servers.heymetra]
url = "https://mcp.heymetra.com/mcp"
```

_Under an [mcp_servers.<name>] section, then codex mcp login._

Full walkthrough: [heymetra.com/mcp/codex/](https://heymetra.com/mcp/codex/)
</details>

<details>
<summary><b>Cursor</b> — ~/.cursor/mcp.json, or .cursor/mcp.json in a project</summary>

```json
{
  "mcpServers": {
    "heymetra": { "url": "https://mcp.heymetra.com/mcp" }
  }
}
```

_Leave the static OAuth fields empty — they exist for servers that cannot register themselves._

Full walkthrough: [heymetra.com/mcp/cursor/](https://heymetra.com/mcp/cursor/)
</details>

<details>
<summary><b>Antigravity</b> — ~/.gemini/config/mcp_config.json, or .agents/mcp_config.json in a project</summary>

```json
{
  "mcpServers": {
    "heymetra": { "serverUrl": "https://mcp.heymetra.com/mcp" }
  }
}
```

_The key is serverUrl, not url — the one every other JSON client spells differently._

Full walkthrough: [heymetra.com/mcp/antigravity/](https://heymetra.com/mcp/antigravity/)
</details>

## What it may and may not touch

Propose a change through this account's own API, for operations HeyMetra does not cover. Nothing is sent until you approve it, and HeyMetra cannot undo it afterwards.

Permissions are switched on per connection, and one you leave off is a tool your assistant never sees.

| Permission | What it covers | Changes anything? |
|---|---|---|
| **Direct API access** | Let your assistant use this account's own API for anything HeyMetra's other operations do not cover. It reads directly, and what comes back is the provider's own answer rather than a figure HeyMetra has checked. It can also propose changes — those are never applied until you approve them, and HeyMetra cannot undo one afterwards — WooCommerce's sales report reads the older order tables, so a store on the newer storage (HPOS) with compatibility mode off reports nothing sold however much it sold. HeyMetra adds the orders up itself when that happens, counting them the way WooCommerce does, and says in the answer that it did.. | Yes — every change waits for your approval |

<details>
<summary>What each permission lets an assistant do, in full</summary>

- Ask this account's own API a question HeyMetra's other operations do not cover. Reads only, and the answer is the provider's own rather than a figure HeyMetra has checked.
- Propose a change through this account's own API, for operations HeyMetra does not cover. Nothing is sent until you approve it, and HeyMetra cannot undo it afterwards.
</details>

Anything that would change something comes back as a proposal you approve, inside bounds that live in code rather than in a prompt: ±50% on a budget, 5 campaigns per action and 20 changes a rolling day, and an approval that expires after 30 minutes. [How that works](https://heymetra.com/security/).

## When something goes wrong

<details>
<summary>Saving fails and the answer says the store redirected the request.</summary>

**Why:** The address on the connection is one the store redirects away from — almost always a www. that belongs, or one that does not. Measured on a live store: the www. form answers 301 and names the address that works.

**Fix:** The message names the address the store redirected to. Put that one on the connection, without the path, and save again.

</details>

<details>
<summary>Saving fails with a login error and both values were copied carefully.</summary>

**Why:** WooCommerce answers a wrong key and a missing key with the same error, so its own message cannot tell you which half is at fault. The usual cause is the secret: it is shown once, and a copy that caught a trailing space or missed a character looks right.

**Fix:** Revoke the key on the REST API screen and issue a new one, copying both values in one sitting. Nothing was stored, so there is nothing to undo.

</details>

<details>
<summary>Saving fails and the store's own /wp-json address opens a 404 page in a browser.</summary>

**Why:** WordPress permalinks are set to Plain. The REST API is reachable at a query-string address in that mode, which is not the address any client uses.

**Fix:** In WordPress, Settings → Permalinks, choose anything other than Plain and save. The setting affects the whole site, so check the store's pages still open as expected.

</details>

<details>
<summary>The connection saves, and an assistant reports no orders for a period you know you sold in.</summary>

**Why:** The period genuinely holds none. Unlike a marketplace, WooCommerce keeps the store's whole history, so an empty answer here is the store's answer rather than a retention limit.

**Fix:** Ask about a wider period. If the store's own Orders screen shows rows in the same dates, check the key's user can see orders — a key made for a customer account reads none.

</details>

<details>
<summary>The sales figures arrive with a note saying HeyMetra added the orders up because the store's own report could not.</summary>

**Why:** The store keeps orders in WooCommerce's newer storage (HPOS) with compatibility mode off. The sales report reads the older tables, which nothing writes to any more, so it reports nothing sold — measured on a live 9.4.5 store, for a whole year it had sold in.

**Fix:** Nothing needs fixing for the figures to be right: they are counted the way WooCommerce counts them — completed, processing and on-hold orders, net being gross less tax and shipping. To have the store's own report answer again, turn on WooCommerce → Settings → Advanced → Features → compatibility mode; it fills the old tables from the new ones from that point on, so figures from before it was turned on stay missing there.

</details>

<details>
<summary>The connection worked and now every question fails to reach the store.</summary>

**Why:** A security plugin or the host's firewall is blocking /wp-json, which several of them do by default after an update.

**Fix:** Allow /wp-json in the plugin's settings, or allow HeyMetra's address. Opening the store's /wp-json in a browser shows whether the block is there rather than in the credential.

</details>

## What HeyMetra reads from WooCommerce

Connect with a REST key whose permission is Read and your MCP client gets three tools: orders for a period with status, items and totals; products with names, SKUs, prices, stock and whether each is published; and WooCommerce's own sales report — gross and net sales, orders, items and refunds, as the store computes them. Stores on the newer order storage have a sales report that cannot see their own orders; there HeyMetra adds the orders up the way WooCommerce would and says so in the answer, rather than reporting the store's zero. A Read key cannot change a product, a price or an order.

<details>
<summary>About WooCommerce</summary>

WooCommerce is the open-source store that runs on your own WordPress site — products, orders, customers, and checkout. Because it is self-hosted, your sales data stays on your server rather than a vendor's.
</details>

## One connection, not seven

The reason to read WooCommerce through HeyMetra rather than through a server that only knows WooCommerce is everything else it can answer in the same breath:

**Ads** — [Google Ads](https://heymetra.com/connectors/google-ads/) · [Meta](https://heymetra.com/connectors/meta-ads/)

**Analytics** — [Google Analytics 4](https://heymetra.com/connectors/google-analytics-4/) · [Google Search Console](https://github.com/zeisoft/google-search-console-mcp)

**Ecommerce** — [Shopify](https://heymetra.com/connectors/shopify/) · [Trendyol](https://github.com/zeisoft/trendyol-mcp) · **WooCommerce**

**Revenue & CRM** — [Stripe](https://heymetra.com/connectors/stripe/) · [HubSpot](https://heymetra.com/connectors/hubspot/) · [Zoho CRM](https://github.com/zeisoft/zoho-crm-mcp) · [Zoho SalesIQ](https://github.com/zeisoft/zoho-salesiq-mcp) · [Zoho Marketing Automation](https://github.com/zeisoft/zoho-marketing-automation-mcp)

**Mobile** — [AppsFlyer](https://github.com/zeisoft/appsflyer-mcp) · [RevenueCat](https://heymetra.com/connectors/revenuecat/) · [Adapty](https://github.com/zeisoft/adapty-mcp) · [App Store Connect](https://github.com/zeisoft/app-store-connect-mcp)

**Channels** — [Slack](https://github.com/zeisoft/slack-mcp) · [Telegram](https://github.com/zeisoft/telegram-mcp)

The full catalogue is at [heymetra.com/connectors/](https://heymetra.com/connectors/).

## Links

- [WooCommerce connector page](https://heymetra.com/connectors/woocommerce/)
- [HeyMetra](https://heymetra.com/) — what the product is
- [Setup for every assistant](https://heymetra.com/mcp/)
- [Security and limits](https://heymetra.com/security/)
- [Pricing](https://heymetra.com/pricing/)
- [HeyMetra's own repository](https://github.com/zeisoft/heymetra-mcp)

---

<sub>Built by <a href="https://zeisoft.com">Zeisoft</a>, who make HeyMetra. Not affiliated with WooCommerce. This README is generated from HeyMetra's live connector catalogue and refreshed daily; corrections are welcome as issues.</sub>
