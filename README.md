# Near-Expiry Food Management Tool — UX Research Prototype

A single-page, Wizard-of-Oz fidelity prototype of a supermarket **near-expiry food management tool**, built for a UX research pilot test (DECO6500).

It simulates the in-store staff screen that shows which near-expiry items are approaching their donation cut-off, and lets the staff member route each item to donation or mark it for discard under visible time pressure.

![screen: six item cards sorted by urgency, with large countdowns and colour-coded urgency bars](docs/screenshot.png)

---

## Running it

Open `index.html` in any modern browser. That's it.

No build step, no dependencies, no server, no backend, no login. The entire prototype is one self-contained HTML file (~16 KB) with inline CSS and JavaScript, so it can be demoed from a laptop with no network connection.

---

## What it does

### Near-expiry item list

Six hardcoded items are shown as cards in a responsive grid, **sorted most-urgent-first**. Each card shows:

- **Item name** and location metadata (department, aisle/bay, unit count)
- **A large countdown** to that item's donation cut-off — `4h 47m remaining` above one hour, switching to `33m 46s remaining` below one hour so seconds become visible exactly when they start to matter
- **A colour-coded urgency bar and badge**, recomputed every second:

| Time remaining | Tier  | Badge      | Colour              |
| -------------- | ----- | ---------- | ------------------- |
| More than 4h   | Green | `ON TRACK` | `#00703c`           |
| 1h – 4h        | Amber | `ACT SOON` | `#8a4b00`           |
| Under 1h       | Red   | `URGENT`   | `#c00d20`           |

Urgency is carried redundantly by colour, badge text, bar length, and card border, so the list is scannable at a glance and does not depend on colour vision alone.

### Decision actions

Each card has **Route to Donation** and **Mark for Discard**. Clicking either puts the card into a confirmation state: it greys out, the buttons are replaced by `✓ Marked for Donation` (or Discard) with a timestamp and a short line of consequence text, and the header's "awaiting decision" counter drops.

Decided cards stay in place rather than moving to the bottom — a reorder mid-task would be a distracting visual event during a timed test.

### Interruption / resume behaviour

This prototype is designed for a scripted *"a customer interrupts you"* test condition.

A deliberately subtle **researcher-only control** sits in the bottom-right corner at 32% opacity, becoming fully visible on hover or keyboard focus:

```
advance by: [ 15 ] min   [ SIMULATE INTERRUPT — researcher only ]
```

1. Clicking **SIMULATE INTERRUPT** raises a near-opaque, blurred overlay reading *"Customer approaching…"* with a **Resume** button. The item list is genuinely obscured, so the participant cannot keep planning during the interruption.
2. Clicking **Resume** returns to the list with every countdown advanced by the number of minutes in the input field.
3. `Ctrl/Cmd + Shift + I` toggles the same overlay, if reaching for the corner is awkward mid-session.

**Why it looks seamless to the participant.** The clock reads `Date.now() + advanceMs`, and the tick function writes into existing DOM nodes rather than rebuilding the list. Resume adds to the offset and repaints *before* the overlay begins to fade, so the participant only ever sees already-correct numbers — no flash, no reset, no reflow. Because every item shifts by the same amount, the sort order is fixed at load and never visibly re-sorts.

### Passing the cut-off

If the researcher advances time past an item's cut-off, that card shows `CUT-OFF PASSED` and its donation button is disabled and relabelled `Donation window closed`; discard remains available. This is a deliberate design choice — the alternative was a card counting into negative time. To avoid participants hitting a locked-out item, keep advances at 15 minutes or under.

---

## Scenario data

One hardcoded scenario, staggered across all three urgency tiers (2 red / 2 amber / 2 green at load). Times are relative to page load, so the scenario is identical for every participant regardless of when the session runs.

| Item                      | Department      | Remaining at load | Tier  |
| ------------------------- | --------------- | ----------------- | ----- |
| Fresh Salmon Fillet 240g  | Chilled Fish    | 34m               | Red   |
| Rotisserie Chicken (Hot)  | Hot Deli        | 51m               | Red   |
| Greek Yogurt 4-pack       | Chilled Dairy   | 1h 22m            | Amber |
| Caesar Salad Kit 320g     | Chilled Produce | 3h 06m            | Amber |
| Sourdough Loaf 800g       | In-store Bakery | 4h 48m            | Green |
| Sliced Roast Ham 200g     | Chilled Deli    | 6h 15m            | Green |

To change the scenario, edit the `SCENARIO` array near the top of the `<script>` block in `index.html`; `mins` is the minutes remaining at page load. The list re-sorts by urgency automatically.

---

## Design intent

Styled as a **retail staff tool**, not a consumer app: high contrast, large tabular-numeral countdowns, heavy type, flat surfaces, no decoration. The target is legibility at arm's length under time pressure, on a shop floor.

## Scope

Deliberately **not** included, to keep the pilot focused: authentication, real API or database integration, donation-partner coordination, manager or corporate dashboards, multi-store support, and real-time sync. All state is in-memory and resets on reload — which is the intended behaviour between participants.

## Files

```
index.html    the entire prototype
README.md     this file
```
