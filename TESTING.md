# Testing AdPlug in Grok, Grok Bot and Cursor

For marketplace reviewers. The login's password is in AdPlug's submission form.

These steps take about 10 minutes. Every ad account on this login is our own. Please preview changes but don't apply any.

1. Install AdPlug.
   - In Grok Bot: open Connect apps in the sidebar (on the phone: tap your avatar, then Connect apps), find AdPlug, click Add, then Authenticate.
   - In Cursor: run /add-plugin adplug in a chat, or install AdPlug from the Marketplace.
   - In Grok (grok.com): open Plugins in the sidebar, click New Connector, choose Custom, enter the name AdPlug and the server URL https://api.adplug.app/mcp , then Add Connector.
   - If AdPlug isn't listed yet: in Grok Bot, send your Bot this message: Add a custom MCP server called AdPlug at https://api.adplug.app/mcp , then click Authorize on the card it posts and Continue. In Cursor, add https://api.adplug.app/mcp as a server in Cursor's MCP settings.

2. A browser tab opens on AdPlug's sign-in page. Sign in with email and password (not "Continue with Google"):
   - Email: mcp-review-grok@adplug.app
   - Password: the one given in AdPlug's marketplace submission (or ask support@adplug.app)

3. Next is AdPlug's "Authorize access" screen. From Grok Bot and Cursor it reads "Cursor wants to access your AdPlug account". That's expected, because Grok Bot connects apps through Cursor. Click Approve. Grok Bot then shows AdPlug as connected (in Cursor, the server shows a green dot and its tools).

4. Check the connection. Ask:
   - Which ad platforms are connected to AdPlug, and which ad accounts can you see?
   - Expected: Google Ads (HomeStagingAI), Meta Ads (seven older ad accounts, most of them disabled, plus their Facebook Pages), LinkedIn Ads (Daniels Ads - AdPlug) and Microsoft Ads (AdPlug) are connected. Reddit Ads shows as not connected on this login, which is expected.

5. Try one report per platform, one at a time:
   - Google Ads: Check my Google Ads performance from January to March 2026, put together a performance snapshot, and come back with insights and recommendations on what needs my attention.
   - Meta Ads: List my Meta ad accounts with their status, and the Facebook Pages I can advertise with. Which account could run ads today?
   - LinkedIn Ads: Show my LinkedIn Ads campaign performance from January to July 2026 and tell me which campaign had the lowest cost per conversion.
   - Microsoft Ads: Show my Microsoft Ads campaign performance for the last 30 days.
   - Notes: the Google Ads and LinkedIn Ads accounts last spent earlier in 2026, so recent date ranges come back empty. The Meta Ads accounts on this login have no campaign history, and the Microsoft Ads account is new with no campaigns, so empty reports there are expected.

6. Preview one change without applying it. Send:
   - Preview adding "free jobs" as a phrase-match negative keyword to the Google Ads campaign "AdPlug Review Sandbox (paused, safe to edit)". Don't apply it.
   - You should get a preview of the exact change, and nothing changes in the account. AdPlug only applies a Google Ads change when the execute tool is called with that preview's ID. If the agent offers to apply it, please say no.

7. Optional, removing it: in Grok Bot, open Connect apps, select AdPlug and click Disconnect. In Cursor, uninstall the plugin or remove the server.

8. Questions or problems: support@adplug.app. Daniel Popa, AdPlug's founder, will reply, usually the same business day.
