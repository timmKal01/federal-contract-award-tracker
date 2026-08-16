# Federal Contract Win Finder — GovCon Leads & Competitor Intel

Search recent U.S. federal contract awards by keyword, NAICS code, agency, or
state. Get back who just won, how much, from which agency, and a link to the
full award record — largest awards first.

Built for GovCon business development teams looking for subcontracting leads
(who just won a prime contract you could support), companies tracking
competitor wins in their NAICS code, and researchers monitoring federal
spending in a sector or region.

## Input

```json
{
  "keyword": "cybersecurity",
  "naicsCodes": ["541512"],
  "agency": "Department of Homeland Security",
  "recipientState": "VA",
  "minAwardAmount": 1000000,
  "daysBack": 30,
  "maxResults": 25
}
```

| Field | Type | Description |
|---|---|---|
| `keyword` | string | Free-text search across contract descriptions. Leave blank to skip. |
| `naicsCodes` | array of strings | Limit to these NAICS industry codes. Leave empty for all industries. |
| `agency` | string | Exact top-tier awarding agency name (e.g. "Department of Defense"). |
| `recipientState` | string | Two-letter US state code — limits to contractors headquartered there. |
| `minAwardAmount` | number | Only return awards at or above this dollar amount. |
| `daysBack` | number | How many days back from today to search. Default `30`. |
| `maxResults` | number | Max awards to return, largest first. Default `25`, max `100`. |

All fields are optional — omit everything to get the largest new contract
awards government-wide over the last 30 days.

## Output

One record per contract award:

```json
{
  "awardId": "70RCSJ23FR0000071",
  "recipientName": "ACCENTURE FEDERAL SERVICES LLC",
  "awardAmount": 43865348.3,
  "awardingAgency": "Department of Homeland Security",
  "awardingSubAgency": "Office of Procurement Operations",
  "contractType": "DELIVERY ORDER",
  "naicsCode": "541512",
  "naicsDescription": "COMPUTER SYSTEMS DESIGN SERVICES",
  "description": "INSIGHTS PROGRAM SUPPORT FOR THE VULNERABILITY MANAGEMENT (VM) CYBERSECURITY DIVISION...",
  "startDate": "2023-09-29",
  "endDate": "2026-09-28",
  "usaspendingUrl": "https://www.usaspending.gov/award/CONT_AWD_70RCSJ23FR0000071_7001_HHSN316201200002W_7529"
}
```

## How it works

One direct call per search to the official [USAspending.gov](https://www.usaspending.gov/)
Award Search API (`api.usaspending.gov`) — the U.S. Treasury's public,
no-key-required transparency API for federal spending data. No proxy, no
login, no scraping: this is the same data source that powers usaspending.gov
itself, built for programmatic reuse.

## Pricing note

Billed per **search**, not per award returned — one charge whether the
search returns 1 award or 100. Run it as a saved search/schedule to catch
new awards in your target NAICS code or agency as they post.

## Related products

Looking for private-sector buying signals instead of federal contracts?

- [Company Buying Signal Report](https://github.com/timmKal01/company-buying-signal-report) — hiring, tech stack & contact info combined per company
- [Company Hiring Tracker](https://github.com/timmKal01/company-hiring-tracker) — open roles per company
- [Federal Grant Award Tracker](https://github.com/timmKal01/federal-grant-award-tracker) — the same USAspending.gov data for grants instead of contracts
