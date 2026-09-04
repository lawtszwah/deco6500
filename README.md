# Near-Expiry Food Management Tool — UX Research Prototype

A single-page, Wizard-of-Oz prototype for a DECO6500 usability pilot. It helps supermarket staff prioritise food approaching its donation cut-off, make donation/discard decisions, and resume safely after an interruption.

## Run locally

Open `index.html` in any modern browser. There is no build step, dependency, server, login, API, or database.

All data is held in the current browser session and resets when the page is refreshed, making the scenario repeatable between participants.

## Current features

- Six realistic near-expiry items sorted by remaining time
- Large live countdowns with red **Critical**, amber **Soon**, and green **On track** states
- **Route to Donation** and **Mark for Discard** decision actions
- Separate **To review**, **Donation list**, and **Discard list** views
- Edit an item's name, category, location, quantity, remaining time, and list status
- Add custom items using category and store-location dropdowns
- Export the current donation or discard list as a UTF-8 CSV file
- Researcher-only interruption control with a configurable simulated time advance
- Seamless countdown updates after resuming from an interruption
- Complete English and Simplified Chinese interface switcher
- Responsive layout for laptop and smaller screens

## Research focus

The prototype supports three evaluation questions:

1. Can a participant identify the item with the least time remaining without help?
2. After an interruption, can they correctly read and trust the updated remaining time?
3. Does clear donation-window information affect confidence in the donate-versus-discard decision?

## Scenario

The default scenario contains two red, two amber, and two green items. Countdown times are relative to page load. Researchers can add or edit items without changing the source file.

## Files

- `index.html` — complete self-contained prototype
- `README.md` — project overview and usage notes
- `docs/screenshot.png` — screenshot of an earlier prototype iteration
