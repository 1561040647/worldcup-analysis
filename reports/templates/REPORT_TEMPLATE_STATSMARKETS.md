# ___ vs ___ -- 2026 FIFA World Cup Group ___ Matchday ___ Statistical & Betting Market Analysis

**Match:** ___ vs ___ | 2026 FIFA World Cup Group ___ Matchday ___
**Date:** ___ (___ local)
**Venue:** ___, ___ (Neutral venue / Home of ___)
**Referee:** ___
**Group:** ___ (also: ___, ___)

**Methodology:** Football-2026 v3.2 quant-engine (Poisson goals model, deMargin, value identification, Kelly criterion, weighted factor scoring, sentiment analysis). Source: `C:\Users\admin\Desktop\worldcup-analysis\Football-2026\js\quant-engine.js`

---

## 1. Poisson Goals Model

### 1.1 Lambda Estimation

Using `estimateLambda()` method (quant-engine lines 127-161): `lambda = attack_strength x defense_weakness x home_factor`

**Input Data:**

| Metric | ___ (FIFA ___) | ___ (FIFA ___) |
|--------|-----------------|-------------------|
| FIFA Ranking | ~___ | ~___ |
| Recent form (last 10) | ___W-___D-___L | ___W-___D-___L |
| Goals per game (actual) | ___ (___ goals in ___ games) | ___ (___ goals in ___ games) |
| xG per game | ___ | ___ |
| Goals conceded per game | ___ (___ GA in ___ games) | ___ (___ GA in ___ games) |
| Recent ___ games goals | ___ goals | ___ goals |
| World Cup history | ___ appearances, best ___ | ___ appearances, best ___ |
| Head-to-head record | ___ | ___ |

**Quality adjustment note:** (Document if either team overperforms or underperforms their xG. State whether using xG or actual goals and why.)

**Calibrated attack/defense data:**

| Team | Adjusted goals scored | Adjusted goals conceded | Notes |
|------|---------------------|----------------------|-------|
| ___ | ___ (using xG/actual) | ___ (xGA estimated) | ___ |
| ___ | ___ (using xG/actual) | ___ (xGA estimated) | ___ |

**Lambda Calculation:**

```
lambda___ = ___ x (___ / 1.30) x ___ = ___
lambda___ = ___ x (___ / 1.30)       = ___
```

(Show work: attack_strength x (opponent_xGA / league_avg) x home_factor)

**Final Lambda:** lambda_1 = ___, lambda_2 = ___

**Total expected goals:** ___ goals

### 1.2 Poisson Goal Probabilities

Using `poissonPmf(k, lambda)` (quant-engine lines 59-62):
P(k; lambda) = (lambda^k * e^(-lambda)) / k!

| Goals | P(k; ___) ___ | P(k; ___) ___ |
|-------|-------------------|---------------------|
| 0 | ___% | ___% |
| 1 | ___% | ___% |
| 2 | ___% | ___% |
| 3 | ___% | ___% |
| 4 | ___% | ___% |
| 5 | ___% | ___% |

### 1.3 Complete Score Probability Matrix

**All scores with >0.5% probability** (independence assumption: P(i:j) = P(i; lambda_1) x P(j; lambda_2)):

| Rank | Score | Calculation | Probability | Cumulative | Scenario |
|------|-------|------------|------|------|---------|
| 1 | **___ -___** | ___ x ___ | **___%** | ___% | ___ |
| 2 | **___ -___** | ___ x ___ | **___%** | ___% | ___ |
| 3 | **___ -___** | ___ x ___ | **___%** | ___% | ___ |
| 4 | **___ -___** | ___ x ___ | **___%** | ___% | ___ |
| 5 | ___ -___ | ___ x ___ | ___% | ___% | ___ |
| 6 | ___ -___ | ___ x ___ | ___% | ___% | ___ |
| 7 | ___ -___ | ___ x ___ | ___% | ___% | ___ |
| 8 | ___ -___ | ___ x ___ | ___% | ___% | ___ |
| 9 | ___ -___ | ___ x ___ | ___% | ___% | ___ |
| 10 | ___ -___ | ___ x ___ | ___% | ___% | ___ |
| 11 | ___ -___ | ___ x ___ | ___% | ___% | ___ |
| 12 | ___ -___ | ___ x ___ | ___% | ___% | ___ |
| 13 | ___ -___ | ___ x ___ | ___% | ___% | ___ |
| 14 | ___ -___ | ___ x ___ | ___% | ___% | ___ |
| 15 | ___ -___ | ___ x ___ | ___% | ___% | ___ |
| 16 | ___ -___ | ___ x ___ | ___% | ___% | ___ |
| -- | Other scores | -- | ~___% | 100% | -- |

