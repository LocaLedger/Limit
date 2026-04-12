# LocaLimit — Feature Roadmap

## Status: 3 high-value features planned

---

## LM-F1: Budget Health Score

**Summary:** A single composite score (0–100) shown prominently on the Dashboard tab that gives users an instant read on their financial health this month.

**Value:** Users don't have to interpret three separate bars — one number tells the story. Shareable, gamified, motivating.

**Calculation:**
- Start at 100
- −20 if savings rate < 10%  
- −10 if savings rate 10–19%  
- −5 per category over budget (max −25)  
- −5 per category at 80–99% of budget (max −15)  
- −20 if no income data connected  
- Floor at 0

**Grade map:** 90–100 = A (emerald), 75–89 = B (cyan), 60–74 = C (amber), 40–59 = D (orange), 0–39 = F (rose)

**UI:** Rendered as a colored card above the 3-stat row on the Dashboard. Shows score, letter grade, and a 2-line explanation of the biggest deduction.

**TODO:**
- [ ] Add `calcHealthScore(income, spending, categories, spendByCategory)` function
- [ ] Render health score card in `renderDashboard()` above the stat row
- [ ] Add `data-testid="health-score"` attribute for testing

---

## LM-F2: What-If Income Scenario Modeler

**Summary:** A slider on the Dashboard that lets users ask "what if my income changes by X%?" — instantly updating the net income and savings rate display.

**Value:** Gig workers and freelancers live with variable income. This is the core pitch of LocaLimit: scenario modeling without a spreadsheet.

**UI:** A `±` slider from −50% to +50% in 5% increments, rendered below the 3-stat row. When moved, the INCOME stat card updates to show the hypothetical income and the NET / Savings Rate update accordingly. A reset button returns it to 0.

**State:** The slider value is ephemeral (not persisted). It resets when the user navigates away.

**TODO:**
- [ ] Add `_scenarioAdj = 0` module-level variable
- [ ] Render scenario strip in `renderDashboard()` with `<input type="range">`
- [ ] On `oninput`, update hypothetical income/net/savings stats in-place without full re-render
- [ ] Add `data-testid="scenario-slider"` and `data-testid="scenario-income"` for tests
- [ ] Reset `_scenarioAdj` on tab switch

---

## LM-F3: Per-Category 3-Month Trend Bars

**Summary:** In the Budgets tab, each category envelope shows three mini bars (last 3 months) so users can see if spending is trending up, down, or flat.

**Value:** A single month's envelope is a snapshot. Three months reveals a pattern. Users can see if their food spending crept up month-over-month even if they're under budget right now.

**UI:** Below each category's existing progress bar, render 3 tiny bars (12px tall each, labeled "2mo ago / last mo / this mo") using LocaLoss expense data grouped by month.

**TODO:**
- [ ] Add `getSpendingByMonth(lossData, categoryKey, numMonths)` helper
- [ ] Render 3-bar mini chart in `renderBudgetList()` below each progress bar
- [ ] Add `data-testid="trend-bars-${key}"` wrapper for tests
- [ ] Show "— no history" text when fewer than 2 months of data exist
