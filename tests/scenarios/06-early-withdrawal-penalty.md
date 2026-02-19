# Scenario 06 — Single Filer, IRA Early Withdrawal (Code 1)
# Tax Year 2025 | Expected result: BALANCE DUE $762
# Tests: 1099-R distribution code 1, 10% early withdrawal penalty, balance due presentation

---

## TAXPAYER PROFILE

| Field | Value |
|-------|-------|
| Filing status | Single |
| Age | 35 |
| Dependents | None |
| State | Georgia |

Taxpayer withdrew $10,000 from a Traditional IRA at age 35. No exception to the 10% penalty applies (code 1 on 1099-R).

---

## INPUT DOCUMENTS

### W-2 — Piedmont Logistics (EIN 58-2345678)
| Box | Label | Value |
|-----|-------|-------|
| 1 | Wages | $45,000.00 |
| 2 | Federal income tax withheld | $4,800.00 |
| 3 | SS wages | $45,000.00 |
| 4 | SS tax withheld | $2,790.00 |

### 1099-R — Vanguard (EIN 23-1234567)
| Box | Label | Value |
|-----|-------|-------|
| 1 | Gross distribution | $10,000.00 |
| 2a | Taxable amount | $10,000.00 |
| 2b | Taxable amount not determined | Not checked |
| 4 | Federal income tax withheld | $0.00 |
| 7 | Distribution code | 1 (Early distribution, no known exception) |
| IRA/SEP/SIMPLE checkbox | — | Checked |

---

## EXPECTED TRIAGE OUTCOME

All five triage questions clear. In scope. Proceed.

1099-R distribution code 1 is in scope per SKILL.md §5d. Agent must:
- Explain the 10% early withdrawal penalty applies
- Calculate penalty as part of total tax
- NOT escalate (code 1 with no exception is handled in-scope)

---

## HAND CALCULATION

### Step 1 — Total Income
```
Wages (W-2 Box 1):                              $45,000.00   → 1040 Line 1z
IRA distribution — gross (1040 Line 4a):        $10,000.00
IRA distribution — taxable (1040 Line 4b):      $10,000.00
  (IRA/SEP/SIMPLE box checked → Lines 4a/4b)
Total income:                                   $55,000.00
```

### Step 2 — Adjustments to Income
```
No adjustments apply.
Total adjustments: $0.00
```

### Step 3 — AGI
```
AGI = $55,000.00   → 1040 Line 11
```

### Step 4 — Standard Deduction
```
Filing status: Single → $15,000.00   → 1040 Line 12
Age 35, not blind → no additional deduction
```

### Step 5 — Taxable Income
```
Taxable income = $55,000.00 − $15,000.00 = $40,000.00   → 1040 Line 15
```

### Step 6 — Income Tax (Bracket Calculation, Single Table)
```
10% on $11,925.00:                          $11,925.00 × 10.00% = $1,192.50
12% on ($40,000.00 − $11,925.00) = $28,075: $28,075.00 × 12.00% = $3,369.00
                                                                   ──────────
Income tax:                                                        $4,561.50
Round to nearest dollar → $4,562.00   → 1040 Line 16
```

### Step 7 — Early Withdrawal Penalty
```
1099-R code 1: 10% early withdrawal penalty on taxable distribution amount
Penalty = $10,000.00 × 10.00% = $1,000.00   → Schedule 2 Line 8 → 1040 Line 23
```

### Step 8 — AMT Check
```
Taxable income $40,000 < Single AMT exemption $88,100 → AMT does not apply.
```

### Step 9 — Total Tax
```
Income tax:                    $4,562.00
Early withdrawal penalty:     +$1,000.00
                               ──────────
Total tax liability:           $5,562.00   → 1040 Line 24
```

No credits apply.

### Step 10 — Payments
```
Federal tax withheld — W-2 Box 2:       $4,800.00   → 1040 Line 25a
Federal tax withheld — 1099-R Box 4:        $0.00
Total payments:                         $4,800.00   → 1040 Line 33
```

### Step 11 — Balance Due
```
Total tax ($5,562.00) > Total payments ($4,800.00)
BALANCE DUE = $5,562.00 − $4,800.00 = $762.00   → 1040 Line 37
```

---

## EXPECTED FINAL SUMMARY OUTPUT

```
FILING STATUS: Single
──────────────────────────────────────────────────
INCOME
  Wages                                $45,000.00
  IRA distribution (taxable, Line 4b)  $10,000.00
    [Line 4a gross: $10,000.00]
Total income                           $55,000.00

ADJUSTMENTS TO INCOME
  (none)
Adjusted Gross Income (AGI)            $55,000.00

DEDUCTIONS
  Standard deduction (Single)         −$15,000.00
Taxable income                         $40,000.00

TAX (bracket calculation)
  10% on $11,925                        $1,192.50
  12% on $28,075                        $3,369.00
Income tax                              $4,562.00

OTHER TAXES
  Early withdrawal penalty (10%)       +$1,000.00
Total tax liability                     $5,562.00

PAYMENTS
  Federal tax withheld (W-2)           $4,800.00
  Federal tax withheld (1099-R)            $0.00
Total payments                         $4,800.00
──────────────────────────────────────────────────
BALANCE DUE:                              $762.00
```

---

## AGENT BEHAVIOR EXPECTATIONS

1. Agent identifies distribution code 1 immediately and explains: "Distribution code 1 means this is an early withdrawal — you took money out before age 59½ and there's no known exception. That means the $10,000 is fully taxable as income AND subject to a 10% penalty, which works out to $1,000."
2. Agent confirms the IRA/SEP/SIMPLE box is checked → routes to Lines 4a/4b.
3. Agent notes $0 withheld on 1099-R: "Nothing was withheld from your IRA distribution, which is part of why there's a balance due."
4. Agent delivers balance due with empathy per SKILL.md §14.
5. Planning note: "To avoid a surprise next year, if you take another early distribution, you can ask the custodian to withhold 10% or more. You can also adjust your W-4 at work to have more withheld."
6. W-2 Box 4 validation: $2,790 = $45,000 × 6.2% ✓
