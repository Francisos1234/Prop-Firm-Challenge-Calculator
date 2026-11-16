# Prop Firm Challenge Calculator.

A trading analysis tool for examining prop firm challenges through the relationship between profit targets, drawdown limits and trading risk.

**Live application:** [Open the Prop Firm Challenge Calculator](https://script.google.com/macros/s/AKfycbwnaxx80HH8lQtKq4RHcDCzDiXhXzvbLEqvZcLG7QeLJSCT9v-QReTIKrf6S_MtXKG1KA/exec)

**Repository:** [Francisos1234/Prop-Firm-Challenge-Calculator](https://github.com/Francisos1234/Prop-Firm-Challenge-Calculator)

An independent project by **Francis Chizurumoke**, developed with coding assistance from Claude.

---

## The idea behind the project

A prop firm challenge is often presented as a simple objective: reach a profit target without breaching a maximum loss or drawdown limit.

But the target alone does not describe the difficulty of the challenge. The trader's win rate, reward-to-risk profile, risk per trade and sequence of wins and losses can all affect the chance of reaching the target before hitting the loss boundary.

I wanted to explore this as a probability and risk-management problem.

The central question is:

> Given a set of trading assumptions and challenge boundaries, how should I think about the likelihood of reaching the profit target before breaching the permitted loss?

The calculator is intended to help traders compare hypothetical scenarios and think more carefully about risk before attempting an evaluation.

## What it helps traders examine

The project is designed around the relationship between:

- **Win rate:** the assumed proportion of trades that are winners.
- **Reward-to-risk:** the average reward relative to the amount risked.
- **Risk per trade:** the percentage of account equity placed at risk on each trade.
- **Profit target:** the required gain or success boundary.
- **Maximum drawdown:** the loss boundary that must not be breached.

The precise inputs, options and outputs should be checked against the live application. This README describes the analytical purpose and the model concepts behind the project; it does not claim that every possible prop firm rule is implemented.

## The probability idea: Gambler's Ruin

One mathematical concept relevant to this project is **Gambler's Ruin**. In broad terms, this family of probability models studies the chance of reaching one boundary before another through a sequence of outcomes.

For a trading challenge, the two boundaries can be described as:

- Success: reaching the required profit target.
- Failure: reaching the maximum permitted loss or drawdown.

A theoretical model can estimate the probability of reaching the success boundary first, given assumptions about the distribution of trade outcomes and the distance to each boundary.

The supporting analysis for this project explored an empirical-distribution-based version of this approach, using historical R-multiples to estimate a parameter for the probability calculation. This is a theoretical approximation, not a full path-by-path simulation of every prop firm's rules.

## Understanding R and risk per trade

R represents the initial amount risked on a trade.

- A result of -1R means the initial risk was lost.
- A result of +2R means the trade made twice the initial risk.
- A result of +3R means the trade made three times the initial risk.
- A result of 0R represents a breakeven trade.

A percentage target and drawdown can be expressed approximately in R units when risk per trade is fixed and the boundaries are compatible.

For illustration only:

- Profit target: 8%.
- Maximum drawdown: 10%.
- Risk per trade: 1%.

This corresponds to an 8R target and a 10R loss boundary under a simplified fixed-risk interpretation. It does not mean eight trades are needed to reach the target. The number of trades depends on the distribution and expectancy of outcomes, and the actual account rules.

## Why risk per trade changes the problem

Increasing risk per trade can make the profit target closer when measured in R, but it also makes the drawdown boundary closer.

Reducing risk per trade generally increases the number of R units needed to reach a fixed percentage target, while also increasing the R distance to a fixed percentage loss boundary.

That is why looking only at how quickly a target might be reached is incomplete. A useful comparison must consider the success and failure boundaries together.

## How I approached the development

The project began with a practical question: how could a trader evaluate a prop firm challenge using probability and risk assumptions rather than focusing only on the headline profit target?

The development process involved:

1. **Identify the decision problem.** Consider the relationship between the target, drawdown limit and risk taken on each trade.
2. **Explore the mathematical framework.** Investigate probability models related to reaching one boundary before another, including Gambler's Ruin.
3. **Plan the calculation workflow.** Define the inputs and supporting calculations needed to examine different hypothetical conditions.
4. **Build the spreadsheet backend.** Use Google Sheets to organise the supporting calculations.
5. **Create the web application.** Use Google Apps Script for the interactive calculator interface and application logic.
6. **Use AI as a coding assistant.** Work with Claude during implementation. I directed the project idea, analytical requirements, workflow and testing.
7. **Manually stress-test the system.** Run a series of hypothetical scenarios, vary the assumptions and review the resulting behaviour.

I have run manual tests and the results have been encouraging so far. This describes my own testing experience; it is not independent mathematical verification or proof of predictive accuracy.

## Technology and structure

| Component | Role |
| --- | --- |
| Google Sheets | Spreadsheet backend for supporting data and calculations |
| Google Apps Script | Application logic and interactive web interface |
| Claude | AI coding assistance during development |

The deployed Apps Script URL provides access to the calculator. Google Sheets supports the calculation workflow behind it.

## Understanding the model and its limitations

The supporting analysis identified several important issues to keep in mind when interpreting a simplified challenge probability model:

1. **Breakeven trades:** A model that only represents wins and losses may not correctly represent trades that close at 0R.
2. **Variable outcomes:** Replacing all wins and losses with average values can hide the variability in actual R-multiple results.
3. **Trailing drawdown:** A simple fixed boundary or rough adjustment does not necessarily reproduce a firm's real trailing drawdown rule. The firm's exact balance- or equity-based definition matters.
4. **Daily loss limits:** A model that does not track daily equity or balance changes cannot be assumed to enforce daily loss rules.
5. **Trade count estimates:** Dividing a target by risk gives a target measured in R, not the number of trades required. Estimating trade count also requires an expectancy assumption and remains uncertain.
6. **Model assumptions:** Theoretical estimates rely on assumptions such as independent outcomes, a representative historical distribution, fixed risk and compatible boundaries.

A full path-based Monte Carlo challenge model can be more appropriate when the rules depend on the path of account equity, daily loss, trailing drawdown or multiple challenge phases. The exact rules must be explicitly represented in the simulation to claim they are modelled.

The current deployed calculator should be checked before attributing specific rule-handling features or outputs to it.

## How traders can use it thoughtfully

A sensible workflow is to:

1. Start with trading statistics drawn from a meaningful sample of your own records.
2. Use the actual profit target and drawdown limits for the challenge being considered.
3. Compare more than one risk-per-trade assumption.
4. Examine how sensitive the estimate is to changes in win rate and reward-to-risk.
5. Consider whether the chosen risk remains acceptable through a losing sequence.
6. Verify the firm's current rules independently before trading.

The calculator is intended to support scenario analysis, not to identify a guaranteed way to pass.

## Screenshots

Screenshots will be added after the initial repository setup.

Suggested files:

- `screenshots/calculator-overview.png` — main calculator interface.
- `screenshots/inputs-and-rules.png` — available inputs.
- `screenshots/results-summary.png` — probability estimate and result summary.
- `screenshots/scenario-comparison.png` — comparison of hypothetical assumptions.

## Related project

The companion [Monte Carlo Trading Simulator](https://github.com/Francisos1234/Monte-Carlo-Simulator) explores the range of outcomes across many hypothetical trading sequences.

My broader [Trading Performance Journal project](https://github.com/Francisos1234/Trading-performance-journal) documents a separate trading-performance analysis workflow.

## Disclaimer

This project is for educational and analytical purposes only. It is not financial advice, a prop firm endorsement or a guarantee of passing a challenge. Estimates depend on the model, data and assumptions used. Always read and verify the current rules of the relevant prop firm.