### 1.4 Win-Draw-Loss Probabilities

Summing joint matrix using `poissonModel()` (quant-engine lines 167-223):

| Outcome | Model Probability | Summation | Market deMargin | Difference |
|---------|---------|---------|-------------|------|
| **___ win** | **___%** | Sum P(i > j) | ___% | +/-___% |
| **Draw** | **___%** | Sum P(i = j) | ___% | +/-___% |
| **___ win** | **___%** | Sum P(i < j) | ___% | +/-___% |

**Win margin analysis (___):**

| Margin | Probability | Impact on Asian Handicap |
|--------|-------------|----------------|
| Win by 2+ goals | ~___% | Full win |
| Win by 1 goal | ~___% | Half win (for -0.75) |
| **Effective -0.75 coverage** | **~___%** | (Full + Half) |
| Draw | ___% | Full loss |
| ___ win | ___% | Full loss |

**Key finding:** (Comment on the distribution shape and any notable patterns)

### 1.5 Both Teams to Score (BTTS)

```
P(___ scores) = 1 - P(0; ___) = 1 - ___ = ___%
P(___ scores) = 1 - P(0; ___) = 1 - ___ = ___%

BTTS Yes = ___% x ___% = ___%
BTTS No  = 100% - ___% = ___%
```

**Market comparison:** BTTS Yes implied ~___%, BTTS No implied ~___%.
**Model edge:** BTTS Yes: ___% vs ___% = +/-___% (value signal).
**Model edge:** BTTS No: ___% vs ___% = +/-___% (value signal).

### 1.6 Over/Under Probabilities

| Line | Over Probability | Under Probability |
|------|---------|----------|
| 0.5 | ___% | ___% |
| 1.5 | ___% | ___% |
| **2.5** | **___%** | **___%** |
| 3.5 | ___% | ___% |
| 4.5 | ___% | ___% |

**Under 2.5 detailed breakdown:**
```
P(total=0) = P(0,0) = ___ x ___ = ___%
P(total=1) = P(1,0) + P(0,1) = ___% + ___% = ___%
P(total=2) = P(2,0) + P(1,1) + P(0,2) = ___% + ___% + ___% = ___%

Under 2.5 = ___% + ___% + ___% = ___%
Over 2.5  = ___%
```

**Market comparison:** Under 2.5 market implied ~___%.
**Model edge:** ___% vs ___% = +/-___% (value signal).

### Model Parameters Locked

| Parameter | Value |
|------|-------|
| lambda___ (final) | **___** |
| lambda___ (final) | **___** |
| Total expected goals | ___ |
| League baseline | 1.30 |
| Home factor | ___ |
| Max calculation | 8 |

---

## 2. Historical & Composite Rating Model

### 2.1 Weighted Factor Scoring

Using `Predictor._compositeScore()` (predictor.js lines 217-306) methodology:

| Factor | Weight | ___ Score | Weighted | ___ Score | Weighted | Difference |
|--------|--------|-------------|-----|----------------|-----|-------|
| FIFA Ranking | 20% | ___ (___/10) | ___ | ___ (___/10) | ___ | +/-___ |
| Recent Form | 25% | ___W-___D-___L (___/10) | ___ | ___W-___D-___L (___/10) | ___ | +/-___ |
| Attack Strength | 20% | xG ___/game (___/10) | ___ | xG ___/game (___/10) | ___ | +/-___ |
| Defense Strength | 20% | GA ___/game (___/10) | ___ | GA ___/game (___/10) | ___ | +/-___ |
| WC Experience | 10% | ___ | ___ | ___ | ___ | +/-___ |
| Injury Situation | 5% | ___ (___/10) | ___ | ___ (___/10) | ___ | +/-___ |
| Manager Factor | 5% | ___ | ___ | ___ | ___ | +/-___ |
| **Total** | **100%** | | **___** | | **___** | **+/-___** |

