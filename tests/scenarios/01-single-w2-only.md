# Scenario 01 — Single Filer, W-2 Only
# Tax Year 2025 | Expected result: REFUND $2,298
# Tests: basic bracket calculation, Single standard deduction, W-2 withholding

---

## TAXPAYER PROFILE

| Field | Value |
|-------|-------|
| Filing status | Single |
| Age | 32 |
| Dependents | None |
| State | Texas (no state income tax) |

---

## INPUT DOCUMENTS

### W-2 — Acme Corp (EIN 12-3456789)
| Box | Label | Value |
|-----|-------|-------|
| 1 | Wages, tips, other comp | $52,000.00 |
| 2 | Federal income tax withheld | $6,500.00 |
| 3 | Social Security wages | $52,000.00 |
| 4 | Social Security tax withheld | $3,224.00 |
| 5 | Medicare wages | $52,000.00 |
| 6 | Medicare tax withheld | $754.00 |
| 12 | Code D (401k contribution) | $3,000.00 |
| 13 | Retirement plan box | Checked |
| 15 | State | TX |
| 17 | State tax withheld | $0.00 |

No other income documents.

---

## EXPECTED TRIAGE OUTCOME

All five triage questions clear. In scope. Proceed to full calculation.

Triage answers:
- Q1 Income: W-2 wages only
- Q2 States: One state (TX), no multi-state issue
- Q3 Investments sold: No
- Q4 Business/rental: No
- Q5 K-1/foreign: No

---

## HAND CALCULATION

### Step 1 — Total Income
```
Wages (W-2 Box 1):        $52,000.00   → 1040 Line 1a / Line 1z
Total income:             $52,000.00
```

### Step 2 — Adjustments to Income
```
No adjustments apply.
Total adjustments:             $0.00
```

Note: 401(k) contributions (W-2 Box 12 Code D, $3,000) are pre-tax and already excluded
from Box 1 wages. No further adjustment needed or allowed.

### Step 3 — Adjusted Gross Income
```
AGI = $52,000.00 − $0.00 = $52,000.00   → 1040 Line 11
```

### Step 4 — Standard Deduction
```
Filing status: Single → $15,000.00   → 1040 Line 12
Age 32, not blind → no additional deduction
Standard deduction: $15,000.00
```

### Step 5 — Taxable Income
```
Taxable income = $52,000.00 − $15,000.00 = $37,000.00   → 1040 Line 15
```

### Step 6 — Income Tax (Bracket Calculation, Single Table)
```
10% on $11,925.00:                          $11,925.00 × 10.00% = $1,192.50
12% on ($37,000.00 − $11,925.00) = $25,075: $25,075.00 × 12.00% = $3,009.00
                                                                   ──────────
Income tax:                                                        $4,201.50
Round to nearest dollar → $4,202.00   → 1040 Line 16
```

Marginal rate: 12%. Effective rate: $4,202 / $52,000 = 8.1% (reference only).

### Step 7 — AMT Check
```
Taxable income $37,000 < Single AMT exemption $88,100 → AMT does not apply.
```

### Step 8 — Tax After Credits
```
No credits apply (no children, no education expenses).
Total tax liability: $4,202.00   → 1040 Line 24
```

### Step 9 — Payments
```
Federal income tax withheld (W-2 Box 2):   $6,500.00   → 1040 Line 25a
Total payments:                            $6,500.00   → 1040 Line 33
```

### Step 10 — Refund
```
Total payments ($6,500.00) > Total tax ($4,202.00)
REFUND = $6,500.00 − $4,202.00 = $2,298.00   → 1040 Line 35a
```

---

## EXPECTED FINAL SUMMARY OUTPUT

```
FILING STATUS: Single
──────────────────────────────────────────────────
INCOME
  Wages                                $52,000.00
Total income                           $52,000.00

ADJUSTMENTS TO INCOME
  (none)
Adjusted Gross Income (AGI)            $52,000.00

DEDUCTIONS
  Standard deduction (Single)         −$15,000.00
Taxable income                         $37,000.00

TAX (bracket calculation)
  10% on $11,925                        $1,192.50
  12% on $25,075                        $3,009.00
Income tax                              $4,202.00

Total tax liability                     $4,202.00

PAYMENTS
  Federal tax withheld (W-2 Box 2)     $6,500.00
Total payments                         $6,500.00
──────────────────────────────────────────────────
REFUND:                                 $2,298.00
```

---

## AGENT BEHAVIOR EXPECTATIONS

1. During document collection, agent reads back: "I'm reading your W-2 as wages of $52,000 and federal tax withheld of $6,500 — does that look right?"
2. Agent notes Box 12 Code D: "Your 401(k) contribution of $3,000 is already excluded from your Box 1 wages — no additional deduction needed."
3. Agent confirms AMT does not apply before presenting results.
4. W-2 Box 4 validation: $3,224 = $52,000 × 6.2% ✓ (within SS wage base)
5. At DIY exit: AGI $52,000 < $84,000 → recommend IRS Free File.
6. Planning opportunity: mention IRA contribution (not enrolled in IRA, within deductible range).
