# PDG Flights: emergency rules

A complete brief for the emergency screens. **Must** items are fixed. Items marked *(recommended)* are proposals you may improve.

## 0. Start here
PDG Flights is a fictional airline for a Product Designer Gym exercise. Travellers describe a trip in their own words and the site answers with cards. This file covers one situation: someone is stuck and needs to leave now.

- **Goal:** within seconds they know where to go, when to leave and which flight to take.
- **Deliver:** every screen in section 4, at desktop (1100px) and phone (375px).
- **Design system:** https://phoebeyudesign.github.io/ProductDesignerGym/design-system/ (Light theme only)
- **No images needed:** section 6 describes every shape in words.
- **Flowchart:** [rules-flowchart.html](rules-flowchart.html)
- **Built example:** https://saipranoy.github.io/Flight/ (skip it if you want a fresh take)

## 1. When this applies
- The request mentions a disruption (stuck, storm, strike, cancelled...) or urgency (urgent, ASAP, next available...).
- Emergency wins over every other kind of request, even if a price or destination is mentioned.
- Example: "Im stuck in milan in a windstorm. i need the next available flight i can get on, from the closest airport as possible."

## 2. What we ask
- Where they are is required. Ask only if it's missing, and ask it first.
- Where to is optional when they want the next available flight. It counts as "Anywhere". Otherwise ask.
- When defaults to "As soon as possible". Who defaults to 1 adult. Don't ask for either.
- One question at a time, with tap answers. Always accept a typed answer. Show what we already know.

| Question | Tap answers |
|---|---|
| Where are you right now? | Edinburgh, London, Manchester, Milan |
| Where do you need to get to? | London, Amsterdam, Dublin, Anywhere I can get to |

## 3. How flights are chosen
- Only show flights they can make: travel time + 45 minutes for check-in.
- Check-in closes = take-off minus 45 minutes. Leave by = check-in closes minus travel time.
- First flight: the soonest departure they can make, even if a closer airport has a later one. Exception: if they gave a deadline, the earliest arrival goes first.
- A deadline means the next time that clock time comes round. Include the date when checking it.
- Apply needs (pet, wheelchair, group, budget). Say how many flights were left out. If none fit, keep the flights and say so.
- If they say "cheapest", keep the soonest first and name the cheapest one they can make.
- Show 2 backup flights when there are that many they can make. If fewer, show what there is.
- Show hotels and other transport only when no flight works.

## 4. Screens and states
| State | What it shows | What happens next |
|---|---|---|
| Loading | "Finding flights" announced to screen readers, 3 skeleton cards | Result or question |
| Question | Note, what we know, one question, tap answers | Answer continues the same request |
| Not understood | Same question with an apology | They try again |
| Plan | Note, luggage tag, boarding pass, airports + rebooking, backups, in that order | See actions |
| Flight chosen | Pass header says "Your chosen flight". Choose is replaced by Get directions as the primary button | They leave |
| No flight works | Note, luggage tag, disruption status, other transport, hotels, safety, alert switch | They wait or change the trip |
| Something failed *(recommended, not built)* | "I couldn't load flights. Try again." with one retry button and the emergency number | Retry |

### Actions
| Control | Result |
|---|---|
| Choose this flight | Flight chosen state. Nothing is booked or held. |
| Switch to this | That backup becomes the chosen pass. The old one joins the backups. |
| Tap a trip field | Asks for that detail, then works the plan out again |
| Remove a need | Works the plan out again without it |
| Get directions | Opens a map to the airport in a new tab |
| I can't get there | No flight works state |
| Start over | Clears the request and returns to the prompt |

No flight works also appears when they say roads or airports are closed, or that they can't get somewhere. The prototype doesn't check this live.

## 5. Components and contents

### Note
Lime 32px square with a sparkle icon, then one to three sentences in `body`.

### Luggage tag
Label "Your trip · tap to change". Fields: From, To, When, Who, then any needs. Each field: label, value, pen icon (needs get ×).

