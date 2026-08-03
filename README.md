# Retirement Drawdown Simulator

Technical documentation and project specification for `retirement_drawdown_simulator.html`.

## Overview

The **Retirement Drawdown Simulator** is a single-file, client-side interactive web application designed to model single-portfolio retirement capital depletion over a custom age horizon. It incorporates annual spending inflation adjustments, compound investment returns, and supplemental annuity income streams starting at a specified target age.

---

## Technical Architecture

* **File:** `retirement_drawdown_simulator.html`
* **Frontend Tech:** HTML5, CSS3, JavaScript (ES6+)
* **Visualization Library:** [Plotly.js v2.32.0](https://cdn.plot.ly/plotly-2.32.0.min.js)
* **Dependencies:** None (standalone execution in browser via CDN)

---

## Core Features

1. **Real-Time Calculation:** Automatically recalculates and updates the visual chart upon altering any input field.
2. **Dual-Trace Plotting:** Visualizes both starting balance (`Start bal`) and end-of-year balance (`End bal`) across the simulation timeline.
3. **Annuity Offset Integration:** Applies a fixed annuity income stream starting from `ann_age` to offset annual expenditures.
4. **Inflation Adjustment:** Compoundly inflates annual expenditures based on configured `infl` percentage.
5. **Interactive Data Inspection:** Enables clicking on chart data points to view specific age and balance callouts.
6. **State Reset:** Features a one-click reset button to restore default parameter values.

---

## Input Parameters & Default Configuration

| Parameter | Input ID | Default Value | Description |
| :--- | :--- | :--- | :--- |
| **Starting Portfolio** | `p0` | `$1,000,000` | Initial retirement capital balance. |
| **Annual Spending** | `spend0` | `$60,000` | Baseline annual living expenses at start age. |
| **Inflation Rate** | `infl` | `2.0%` | Compound annual inflation rate percentage. |
| **Return Rate** | `ret` | `5.0%` | Expected annual investment return percentage. |
| **Annuity Age** | `ann_age` | `65` | Age at which guaranteed annuity income commences. |
| **Annuity Payment** | `ann` | `$21,360` | Fixed annual payout received from the annuity. |
| **Start Age** | `start_age` | `55` | Retirement start age for simulation onset. |
| **End Age** | `end_age` | `95` | End age limit for the retirement simulation. |

---

## Mathematical Model

For each age $t$ from `start_age` to `end_age`:

1. **Inflation-Adjusted Spending ($S_t$):**
   $$S_t = 	ext{spend0} 	imes \left(1 + rac{	ext{infl}}{100}
ight)^{(t - 	ext{start\_age})}$$

2. **Annuity Income ($A_t$):**
   $$A_t = egin{cases} 	ext{ann}, & 	ext{if } t \ge 	ext{ann\_age} \ 0, & 	ext{if } t < 	ext{ann\_age} \end{cases}$$

3. **Net Drawdown Requirement ($N_t$):**
   $$N_t = \max(0, S_t - A_t)$$

4. **End-of-Year Balance ($B_{	ext{end}}$):**
   $$B_{	ext{end}} = (B_{	ext{start}} - N_t) 	imes \left(1 + rac{	ext{ret}}{100}
ight)$$

---

## Application Usage & Execution

### Running the Application

Because the application is delivered as a self-contained HTML document with inline CSS/JS and external CDN dependency loading, no build tools or package managers are needed.

1. Clone or download the repository containing `retirement_drawdown_simulator.html`.
2. Open the file directly in any web browser:
   ```bash
   # Modern browser opening
   open retirement_drawdown_simulator.html
   ```

### Reading the Graph

* **Portfolio Depletion:** If the visual lines drop below $0 on the vertical axis ($Y$-axis), the portfolio runs out of capital at that corresponding age.
* **Capital Retention:** If $0 is not crossed on the $Y$-axis, capital persists throughout the designated simulation horizon.

---

## Disclaimer

This application is built as a simplified educational drawdown simulator using deterministic assumptions (constant rate of return and constant inflation). It does not model sequence-of-returns risk, dynamic asset allocations, taxation, or market volatility. It is not financial advice.
