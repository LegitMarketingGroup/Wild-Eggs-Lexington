# Wild Eggs Lexington: Google Business Profile Dashboard

Google Business Profile performance for the three Wild Eggs restaurants in Lexington, Kentucky (Hamburg, Palomar
Centre and Tates Creek), prepared by Legit Marketing Group.

Live at <https://dashboards.legitrics.com/Wild-Eggs-Lexington/>, behind a password.

## What it shows

Filter by location (all three, or one at a time) and by period (last 6 months, last 12, or all 18). Every number
on the page responds to both.

| Section | Contents |
|---|---|
| Totals | Profile views, customer actions, action rate, recorded searches, website clicks, direction requests, phone calls, menu views, food orders, new reviews and average stars |
| Views and actions | Monthly series, per restaurant when unfiltered |
| What people did | The five recorded action types, sized against each other |
| How people searched | Discovery, Branded and Competitor searches by month, the largest discovery terms, and the rival names that surfaced a Wild Eggs profile |
| Reviews | New reviews per month with the average star rating |

Every chart has a hover tooltip, keyboard focusable bars, and a Table view button, so the numbers behind a chart
can be read without it.

## Where the numbers come from

The page holds no numbers of its own. It reads one file from the Master Dashboard's site:

    https://dashboards.legitrics.com/WildEggs-Master/data/gbp-data.js

That file is rebuilt once a month by the "Google monthly refresh" job in the WildEggs-Master repository. The job
reads Google Business Profile through Google's own API, keeps every pull, and writes the latest 18 full months.
Nobody has to export anything or edit this page: when the month's file is published, the page shows it.

- **Views and actions** are Google's own daily figures added up by month. Total actions are phone calls, website
  clicks, direction requests, bookings and food orders, which is how Google's export totals them. Menu views are
  reported beside them.
- **Searches** are the terms Google recorded for each profile, split three ways. Branded: the search names Wild
  Eggs, misspellings included. Competitor: it names another restaurant. Discovery: everything else. The list of
  competitor names is kept in `pipeline/google/build_gbp.py` in the WildEggs-Master repository; adding a name
  there is one line.
- **Reviews** are the reviews written in each month that are on the profile today, with their average stars. A
  review Google or its author has since removed is not counted.

## Data notes

- Google serves about 18 months of profile data at a time. Older months stay available here only because every
  monthly pull is kept.
- Google reports a term with fewer than roughly 15 impressions in a month as below its threshold. Those count as
  0, so the long tail is understated. Totals are what Google reports, not an estimate of true volume.
- Food orders are recorded by Google only for orders placed through a connected provider. The small counts
  reflect that, not the restaurants' order volume.
- Tates Creek opened on 21 August 2025, so its series starts part way through.

## Changing the page

`index.html` is the whole page: layout, charts, logos and the password gate. It was made from the earlier single
file version, which carried the numbers inside it, by `patch_gbp.py` (kept with the Master Dashboard's working
files). To change the look or the wording, edit `index.html` and commit; GitHub Pages republishes it in about a
minute.

Built to the Legit Marketing Group brand standard: navy `#003057`, Fira Sans, square corners, white chart
surfaces, official logo artwork. Series colors are navy for Discovery, steel `#5E7C99` for Branded and a warm
`#A8550D` for Competitor, chosen so the three stay apart for color blind readers.
