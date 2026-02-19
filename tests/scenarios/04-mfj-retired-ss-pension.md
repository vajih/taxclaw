# Scenario 04 — MFJ Retirees, Social Security + Pension + Interest
# Tax Year 2025 | Expected result: REFUND $2,640
# Tests: SS taxability worksheet (50% tier), age 65+ additional standard deduction,
#        1099-R (code 7), 1099-INT, no credits

---

## TAXPAYER PROFILE

| Field | Value |
|-------|-------|
| Filing status | Married Filing Jointly |
| Taxpayer age | 72 |
| Spouse age | 70 |
| Dependents | None |
| State | Florida (no state income tax) |

Both taxpayer and spouse are age 65 or older.

---

## INPUT DOCUMENTS

### SSA-1099 (combined household — one form for each recipient; total)
| Box | Label | Value |
|-----|-------|-------|
| 5 | Net Social Security benefits received | $24,000.00 |
| 6 | Voluntary federal tax withheld | $0.00 |

### 1099-R — Pension, Retired Teachers Pension Fund (EIN 59-1234567)
| Box | Label | Value |
|-----|-------|-------|
| 1 | Gross distribution | $30,000.00 |
| 2a | Taxable amount | $30,000.00 |
| 2b | Taxable amount not determined | Not checked |
| 4 | Federal income tax withheld | $3,000.00 |
| 7 | Distribution code | 7 (Normal distribution, age 59½+) |
| IRA/SEP/SIMPLE checkbox | — | Not checked (pension) |

### 1099-INT — Coastal Savings Bank
| Box | Label | Value |
|-----|-------|-------|
| 1 | Interest income | $1,200.00 |
| 4 | Federal tax withheld | $0.00 |

---

## EXPECTED TRIAGE OUTCOME

All five triage questions clear. In scope. Proceed.

1099-R code 7: normal distribution — no penalty, fully in scope.
1099-R IRA/SEP/SIMPLE not checked → pension → goes on 1040 Lines 5a/5b.

---

## HAND CALCULATION

### Step 9b — Social Security Taxability Worksheet
(Run before Step 1; requires provisional income)

Provisional income requires "AGI before SS," which requires the other income lines.

```
Income excluding SS benefits:
  Pension (taxable):          $30,000.00
  Interest income:             $1,200.00
  Total (AGI before SS):      $31,200.00

Adjustments to income:        $0.00
AGI before SS:                $31,200.00

Tax-exempt interest:           $0.00

50% of SS benefits:
  $24,000.00 × 50% =         $12,000.00

Provisional income = $31,200.00 + $0.00 + $12,000.00 = $43,200.00
```

MFJ thresholds:
- Below $32,000: $0 taxable
- $32,000–$44,000: up to 50% taxable tier
- Above $44,000: up to 85% taxable tier

$43,200 falls in the $32,000–$44,000 range → 50% taxable tier.

```
Taxable SS worksheet (50% tier):
  (A) 50% × (PI − $32,000) = 50% × ($43,200 − $32,000)
                            = 50% × $11,200
                            = $5,600.00

  (B) 50% × total SS benefits = 50% × $24,000
                               = $12,000.00

  Taxable SS = lesser of (A) and (B) = min($5,600.00, $12,000.00) = $5,600.00
```

→ 1040 Line 6a: $24,000.00 (gross SS)
→ 1040 Line 6b: $5,600.00 (taxable SS)

Non-taxable SS = $24,000.00 − $5,600.00 = $18,400.00 (not on return)

### Step 1 — Total Income
```
Pension distributions — taxable (1040 Line 5b):   $30,000.00
Taxable interest (1040 Line 2b):                   $1,200.00
Social Security — taxable (1040 Line 6b):          $5,600.00
Total income:                                      $36,800.00
```

### Step 2 — Adjustments to Income
```
No adjustments apply.
Total adjustments: $0.00
```

### Step 3 — AGI
```
AGI = $36,800.00   → 1040 Line 11
```

### Step 4 — Standard Deduction
```
Base standard deduction (MFJ):                    $30,000.00
Additional deduction — taxpayer (age 72, married): +$1,600.00
Additional deduction — spouse (age 70, married):   +$1,600.00
Total standard deduction:                         $33,200.00   → 1040 Line 12
```

### Step 5 — Taxable Income
```
Taxable income = $36,800.00 − $33,200.00 = $3,600.00   → 1040 Line 15
```

### Step 6 — Income Tax (Bracket Calculation, MFJ Table)
```
10% on $3,600.00 (entire taxable income falls in 10% bracket, which runs to $23,850):
  $3,600.00 × 10.00% = $360.00
                        ───────
Income tax:             $360.00   → 1040 Line 16
```

### Step 7 — AMT Check
```
Taxable income $3,600 < MFJ AMT exemption $137,000 → AMT does not apply.
```

### Step 8 — Credits
```
No credits apply (no children, no education expenses).
Total tax liability: $360.00   → 1040 Line 24
```

### Step 9 — Payments
```
Federal tax withheld (1099-R Box 4):   $3,000.00   → 1040 Line 25b
Total payments:                        $3,000.00   → 1040 Line 33
```

### Step 10 — Refund
```
Total payments ($3,000.00) > Total tax ($360.00)
REFUND = $3,000.00 − $360.00 = $2,640.00   → 1040 Line 35a
```

---

## EXPECTED FINAL SUMMARY OUTPUT

```
FILING STATUS: Married Filing Jointly
──────────────────────────────────────────────────
INCOME
  Pension distributions (taxable)      $30,000.00
  Taxable interest                      $1,200.00
  Social Security (taxable, Line 6b)    $5,600.00
    [Line 6a gross SS: $24,000.00]
Total income                           $36,800.00

ADJUSTMENTS TO INCOME
  (none)
Adjusted Gross Income (AGI)            $36,800.00

DEDUCTIONS
  Standard deduction (MFJ base)       −$30,000.00
  Additional (taxpayer, age 72)        −$1,600.00
  Additional (spouse, age 70)          −$1,600.00
Total standard deduction              −$33,200.00
Taxable income                          $3,600.00

TAX (bracket calculation)
  10% on $3,600                           $360.00
Income tax                               $360.00

Total tax liability                       $360.00

PAYMENTS
  Federal tax withheld (1099-R)        $3,000.00
Total payments                         $3,000.00
──────────────────────────────────────────────────
REFUND:                                 $2,640.00
```

---

## AGENT BEHAVIOR EXPECTATIONS

1. Agent collects SSA-1099 Box 5 but does NOT announce taxable SS amount until the worksheet runs.
2. Agent explains the SS worksheet step by step: "Your provisional income — that's your other income plus half your Social Security — is $43,200. That puts you in the middle tier, where up to 50% of your benefits can be taxable. The worksheet gives us $5,600 of your $24,000 in benefits as taxable."
3. Agent explains the 1099-R code 7: "Distribution code 7 means this is a regular retirement distribution — no early withdrawal penalty."
4. Agent notes pension (IRA checkbox not checked) → Lines 5a/5b, not 4a/4b.
5. Agent explains the age bonus: "Since you're both over 65, you each get an extra $1,600 added to your standard deduction — that's $3,200 in additional deduction, bringing your total to $33,200."
6. Planning opportunity: withholding check — tax is $360 on $3,000 withheld, so withholding could be reduced.
