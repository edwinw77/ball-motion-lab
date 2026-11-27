# Ball Motion Lab

**Live page: https://edwinw77.github.io/ball-motion-lab/**

A single-page simulator that shows how a bowling ball moves down the lane: where it skids, where it hooks and where it rolls. It compares balls by their published specs under the same conditions. It models a right-handed bowler on fresh oil.

## What it does

- **Compare one ball across weights.** Each weight has its own RG and differential, so lighter balls can behave differently.
- **Compare balls at one weight.** Up to 6 lines at once.
- **Conditions:** oil pattern (House 40 / Short 35 / Long 45 / Sport 41), ball speed and rev rate (preset buttons or sliders), and release board.
- **Aim modes:**
  - **Each ball:** each ball gets its own line to the pocket. Leave the release board empty to find the optimal line (entry angle as close to 6° as possible, breakpoint at board 4 or further left).
  - **Same line:** every ball is thrown on one shared line (the average of their own lines), so the differences show directly.
  - **Manual:** you set the release and the target at the arrows.
- **Readouts per ball:** release, target, hook start, breakpoint, roll point, hook shape (angular / medium / arc), entry angle, board at the pins and speed at the pins.
- Hover over the lane to see each ball's board and phase (skid / hook / roll) at any distance.
- Speed can be shown in mph or km/h.

## Ball data

Ball specs live in [`balls.csv`](balls.csv) and are also built into the page. To use your own list, click **Load CSV** on the page. It is remembered in your browser, and **Built-in data** switches back. Use one row per ball per weight:

```csv
name,brand,coverstock type,surface finish (grit),symmetric/asymmetric,weight,RG,differential,intermediate differential (asym only)
Ion Pro Pearl,Storm,Pearl Reactive,4000-grit Abralon,Asymmetric,15lb,2.47,0.035,0.014
Bionic,Storm,Hybrid Reactive (NRG Hybrid),4000-grit Abralon,Symmetric,15 lb,2.47,0.050,N/A
```

- **Coverstock:** any text containing plastic, urethane, solid, hybrid or pearl.
- **Surface finish:** the grit is read from the text, and multi-step finishes use the final grit. "Polished" / "gloss" counts as polished; "compound" counts as a light polish. A polish or compound over a coarse base grit (e.g. "500 Siaair / Factory Polish") is treated as a smooth surface, not as the base grit.
- **Weight** can be written `15`, `15lb` or `15 lb`. Intermediate differential can be blank or `N/A` for symmetric balls.

## How the model works

- The ball is a rigid sphere that slides and spins on the lane. Friction against the slip at the contact point slows it, turns it (the hook) and converts its spin until it rolls.
- **RG** sets the moment of inertia: a lower RG revs up and rolls sooner.
- **Differential** (plus intermediate differential for asymmetric balls) stands in for flare and adds hook.
- **Cover and finish** set friction in oil and on dry boards, and how sharply friction rises as the oil thins. Sanded solid and hybrid covers read early with a smooth arc. Pearl and polished covers skid longer, then snap.
- **Weight** on its own barely changes the path. Weights differ through their RG and differential.

The friction and flare values are calibrated estimates, not lab measurements. Use the results to compare balls, not to predict exact boards.

**Not modelled:** layout (pin-to-PAP, drilling angle), oil breakdown over a session, left-handed bowlers, and pin action.

## Running locally

No build or install: open `index.html` in a browser.
