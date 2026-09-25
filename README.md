# English Football Pricing Model

A pre-match football analytics and pricing framework covering the Premier League, Championship, League One and League Two.

The project is built on a historical database of 8,500+ matches and is designed to turn historical team and player performance into pre-match probabilities and fair betting prices.

## Project Aim

The aim is to build a repeatable football pricing system rather than predict individual matches in isolation.

The modelling framework follows:

**Team Strength → Match Context → Team Distributions → Player Distributions → Market Probabilities → Fair Prices**

Models are evaluated chronologically so that predictions are tested only against matches that occurred after the data used to build them.

## Current Models

### Team Strength
Pre-match attacking and defensive strength ratings using historical performance, opponent adjustment, time weighting and regression toward league averages.

### Team Shots
Expected team-shot model combining:

- League home/away shot environment
- Team shot-creation strength
- Opposition shot-concession strength
- Regression toward league averages

The final model improved out-of-sample MAE from **3.87 shots using the league baseline to 3.63 shots**.

### Player Shots
Player-shot pricing model combining:

- Expected team shots
- Player previous-10 shot share
- Confirmed starting XI
- Expected minutes
- Probability calibration

Outputs are converted into fair probabilities and prices for:

**1+ | 2+ | 3+ | 4+ | 5+ player shots**

## Model Development

Features are not retained simply because they make football sense.

Each addition is tested historically and rejected if it does not improve performance on unseen matches.

For example, opponent positional shot-concession rates were tested across multiple historical windows but failed to improve player-shot prediction and were therefore excluded from the first version of the model.

## Historical Fake-Live Testing

Models can also be tested by recreating historical matches using only information that would have been available before kick-off.

### Liverpool v Brentford — 24 May 2026

Before revealing the match outcome, the model forecast:

**Brentford expected team shots: 9.69**

Actual Brentford shots: **11**

The four highest-rated Brentford shooters were:

| Player | Expected Shots | Actual Shots |
|---|---:|---:|
| Dango Ouattara | 1.97 | 3 |
| Igor Thiago | 1.49 | 2 |
| Kevin Schade | 1.10 | 4 |
| Keane Lewis-Potter | 1.09 | 1 |

These four players subsequently accounted for **10 of Brentford's 11 shots**.

This single match is presented as an illustration of the pricing process rather than evidence of model accuracy. Model evaluation is based on the much larger historical out-of-sample testing framework.

## Development Roadmap

The wider project is being developed to include:

- Match result and goal pricing
- Team and player shots
- Corners
- Player fouls
- Player cards
- Referee effects
- Match simulation
- Market-price comparison
- Model-performance tracking

## Repository Scope

This repository is a portfolio version of a larger football analytics project.

It contains selected methodology, validation results and case studies. The full historical database, data-collection pipeline, production feature-engineering code and live pricing implementation are intentionally not included.
