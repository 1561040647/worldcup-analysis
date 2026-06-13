# Monte Carlo Simulation Report: ___ vs ___
## 2026 FIFA World Cup -- Group ___, Matchday ___ | ___
## ___, ___ (Neutral Venue / Home of ___)

**Generated:** ___
**Model:** 2026 World Cup Predictor (Elo + Poisson xG + Bradley-Terry + factor adjustments)
**Repository:** `C:\Users\admin\Desktop\worldcup-analysis\2026-world-cup-predictor`

---

## Table of Contents

1. [Methodology Overview](#1-methodology-overview)
2. [Base Elo Analysis](#2-base-elo-analysis)
3. [Factor-Adjusted Elo Calculations](#3-factor-adjusted-elo-calculations)
4. [Injury Impact & News Incorporation](#4-injury-impact--news-incorporation)
5. [Squad Composition & Player Scoring](#5-squad-composition--player-scoring)
6. [Poisson xG Expected Goals](#6-poisson-xg-expected-goals)
7. [Score Probability Distribution](#7-score-probability-distribution)
8. [Goal Market Analysis](#8-goal-market-analysis)
9. [Bradley-Terry & Simple Elo Models](#9-bradley-terry--simple-elo-models)
10. [Squad Depth & Substitution Impact](#10-squad-depth--substitution-impact)
11. [Key Player Analysis](#11-key-player-analysis)
12. [Historical Context & Group ___](#12-historical-context--group-___)
13. [Value Discovery vs Market](#13-value-discovery-vs-market)
14. [Sensitivity Analysis](#14-sensitivity-analysis)
15. [Mystic Factor Framework](#15-mystic-factor-framework)
16. [Verdict & Three Deciding Factors](#16-verdict--three-deciding-factors)

---

## 1. Methodology Overview

Three-layer model architecture applied to ___ vs ___:

**Layer 1: Elo Foundation** -- FiveThirtyEight-style ratings from `data/elo_cache_2026.json`
- ___ Elo: ___ (file: `C:\...\data\elo_cache_2026.json`)
- ___ Elo: ___
- Raw gap: ___

**Layer 2: Factor Adjustments** (from `config.py` and `team_scoring.py`)
- Age structure (20% weight): squad maturity index based on median age + prime player ratio
- Tournament experience (25% weight): caps >= 30 as proxy; penalty for no recent WC history
- Recent form (15% weight): actual match results blended with seed form data
- Coaching factor (10% weight): manager experience assessment
- Mystic factors (5% weight): ___ (document any host/defending champion/revenge/return bonuses)
- Venue: ___ (neutral / home for ___ / home for ___)

**Layer 3: Monte Carlo Simulation**
- Poisson xG for match-level score distribution (recommended for group stage)
- Bradley-Terry for tournament-level win probability
- Simple Elo linear model as intermediate reference

**Key adjustments in this analysis:**
- ___ injury (-___ Elo): ___
- ___ fitness doubt (-___ Elo): ___
- ___ (other key news)

---

## 2. Base Elo Analysis

### 2.1 Source Data

From `data/elo_cache_2026.json`:

```
___:     ___
___:  ___
Raw gap:    ___
```

### 2.2 What +___ Elo Means

An Elo gap of +___ means ___ is expected to score approximately ___x the goals of ___ in a neutral setting. In practical terms:

| Elo Gap | Percentile | Typical Matchup |
|---------|-----------|-----------------|
| +250 | 99th | Elite vs minnow (Brazil vs Qatar) |
| +150 | 90th | Strong favorite (France vs Morocco) |
| **+___** | **___th** | **___ (___ vs ___** |
| +50 | 55th | Slight edge (even matchup) |
| 0 | 50th | Perfectly even |

### 2.3 Elo Context in Group ___

| Team | Elo | Group Rank | Overall Rank (48 teams) |
|------|-----|-------------|------------------------|
| ___ | ___ | #___ | ~___th |
| ___ | ___ | #___ | ~___th |
| ___ | ___ | #___ | ~___th |
| ___ | ___ | #___ | ~___th |

(fill all four teams in the group)

---

## 3. Factor-Adjusted Elo Calculations

### 3.1 Full-Strength Modified Elo

Computed via `_compute_modified_elo()` in `team_scoring.py`:

| Metric | ___ | ___ |
|--------|--------|-----------|
| Base Elo | ___ | ___ |
| **Modified Elo** | **___** | **___** |
| Net adjustment | ___ | ___ |
| **Effective gap (full strength)** | | **+___** |

### 3.2 Age Structure Factor (Weight: 20%)

**___:** Mean age ___, Median ___ -- ___/___ players (___%) in golden-to-peak range (25-31)
- Squad maturity index: **___** (very high / high / moderate / low)
- Age buckets: ___ young (U22), ___ rising, ___ golden, ___ peak, ___ veteran, ___ elder

**___:** Mean age ___, Median ___ -- ___/___ players (___%) in golden range
- Squad maturity index: **___** (very high / high / moderate / low)
- Age distribution: ___ young, ___ rising, ___ golden, ___ peak, ___ veteran, ___ elder

**Winner: ___** -- ___ (reason based on age profile)

### 3.3 Tournament Experience Factor (Weight: 25%)

| Metric | ___ | ___ |
|--------|--------|-----------|
| Players with 30+ caps | ___/___ (___%) | ___/___ (___%) |
| Players with 50+ caps | ___/___ | ___/___ |
| Most capped player | ___ (___ caps) | ___ (___ caps) |
| Squad avg caps | ___ | ___ |

(Add qualitative assessment of cap quality: which leagues do the caps come from? Any World Cup experience?)

**Winner: ___**

### 3.4 Recent Form Factor (Weight: 15%)

**___:** (Recent record: W-D-L in last 10 matches, key results, goal difference)

**___:** (Recent record: W-D-L in last 10 matches, key results, goal difference)

**Winner: ___**

### 3.5 Coaching Factor (Weight: 10%)

| Manager | Team | Experience | Tournament Record |
|---------|------|-----------|-------------------|
| ___ | ___ | ___ | ___ |
| ___ | ___ | ___ | ___ |

**Winner: ___**

### 3.6 Mystic Factors (Weight: 5%)

List applicable factors:
- Venue type (neutral/home): ___
- Defending champion curse: ___
- Long absence return factor: ___
- Other qualitative factors: ___

**Result: ___ (positive / neutral / negative for ___)**

---

## 4. Injury Impact & News Incorporation

### 4.1 Confirmed Absences

**___ -- OUT (___)**
- Position: ___, Club: ___
- Age: ___, Caps: ___, Goals: ___
- ___ season stats: ___
- **Elo impact: -___ points**
- Replacement: ___ -- (quality assessment)

(Repeat for each confirmed absence)

### 4.2 Doubtful / Limited

**___ -- Expected to start, limited (___)**
- Position: ___, Club: ___
- Age: ___, Caps: ___, Goals: ___
- Injury detail: ___
- **Elo impact: -___ points**
- (Assessment of what % capacity they offer)

(Repeat for each doubtful player)

### 4.3 Positive News

- ___ (player) -- Fully fit and in good form: (details)
- ___ (player) -- Recovered from knock: (details)

### 4.4 Adjusted Elo Summary

| Scenario | ___ Elo | ___ Elo | Gap | BT ___ | BT ___ | Simple ___ |
|----------|-----------|-------------|-----|-----------|--------|-----------|
| Full strength | ___ | ___ | ___ | ___% | ___% | ___% |
| **___ (injured) + ___ (limited)** | **___** | **___** | **___** | **___%** | **___%** | **___%** |
| If ___ also out | ___ | ___ | ___ | ___% | ___% | ___% |

**Recommended operating estimate: ___ vs ___ (gap +___)**

---

## 5. Squad Composition & Player Scoring

### 5.1 Model-Generated Player Scores

| Metric | ___ | ___ |
|--------|--------|-----------|
| Average player score | **___** | **___** |
| Maximum player score | **___** | **___** |
| Starting XI avg | **___** | **___** |
| Bench (12-26) avg | **___** | **___** |
| Starting-bench gap | **___** | **___** |
| **Depth score** | **___** | **___** |

### 5.2 Highest-Rated Players

**___ (top 5 by score):**
| Player | Score | Key Attribute |
|--------|-------|-------------|
| ___ | ___ | ___ |
| ___ | ___ | ___ |
| ___ | ___ | ___ |
| ___ | ___ | ___ |
| ___ | ___ | ___ |

**___ (top 5 by score):**
| Player | Score | Key Attribute |
|--------|-------|-------------|
| ___ | ___ | ___ |
| ___ | ___ | ___ |
| ___ | ___ | ___ |
| ___ | ___ | ___ |
| ___ | ___ | ___ |

### 5.3 Squad Market Value Comparison

```
___:  ~$___ million
___: ~$___ million

Ratio: ___x in ___'s favor
```

(Add qualitative assessment of where players play -- top 5 leagues vs lower leagues)

---

## 6. Poisson xG Expected Goals

### 6.1 Formula

From README: `lambda = 1.3 + (modified_elo - 1700) / 500`

Using **adjusted Elo** (as computed in Section 4.4):

```
___ lambda    = 1.3 + (___ - 1700) / 500 = ___
___ lambda = 1.3 + (___ - 1700) / 500 = ___

Total expected goals: ___
```

### 6.2 Poisson Probability Distributions

**___ goals (lambda = ___):**
P(k; lambda) = (lambda^k * e^(-lambda)) / k!

| Goals | Probability | Cumulative |
|-------|-----------|------------|
| 0 | ___% | ___% |
| 1 | ___% | ___% |
| 2 | ___% | ___% |
| 3 | ___% | ___% |
| 4 | ___% | ___% |
| 5+ | ___% | 100.0% |

**___ goals (lambda = ___):**

| Goals | Probability | Cumulative |
|-------|-----------|------------|
| 0 | ___% | ___% |
| 1 | ___% | ___% |
| 2 | ___% | ___% |
| 3 | ___% | ___% |
| 4 | ___% | ___% |
| 5+ | ___% | 100.0% |

---

## 7. Score Probability Distribution

### 7.1 Match Outcome Probabilities (Poisson xG)

| Outcome | Probability | Implied Odds | vs Market | vs Opta |
|---------|-----------|-------------|-----------|---------|
| **___ win** | **___%** | ~___ | Market: ___% | Opta: ___% |
| Draw | ___% | ~___ | Market: ___% | Opta: ___% |
| ___ win | ___% | ~___ | Market: ___% | Opta: ___% |

**Key finding:** (Compare model with market - any significant discrepancies? What drives them?)

### 7.2 Top 10 Most Likely Scores

Score probability matrix computed as: P(i,j) = P(i; lambda_A) x P(j; lambda_B) for all i,j >= 0

| Rank | Score | Probability | Cumulative |
|------|-------|-----------|------------|
| 1 | **___ -___ ___** | **___%** | ___% |
| 2 | **___ -___ ___** | **___%** | ___% |
| 3 | ___ -___ ___ | ___% | ___% |
| 4 | ___ -___ ___ | ___% | ___% |
| 5 | ___ -___ ___ | ___% | ___% |
| 6 | ___ -___ ___ | ___% | ___% |
| 7 | ___ -___ ___ | ___% | ___% |
| 8 | ___ -___ ___ | ___% | ___% |
| 9 | ___ -___ ___ | ___% | ___% |
| 10 | ___ -___ ___ | ___% | ___% |

(Add qualitative commentary on the shape of the distribution)

### 7.3 Score Margin Distribution

| Margin | Probability |
|--------|-----------|
| ___ by 1 | ~___% |
| ___ by 2 | ~___% |
| ___ by 3+ | ~___% |
| Draw | ~___% |
| ___ by 1 | ~___% |
| ___ by 2 | ~___% |
| ___ by 3+ | ~___% |

---

## 8. Goal Market Analysis

### 8.1 Over/Under 2.5 Goals

```
Under 2.5 goals:  ___%
Over 2.5 goals:   ___%
```

**Breakdown:**
| Total Goals | Probability |
|-------------|-----------|
| 0 | ___% |
| 1 | ___% |
| 2 | **___%** (most common total) |
| 3 | ___% |
| 4 | ___% |
| 5+ | ___% |

**Assessment:** (Comment on goal expectation based on playing styles, group stage dynamics, injuries)

### 8.2 Both Teams to Score (BTTS)

```
BTTS Yes: ___%
BTTS No:  ___%
```

(Calculation: P(BTTS Yes) = (1 - P(0; lambda_A)) * (1 - P(0; lambda_B)))

**Assessment:** (Comment on BTTS likelihood based on team profiles)

### 8.3 Clean Sheet Probabilities

| Team | Clean Sheet Probability |
|------|----------------------|
| ___ | ___% |
| ___ | ___% |
| Neither | ___% |

---

## 9. Bradley-Terry & Simple Elo Models

### 9.1 Bradley-Terry Tournament Model

Formula: `prob = 1.0 / (1.0 + exp(-(elo_a - elo_b) / 80))`

Using adjusted Elos:
```
prob___ = 1.0 / (1.0 + exp(-___ / 80))
        = 1.0 / (1.0 + exp(-___))
        = 1.0 / (1.0 + ___)
        = ___%
```

### 9.2 Simple Elo Model

Formula: `prob = 0.5 + (elo_diff / 1000)`

```
prob___ = 0.5 + ___/1000 = ___%
```

### 9.3 Three-Model Comparison

| Model | ___ Win | Draw | ___ Win | Best Use |
|-------|-----------|------|-------------|----------|
| Poisson xG | **___%** | ___% | ___% | Match prediction (recommended) |
| Simple Elo | **___%** | ~___% | ~___% | Upper bound / market comp |
| Bradley-Terry | **___%** | NA | ___% | Knockout scenario only |
| Opta Supercomputer | ___% | ___% | ___% | External reference |
| Market implied | ___% | ___% | ___% | Betting market |

### 9.4 Recommended Operating Range

```
___ win:  ___ - ___%      (___ lower bound, ___ upper bound)
Draw:        ___ - ___%      (___ lower bound, ___ upper bound)
___ win: ___ - ___%    (___ lower bound, ___ upper bound)
```

(Comment on the "true probability" blend)

---

## 10. Squad Depth & Substitution Impact

### 10.1 Depth Score Comparison

```
___:    Starting: ___
           Bench:    ___   Gap: ___
           Depth:    ___ (EXCELLENT / GOOD / POOR / VERY POOR)

___: Starting: ___
           Bench:    ___   Gap: ___
           Depth:    ___ (EXCELLENT / GOOD / POOR / VERY POOR)
```

### 10.2 Practical Impact Analysis

**60th minute -- ___ leading 1-0:**
- ___ brings on ___ (___) for tired player -- quality assessment
- ___ brings on ___ (___) -- quality assessment
- (Impact on game state)

**60th minute -- ___ leading 1-0:**
- ___ brings on ___ (___) -- quality assessment
- ___ brings on ___ (___) -- quality assessment
- (Impact on game state)

**75th minute -- 0-0:**
- ___ attacking options from bench: ___
- ___ attacking options from bench: ___

### 10.3 Key Substitutes

**___:**
| Player | Age | Caps | Position | Profile |
|--------|-----|------|----------|---------|
| ___ | ___ | ___ | ___ | ___ |
| ___ | ___ | ___ | ___ | ___ |
| ___ | ___ | ___ | ___ | ___ |

**___:**
| Player | Age | Caps | Position | Profile |
|--------|-----|------|----------|---------|
| ___ | ___ | ___ | ___ | ___ |
| ___ | ___ | ___ | ___ | ___ |
| ___ | ___ | ___ | ___ | ___ |

---

## 11. Key Player Analysis

### 11.1 ___'s Key Players

**___ (age, club)** -- INJURY STATUS
- Season stats: ___
- Role / tactical importance: ___
- What the opponent must do to contain them: ___

**___ (age, club)** -- INJURY STATUS
- Season stats: ___
- Role: ___

(Continue for 3-5 key players per team)

### 11.2 ___'s Key Players

**___ (age, club)** -- INJURY STATUS
- Season stats: ___
- Role: ___

(Continue for 3-5 key players)

### 11.3 Position-by-Position Comparison

| Position | ___ | ___ | Edge |
|----------|--------|-----------|------|
| GK | ___ (age, caps) | ___ (age, caps) | **___** |
| CB | ___ | ___ | **___** |
| FB | ___ | ___ | **___** |
| CM | ___ | ___ | **___** |
| AM | ___ | ___ | **___** |
| Winger | ___ | ___ | **___** |
| Forward | ___ | ___ | **___** |
| **Depth** | **Bench avg ___** | **Bench avg ___** | **___** |

---

## 12. Historical Context & Group ___

### 12.1 World Cup Pedigree

| Team | WC Apps | Best Finish | Last WC | Gap |
|------|---------|-------------|---------|-----|
| ___ | ___ | **___** | ___ | ___ |
| ___ | ___ | **___** | ___ | ___ |

### 12.2 Head-to-Head Record

(Recent meetings with scores, dates, venues)

### 12.3 Group ___ Strategy

| Team | Elo | Key Strength | Key Weakness |
|------|-----|-------------|-------------|
| ___ | ___ | ___ | ___ |
| ___ | ___ | ___ | ___ |
| ___ | ___ | ___ | ___ |
| ___ | ___ | ___ | ___ |

(Comment on what a draw vs win vs loss means for each team's group prospects)

---

## 13. Value Discovery vs Market

### 13.1 Market vs Model Comparison

| Outcome | Market Odds | Market Implied | Poisson Model | Opta | Value Assessment |
|---------|------------|---------------|-----------|------|-----------------|
| ___ win | ___ | ___% | ___% | ___% | ___ |
| Draw | ___ | ___% | ___% | ___% | ___ |
| ___ win | ___ | ___% | ___% | ___% | ___ |
| Over 2.5 | ~___ | ___% | ___% | -- | ___ |
| BTTS Yes | ~___ | ___% | ___% | -- | ___ |

### 13.2 Why the Market May Be Wrong

1. ___ (reason 1)
2. ___ (reason 2)
3. ___ (reason 3)
4. ___ (reason 4)

### 13.3 Value Recommendations

| Bet | Model Price | Market Price | Edge | Kelly Fraction |
|-----|------------|-------------|------|---------------|
| ___ @ ___ | ___ (___%) | ___ (___%) | +___% | ___% of bankroll |
| ___ @ ___ | ___ (___%) | ___ (___%) | +___% | ___% of bankroll |
| ___ @ ___ | ___ (___%) | ___ (___%) | +___% | ___% of bankroll |

**Best value:** ___ @ ___ (+___% edge).
**Safest value:** ___ @ ___ (+___% edge).

---

## 14. Sensitivity Analysis

### 14.1 Scenario Matrix

| Scenario | ___ Win | Draw | ___ Win | Rationale |
|----------|-----------|------|-------------|-----------|
| **Baseline (current injuries)** | **___%** | **___%** | **___%** | Current best estimate |
| Both teams at full strength | ___% | ___% | ___% | (Effects) |
| ___ also OUT | ___% | ___% | ___% | (Effects) |
| ___ scores first (___%) | ~___% | ~0% | ~___% | (Game state) |
| ___ scores first (___%) | ~___% | ~0% | ~___% | (Game state) |
| Scoreless at 60' (___%) | ~___% | ~___% | ~___% | Cautious settling for point |
| (Other scenario) | ___% | ___% | ___% | (Rationale) |
| (Other scenario) | ___% | ___% | ___% | (Rationale) |

### 14.2 Key Injury Sensitivity

| ___ Status | ___ Win | Draw | ___ Win |
|-------------------|-----------|------|-------------|
| Full strength (100%) | ___% | ___% | ___% |
| **Limited (current estimate)** | **___%** | **___%** | **___%** |
| Out entirely | ___% | ___% | ___% |

### 14.3 First Goal Scorer Sensitivity

| First Scorer | Conditional Probability | Final Score Most Likely |
|-------------|----------------------|----------------------|
| ___ scores first | ___% | ___ |
| ___ scores first | ___% | ___ |
| No goal before 60' | ___% | 0-0 or 1-1 draw |

---

## 15. Mystic Factor Framework

### 15.1 Zen Three Stages

**First Stage -- "Mountain is Mountain" (Raw Data):**
(Describe the straightforward reading of the data -- who is better and why)

**Second Stage -- "Mountain is Not Mountain" (Bias Detection):**
- **Lottery paradox:** (Is anyone over-bet by the market? Is there a hidden variable?)
- **Experience gap:** (What does Elo not capture? Set-piece variance? Tournament experience?)
- **Other biases:** (Surface, weather, referee, narrative factors)

**Third Stage -- "Mountain is Mountain" (Essence):**
(Synthesize -- who actually wins and why?)

### 15.2 Tao Te Ching Analysis

**Reversal risk (___):** LOW / MODERATE / HIGH (___)

**Soft power (___):** LOW / MODERATE / HIGH (___)

### 15.3 I Ching / Qualitative Assessment

**___ -- (Hexagram name / element):**
(Philosophical assessment of playing style)

**___ -- (Hexagram name / element):**
(Philosophical assessment of playing style)

---

## 16. Verdict & Three Deciding Factors

### 16.1 Most Likely Result

```
___ -___ ___  (___%)
```

### 16.2 Predicted Scoreline Rankings

1. **___ -___ ___** (___%) -- (description)
2. ___ -___ ___ (___%) -- (description)
3. ___ -___ ___ (___%) -- (description)
4. ___ -___ ___ (___%) -- (description)
5. ___ -___ ___ (___%) -- (description)
6. ___ -___ ___ (___%) -- (description)

### 16.3 Confidence Assessment

**Overall confidence: ___/10**

**Reasons for (high/low) confidence:**
1. ___
2. ___
3. ___
4. ___
5. ___

### 16.4 Three Key Deciding Factors

1. **___:** (Description of why this matters, what to watch for, probability estimate)

2. **___:** (Description)

3. **___:** (Description)

### 16.5 Bottom Line

(Concise summary paragraph: who wins, why, key risks, and best value angles)

---

*Report generated using the 2026 World Cup Predictor framework. Model: Poisson xG with Elo factor adjustments. Injury adjustments: ___. All probabilities computed from model outputs or manually verified against model formulas.*