### Boarding pass
| Area | Contents |
|---|---|
| Header | "Your way out" left, airline right, "Fare" over the stub |
| Headline | "Leave by {time} for {airport}" |
| Route | Both airport codes with their names, dotted line and plane between |
| Stamps | Own row |
| Times | Leave by, Check-in closes, Takes off, Lands (+1 if next day) |
| Travel | Drive time, road, distance, flight time, stops |
| Safety line | See section 8 |
| Other actions | Get directions (secondary), I can't get there (ghost) |
| Stub | Price per person (and group total), flight number, seats left, barcode, primary button, "Not a real ticket. Nothing is booked or held." |

### Stamps
| Stamp | When | Colour token | Icon |
|---|---|---|---|
| Next you can make | Soonest reachable departure | success | Bolt |
| Closest airport | Leaves from the nearest open airport, and more than one is open | primary-text | Pin |
| Few seats left | Fewer than 10 seats. Shows the number: "4 seats left" | warning | Triangle |
| Cheapest | Lowest fare they can make, and there is more than one flight | success | Tag |

A ticket can carry more than one stamp. Stamps must not cover times, airports or prices.

### Ticket row (backup)
Destination, route + airline + flight number, airport + drive time + seats, leave by, check-in closes, take-off to landing + duration + stops, stamps, price, Switch to this.

### Airports card
"Airports near you, closest first". Title says how many stopped flying. Each row: name (code), distance, drive time or "No departures", and an Open or Suspended badge. Ends with the cause and expected restart.

### Rebooking card
"Rebook your flight instead": one sentence, a 6-character booking reference field, Find booking (secondary). It never blocks the plan.

### No flight works cards
- Status: what's closed and why.
- Other transport: up to 3, each with time, condition and price. Only routes that are possible.
- Hotels: 3, each with distance, one useful fact and price.
- Safety: 3 lines, including the local emergency number.
- Alert switch: "Tell me as soon as a flight opens up".

## 6. Visual style
Light theme of the design system. The results look like paper travel documents: tidy and calm, with little decoration.

### Shapes
- **Luggage tag:** a white, wide, short card with a thin border. Both left corners are cut diagonally (24px across, 24px down), so the left end tapers like a tag. A 12px punched hole sits 16px from the left edge, centred vertically, showing the canvas colour. The right corners are rounded 12px. Fields are dashed boxes with 4px corners, in a row that wraps.
- **Boarding pass:** a white card, wider than it is tall on desktop. A lime bar runs across the top with small uppercase ink labels. Below it, the main part is on the left and the 240px fare stub is on the right.
- **Perforation:** a 1px dashed line between the main part and the stub. Where it meets the card's edges, a half-circle notch (18px wide) bites into the card, showing the canvas colour with a thin border.
- **Route:** two large bold airport codes with names underneath. Between them, a dotted line leads to a small plane pointing at the destination.
- **Barcode:** plain vertical ink bars of mixed widths across the stub. Decoration only.
- **Stamps:** small rectangles like a clean rubber stamp: a 2px outline, a thin second line inside it, an icon and uppercase words, all in one colour. Tilted slightly, alternating direction. No worn or ink texture, and never overlapping.
- **Ticket row:** the pass made slim: one short white card, details on the left, a perforation with notches, then price and button on the right. No lime bar or barcode.

Don't use: postcards, postmarks, mystery tickets, or a black or red header.

### Tokens
| Use | Value |
|---|---|
| Lime fill / its label | `primary` #E4F222 / `on-primary` #1A1919 |
| Primary as text or icon | `primary-text` #5A6200 (never lime text) |
| Canvas / cards | `background` #F4F2EE / `surface` #FFFFFF |
| Text / secondary text | `text` #1A1919 / `text-muted` #5F5B55 |
| Border | `border` #D9D5CE, 1px |
| Status | `success` #157A43, `warning` #8F5A00, `error` #C62828 |
| Spacing | 4, 8, 12, 16, 24, 32, 48px |
| Type (DM Sans) | h1 40/48, h3 24/32, h4 20/28, body 16/24, caption 14/20, small 12/16 |

No shadows or coloured left edges.

### Layout
| | Desktop | Phone |
|---|---|---|
| Page | Max 960px wide, 32px side padding (from 720px) | 16px side padding |
| Card gap | 16px | 16px |
| Pass | Main + 240px stub, 24px padding, 16px radius | Stub moves below, dashed line on top, 16px padding |
| Pass times | 4 in a row | 2 by 2 |
| Airports + rebooking | Side by side | Stacked |
| Ticket row | Main + stub, 12px radius | Stub moves below |
| Primary button | Bottom of the stub | Full width, in the stub |

