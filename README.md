# AdPlug for Grok Bot and Cursor

AdPlug is a hosted MCP server that safely connects Google Ads, LinkedIn Ads and Microsoft Ads to Grok Bot and Cursor.

Your agent can check campaigns, flag what needs attention and, on a paid plan, make the changes you approve.

The plugin adds one remote MCP server, `https://api.adplug.app/mcp`, and nothing else. There's no code, no script and no hook in it.

## Install in Grok Bot

1. Open **Connect apps** in the sidebar. On your phone, tap your avatar at the top left, then **Connect apps**.
2. Find **AdPlug** and click **Add**.
3. Click **Authenticate** (it says **Authorize** on the phone).
4. Sign in to AdPlug, or create a free account, and click **Approve**. The approval screen says "Cursor wants to access your AdPlug account". That's expected: Grok Bot connects apps through Cursor.

AdPlug then shows as connected.

You can also add AdPlug from a chat. Send your Bot this message:

> Add a custom MCP server called AdPlug at https://api.adplug.app/mcp

Click **Authorize** on the card it posts, then **Continue**, then sign in to AdPlug in the browser tab that opens and click **Approve**. The [Google Ads and Grok Bot guide](https://adplug.app/guides/google-ads-grok-bot) walks through this route with screenshots, using AdPlug's Google Ads address.

## Install in Cursor

Run `/add-plugin adplug` in a chat, or install AdPlug from the Cursor Marketplace.

To set it up by hand, add `https://api.adplug.app/mcp` as a server in Cursor's MCP settings, or put this in `.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "adplug": {
      "url": "https://api.adplug.app/mcp"
    }
  }
}
```

The first time you connect, a browser tab opens on AdPlug's sign-in. Sign in, or create a free account, and click **Approve**.

## What you need

- An AdPlug account. The free plan connects one ad platform, comes with a monthly request limit and is view only: your agent can read your accounts and preview changes, but not apply them. A paid plan connects all three and lets the agent make changes: see [adplug.app/pricing](https://adplug.app/pricing).
- Your ad accounts connected once in AdPlug, at [adplug.app/dashboard/connections](https://adplug.app/dashboard/connections), each with the platform's own sign-in (Google, LinkedIn or Microsoft).

There's no API key or client ID to set up. Sign-in is OAuth 2.1 with dynamic client registration and PKCE.

## What your agent can do

Ask in plain words and the agent pulls the numbers itself (no exports, no CSVs, no clicking six levels deep to find one number).

### Google Ads

- **Reads:** every account under a manager (MCC) account. Account, campaign, ad, keyword, bidding-strategy and Shopping product performance. Day-by-day trends and conversions by action. Search terms, Dynamic Search Ads included. Shared negative keyword lists, keyword ideas and search volumes from Keyword Planner, Google's own Recommendations, and any custom GAQL report.
- **Changes:** pause, enable and remove. Budgets and bids. Negative keywords at campaign or shared-list level. New campaigns, ad groups, ads and assets. Apply or dismiss Google's Recommendations.

### LinkedIn Ads

- **Reads:** campaign, creative, daily, conversion, lead gen form, demographic and reach reports. Campaigns, ad sets, ads, conversions, lead forms and matched audiences. Targeting search for job titles, companies and skills, with audience size. LinkedIn's public Ad Library, to look up a competitor's ads.
- **Changes:** create and edit campaigns, ad sets and ads (campaign groups, campaigns and creatives in LinkedIn's API). Send conversions through LinkedIn's Conversions API.

### Microsoft Ads (formerly Bing Ads)

- **Reads:** reports by account, campaign, ad group, ad, keyword, search query, location, and age and gender. Professional demographics (LinkedIn company, industry and job function), share of voice (auction insights), audience, conversion and change history reports. Campaigns, ad groups, ads, keywords, budgets, negative keyword lists, audiences, UET tags, conversion goals, Microsoft's recommendations and its scheduled Google Ads imports. Keyword research and bulk download.
- **Changes:** around 90 change operations, including appealing disapproved ads, plus bulk upload.

`adplug_get_status` tells the agent which platforms you've connected and what your plan allows.

AdPlug's HubSpot and Google Search Console connectors aren't part of this plugin. They have their own addresses (`https://api.adplug.app/mcp/hubspot` and `https://api.adplug.app/mcp/google-search-console`), and you set them up from your AdPlug dashboard.