**Interpretation:** (Who leads and why)

### 2.2 Core Matchup Analysis

| Matchup | ___ | ___ | Net |
|---------|-------------|----------------|-----|
| ___ attack vs ___ defense | xG ___ | xGA ___ | ___ |
| ___ attack vs ___ defense | xG ___ | xGA ___ | ___ |
| Individual quality gap | (Key players) | (Key players) | ___ |

**Key insight:** (What is the fundamental nature of this matchup?)

### 2.3 Historical World Cup Match Patterns

**___ WC opening match history:**
| Year | Opponent | Result | Margin |
|------|----------|--------|--------|
| ___ | ___ | ___ | ___ |
| ___ | ___ | ___ | ___ |
| ___ | ___ | ___ | ___ |

**___ WC opening match history:**
| Year | Opponent | Result | Margin |
|------|----------|--------|--------|
| ___ | ___ | ___ | ___ |

**Closely ranked teams in WC group stage openers (n=48, since 1998):**
| Result | Frequency |
|--------|----------|
| Higher ranked win | ___% |
| Draw | ___% |
| Lower ranked win | ___% |
| Avg goals | ___ |

**Group ___ context:** (Explain what a win/draw/loss means for both teams)

---

## 3. Betting Market Deep Dive

### 3.1 deMargin True Probability

Using `deMargin()` (quant-engine lines 85-109):

| Market | ___ | Draw | ___ | Total |
|--------|--------|------|-----------|-------|
| Representative odds | ___ | ___ | ___ | -- |
| Raw implied probability | ___% | ___% | ___% | ___% |
| **deMargin true probability** | **___%** | **___%** | **___%** | **100%** |
| Fair odds | ___ | ___ | ___ | -- |

**Overround analysis:** ___% overround is (HIGH / MODERATE / LOW). Interpretation: (What does the overround level tell us about market certainty?)

### 3.2 Value Identification

Using `evaluateValue()` (quant-engine lines 255-283): edge = model probability - market deMargin probability

| Bet | Model Probability | Market deMargin | Edge % | EV/unit | Kelly (1/4) | Rating |
|-----|----------------|-----------------|--------|---------|-------------|------|
| ___ win | ___% | ___% | +/-___% | +/-___ | ___ | Value / Neutral / Low value |
| Draw | ___% | ___% | +/-___% | +/-___ | ___ | Value / Neutral / Low value |
| ___ win | ___% | ___% | +/-___% | +/-___ | ___ | Value / Neutral / Low value |
| Over 2.5 | ___% | ~___% | +/-___% | +/-___ | ___ | Value / Neutral / Low value |
| Under 2.5 | ___% | ~___% | +/-___% | +/-___ | ___ | Value / Neutral / Low value |
| BTTS Yes | ___% | ~___% | +/-___% | +/-___ | ___ | Value / Neutral / Low value |
| **BTTS No** | **___%** | **~___%** | **+/-___%** | **+/-___** | **___** | **Value / Neutral / Low value** |

**Sample Kelly calculation (for best value bet):**
```
Bet: ___ @ ___
Odds = ___, b = ___ - 1 = ___
p = ___ (model probability), q = 1 - p = ___
f_full = (___ x ___ - ___) / ___ = ___
f_fractional (1/4) = ___ x 0.25 = ___

Recommended stake: ___% of bankroll
```

### 3.3 Asian Handicap Analysis

**___ -0.75 line evaluation:**

| Scenario | Probability | Bet Result | 1 unit @ ___ Payout |
|----------|-------------|------------|-----------------|
| ___ win by 2+ | ___% | Full win | +___ units |
| ___ win by 1 | ___% | Half win | +___ units |
| Draw | ___% | Full loss | -1.00 units |
| ___ win | ___% | Full loss | -1.00 units |

**EV Calculation:**
```
EV = ___ x ___ + ___ x ___ + ___ x (-1.00) + ___ x (-1.00)
   = ___ + ___ - ___ - ___
   = ___
```

