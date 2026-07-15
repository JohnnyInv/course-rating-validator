# Course Rating Validator

A small, self-contained web tool for validating the Course Rating and Slope
Rating of a custom or combination golf tee, using the official USGA/WHS
procedure for unrated tees.

**Live site:** _(added after the first GitHub Pages deploy)_

## What it does

Golf tees that don't match a course's standard, already-rated tee boxes
(for example, a shortened combo setup for a junior event) don't have an
official Course Rating or Slope Rating of their own. The World Handicap
System defines a documented procedure for deriving a temporary rating for
that kind of tee, based on its yardage difference from a nearby tee that
*is* already rated.

This tool implements that procedure:

1. Enter the gender, and the yardage/Course Rating/Slope Rating of a
   nearby tee that's already officially rated (read straight off the
   course's scorecard). You can optionally enter a second candidate
   reference tee — the tool will automatically use whichever one is
   numerically closer in yardage to the target tee.
2. Enter the target tee's total yardage.
3. The tool reports:
   - **Under 100 yards difference** — no adjustment needed; the target
     tee uses the reference tee's numbers as-is.
   - **100–300 yards difference** — the official adjustment table value
     is looked up and applied (added if the target is longer, subtracted
     if shorter). The exact table row used is shown for transparency.
   - **Over 300 yards difference** — not eligible for this method; a full
     independent rating is required, or the Authorized Association must
     pre-approve the round.
4. Optionally, enter a Course Rating/Slope Rating you're about to submit
   somewhere, and the tool will flag whether it matches the computed
   value.

All calculation happens client-side in the browser. Nothing is sent to a
server, and no AI/LLM is involved in the calculation — it's a
deterministic table lookup.

## Methodology and source

- **Rule:** WHS Rule 7f1 / Appendix G, formerly USGA Handicap Manual
  Section 5-2g, "Ratings Adjustments from Unrated Tees."
- **Table data:** transcribed and cross-checked against two independent
  copies of the 2016 USGA Handicap Manual table (one official USGA PDF,
  one third-party copy distributed by the American Junior Golf
  Association). Both matched exactly, row for row.
- **Known limitation:** the current, live USGA/WHS Appendix G page could
  not be independently fetched to confirm the table hasn't been revised
  since 2016. Treat this tool as a strong first validation, not a
  replacement for sign-off from the relevant Authorized Association
  (the state/regional golf association that governs ratings in your
  area).

This tool does not issue official ratings.

## Running it locally

It's a single static HTML file with no build step and no dependencies.
Open `index.html` directly in a browser, or serve the folder with any
static file server.

## Project structure

```
course-rating-validator/
├── index.html   # the tool itself (HTML + CSS + JS, self-contained)
└── README.md    # this file
```
