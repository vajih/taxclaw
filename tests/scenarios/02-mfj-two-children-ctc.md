# Scenario 02 — Married Filing Jointly, Two Children, Child Tax Credit
# Tax Year 2025 | Expected result: REFUND $6,777
# Tests: MFJ brackets, CTC ($2,200/child), CTC fully absorbs tax (no ACTC), joint withholding

---

## TAXPAYER PROFILE

| Field | Value |
|-------|-------|
| Filing status | Married Filing Jointly |
| Taxpayer age | 38 |
| Spouse age | 36 |
| Dependents | 2 qualifying children: Emma (age 8, SSN valid) and Lucas (age 11, SSN valid) |
| State | Illinois |

---

## INPUT DOCUMENTS

### W-2 #1 — Taxpayer, Northside Hospital (EIN 36-1234567)
| Box | Label | Value |
|-----|-------|-------|
| 1 | Wages | $75,000.00 |
| 2 | Federal income tax withheld | $8,000.00 |
| 3 | SS wages | $75,000.00 |
| 4 | SS tax withheld | $4,650.00 |
| 5 | Medicare wages | $75,000.00 |
| 6 | Medicare withheld | $1,087.50 |
| 13 | Retirement plan | Not checked |

### W-2 #2 — Spouse, Lakeview School District (EIN 36-7654321)
| Box | Label | Value |
|-----|-------|-------|
| 1 | Wages | $35,000.00 |
| 2 | Federal income tax withheld | $3,500.00 |
| 3 | SS wages | $35,000.00 |
| 4 | SS tax withheld | $2,170.00 |
| 5 | Medicare wages | $35,000.00 |
| 6 | Medicare withheld | $507.50 |
| 13 | Retirement plan | Checked |

No other income documents.

---

## EXPECTED TRIAGE OUTCOME

All five triage questions clear. In scope. Proceed.

---

## HAND CALCULATION

### Step 1 — Total Income
```
Wages — taxpayer (W-2 #1 Box 1):     $75,000.00
Wages — spouse (W-2 #2 Box 1):       $35,000.00
Total wages (1040 Line 1z):          $110,000.00
Total income:                        $110,000.00
```

### Step 2 — Adjustments to Income
```
No adjustments apply.
(Spouse has retirement plan; if traditional IRA deduction were claimed, phase-out
would apply at $126,000−$146,000 MFJ — but no IRA contribution in this scenario.)
Total adjustments: $0.00
```

### Step 3 — AGI
```
AGI = $110,000.00   → 1040 Line 11
```

### Step 4 — Standard Deduction
```
Filing status: MFJ → $30,000.00
Neither spouse is age 65+ or blind → no additional deduction
Standard deduction: $30,000.00   → 1040 Line 12
```

### Step 5 — Taxable Income
```
Taxable income = $110,000.00 − $30,000.00 = $80,000.00   → 1040 Line 15
```

### Step 6 — Income Tax (Bracket Calculation, MFJ Table)
```
10% on $23,850.00:                           $23,850.00 × 10.00% = $2,385.00
12% on ($80,000.00 − $23,850.00) = $56,150:  $56,150.00 × 12.00% = $6,738.00
                                                                    ──────────
Income tax:                                                         $9,123.00
Already a whole dollar → $9,123.00   → 1040 Line 16
```

Marginal rate: 12%.

### Step 7 — AMT Check
```
Taxable income $80,000 < MFJ AMT exemption $137,000 → AMT does not apply.
```

### Step 8 — Child Tax Credit (CTC)

Qualifying children: Emma (age 8) and Lucas (age 11) — both under 17, both have SSNs.

```
Tentative CTC = 2 children × $2,200 = $4,400.00

Phase-out check:
  Modified AGI = $110,000
  MFJ threshold = $400,000
  $110,000 < $400,000 → NO phase-out → full CTC applies

CTC applied against tax:
  min($4,400.00, $9,123.00) = $4,400.00
  Tax after CTC = $9,123.00 − $4,400.00 = $4,723.00

Unused CTC = $4,400.00 − $4,400.00 = $0.00
→ No ACTC (CTC fully absorbed by tax liability)
```

Total tax liability: $4,723.00   → 1040 Line 24

### Step 9 — Payments
```
Federal tax withheld — W-2 #1 Box 2:   $8,000.00
Federal tax withheld — W-2 #2 Box 2:   $3,500.00
Total withholding (1040 Line 25a):     $11,500.00
Total payments:                        $11,500.00   → 1040 Line 33
```

### Step 10 — Refund
```
Total payments ($11,500.00) > Total tax ($4,723.00)
REFUND = $11,500.00 − $4,723.00 = $6,777.00   → 1040 Line 35a
```

---

## EXPECTED FINAL SUMMARY OUTPUT

```
FILING STATUS: Married Filing Jointly
──────────────────────────────────────────────────
INCOME
  Wages (taxpayer)                     $75,000.00
  Wages (spouse)                       $35,000.00
Total income                          $110,000.00

ADJUSTMENTS TO INCOME
  (none)
Adjusted Gross Income (AGI)           $110,000.00

DEDUCTIONS
  Standard deduction (MFJ)            −$30,000.00
Taxable income                         $80,000.00

TAX (bracket calculation)
  10% on $23,850                        $2,385.00
  12% on $56,150                        $6,738.00
Income tax                              $9,123.00

NON-REFUNDABLE CREDITS
  Child Tax Credit (2 children)        −$4,400.00
Total tax liability                     $4,723.00

PAYMENTS
  Federal tax withheld (W-2s)         $11,500.00
Total payments                        $11,500.00
──────────────────────────────────────────────────
REFUND:                                 $6,777.00
```

---

## AGENT BEHAVIOR EXPECTATIONS

1. Agent confirms each W-2 separately before combining.
2. Agent notes spouse has retirement plan checked (Box 13) — relevant if IRA deduction later claimed.
3. Agent explains CTC: "Your 2 qualifying children give you a maximum Child Tax Credit of $4,400. Your income of $110,000 is well below the $400,000 phase-out threshold, so you get the full amount. That credit offsets $4,400 of your $9,123 tax bill, leaving $4,723 in tax."
4. Agent explains why ACTC is $0: "The Child Tax Credit fully absorbed your tax, with no 'leftover' credit — so there's no Additional Child Tax Credit this time."
5. W-2 #1 Box 4 validation: $4,650 = $75,000 × 6.2% ✓
6. W-2 #2 Box 4 validation: $2,170 = $35,000 × 6.2% ✓
