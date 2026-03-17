# Design Decisions — LEGO House Tickets

## The problem

LEGO House has ~25 bookable products across wildly different categories — from a 169 DKK afternoon ticket to a 25,000 DKK 3-day insider tour. The audience ranges from a local parent grabbing day tickets to a superfan from Japan planning a bucket-list pilgrimage. One interface must serve both without overwhelming either.

## Three visitor personas

1. **Quick Booker** (local/near traveler) — knows LEGO House, just wants a day ticket. Should book in under 10 seconds.
2. **The Planner** (family trip, 1-3 months ahead) — exploring options, might add Academy or combo. Needs clarity on what's included.
3. **The Superfan** (bucket list, books months ahead) — willing to spend 5,000-25,000 DKK. Needs detail to justify the price.

## UX principles applied

### Hick's Law
Don't show 25 products on first view. The tickets page opens with 4 entry ticket options — the decision most visitors actually need to make. Everything else is one scroll or one category pill away.

### Progressive disclosure
- **Simple products** (day ticket): compact card, price, one-line description, Book Now. Done.
- **Medium products** (Academy, stays): enough detail to understand value, with a link to deeper content.
- **Complex products** (premium tours at 1,899-25,000 DKK): accordion pattern — title + price visible, click to expand full justification copy and feature list.

### Visual hierarchy
- Day Ticket is the **hero card** — full width, yellow accent border, largest CTA. This is what 80% of visitors want.
- Afternoon + Combo tickets sit at medium weight, side by side.
- Annual Pass is a compact row — present but not competing.
- Premium and Groups/Schools are further down, serving specific audiences.

### Cognitive load
- **Sticky category pills** (Tickets / Academy / Stays / Premium / Groups & Schools) let users jump without scrolling through irrelevant content.
- **Visual grouping** with distinct background colors per section (yellow for Academy, white for tickets, etc.)
- **Price is always the first number you see** — scannable without reading descriptions.

## Key UI pattern choices

### Sticky category navigation
Horizontal pill bar that highlights the active section via Intersection Observer. Reduces the "where am I?" problem on a long page.

### Accordion for Premium Experiences
Premium products need MORE explanation than simple tickets — a 25,000 DKK Inside Tour needs justification that a 239 DKK day ticket doesn't. Accordion lets casual visitors skip past quickly while giving superfans the detail they need. Ordered by price ascending for natural price anchoring.

### Academy as a separate page
Academy has enough depth (4 levels, multiple languages, session scheduling, concept explanation) that keeping it on the tickets page either makes the page too long OR makes Academy too shallow. Solution: a teaser card on the tickets page linking to a dedicated Academy page.

### Academy page — language filter
Each Academy level runs in multiple languages (Danish, English, potentially more). Each language session is a separate bookable product. Filter pills (All / Danish / English) let users narrow without losing context of the full level progression.

### Academy — level progression
Levels are displayed as a vertical progression (1→2→3→4) with visual connectors, not a flat grid. This communicates that they build on each other. Level 4 is shown at reduced opacity as "Coming 2026" — visible enough to create anticipation, muted enough to not confuse.

### Tabs for Groups & Schools
These serve completely different audiences (event organizers vs. teachers). Showing both simultaneously adds noise for families — the primary audience. Tabs keep them accessible without polluting the main flow.

### Stay packages — always expanded
At 2,000-3,000 DKK, families need to see what's included before engaging. Feature lists are always visible — no accordion, no "show more". The price demands upfront justification.

## What we intentionally didn't do

- **No filters on the tickets page** — with only 4 entry tickets, filtering adds complexity without value. The sticky pills serve the navigation need.
- **No hero images** — the original site uses hero images per product. We prioritized scanability and speed over decoration. Images can be added later.
- **No date picker inline** — booking flow happens on book.legohouse.com. We show the overview and link out.
- **No price comparison table** — the visual hierarchy of card sizes communicates relative importance better than a flat table.

## Brand alignment

- LEGO Yellow (#FFD500), Red (#E3000B), Blue (#006DB7), Green (#00A850) used as accents
- Playful but not childish — rounded corners, clean spacing, system fonts
- Warm light background (#F5F5F0) instead of cold white
- Consistent with legohouse.com's family-friendly, premium tourist attraction positioning

## Data source

All prices, descriptions, and product details sourced from `legohouse-tickets-flat.json` and verified against legohouse.com (March 2026).
