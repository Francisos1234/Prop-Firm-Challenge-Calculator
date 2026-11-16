# Prop Firm Challenge Calculator

A probability and risk-analysis tool I built to help traders examine the difficulty and potential cost of passing one-phase and two-phase prop firm challenges.

**Live application:** [Open the Prop Firm Challenge Calculator](https://script.google.com/macros/s/AKfycbwnaxx80HH8lQtKq4RHcDCzDiXhXzvbLEqvZcLG7QeLJSCT9v-QReTIKrf6S_MtXKG1KA/exec)

**Repository:** [Francisos1234/Prop-Firm-Challenge-Calculator](https://github.com/Francisos1234/Prop-Firm-Challenge-Calculator)

An independent project by **Francis Chizurumoke**, developed with coding assistance from Claude.

---

## Project overview

I built this calculator to examine how a trader's win rate, reward-to-risk ratio and risk per trade interact with the profit target and drawdown limits of a prop firm challenge.

The calculator supports four setup combinations:

- **1-Phase with Initial Drawdown**
- **1-Phase with Trailing Drawdown**
- **2-Phase with Initial Drawdown**
- **2-Phase with Trailing Drawdown**

For a two-phase challenge, the user can enter separate profit targets, maximum drawdown limits and risk-per-trade settings for Phase 1 and Phase 2.

After the assumptions are entered, the calculator produces probability and cost estimates and compares different risk levels. The aim is to make it easier to see how changing risk affects the estimated chance of passing and the potential cost of repeated attempts.

## The problem I wanted to explore

Many traders look at a prop firm challenge and focus mainly on the profit target. For example, they see an 8% or 10% target and start thinking about how quickly they can reach it.

But the target is only one part of the challenge.

A trader also has to stay within the maximum drawdown, manage risk across a sequence of trades and, in some programs, pass more than one evaluation phase. Challenge fees matter too. Failing several attempts can become expensive, even when the account size looks attractive.

I wanted to build something that brought these factors together.

The question behind the project was simple:

> Based on my trading assumptions and the challenge rules I enter, what does the probability of passing look like, how many attempts might be needed, and what could those attempts cost?

I did not want to look at risk per trade in isolation. I wanted to compare it against both the profit target and the loss boundary.

## How one-phase and two-phase challenges work

Prop firms do not all use the same evaluation rules. However, the two common structures can be explained as follows.

### One-phase challenge

A one-phase challenge has a single evaluation stage. The trader must reach the required profit target while staying within the firm's drawdown and any other applicable rules.

Once the evaluation objectives are met and the firm completes its review, the trader may progress to the firm's funded or rewards account arrangement. There is no second evaluation phase in this structure.

### Two-phase challenge

A two-phase challenge has two evaluation stages.

1. **Phase 1:** The trader must reach the first profit target without breaching the applicable loss limits.
2. **Phase 2:** After passing Phase 1, the trader must meet a second profit target while continuing to respect the applicable rules.

The second target is often lower than the first, but the exact targets and loss limits depend on the firm and program. Passing both evaluation phases may lead to a funded or rewards account after the firm's review and onboarding requirements.

### Initial drawdown and trailing drawdown

The calculator also lets the user choose between two drawdown approaches.

- **Initial drawdown:** The loss boundary is measured against the starting account balance. The boundary does not move up with account growth under a simple fixed-limit interpretation.
- **Trailing drawdown:** The loss boundary follows a defined account high-water mark or another reference point set by the firm. The exact calculation can depend on whether the firm uses balance or equity, intraday or end-of-day values, and whether the limit stops trailing at a particular level.

The calculator displays a simplified trailing drawdown option and states that its effective limit is 70% of the stated amount. This is a calculator assumption, not a universal prop firm rule. It should not be treated as an exact reproduction of any firm's trailing drawdown policy.

For examples of how actual firms define their products, see the official rule pages linked in the references section below. Always check the current rules for the exact challenge you intend to take.

## Your contribution

This is my own project. I came up with the idea, identified the problem I wanted to solve and planned how the calculator should work.

My contribution included:

- Defining the purpose of the calculator and the questions it should help answer.
- Planning the one-phase and two-phase challenge options.
- Deciding that users should be able to compare initial and trailing drawdown setups.
- Identifying the inputs needed for the analysis, including win rate, reward-to-risk, phase targets, drawdown limits and risk per trade.
- Planning the comparison of multiple risk levels and the result summaries.
- Reviewing the interface and the way the information is presented.
- Running manual tests with different hypothetical inputs and reviewing the outputs.

I used Claude as a coding assistant during development. It helped with implementation, but the project direction, requirements, workflow and testing decisions came from me.

## Tools and technology

| Tool | How I used it |
| --- | --- |
| Google Sheets | Spreadsheet backend for supporting calculations and data |
| Google Apps Script | Application logic and web interface |
| Claude | AI coding assistance during development |
| GitHub | Project repository, version history, README and screenshots |
| Browser testing | Opening the live calculator and checking different input combinations |

I used the tools to turn the idea into an interactive calculator that people can access through a browser.

## Methodology

I approached the project by breaking the challenge into its main variables and then organising them into a workflow.

### 1. Define the challenge structure

I started with the two evaluation formats: one-phase and two-phase. I then included the choice between initial and trailing drawdown, giving the calculator four setup combinations.

### 2. Identify the inputs

The calculator allows the user to set or select:

- Win rate.
- Reward-to-risk ratio.
- Challenge phase structure.
- Drawdown type.
- Profit target for each applicable phase.
- Maximum drawdown for each applicable phase.
- Risk per trade for each applicable phase.
- Challenge fee.
- Account size.
- Profit split.

The risk-per-trade options are compared across multiple levels, so the user can see how the estimates change rather than relying on a single risk setting.

### 3. Apply a probability framework

The calculator is labelled as using a **Gambler's Ruin formula**. Gambler's Ruin is a family of probability problems concerned with reaching one boundary before another.

That idea is relevant to a challenge: the trader is trying to reach a profit boundary without first reaching a loss boundary.

The calculator uses the inputs to estimate the probability of passing the selected phase structure. For a two-phase setup, the results show the estimated probability for each phase and a combined estimate.

These figures should be understood as model outputs based on the assumptions entered, not as observed pass rates for a particular prop firm or a guarantee of what will happen to an individual trader.

### 4. Compare risk levels

Instead of showing only one result, the calculator presents a table comparing different risk-per-trade settings.

This makes it easier to examine the trade-off. Increasing risk may bring the profit target closer in R terms, but it also brings the drawdown boundary closer. A higher risk setting is not automatically a better choice just because it may reduce the estimated number of trades or attempts.

### 5. Examine the financial side

The calculator also considers the challenge fee and profit split. Its result summary includes estimates such as:

- **Pass rate:** the model's estimated probability of passing the selected setup.
- **Attempts for 90%:** an estimate of how many attempts may be needed to reach a cumulative 90% chance of success under the model's assumptions.
- **Expected trades to fund:** an estimate associated with reaching the funded stage.
- **Expected cost:** an estimate of challenge costs across the attempts considered.
- **5+ failure risk:** an estimate of the risk of needing five or more failed attempts.
- **Break-even return on funded account:** the return indicated as necessary to recover the challenge costs, based on the inputs.

These are estimates, not promises. Their usefulness depends on whether the assumptions are realistic and whether the calculation represents the actual challenge rules closely enough.

## Validation

I checked the calculator by manually entering different hypothetical scenarios and changing the inputs to see how the results responded.

My checks included:

- Comparing one-phase and two-phase setups.
- Switching between initial and trailing drawdown.
- Changing win rate and reward-to-risk assumptions.
- Changing the profit target and maximum drawdown.
- Comparing lower and higher risk-per-trade settings.
- Reviewing the pass-rate, attempts, trade-count and cost outputs.
- Checking whether the displayed comparisons changed when the inputs changed.

I also reviewed the interface and the result table to make sure the selected risk level was identifiable and the different outputs could be compared.

The results of my manual testing have been encouraging, but this is not an independent audit of the mathematical model. I have not established that the estimates predict the real-world pass rate of traders or reproduce every prop firm's evaluation rules.

## Limitations

There are important things this calculator does not establish.

1. **It does not guarantee a pass.** A probability estimate cannot tell an individual trader what will happen on their next attempt.
2. **It does not represent every prop firm.** Firms can use different profit targets, daily loss limits, maximum loss rules, consistency requirements, minimum trading days, time limits and prohibited trading practices.
3. **Daily loss rules are not the same as overall drawdown.** A challenge can be failed by breaching a daily loss limit even when the overall account is still within its maximum drawdown. Do not assume the calculator checks a firm's daily limit unless that rule is explicitly represented in the live version.
4. **Trailing drawdown rules vary.** Firms may calculate trailing limits using balance or equity, intraday or end-of-day values, and different high-water-mark rules. The calculator's displayed 70% effective-limit assumption is simplified and should not be treated as a firm's exact rule.
5. **The model depends on the inputs.** An inaccurate win rate or reward-to-risk assumption can make the output misleading. A small or unrepresentative trading sample may not reflect future performance.
6. **Trading outcomes are not necessarily independent.** Real results can change with market conditions, strategy performance, execution, slippage, fees and trader behaviour.
7. **Estimated attempts and costs are not guaranteed expenses.** They are model-based estimates and depend on the assumptions used.
8. **Passing an evaluation is not the same as receiving a payout.** Firms may have additional onboarding, account, consistency, payout and ongoing risk rules after the evaluation.

The calculator is best used for comparing hypothetical scenarios and thinking about risk. It should not replace reading the firm's current rules or testing a strategy with a meaningful sample of trading data.

## Evidence and project links

The repository contains the project documentation and screenshots of the actual interface. The live application can be opened separately.

- **[Open the live calculator](https://script.google.com/macros/s/AKfycbwnaxx80HH8lQtKq4RHcDCzDiXhXzvbLEqvZcLG7QeLJSCT9v-QReTIKrf6S_MtXKG1KA/exec)**
- **[View the GitHub repository](https://github.com/Francisos1234/Prop-Firm-Challenge-Calculator)**
- **[View the project screenshots](https://github.com/Francisos1234/Prop-Firm-Challenge-Calculator/tree/main)**

### Screenshots

#### 1. Calculator overview

The starting screen, showing the one-phase and two-phase challenge options and the calculator's insights section.

![Prop Firm Challenge Calculator overview](1-%20overview%20A.png)

#### 2. Choosing the challenge structure and drawdown type

The user selects one-phase or two-phase, then chooses initial or trailing drawdown.

![Choosing challenge phases and drawdown type](2-%20overview%20B%20choosing%20challenge%20phases.png)

#### 3. Entering challenge parameters

The setup screen shows the win rate, reward-to-risk, phase targets, maximum drawdown, risk-per-trade selections, challenge fee, account size and profit split.

![Choosing challenge parameters](3-%20overview%20C%20choosing%20challenge%20parameters.png)

#### 4. Reviewing the results

The results include a summary for the selected risk level and a comparison table across the available risk settings.

![Simulation result](4-%20Simulation%20esult.png)

#### 5. Insights and common mistakes

The calculator also includes explanations and reminders about strategy requirements, risk management, phase comparisons, drawdown types and common challenge mistakes.

![Understanding the simulator](5-%20Understanding%20the%20simulator.png)

## References: examples of prop firm evaluation rules

These official pages helped me understand how different firms describe one-step and two-step evaluations. They are examples, not rules that the calculator automatically applies.

- [FTMO 1-Step Challenge](https://ftmo.com/en/1-step-challenge/)
- [FTMO 2-Step Challenge](https://ftmo.com/en/2-step-challenge/)
- [FTMO Trading Objectives](https://ftmo.com/en/trading-objectives/)
- [The5ers 1-Step Plan Rules](https://the5ers.com/faqs/1-step-plan-rules-specifications/)
- [The5ers 2-Step Plan Rules](https://the5ers.com/faqs/2-step-plan-rules-specifications/)

Prop firm rules can change. Always verify the current terms directly with the firm before purchasing or trading a challenge.

## Related projects

- [Monte Carlo Trading Simulator](https://github.com/Francisos1234/Monte-Carlo-Simulator) — explores the range of outcomes across many hypothetical trading sequences.
- [Trading Performance Journal](https://github.com/Francisos1234/Trading-performance-journal) — documents a separate trading-performance analysis workflow.

## Disclaimer

This project is for educational and analytical purposes only. It is not financial advice, a prop firm endorsement or a guarantee of passing a challenge. The estimates depend on the model and the assumptions entered. I have manually tested scenarios, but the calculator has not been independently audited or proven to predict real-world outcomes. Always read and verify the current rules of the relevant prop firm.
