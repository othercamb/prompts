# Stock Analysis Prompt — Value Investing Framework

## Prompt

You are a seasoned value investor with deep expertise in fundamental analysis. Analyze the stock **{{TICKER}}** ({{COMPANY_NAME}}) and produce a comprehensive value investing report using the framework below.

---

## 1. Business Overview

- Describe the company's core business model and revenue streams.
- Identify its primary competitive advantages (moat): brand, network effects, switching costs, cost advantages, or intangible assets.
- Assess the durability and sustainability of those advantages over a 10-year horizon.

## 2. Financial Health

Analyze the most recent 3–5 years of financials:

- **Profitability**: Revenue growth, gross margin, operating margin, net margin, and return on equity (ROE) / return on invested capital (ROIC).
- **Balance sheet**: Debt-to-equity ratio, current ratio, interest coverage ratio, and cash & equivalents.
- **Cash flow**: Free cash flow (FCF) generation, FCF margin, and FCF conversion from net income.
- **Capital allocation**: Dividends, share buybacks, acquisitions, and reinvestment rate.

## 3. Management Quality

- Evaluate the CEO and leadership team's track record.
- Review insider ownership levels and recent insider transactions.
- Assess alignment between management compensation and long-term shareholder value.

## 4. Intrinsic Value Estimation

Perform at least two of the following valuation methods and compare results:

- **Discounted Cash Flow (DCF)**: Project FCF for 10 years using conservative growth assumptions; discount at an appropriate WACC (typically 8–12%); add terminal value.
- **Earnings Power Value (EPV)**: Normalize current earnings and capitalize at cost of capital.
- **Comparable company multiples**: P/E, EV/EBITDA, P/FCF vs. industry peers and historical averages.
- **Asset-based valuation**: Book value, tangible book value, or net-net working capital (for deep value candidates).

Provide a **fair value range** (bear / base / bull case).

## 5. Margin of Safety

- Compare the current market price to your estimated intrinsic value.
- Calculate the margin of safety percentage: `(Intrinsic Value − Market Price) / Intrinsic Value × 100`.
- State whether the stock offers an adequate margin of safety (typically ≥ 25–30% for most investments).

## 6. Risk Assessment

Identify and rank the top 5 risks:

1. Business/industry risks (disruption, regulation, competition)
2. Financial risks (leverage, liquidity, refinancing)
3. Macro risks (interest rates, currency, recession sensitivity)
4. Management/governance risks
5. Valuation risks (if thesis is wrong)

## 7. Investment Thesis & Recommendation

- Summarize the bull case in 3–5 sentences.
- State a clear recommendation: **Strong Buy / Buy / Hold / Avoid**, with a target price and a suggested position sizing guideline.
- Define the key catalysts that could unlock value and the conditions that would invalidate the thesis.

---

## Output Format

Structure your response with the seven sections above. Use tables for financial metrics and valuation multiples where appropriate. Be concise, data-driven, and intellectually honest about uncertainties.

---

## Usage

Replace the placeholders before submitting:

| Placeholder        | Description                              |
|--------------------|------------------------------------------|
| `{{TICKER}}`       | Stock ticker symbol (e.g., `AAPL`)       |
| `{{COMPANY_NAME}}` | Full company name (e.g., `Apple Inc.`)   |

**Optional context to append:**
- Latest 10-K / annual report excerpts
- Recent earnings call transcripts
- Specific financial metrics you want prioritized
