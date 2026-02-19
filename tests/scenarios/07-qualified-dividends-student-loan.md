# Scenario 07 — Single Filer, Qualified Dividends + Student Loan Interest Deduction
# Tax Year 2025 | Expected result: REFUND $820
# Tests: student loan interest deduction (above-the-line), qualified dividends at 0% LTCG rate,
#        1099-INT, 1099-DIV, ordinary income bracket separation from QD

---

## TAXPAYER PROFILE

| Field | Value |
|-------|-------|
| Filing status | Single |
| Age | 29 |
| Dependents | None |
| State | Colorado |

---

## INPUT DOCUMENTS

### W-2 — Centennial Software (EIN 84-3344556)
| Box | Label | Value |
|-----|-------|-------|
| 1 | Wages | $38,000.00 |
| 2 | Federal income tax withheld | $3,200.00 |

### 1099-INT — First National Bank
| Box | Label | Value |
|-----|-------|-------|
| 1 | Interest income | $420.00 |
| 4 | Federal tax withheld | $0.00 |

### 1099-DIV — Fidelity Investments
| Box | Label | Value |
|-----|-------|-------|
| 1a | Total ordinary dividends | $800.00 |
| 1b | Qualified dividends | $600.00 |
| 2a | Total capital gain distributions | $0.00 |
| 4 | Federal tax withheld | $0.00 |

Note: Box 1b ($600) ≤ Box 1a ($800) ✓

### 1098-E — Navient (student loan servicer)
| Box | Label | Value |
|-----|-------|-------|
| 1 | Student loan interest received | $1,800.00 |

---

## EXPECTED TRIAGE OUTCOME

All five triage questions clear. In scope. Proceed.

Note: 1099-DIV is in scope (dividends are in scope; no investment SALES on 1099-B).
1098-E is in scope. Student loan interest deduction applies.

---

## HAND CALCULATION

### Step 1 — Total Income (before adjustments)
```
Wages (1040 Line 1z):            $38,000.00
Taxable interest (Line 2b):          $420.00
Ordinary dividends (Line 3b):        $800.00
  (includes $600 qualified dividends)
Total gross income:              $39,220.00
```

### Step 2 — Student Loan Interest Deduction

MAGI for SLI phase-out purposes = total income before SLI deduction = $39,220.00

```
Phase-out range (Single): $85,000 − $100,000
MAGI $39,220 < $85,000 → below phase-out floor → full deduction

Actual interest paid: $1,800.00
Statutory maximum: $2,500.00
Deduction = min($1,800.00, $2,500.00) = $1,800.00   → Schedule 1 Line 21
```

### Step 3 — AGI
```
Total income:                $39,220.00
Student loan interest:       −$1,800.00
AGI:                         $37,420.00   → 1040 Line 11
```

### Step 4 — Standard Deduction
```
Filing status: Single → $15,000.00   → 1040 Line 12
Age 29, not blind → no additional deduction
```

### Step 5 — Taxable Income
```
Taxable income = $37,420.00 − $15,000.00 = $22,420.00   → 1040 Line 15
```

### Step 6 — Income Tax with Qualified Dividend Separation

Qualified dividends ($600) are taxed at preferential rates; remaining income is taxed at bracket rates.

```
Ordinary (non-QD) income = Taxable income − Qualified dividends
                         = $22,420.00 − $600.00 = $21,820.00

Tax on ordinary income (Single bracket table):
  10% on $11,925.00:                                $1,192.50
  12% on ($21,820.00 − $11,925.00) = $9,895.00:    $1,187.40
  Ordinary income tax subtotal:                     $2,379.90

Tax on qualified dividends:
  0% rate applies up to $48,350 of taxable income (Single)
  Taxable income $22,420 < $48,350 → ALL qualified dividends taxed at 0%
  $600.00 × 0% = $0.00

Total income tax = $2,379.90 + $0.00 = $2,379.90
Round to nearest dollar → $2,380.00   → 1040 Line 16
```

### Step 7 — AMT Check
```
Taxable income $22,420 < Single AMT exemption $88,100 → AMT does not apply.
```

### Step 8 — Credits
```
No credits apply.
Total tax liability: $2,380.00   → 1040 Line 24
```

### Step 9 — Payments
```
Federal tax withheld — W-2 Box 2:   $3,200.00   → 1040 Line 25a
Total payments:                     $3,200.00   → 1040 Line 33
```

### Step 10 — Refund
```
Total payments ($3,200.00) > Total tax ($2,380.00)
REFUND = $3,200.00 − $2,380.00 = $820.00   → 1040 Line 35a
```

---

## EXPECTED FINAL SUMMARY OUTPUT

```
FILING STATUS: Single
──────────────────────────────────────────────────
INCOME
  Wages                                $38,000.00
  Taxable interest                        $420.00
  Ordinary dividends                      $800.00
    [of which qualified dividends:        $600.00]
Total income                           $39,220.00

ADJUSTMENTS TO INCOME
  Student loan interest deduction      −$1,800.00
Adjusted Gross Income (AGI)            $37,420.00

DEDUCTIONS
  Standard deduction (Single)         −$15,000.00
Taxable income                         $22,420.00

TAX (bracket calculation)
  Ordinary income ($21,820):
    10% on $11,925                      $1,192.50
    12% on $9,895                       $1,187.40
  Qualified dividends ($600 at 0%):         $0.00
Income tax                              $2,380.00

Total tax liability                     $2,380.00

PAYMENTS
  Federal tax withheld (W-2)           $3,200.00
Total payments                         $3,200.00
──────────────────────────────────────────────────
REFUND:                                   $820.00
```

---

## AGENT BEHAVIOR EXPECTATIONS

1. Agent confirms 1099-DIV does not include a 1099-B (no investment sales — dividends only is in scope).
2. Agent validates Box 1b ≤ Box 1a: "$600 qualified ≤ $800 ordinary ✓"
3. Agent explains the student loan interest: "I'm applying a $1,800 deduction for your student loan interest — that comes right off the top before we calculate your AGI. Your MAGI of $39,220 is well below the $85,000 phase-out floor, so you get the full deduction."
4. Agent explains the qualified dividend tax rate: "Your $600 in qualified dividends are taxed at the capital gains rate — since your total taxable income of $22,420 is below the $48,350 threshold for single filers, those dividends are taxed at 0%."
5. Agent notes the deduction saved taxes at the 12% marginal rate: "$1,800 × 12% = $216 in tax saved."
