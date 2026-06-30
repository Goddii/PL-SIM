# Full Season Simulator — README

## What this is

A single self-contained HTML file (`pl-runin-sim.html`) that simulates an
entire 38-gameweek football season for the 20 clubs in your standings table,
using a Poisson-distribution goal model. Open it in any browser — no server,
no build step, no dependencies.

## What it does

1. Takes the current league table (points, wins, draws, losses, goals
   for/against) for 20 clubs as hard-coded input data.
2. Converts each club's goals-for and goals-against into a per-game rate —
   this becomes that club's "attack strength" and "defense weakness."
3. Generates a synthetic fixture list: a standard double round-robin where
   every club plays every other club twice (once home, once away), spread
   across 38 gameweeks of 10 matches each.
4. Simulates every match using a Poisson random goal model, adjusted for
   each side's attack/defense strength relative to the league average, plus
   a configurable home-advantage boost.
5. Builds a final league table from the simulated results (0 points start,
   3 for a win, 1 each for a draw) and lets you step through every
   gameweek's scores one at a time.

## What it is NOT

- **Not a prediction.** It's a random simulation. Run it twice and you'll
  get two different seasons. It's useful for exploring "what could plausibly
  happen given these teams' current scoring rates," not for forecasting the
  real season.
- **Not the real fixture list.** No actual remaining/future Premier League
  fixtures were provided, so the schedule is a generated round-robin, not
  the real calendar. Match dates, kickoff order, and specific opponents on
  specific weeks won't match the real season.
- **Not based on scraped or live data.** All team data is the table you
  gave me, hard-coded into the file. There's no live odds, injury, or form
  data feeding in beyond the season-to-date goals/points you supplied.

## How to use it

1. Open the HTML file in a browser (double-click it, or drag it into a
   browser tab).
2. Optionally adjust the **Home advantage** slider (0–40%). This multiplies
   the home team's expected goals upward before the random draw — higher
   values make home wins more common.
3. Click **Simulate 38-game season**. This runs the entire season instantly
   (no animation/delay beyond a fraction of a second).
4. Use **Prev / Next** to step through each of the 38 simulated gameweeks
   and see every match score.
5. Scroll down to see the final simulated table (W/D/L/GF/GA/GD/Pts), with
   the top 5 highlighted green (European-spot proxy) and bottom 3
   highlighted red (relegation proxy).
6. Click the button again to re-roll a brand new random season from
   scratch.

## The model, in plain terms

For a given match between a home club and an away club:

- Each club has an **attack rate** (average goals scored per game this
  season) and a **defense rate** (average goals conceded per game).
- The "expected goals" for each side in this match = league-average goals
  per game × (that side's attack rate ÷ league average) ×
  (opponent's defense rate ÷ league average).
- The home side's expected goals are then multiplied by the home-advantage
  setting.
- The actual goals scored are drawn randomly from a **Poisson
  distribution** using that expected value as its mean. Poisson is the
  standard statistical model for "number of independent events in a fixed
  window" — it's widely used for football score simulation because goals
  are relatively rare, discrete events.

## Known limitations / simplifications

- Attack/defense strength is estimated purely from season-to-date
  goals-for/against — it ignores who those goals came against (a team that
  scored a lot against weak defenses looks artificially strong).
- The "Form" column from your original table wasn't used, since no actual
  values were supplied for it.
- No injuries, suspensions, fatigue, manager changes, or any other
  real-world variable are modeled — only goal-scoring rate and home
  advantage.
- The synthetic schedule is structurally realistic (everyone plays everyone
  home and away once) but is not the true fixture calendar.

## Files

- `pl-runin-sim.html` — the simulator itself (open this).