**EV = ___% -- (Positive / Neutral / Negative value).**

### 3.4 Odds Movement Signals

Using `oddsMovement()` (quant-engine lines 293-345):

| Market | Opening | Current | Change | Signal |
|--------|---------|---------|--------|--------|
| ___ win | ~___ | ~___ | ___ | ___ |
| Draw | ~___ | ~___ | ___ | ___ |
| ___ win | ~___ | ~___ | ___ | ___ |
| Asian Handicap | ___ | ___ | ___ | ___ |
| Over/Under 2.5 Over | ~___ | ~___ | ___ | ___ |
| Over/Under 2.5 Under | ~___ | ~___ | ___ | ___ |

**Signal interpretation:**
- (Direction of smart money, any signs of steam moves, public bias assessment)
- (Relationship between handicap movement and over/under movement -- consistent or contradictory?)

### 3.5 AI Model Consensus

| AI Model | Recommendation | Logic | Assessment |
|-----------|-------|---------|-------------|
| ChatGPT | ___ | ___ | ___ |
| Claude | ___ | ___ | ___ |
| Gemini | ___ | ___ | ___ |

---

## 4. News Sentiment Analysis

### 4.1 Quantified Sentiment Score

| Event | Impact | Score |
|-------------|--------|-------|
| (Event with details) | Positive/Negative for ___ | +/-___ |
| (Event with details) | Positive/Negative for ___ | +/-___ |
| (Event with details) | Positive/Negative for ___ | +/-___ |
| (Event with details) | Positive/Negative for ___ | +/-___ |
| (Event with details) | Positive/Negative for ___ | +/-___ |
| (Event with details) | Positive/Negative for ___ | +/-___ |

**Net sentiment score:**
- ___: **+/-___** (Strongly positive / Positive / Neutral / Negative / Strongly negative)
- ___: **+/-___** (Strongly positive / Positive / Neutral / Negative / Strongly negative)
- Sentiment differential: **+/-___** favoring ___

### 4.2 Sentiment-Market Correlation Analysis

Based on Football-2026 database (128+ World Cup matches since 2018):

| Sentiment Differential | Matches | Expected Win % | Actual Win % | Deviation |
|-------------|-------|-----------------|--------------|-------|
| Favorite > +3.0 | ___ | ___% | ___% | ___% underperformance |
| Favorite +1.0 to +3.0 | ___ | ___% | ___% | ___% underperformance |
| Balanced -1.0 to +1.0 | ___ | ___% | ___% | ___% outperformance |
| Favorite < -1.0 (underdog) | ___ | ___% | ___% | ___% outperformance |

**Application to this match:** (What does history say about teams with similar sentiment profiles?)

### 4.3 Key Narrative Factors

**___ Narrative:**
1. (Narrative point 1)
2. (Narrative point 2)
3. (Narrative point 3)

**___ Narrative:**
1. (Narrative point 1)
2. (Narrative point 2)
3. (Narrative point 3)

---

## 5. Upset Risk Assessment

### 5.1 Quantified Upset Probability

| Scenario | Model Probability | Historical Baseline | Range |
|----------|-----------------|---------------------|-------|
| ___ win (full upset) | ___% | ~___% | ___% |
| Draw (semi-upset) | ___% | ~___% | ___% |
| **___ at least 1 point** | **___%** | ~___% | **___%** |

**Key finding:** (What is the true upset risk?)

### 5.2 Most Likely Upset Paths

**Path A: Defensive Stalemate (Most Likely -- ~___% probability)**
1. (Phase-by-phase scenario description)
2. Most likely scores: ___ (___%)
3. **Combined probability:** ___%

**Monitoring indicators:**
- (Indicator 1)
- (Indicator 2)
- (Indicator 3)

**Path B: Counter-attack Upset (~___% probability)**
1. (Phase-by-phase scenario description)
2. Most likely scores: ___ (___%)
3. **Combined probability:** ___%

**Monitoring indicators:**
- (Indicator 1)
- (Indicator 2)
- (Indicator 3)

### 5.3 Upset Factor Analysis

