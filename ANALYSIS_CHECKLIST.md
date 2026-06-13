# Mandatory Match Analysis Checklist

> **Purpose**: Every match analysis MUST pass every applicable item on this checklist before the final report is generated.
> **Enforcement**: Each analyst report must include a completed checklist section at the bottom confirming all items are passed.
> **Reference**: Australia vs Turkey reports (`montecarlo_report_australia_turkey.md`, `statsmarkets_report_australia_turkey.md`, `scout_tactical_report_australia_turkey.md`) are the quality benchmark.

---

## PRE-FLIGHT (Before Any Analysis Begins)

These items MUST be completed before any analysis work starts. Mark each completed or N/A.

- [ ] **Elo values read from `elo_cache_2026.json`** -- NOT estimated, NOT from memory. Record the exact values.
      - Team A Elo: _______
      - Team B Elo: _______
      - File path verified: `___/data/elo_cache_2026.json`
- [ ] **Squad data read from team squad JSON files** (ScoutFootball data or `wc2026_players_processed.json`)
      - Source file(s): _______
      - Number of players per team verified: Team A ___, Team B ___
- [ ] **All named players confirmed to exist in squad data** -- Grep the squad JSON for every player name used in the report BEFORE writing.
      - Team A players verified: _______
      - Team B players verified: _______
- [ ] **Real-time news searched** with specific source URLs, including:
      - Injuries and lineup confirmations (pre-match press conference)
      - Recent friendly/warm-up match results
      - Team camp reports (morale, travel, weather)
      - Source URL(s): _______
- [ ] **Actual betting odds sourced** -- Record source name, timestamp, and specific odds.
      - Source: _______ (e.g., Bet365, Pinnacle, local bookmaker)
      - Timestamp: _______
      - 1X2 odds recorded: `___ / ___ / ___`
      - Asian handicap: `___`
      - Over/Under 2.5: `___`
- [ ] **Head-to-head historical data collected**
      - Last 5 meetings (or all available): _______
- [ ] **Group/competition context reviewed**
      - Opponents remaining in group, points scenario: _______

---

## MONTE CARLO ANALYST CHECKLIST

- [ ] **Poisson lambda calculated with the exact formula**:
      ```
      lambda = 1.3 + (modified_elo - 1700) / 500
      ```
      - Team A modified Elo: ___, lambda_A = ___
      - Team B modified Elo: ___, lambda_B = ___
- [ ] **Full P(k;lambda) table for both teams** (0 through 5+ goals) -- Poisson probability distribution computed and displayed.
- [ ] **Complete score probability matrix** -- All scores with >1% probability listed with exact joint probability.
- [ ] **Three-model comparison table** including:
      - Poisson xG
      - Simple Elo (`0.5 + elo_diff/1000`)
      - Bradley-Terry (`1.0 / (1.0 + exp(-elo_diff/80))`)
      - Market implied probabilities
      - Optional: Opta or other external reference
- [ ] **Squad depth analysis** computed from player ratings:
      - Starting XI average rating vs bench (players 12-26) average rating
      - Depth score (quantitative)
      - Both teams comparable
- [ ] **6+ scenario sensitivity analysis** -- At least 6 scenarios varying key inputs:
      - Baseline (current best estimate)
      - Full strength both teams
      - Key injury scenarios (each major doubt in/out)
      - "First goal" conditional scenarios
      - Extreme weather / red card / other match events
- [ ] **Modified Elo computed via actual model code** (run `_compute_modified_elo()` from `team_scoring.py`), not manual guesswork.
      - If code cannot be run, document WHY and use exact formula from config:
        - Age structure (20%), tournament experience (25%), recent form (15%), coaching (10%), mystic (5%), base Elo anchor (35%)
- [ ] **Injury/absence impact quantified in Elo terms** -- Each confirmed absence gets a specific Elo adjustment value with rationale.
- [ ] **Goal market analysis**:
      - Over/Under 2.5 probability computed
      - BTTS Yes/No probability with formula
      - Clean sheet probabilities for each team

---

## SCOUTTACTICAL ANALYST CHECKLIST

- [ ] **All mentioned players verified against squad JSON** -- Run `grep -i "player_name" squad_file.json` for EVERY named player before writing the report.
      - If a named player is NOT found in squad data, REMOVE the reference
      - Document which players were verified: _______
- [ ] **ASCII formation diagrams** use confirmed players only -- NO speculative lineup names.
      - Formation diagram for Team A: ___
      - Formation diagram for Team B: ___
- [ ] **5+ detailed matchup tables** with quantitative ratings (minimum structure):
      - Player comparison (club, height, key stats)
      - Numerical rating per dimension (e.g., +3/-3 scale or 1-10)
      - Net advantage with explanation
- [ ] **Three match pathways** with:
      - Trigger condition for each pathway
      - Phase-by-phase timeline (0-25', 25-45', 45-70', 70-90')
      - Probability assigned to each pathway
      - Most likely score for each pathway
- [ ] **Poisson prediction** with injury/home/surface modifiers applied:
      - Attack Strength (xGF/90) for each team
      - Defense Strength (xGA/90) for each team
      - Surface modifier (if applicable)
      - Injury/absence modifier with specific value
      - Final lambda calculation shown
- [ ] **Tactical X-factors identified** (minimum 3):
      - Surface/turf analysis with quantified impact
      - Set piece asymmetry with height comparison table
      - Key positional battle with structural analysis
