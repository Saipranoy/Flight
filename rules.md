# PDG Flights: emergency rules

Status: agreed and applied in `index.html`.

## 1. When this applies
- The request mentions a disruption (stuck, storm, strike, cancelled...) or urgency (urgent, ASAP, next available...).
- Emergency wins over every other kind of request, even if a price or destination is mentioned.
- Example: "Im stuck in milan in a windstorm. i need the next available flight i can get on, from the closest airport as possible."

## 2. What we ask
- Where they are is required. Ask only if it's missing.
- Where to is optional when they want the next available flight. It counts as "Anywhere".
- When defaults to "As soon as possible".
- One question at a time, with tap answers. Always accept a typed answer.

## 3. What we show
Order: short note, trip, plan, nearby airports with rebooking, other flights.
- Only show flights they can make: travel time + 45 minutes for check-in.
- Show 2 backup flights when there are that many they can make. If fewer, show what there is.
- Show hotels and other transport only when no flight works.
- First flight: the soonest departure they can make, even if a closer airport has a later one. Exception: if they gave a deadline, the earliest arrival goes first.

## 4. Visual style
Base: Product Designer Gym design system, Light theme. Reference: the travel-document image (Miro).

Decided: tickets with less decoration.

| Part | Emergency treatment |
|---|---|
| Note | Plain note. No postcard or postmark. |
| Trip | Luggage tag with dashed, tappable fields: From, To, When, Who. |
| Main flight | Boarding pass: lime header with ink text, perforation, fare stub, barcode, one primary button. |
| Other flights | Slim ticket rows with a perforated price stub and a secondary button. |
| Stamps | Status only, never decoration. |

The main pass must also show: leave by, travel to the airport, check-in closes, take-off, the safety line, directions and "I can't get there".

### Stamps
| Stamp | When | Colour token |
|---|---|---|
| Next you can make | Soonest reachable departure | success |
| Closest airport | Leaves from the nearest open airport | primary-text |
| Few seats left | Fewer than 10 seats. Shows the number, e.g. "4 seats left" | warning |
| Cheapest | Lowest fare among flights they can make | success |

Closest airport only shows when there is more than one open airport. Cheapest only shows when there is more than one flight. A ticket can carry more than one stamp. Stamps must not cover times, airports or prices.

Not used in emergencies: postcard, postmark, mystery ticket, ink header, red header.

Must still hold:
- Status always has a word, never colour alone.
- Nothing essential is below 12px or only in a stamp or barcode.

## 5. Tone
- Warm throughout: reassure in the note, the plan and the alternatives.
- Keep it short, and put times and actions first. Warmth never delays the next step.
- Safety wording stays plain.
- Never promise an outcome ("you'll be fine") and don't joke about the situation. Playful lines like "Lucky you" are for spontaneous trips.

## 6. Safety
- Only set off if the road is safe. If officials say stay put, stay.
- Show the local emergency number.
- Never imply a seat is booked or held when it isn't.

## 7. Never
- Never show a flight they can't reach.
- Never mark a flight "in time" if it misses the deadline.
- Never drop a need silently (pet, wheelchair, group, budget).
