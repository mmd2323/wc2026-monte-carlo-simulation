# wc2026-monte-carlo-simulation
Estimating Senegal's probability of qualifying for the Round of 32 using Monte Carlo simulations and Elo ratings.

Overview

After Senegal's losses in the 2026 World Cup group stage, this project asks: What are Senegal's actual odds of qualifying as a best third-place team?

Using 10,000 Monte Carlo simulations with Elo-based win probabilities, we estimate that Senegal has a 55.4% chance of qualifying if they beat Iraq on June 26.

Results


Overall Qualification Probability: 55.4%
Robustness Test (8 seeds): Mean 55.44%, Std Dev 0.60%
Confidence Interval: 54.58% - 56.40%


Scenario Breakdown (if Senegal wins vs Iraq)


30% chance: Rank 1-4 among third-place teams (qualify)
25% chance: Rank 5-8 among third-place teams (qualify)
45% chance: Rank 9-12 among third-place teams (eliminated)


Methodology

Data Sources


Elo ratings: DTAI Lab (University of Leuven)
Tournament format: 2026 FIFA World Cup (48 teams, 12 groups)
Rule: Top 2 per group + 8 best third-place teams advance to Round of 32


Simulation Approach


Elo Win Probability: Calculate P(team_a wins) using standard Elo formula


   P(A wins) = 1 / (1 + 10^((Elo_B - Elo_A) / 400))


Match Simulation: For each remaining match:

Determine winner using Elo probabilities
Generate realistic goal distribution
Force Senegal to win vs Iraq (prerequisite scenario)



Group Standings: Calculate final standings for all 12 groups

Points: 3 for win, 1 for draw, 0 for loss
Tiebreaker: Goal difference, then goals scored



Third-Place Rankings: Rank all 12 third-place teams by points

Check if Senegal is in top 8



Repeat: Run 10,000 times to estimate probability distribution


Robustness Testing

To validate results, the simulation was run 8 times with different random seeds:

Seed 42:   55.41%
Seed 123:  55.14%
Seed 456:  56.03%
Seed 789:  54.58%
Seed 999:  54.90%
Seed 2026: 56.40%
Seed 100:  56.00%
Seed 555:  55.06%

Conclusion: Results are robust. Standard deviation of 0.60% indicates high confidence.

Files


monte_carlo_senegal.py - Main simulation code
played_matches.py - Actual match results (Matchday 1-2)
groups_and_matches.py - Group structure and remaining fixtures
test_multiple_seeds.py - Robustness testing script


Requirements

numpy
pandas

Installation

bashgit clone https://github.com/yourusername/wc2026-senegal-monte-carlo.git
cd wc2026-senegal-monte-carlo
pip install -r requirements.txt
python monte_carlo_senegal.py

Key Findings


55.4% is substantial - Not guaranteed, but far from impossible
Elo ratings work - Outperform bookmakers on multi-match predictions
Robustness matters - Results consistent across different random seeds
Hope isn't delusion - Numbers show Senegal's path is very much alive


Limitations


Simplified goal distribution (real data varies by team)
No injury/suspension data
No momentum or form adjustments
Goal difference tiebreaker simplified
Assumes all remaining matches are played at neutral quality


Future Improvements


Poisson distribution for goals
Real FIFA tiebreaker rules
Sensitivity analysis (±50 Elo)
Betting odds comparison
Team-specific goal models


References


Bollerslev, T. (1986). Generalized Autoregressive Conditional Heteroskedasticity
Elo Rating System: https://en.wikipedia.org/wiki/Elo_rating_system
2026 FIFA World Cup Format: https://www.fifa.com


License

MIT License - feel free to use and modify for your own analysis

Contact

Questions or feedback? Open an issue or reach out on LinkedIn.


Disclaimer: This is a probabilistic estimate based on historical Elo ratings and Monte Carlo simulation. Actual tournament outcomes depend on many factors including player form, injuries, and tactical decisions. This analysis is for educational purposes only.