## Example prompts

- **Google Ads:** "Check my Google Ads performance for the last 30 days, put together a performance snapshot, and come back with insights and recommendations on what needs my attention."
- **LinkedIn Ads:** "Which LinkedIn campaigns aren't spending their budget, and why: bid, audience size or ads? Show me the fixes as a preview."
- **Microsoft Ads:** "Compare my Microsoft Ads campaigns for the last 7 days against the previous 7. Flag the biggest spend and CPA movers, and tell me where I'm losing impression share to budget versus rank."
- **Google Ads to Microsoft Ads** (needs a paid plan, with both platforms connected): "Copy my best Google Ads Search campaign into Microsoft Ads, paused, and show me the plan before anything is created."
- **LinkedIn competitor research:** "Search the LinkedIn Ad Library for our top competitor and list their active ads with links. Summarise what they seem to be testing."

## How changes are kept safe

Most of AdPlug's change tools come in pairs: a preview, which shows the exact change without making it, and an execute, which makes it.

- **Google Ads:** AdPlug's server refuses a change that wasn't previewed first. The execute tool needs the preview's ID.
- **LinkedIn Ads and Microsoft Ads:** the execute tool takes the same change as the preview, and AdPlug's tool descriptions tell the agent to preview first. That's an instruction to the agent, not a block on the server.
- **Two tools have no preview step:** Microsoft Ads bulk upload, whose description tells the agent to show you the file first, and LinkedIn's Conversions API upload, which sends conversion events.
- New campaigns start paused (as drafts on LinkedIn Ads), and so do most new ads. On Google Ads, a new Dynamic Search Ad or Shopping product ad starts enabled unless the agent sets it to paused.
- On the free plan, the change tools refuse to apply anything.
- On Max and Agency plans, a team owner can set a teammate to View only for any platform. AdPlug then hides and blocks that platform's change tools for that teammate.
- Grok Bot and Cursor can also ask you before a tool runs, depending on your settings.
- Every call is logged on the [usage page](https://adplug.app/dashboard/usage) of your AdPlug dashboard.

## Your data and where it goes

Every tool call goes to one endpoint, `https://api.adplug.app/mcp`. Sign-in goes through AdPlug's pages on adplug.app and its sign-in provider, Supabase (named in api.adplug.app's OAuth metadata). The plugin adds no software and runs no scripts on your computer.

Account data travels between your ad platforms and your agent through AdPlug's servers at api.adplug.app. Reports are fetched live and not kept. AdPlug logs each call's tool, ad account and time for your usage page, never its arguments or results, and keeps a Google Ads change preview for up to two days so it can be applied. Platform sign-in tokens are stored encrypted.

This repo holds the plugin manifest (`.cursor-plugin/plugin.json`), the server address (`mcp.json`), the logo, this README, a changelog and the licence.

- Privacy policy: [adplug.app/privacy](https://adplug.app/privacy)
- Terms: [adplug.app/terms](https://adplug.app/terms)
- Data processing agreement: [adplug.app/dpa](https://adplug.app/dpa)

## Support and links

- Email [support@adplug.app](mailto:support@adplug.app) and Daniel Popa, AdPlug's founder, will reply, usually the same business day.
- Website: [adplug.app](https://adplug.app)
- Plans: [adplug.app/pricing](https://adplug.app/pricing)
- Google Ads in Grok Bot, step by step: [adplug.app/guides/google-ads-grok-bot](https://adplug.app/guides/google-ads-grok-bot)
- LinkedIn Ads in Grok Bot: [adplug.app/guides/linkedin-ads-grok-bot](https://adplug.app/guides/linkedin-ads-grok-bot)

## Licence

MIT, see [LICENSE](LICENSE). Published by AdPlug, the trading name of MEANDATA IT SRL.