Sizes: pass codes 32/40 bold; labels 12/16 semibold, uppercase, 0.08em spacing; buttons and tag fields at least 40px tall, buttons 8px radius; perforation 1px dashed with 18px notches; barcode 48px; stamps 12/16 bold, 2px outline with a thin inner line, tilted 2 to 3 degrees.

One primary button in the results. Search in the prompt box keeps its own.

## 7. Tone
- Warm throughout: reassure in the note, the plan and the alternatives.
- Keep it short, and put times and actions first. Warmth never delays the next step.
- Safety wording stays plain.
- Never promise an outcome ("you'll be fine") and don't joke about the situation.

| Moment | Wording |
|---|---|
| Plan | "I'm sorry you're stuck. There is a way out: this is the next flight you can make, from Milan Bergamo." |
| Destination is Anywhere | "I put leaving soonest first. Tap “To” to pick a place." |
| Question | "I'm sorry you're stuck. I'll find the fastest way out, I just need one detail first." |
| Not understood | "Sorry, I didn't catch that. Could you try again? You can tap an answer too." |
| Chosen | "Good choice, let's get you moving. Head for Milan Bergamo and leave by 18:35 to catch NL 207 to Rome." |
| Backups | "If that one doesn't work for you. Take a breath. You can still make these too." |
| No flight works | "I'm sorry, there are no flights you can safely reach tonight. Let's keep you comfortable until there are." |

## 8. Safety
- Line on every pass: "Only set off if the road is safe. If officials tell you to stay put, stay. In danger, call {local number}." Milan is 112, the UK is 999.
- Never imply a seat is booked or held when it isn't.

## 9. Accessibility
- WCAG AA: 4.5:1 text, 3:1 large text and meaningful graphics.
- Status always has a word, never colour alone.
- Nothing essential is below 12px or only in a stamp or barcode.
- Focus ring: 2px `focus-ring` #1A1919 with a 2px offset on every control.
- After an action replaces the screen, move focus to the new pass or question, and announce it.
- Barcode and icons are hidden from screen readers. Switch buttons name their flight.
- Text must not cause sideways scrolling at 375px. Respect reduced motion.

## 10. Sample data
All invented. Request made at 18:00 from Milan, windstorm, no destination.

| Airport | Distance | Drive | Status |
|---|---|---|---|
| Milan Linate (LIN) | 8 km | – | Suspended |
| Milan Bergamo (BGY) | 48 km, A4 | 1 h | Open |
| Milan Malpensa (MXP) | 49 km | – | Suspended |
| Turin (TRN) | 150 km, A4 | 1 h 45 min | Open |

Cause: high winds, gusts up to 110 km/h, restart expected around 23:00.

| | First | Backup | Backup |
|---|---|---|---|
| Flight | Northline NL 207 | Skylark Air SK 552 | Coastal Jet CJ 390 |
| Route | BGY → FCO Rome | BGY → CDG Paris | TRN → AMS Amsterdam |
| Leave by | 18:35 | 19:20 | 19:15 |
| Check-in closes | 19:35 | 20:20 | 21:00 |
| Takes off | 20:20 | 21:05 | 21:45 |
| Lands | 21:30 | 22:40 | 23:35 |
| Duration | 1h 10m, direct | 1h 35m, direct | 1h 50m, direct |
| Price | £164 | £131 | £98 |
| Seats left | 4 | 11 | 24 |
| Stamps | Next you can make, Closest airport, 4 seats left | Closest airport | Cheapest |

No flight works, to Rome: coach to Bergamo 06:40 £12 (if the A4 reopens), flight from Linate 07:05 £96 (if it reopens), train 06:00 £64 (if the line is open). Hotels: Station Hotel £89, Old Town Rooms £112, Airport Lodge £74.

Also test: no location ("I'm stuck in a windstorm, next available flight"), a need and deadline ("stuck in Milan, get me to London by 23:59 with my dog, 2 adults"), blocked roads ("stuck in Milan, roads are blocked").

## 11. Never
- Never show a flight they can't reach.
- Never mark a flight "in time" if it misses the deadline.
- Never drop a need silently.
- Never use more than one primary button in the results.