| Factor | Impact | Direction |
|--------|--------|---------|
| (Factor 1) | High/Medium/Low | (Effect on match) |
| (Factor 2) | High/Medium/Low | (Effect on match) |
| (Factor 3) | High/Medium/Low | (Effect on match) |
| (Factor 4) | High/Medium/Low | (Effect on match) |

**Combined upset risk:** **Low / Medium-Low / Medium / Medium-High / High**
(Rationale for the rating)

---

## 6. Score Probability Distribution Top 6

| Rank | Score | Probability | Cumulative | Scenario |
|------|-------|-------------|------------|----------|
| 1 | **___ -___** | **___%** | ___% | ___ |
| 2 | **___ -___** | **___%** | ___% | ___ |
| 3 | **___ -___** | **___%** | ___% | ___ |
| 4 | **___ -___** | **___%** | ___% | ___ |
| 5 | **___ -___** | **___%** | ___% | ___ |
| 6 | **___ -___** | **___%** | ___% | ___ |

**Score group analysis:**
- ___ clean sheet wins: ___%
- Both teams score: ___%
- Draws: ___%
- ___ clean sheet wins: ___%

---

## 7. Conclusion

### 7.1 Primary Prediction

**___ (prediction)**

| Metric | Value |
|--------|-------|
| Model probability (___ outcome) | ___% |
| Market implied probability | ~___% |
| **Most exact score:** ___ -___ (___%) |
| **Model confidence:** ___/100 |
| **Trap match warning:** Yes / No |

**Core assessment:** (Who wins, why, and is the market efficient?)

### 7.2 High Value Recommendations

| Bet | Model Probability | Fair Odds | Market Odds | Edge % | Kelly Stake | Rating |
|-------|-----------|-----------|-------------|--------|-------------|------|
| ___ | ___% | ___ | ___ | +/-___% | ___% | Value Rating |
| ___ | ___% | ___ | ___ | +/-___% | ___% | Value Rating |

**Combination recommendation (10 units):**
- ___ units ___ @ ___
- ___ units ___ @ ___
- ___ units reserve for live betting

### 7.3 Bets to Avoid

| Bet | Reason to Avoid |
|-------|-------------|
| ___ | ___ |
| ___ | ___ |
| ___ | ___ |

### 7.4 Three Key Deciding Factors

1. **___:** (Factor description)

2. **___:** (Factor description)

3. **___:** (Factor description)

### 7.5 Final Assessment

| Dimension | Assessment |
|-----------|------------|
| **Most likely score** | ___ -___ (___%) |
| **Result lean** | ___ (___%) |
| **Best value bet** | ___ (+/-___% edge) |
| **Secondary value** | ___ |
| **Signal consistency** | ___ |
| **Landmines to avoid** | ___ |
| **Model confidence** | ___/100 |
| **Upset warning** | ___% at least 1 point for ___ |
| **Trap match assessment** | Yes / No |
| **Market efficiency** | ___ |

### 7.6 Risk Warnings

- (Risk factor 1)
- (Risk factor 2)
- (Risk factor 3)
- (Risk factor 4)

**Bottom line:** (One-paragraph final assessment)

---

## Appendix: Methodology Reference

All calculations follow Football-2026 v3.2 `quant-engine.js` methodology:

| Function | File:Line | Purpose |
|--------|-----------|---------|
| `deMargin()` | `quant-engine.js:85-109` | Remove overround, restore true probability |
| `estimateLambda()` | `quant-engine.js:127-161` | Attack-defense cross method for expected goals |
| `poissonModel()` | `quant-engine.js:167-223` | Derive complete score matrix from lambda |
| `kelly()` | `quant-engine.js:234-249` | Kelly criterion optimal stake |
| `evaluateValue()` | `quant-engine.js:255-283` | Value identification (model vs market) |
| `oddsMovement()` | `quant-engine.js:293-345` | Odds movement signal identification |
| `Predictor._compositeScore()` | `predictor.js:217-306` | Weighted multi-factor composite scoring |

**Framework:** Football-2026 v3.2 (`C:\Users\admin\Desktop\worldcup-analysis\Football-2026`)
**Analyst:** Analyst-StatsMarkets
**Date:** ___
