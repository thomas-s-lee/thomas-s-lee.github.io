---
layout: single
title: ""
permalink: /projects/
---
# The Real Effects of Debt Relief on Education Outcomes
![Estimated Effects Over Time](../assets/images/result_sub_pct_m_std_cf.png)
## Overview
This project looks at whether upgrading school buildings—like fixing old classrooms or building new facilities—helps students do better in school and later in life. I study a program in Texas where the state helped certain school districts pay off their debt, which made it easier for them to spend money on big improvement projects. The results show that when schools were able to invest more in their buildings, students had better test scores, were more likely to graduate, and even earned more in their early careers. This matters because it shows that helping debt-strapped schools with their debt can lead to real improvements in students’ lives—not just nicer buildings, but better chances at success.

---

## Objectives
- Examine whether increased capital investment improves student outcomes.
- Focus on the effects of marginal capital projects initiated by heavily indebted school districts, where funding constraints are most binding.

---

## Data Sources

- **Texas Education Agency (TEA)** – Student-level K-12 data
- **Texas Higher Education Coordinating Board (THECB)** – College outcomes
- **National Center for Education Statistics (NCES)** – School finances across the U.S.
- **Academic Excellence Indicator System (AEIS)** – District demographics and performance in Texas
- **U.S. Census (1990 & 2000)** – Socioeconomic controls

---

## Tools & Techniques

- **Languages**: Python, Stata
- **Methods**:
  - Two-stage least squares (2SLS)
  - Difference-in-differences
- **Data Engineering**:
  - Merging and cleaning multi-source administrative data
  - Imputing policy eligibility from funding formulas
  - Standardizing scores and constructing derived metrics

---

## Methodology - Instrumental Variable

### Step 1: Instrumental Variable Construction
To isolate the causal effect of capital investment, I use an instrumental variable strategy. This is necessary because wealthier districts can both afford more capital spending and achieve better outcomes for reasons unrelated to infrastructure, creating endogeneity concerns in naïve comparisons.

- **Instrument**: `DTL_High × Post`
- `DTL_High`: High pre-policy debt-to-property-tax-levy ratio (1987–1991)
- `Post`: Indicator for post-policy period (1998 onward)
- Motivation: Districts with high levels of existing debt were more likely to qualify for and benefit from state subsidies, which gave them room to increase capital investment in their school facilities.

### Step 2: Estimation

- **First Stage**:  
  Capital spending instrumented using policy interaction  
  `Cap_{i,t} = π(DTL_High × Post) + controls + FE + ε`
  - `Cap_{i,t}`: Capital spending per pupil in district i at year t (3-year cumulative total)
  - `DTL_High_i`: Indicator for districts with above-median debt-to-tax levy ratio before the policy
  - `Post_t`: Indicator for post-policy years (1998 and later)
  - controls: Observable, time-varying district characteristics (e.g., current spending, cash holdings)
  - FE: District, year fixed effects
  
- **Second Stage**:  
  Estimate impact of capital on outcomes  
  `Ȳ_{i,t} = β × Ĉap_{i,t} + controls + FE + u`
  - \bar{Y}_{i,t}: Average educational or labor market outcome for district i following year t
  - \hat{Cap}_{i,t}: Predicted capital spending from the first stage
  - β: Coefficient of interest—the causal effect of capital investment

- **Outcomes Measured**:
  - Standardized test scores (reading & math)
  - Graduation & attendance rates
  - College enrollment & exam participation rates
  - Early-career income (ages 24–26)

---

## 📊 Key Results

| Outcome | Effect per $1,000 per pupil | Significance |
|--------|-----------------------------|--------------|
| Math test scores | +0.12 SD | ✅ Significant |
| Reading test scores | +0.06 SD | ✅ Significant |
| Graduation rate | +1.9 percentage points | ✅ Significant |
| Attendance rate | +0.12 percentage points | ✅ Significant |
| College enrollment | +0.9 percentage points | Not statistically significant |
| Early-career earnings | +2% (non-college grads) | ✅ Significant |

---

## [Read more](https://thomas-s-lee.github.io/files/JMP.pdf)

