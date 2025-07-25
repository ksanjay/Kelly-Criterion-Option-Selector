# Kelly Criterion LEAP-Option Allocator

A self-contained Jupyter notebook (kelly_leaps.ipynb) that sizes long-dated call-option trades using the Kelly Criterion.  It fetches live quotes, calculates edge and optimal bet sizes, and outputs a position table— all with just two prompts from the user.

⸻

1  Features

Capability	Detail
Interactive prompts	Tick-in four tickers & bankroll (≥ $3 500) right in the notebook.
Live market data	Uses Yahoo Finance (via yfinance) to pull the latest stock price and first LEAP expiry after 30 Sep 2026.
ATM-Call focus	Picks the strike closest to spot for each ticker— the most liquid, information-dense option.
Black-Scholes win-probability	Approximates p with N(d₂) and computes net-odds b from option Greeks.
Kelly-optimal sizing	Outputs fraction f and converts to whole-contract counts, respecting bankroll & granularity.
Rollover guide	Markdown cell with suggested exit / roll triggers (delta, price move, time-to-expiry).
Clean pandas output	One glance shows strike, premium, probability, Kelly f, contracts, and dollar cost.


⸻

2  Quick Start

Prerequisites

python -m pip install --upgrade yfinance pandas numpy scipy matplotlib

Run
	1.	Open the notebook in Jupyter Lab, VS Code, or Colab.
	2.	Execute cells top-to-bottom.  When prompted:
	•	Enter four tickers (e.g. GOOGL BRK.B ARM ABNB).
	•	Enter bankroll (≥ $3 500).
	3.	Review the results table and rollover rules.

Tip  Want to rerun with different tickers?  Restart the kernel and execute again.

⸻

3  Methodology & Assumptions
	•	p – Probability ITM: N(d₂) from Black-Scholes, using the option’s published IV and a 4.5 % risk-free rate.
	•	b – Net odds: (S − K)/Premium − 1 (how many dollars you win per dollar risked if ITM at expiry).
	•	Kelly fraction: f* = (p·b − (1−p)) ⁄ b, capped at zero for negative edge.
	•	Whole-contracts: The smallest integer contracts that doesn’t exceed f* × bankroll; minimum 1 if f > 0.
	•	Data freshness: Live pull at execution time; rerun for updated quotes.

⸻

4  Interpreting the Output

Column	Meaning
Prob.ITM	Modeled chance the call finishes in-the-money.
b	Risk-reward multiple; higher b ⇒ bigger edge.
Kelly f	Optimal bankroll % to risk on this trade.
Contracts	Whole contracts suggested.
Cost($)	Capital actually deployed.

Total deployed vs. bankroll is printed below the table.

⸻

5  Rollover / Exit Cheatsheet

Trigger	Action
Δ ≥ 0.75  or  option value ≥ 3× cost	Sell ½ position to lock gains.
−10 % price drop & Δ < 0.20	Close— edge likely gone.
365 days to expiry	Roll to next-Jan LEAP one strike higher.

All exits are suggestions; adjust to your risk tolerance and tax situation.

⸻

6  Disclaimer

This notebook is educational material only.  It is not investment advice.  Options involve risk and may not be suitable for all investors.  Past performance ≠ future results.  Always do your own research or consult a qualified adviser.

⸻

7  License

MIT License © 2025
Feel free to fork, extend, and share— just keep this attribution intact.
