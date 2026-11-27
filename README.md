<p align="center"><img src="logo.png" width="96" alt="Car Rental Brain"></p>

# Car Rental Brain MCP server

**The real cost of car hire, for AI assistants.** Second-driver fees, deposits, debit-card acceptance, desk hours and
what excess cover really costs, measured at 180+ airports in Europe, the UK and the US - plus live offers for a
person's exact dates, ranked by the total they will actually pay.

Free. No API key. No login. Read-only.

**MCP endpoint (streamable HTTP):**

```
https://app.carrentalbrain.com/mcp
```

**Gemini CLI:** `gemini extensions install https://github.com/jimiwalters-cmyk/car-rental-brain-mcp`

Listed in the official [MCP Registry](https://registry.modelcontextprotocol.io) as `com.carrentalbrain/car-rental-brain`.
Website: [carrentalbrain.com](https://carrentalbrain.com) · Agent page: [carrentalbrain.com/ai](https://carrentalbrain.com/ai/)

## Why it exists

Car-hire search shows the headline price. The bill at the desk is different: a second driver adds a fee, the desk
blocks a deposit on the card, many desks refuse debit cards, some close before a late flight lands, and the desk
sells its own excess cover. Car Rental Brain measures these from its own repeated searches and answers with the
numbers, so an assistant can say what a rental will really cost - not just what it is advertised at.

## Tools

| Tool | What it answers |
|---|---|
| `search_rentals` | Live offers for exact dates and needs, ranked by the total paid, each with deposit, excess, debit card, fuel, mileage, free cancellation and desk hours, plus a link to the same cars (5 new searches per conversation; re-asks with a different car for the same place and dates are free) |
| `track_price_link` | Price-drop alerts: a link where the person enters and confirms their own email, then hears if the price drops (no email passes through the assistant) |
| `recommend_rental` | A planned trip and its needs (second driver, automatic, debit card, car size, seven seats, deposit limit): the companies that usually suit them, priced for the trip month |
| `desks_open` | Which desks are still open when a flight lands, each desk's measured closing time and the late pick-up fee |
| `get_capabilities` | What is measured, how fresh it is, which airports and countries are covered |
| `list_airports` | Airports measured, with the typical price per day; filter by country |
| `airport_costs` | One airport's real cost: car only, with a second driver, with full cover, automatic, no-deposit; by pick-up month; deposits; debit cards; desk hours and out-of-hours fees |
| `compare_airports` | Rank airports by real cost, deposit, debit-card friendliness or late desk hours |
| `supplier_terms` | Per supplier at an airport: price, second-driver fee, full-cover price, deposit, debit card, desk review scores |
| `build_search_link` | A link for the person: live prices for their exact dates and needs, ranked by the total they will pay, where they can book |

In clients that show MCP Apps (Claude, ChatGPT), `search_rentals` results appear as interactive cards: a photo of each car, the total paid, deposit, excess and debit card, with car-size tabs, filters (automatic, debit card, low deposit, free cancellation, zero excess), side-by-side compare and a Book button.

Measured answers are dated and say how many searches they rest on; live offers say when they were searched. Booking happens on DiscoverCars through Car Rental Brain's link (affiliate; the traveller pays the same price).

## Example questions

- "Find me the cheapest car at Faro Airport from 15 to 22 January - I live in the UK."
- "What does it really cost to hire a car at Faro Airport for a week in November with two drivers?"
- "Which Spanish airport is cheapest for car hire in March?"
- "I only have a debit card - where can I pick up a car in Portugal?"
- "My flight lands at 23:30 in Malaga - which desks are still open?"
- "Is the desk's excess cover cheaper than buying full coverage in advance at Lisbon?"

## Connect

<details>
<summary><strong>Claude (claude.ai / Claude Desktop)</strong></summary>

Settings → Connectors → Add custom connector → URL `https://app.carrentalbrain.com/mcp`.

Or in `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "car-rental-brain": { "url": "https://app.carrentalbrain.com/mcp" }
  }
}
```
</details>

<details>
<summary><strong>ChatGPT</strong></summary>

Car Rental Brain is an approved ChatGPT app - nothing to set up.
[Install in ChatGPT](https://chatgpt.com/plugins/plugin_asdk_app_6adcda8a3b988191b45dee1d3c7bc428), then ask e.g.
"Using Car Rental Brain, find me a car at Faro from 15 to 22 January".
</details>

<details>
<summary><strong>Claude Code</strong></summary>

As a plugin (from this repository):

```
/plugin marketplace add jimiwalters-cmyk/car-rental-brain-mcp
/plugin install car-rental-brain@car-rental-brain
```

Or add the server directly:

```
claude mcp add --transport http car-rental-brain https://app.carrentalbrain.com/mcp
```
</details>

<details>
<summary><strong>Cursor / Windsurf / Cline / VS Code</strong></summary>

```json
{
  "mcpServers": {
    "car-rental-brain": { "url": "https://app.carrentalbrain.com/mcp" }
  }
}
```
</details>

<details>
<summary><strong>Stdio-only clients</strong></summary>

```bash
npx mcp-remote https://app.carrentalbrain.com/mcp
```
</details>

<details>
<summary><strong>Plain HTTP (JSON API)</strong></summary>

The same tools are available as a plain JSON API (e.g. `https://app.carrentalbrain.com/api/v1/get_capabilities`) - see
[carrentalbrain.com/ai](https://carrentalbrain.com/ai/).
</details>

## How the numbers are made

Each airport is searched repeatedly across trip lengths and pick-up months; a report is published only once enough
searches agree. Second-driver fees are the suppliers' own quoted fees (a fee nobody publishes is never counted as
free). Desk excess-cover prices come only from each supplier's own published price list, with the source and the
date read. Full method: [carrentalbrain.com/methodology](https://carrentalbrain.com/methodology).

## Affiliate disclosure

Car Rental Brain is free. Booking happens on DiscoverCars through the link the tools return, and Car Rental Brain
earns a commission on bookings, at no extra cost to the person booking. Results are ranked by the total the person
will pay, never by commission.

## Privacy

The tools take no personal data and need no account. Searches are logged without names or contact details.
Privacy policy: [carrentalbrain.com/privacy](https://app.carrentalbrain.com/privacy).

## Contact

hello@carrentalbrain.com

## Licence

The files in this repository are licensed under the [Apache License 2.0](LICENSE); see [NOTICE](NOTICE).
The **Car Rental Brain name and logo are not covered by this licence** and remain the property of Jimi Walters.
The server, its code and its data are not in this repository; use of the server is governed by
[the terms](https://app.carrentalbrain.com/terms).
