# Scenario 03 — Head of Household, EITC + ACTC + CTC
# Tax Year 2025 | Expected result: REFUND $6,635
# Tests: HOH filing status, CTC (partial absorption), ACTC calculation, EITC calculation

---

## TAXPAYER PROFILE

| Field | Value |
|-------|-------|
| Filing status | Head of Household |
| Age | 29 |
| Dependents | 1 qualifying child: Maya (age 5, SSN valid, lived in home all year) |
| Marital status | Unmarried |
| Household costs paid by taxpayer | >50% |
| State | Ohio |

---

## INPUT DOCUMENTS

### W-2 — Riverside Café (EIN 31-9876543)
| Box | Label | Value |
|-----|-------|-------|
| 1 | Wages | $28,000.00 |
| 2 | Federal income tax withheld | $1,400.00 |
| 3 | SS wages | $28,000.00 |
| 4 | SS tax withheld | $1,736.00 |
| 5 | Medicare wages | $28,000.00 |
| 6 | Medicare withheld | $406.00 |
| 13 | Retirement plan | Not checked |

No other income documents.

---

## EXPECTED TRIAGE OUTCOME

All five triage questions clear. In scope. Proceed.

HOH soft-flag: Agent confirms:
- Taxpayer is unmarried ✓
- Maya (age 5) lived with taxpayer more than half the year ✓
- Taxpayer paid more than 50% of household costs ✓
- HOH status confirmed.

---

## HAND CALCULATION

### Step 1 — Total Income
```
Wages (W-2 Box 1):     $28,000.00   → 1040 Line 1z
Total income:          $28,000.00
```

### Step 2 — Adjustments to Income
```
No adjustments apply.
Total adjustments: $0.00
```

### Step 3 — AGI
```
AGI = $28,000.00   → 1040 Line 11
Earned income = $28,000.00 (wages only)
```

### Step 4 — Standard Deduction
```
Filing status: Head of Household → $22,500.00   → 1040 Line 12
Age 29, not blind → no additional deduction
```

### Step 5 — Taxable Income
```
Taxable income = $28,000.00 − $22,500.00 = $5,500.00   → 1040 Line 15
```

### Step 6 — Income Tax (Bracket Calculation, HOH Table)
```
10% on $5,500.00 (entire taxable income falls in 10% bracket, which runs to $17,000):
  $5,500.00 × 10.00% = $550.00
                        ───────
Income tax:             $550.00   → 1040 Line 16
```

### Step 7 — AMT Check
```
Taxable income $5,500 < Single/HOH AMT exemption $88,100 → AMT does not apply.
```

### Step 8 — Child Tax Credit (CTC)

Qualifying child: Maya, age 5 (under 17), valid SSN.

```
Tentative CTC = 1 child × $2,200 = $2,200.00

Phase-out check:
  Modified AGI = $28,000
  All other statuses threshold = $200,000
  $28,000 < $200,000 → NO phase-out → full CTC

CTC applied against tax:
  min($2,200.00, $550.00) = $550.00   [CTC capped by tax liability]
  Tax after CTC = $550.00 − $550.00 = $0.00

Unused CTC = $2,200.00 − $550.00 = $1,650.00
```

### Step 8b — Additional Child Tax Credit (ACTC)

Unused CTC = $1,650 > $0, so ACTC applies.

```
Step 1: ACTC formula
  15% × (earned income − $2,500)
  = 15% × ($28,000.00 − $2,500.00)
  = 15% × $25,500.00
  = $3,825.00

Step 2: Per-child cap
  $1,700 × 1 qualifying child = $1,700.00

Step 3: Unused CTC cap
  Unused CTC = $1,650.00

ACTC = min($3,825.00, $1,700.00, $1,650.00) = $1,650.00   → 1040 Line 28
```

### Step 9 — Earned Income Tax Credit (EITC)

Eligibility gates:
- Earned income: $28,000 ✓ (wages)
- Filing status: HOH (not MFS) ✓
- Investment income: $0 < $11,950 ✓
- Valid SSNs for taxpayer and Maya ✓
- US citizen ✓

```
Qualifying children: 1
Filing status: HOH (use "all other statuses" column)

Phase-in check:
  Earned income $28,000 > plateau $12,730 → credit is at or past plateau → use max credit $4,328

Phase-out check:
  Greater of (AGI, earned income) = $28,000
  Phase-out start (all other, 1 child) = $23,350
  Phase-out complete (all other, 1 child) = $50,434
  $28,000 is in the phase-out zone.

Phase-out calculation:
  Excess over start = $28,000 − $23,350 = $4,650.00
  Phase-out rate (1 child) = 15.98%
  Reduction = $4,650.00 × 15.98% = $743.07
  EITC = $4,328.00 − $743.07 = $3,584.93 → $3,585.00   → 1040 Line 27

Note: IRS EITC tables are the authoritative source for the exact dollar amount.
The formula above may differ from the table by ±$1. For validation, cross-reference
IRS Publication 596 (2025) EITC tables at earned income = $28,000, 1 child, HOH.
```

Total tax liability: $0.00   → 1040 Line 24

### Step 10 — Payments and Refundable Credits
```
Federal tax withheld (W-2 Box 2):   $1,400.00   → 1040 Line 25a
EITC:                              +$3,585.00   → 1040 Line 27
ACTC:                              +$1,650.00   → 1040 Line 28
Total payments + credits:           $6,635.00   → 1040 Line 33
```

### Step 11 — Refund
```
Total payments ($6,635.00) > Total tax ($0.00)
REFUND = $6,635.00   → 1040 Line 35a
```

---

## EXPECTED FINAL SUMMARY OUTPUT

```
FILING STATUS: Head of Household
──────────────────────────────────────────────────
INCOME
  Wages                                $28,000.00
Total income                           $28,000.00

ADJUSTMENTS TO INCOME
  (none)
Adjusted Gross Income (AGI)            $28,000.00

DEDUCTIONS
  Standard deduction (HOH)            −$22,500.00
Taxable income                          $5,500.00

TAX (bracket calculation)
  10% on $5,500                           $550.00
Income tax                               $550.00

NON-REFUNDABLE CREDITS
  Child Tax Credit (1 child, partial)    −$550.00
Total tax liability                         $0.00

PAYMENTS & REFUNDABLE CREDITS
  Federal tax withheld (W-2)           $1,400.00
  Earned Income Credit (EITC)         +$3,585.00
  Additional Child Tax Credit (ACTC)  +$1,650.00
Total payments + credits               $6,635.00
──────────────────────────────────────────────────
REFUND:                                 $6,635.00
```

---

## AGENT BEHAVIOR EXPECTATIONS

1. Agent soft-flags HOH status and confirms the three qualifying criteria before proceeding.
2. Agent explains CTC partial absorption: "Your Child Tax Credit is $2,200, but your tax is only $550 — so the credit wipes out your entire tax bill, and the remaining $1,650 becomes a refundable Additional Child Tax Credit."
3. Agent explains ACTC: "Your earned income of $28,000 × 15% after the $2,500 floor = $3,825. That's higher than the $1,650 unused credit and the $1,700 per-child cap, so your ACTC is $1,650."
4. Agent explains EITC: "The Earned Income Credit is $3,585 — this is fully refundable, so it adds directly to your refund even though your tax is already zero."
5. Total refund of $6,635 should be clearly celebrated.
6. W-2 Box 4 validation: $1,736 = $28,000 × 6.2% ✓