- [ ] **Set-piece analysis**:
      - Height comparison table (attackers vs defenders on set pieces)
      - Set-piece goal probability for each team
      - Key taker and delivery analysis

---

## STATSMARKETS ANALYST CHECKLIST

- [ ] **Poisson lambda via `attack x defense / league_avg` method** (NOT the Monte Carlo formula -- this is a different model):
      ```
      lambda_A = attack_strength_A * defense_weakness_B / league_avg
      lambda_B = attack_strength_B * defense_weakness_A / league_avg
      ```
      - Team A attack strength (xG/90 or actual G/90): ___
      - Team B defense weakness (xGA/90 or actual GA/90): ___
      - League average: ___ (default 1.30 if unavailable)
- [ ] **xG calibration applied** -- Distinguish between actual goals and expected goals (xG). Note if a team is overperforming or underperforming their xG. Use xG as the primary input, not actual goals.
- [ ] **Full score matrix displayed** -- All scores with >0.5% probability, sorted by probability, with:
      - Rank, score, calculation (P(i) x P(j)), cumulative probability
- [ ] **deMargin calculation shown** with raw odds:
      - Raw odds: `___ / ___ / ___`
      - Raw implied: `___% / ___% / ___%`
      - Total overround: `___%`
      - deMargin formula: `true_prob = implied_prob / total_overround`
      - Fair odds: `___ / ___ / ___`
- [ ] **Kelly criterion computed for each value bet**:
      ```
      f* = (b * p - q) / b
      where b = decimal_odds - 1, p = model probability, q = 1 - p
      ```
      - At least 3 candidate bets evaluated
      - Recommended fractional Kelly (1/4) shown
      - Bet size as % of bankroll specified
- [ ] **Sentiment analysis with historical correlation**:
      - 5+ sentiment events listed with direction and magnitude
      - Net sentiment score for each team
      - Historical comparison: how teams with similar sentiment differential performed (128+ match database reference)
- [ ] **Odds movement analysis**:
      - Opening vs current odds for all major markets
      - Asian handicap line movement
      - Over/Under line movement
      - Direction signal (smart money or public money?)
- [ ] **AI model consensus comparison** (if available):
      - ChatGPT recommendation and rationale
      - Claude recommendation and rationale
      - Gemini or other model recommendation
      - Comparison with own analysis
- [ ] **BTTS (Both Teams to Score) calculation**:
      ```
      P(Team A scores) = 1 - P(0; lambda_A)
      P(Team B scores) = 1 - P(0; lambda_B)
      BTTS Yes = P(Team A scores) * P(Team B scores)
      ```
- [ ] **Over/Under probabilities for multiple lines** (0.5, 1.5, 2.5, 3.5, 4.5)

---

## CROSS-VALIDATION AND SYNTHESIS CHECKLIST

- [ ] **Three independent report files saved** to the project root:
      - `monte_carlo_report_<match>.md` (Analyst 1)
      - `scout_tactical_report_<match>.md` (Analyst 2)
      - `statsmarkets_report_<match>.md` (Analyst 3)
- [ ] **All three analysts output standardized probability triplets** `{TeamA_win%, Draw%, TeamB_win%}` in matching format.
      - Analyst 1 (MonteCarlo): `___ / ___ / ___`
      - Analyst 2 (ScoutTactical): `___ / ___ / ___`
      - Analyst 3 (StatsMarkets): `___ / ___ / ___`
- [ ] **Consensus table with quantified agreement percentages** for each debated proposition:
      - Proposition 1 consensus: __%
      - Proposition 2 consensus: __%
      - Proposition 3 consensus: __%
- [ ] **Weighted average computed** with specified weights:
      - MonteCarlo: 35%, ScoutTactical: 35%, StatsMarkets: 30%
      - Calculation shown: `final_X = 0.35 * MC_X + 0.35 * ST_X + 0.30 * SM_X`
- [ ] **Investment ratings follow the star system exactly**:
      - *** = Triple consensus + edge >5%
      - ** = Dual consensus + edge >2%
      - * = Single signal, independent judgment needed
      - X = Deep negative EV or unanimous negative
- [ ] **Cross-debate section** documents 3 core disagreements with each analyst's position in a structured ASCII block.
- [ ] **Key data sources documented** in appendix with source name and URL.

---

## Quality Benchmark Reference

Each section of the analysis should match or exceed the corresponding section in:

| Reference Report | File | Key Sections |
|---|---|---|
| Monte Carlo | `montecarlo_report_australia_turkey.md` | 16 sections: Elo base, factor adjustments, injury impact, squad scoring, Poisson xG, score distribution, goal market, 3-model comparison, depth, key players, sensitivity, verdict |
| StatsMarkets | `statsmarkets_report_australia_turkey.md` | 7 sections: Poisson model with lambda, historical stats, deMargin/Kelly, odds movement, sentiment, upset risk, conclusion |
| ScoutTactical | `scout_tactical_report_australia_turkey.md` | 8 sections: formation matchup, 6 matchup tables, X-factors, 3 pathways, Poisson, MVP, formation diagram, conclusion |

---

## Checklist Sign-off

```
Report: <TeamA> vs <TeamB>
Analyst: <Name>
Date: <YYYY-MM-DD>

Pre-flight items passed:  __/__
Monte Carlo items passed: __/__
ScoutTactical items passed: __/__
StatsMarkets items passed: __/__
Cross-validation items passed: __/__

All critical items (marked RED in deep review) confirmed: YES / NO
Notes: ________________________________________
```
