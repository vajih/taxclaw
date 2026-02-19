# Scenario 10 — Single Retiree, Social Security at 85% Taxable Tier
# Tax Year 2025 | Expected result: REFUND $1,127
# Tests: SS taxability worksheet (85% tier), age 65+ additional standard deduction,
#        1099-R code 7 (IRA), 1099-INT

---

## TAXPAYER PROFILE

| Field | Value |
|-------|-------|
| Filing status | Single |
| Age | 68 |
| Dependents | None |
| State | Arizona |

Taxpayer is a retired teacher. Receives Social Security and takes IRA distributions.

---

## INPUT DOCUMENTS

### SSA-1099
| Box | Label | Value |
|-----|-------|-------|
| 5 | Net Social Security benefits received | $18,000.00 |
| 6 | Voluntary federal tax withheld | $0.00 |

### 1099-R — Fidelity IRA (EIN 04-1234567)
| Box | Label | Value |
|-----|-------|-------|
| 1 | Gross distribution | $25,000.00 |
| 2a | Taxable amount | $25,000.00 |
| 2b | Taxable amount not determined | Not checked |
| 4 | Federal income tax withheld | $2,500.00 |
| 7 | Distribution code | 7 (Normal distribution — taxpayer is 68, age 59½+ ✓) |
| IRA/SEP/SIMPLE checkbox | — | Checked |

### 1099-INT — Desert Community Bank
| Box | Label | Value |
|-----|-------|-------|
| 1 | Interest income | $500.00 |
| 4 | Federal tax withheld | $0.00 |

---

## EXPECTED TRIAGE OUTCOME

All five triage questions clear. In scope. Proceed.

1099-R code 7: normal distribution, age-eligible. In scope.
IRA/SEP/SIMPLE checked → Lines 4a/4b.

---

## HAND CALCULATION

### Step 9b — Social Security Taxability Worksheet
(Run first; needs all other income)

```
Income excluding SS:
  IRA distribution (taxable):   $25,000.00   → 1040 Line 4b
  Taxable interest:                 $500.00   → 1040 Line 2b
  Total non-SS income:           $25,500.00

Adjustments to income: $0.00
AGI before SS: $25,500.00

Tax-exempt interest: $0.00

50% of SS benefits:
  $18,000.00 × 50% = $9,000.00

Provisional income = $25,500.00 + $0.00 + $9,000.00 = $34,500.00
```

Single thresholds:
- Below $25,000: $0 taxable
- $25,000–$34,000: up to 50% taxable
- Above $34,000: up to 85% taxable

$34,500 > $34,000 → **85% taxable tier**

```
Taxable SS worksheet (85% tier):

  (A) 85% × total SS benefits
      = 85% × $18,000.00 = $15,300.00

  (B) 85% × (PI − $34,000) + $4,500
      = 85% × ($34,500.00 − $34,000.00) + $4,500.00
      = 85% × $500.00 + $4,500.00
      = $425.00 + $4,500.00
      = $4,925.00

  Taxable SS = lesser of (A) and (B)
             = min($15,300.00, $4,925.00)
             = $4,925.00
```

→ 1040 Line 6a: $18,000.00 (gross SS benefits)
→ 1040 Line 6b: $4,925.00 (taxable SS)

Non-taxable SS = $18,000.00 − $4,925.00 = $13,075.00

### Step 1 — Total Income
```
IRA distribution — taxable (1040 Line 4b):   $25,000.00
  [Line 4a gross: $25,000.00]
Taxable interest (1040 Line 2b):                 $500.00
Social Security — taxable (1040 Line 6b):      $4,925.00
Total income:                                 $30,425.00
```

### Step 2 — Adjustments to Income
```
No adjustments apply.
Total adjustments: $0.00
```

### Step 3 — AGI
```
AGI = $30,425.00   → 1040 Line 11
```

### Step 4 — Standard Deduction
```
Filing status: Single → $15,000.00
Age 68 (65+), not blind → additional $2,000.00
Total standard deduction: $17,000.00   → 1040 Line 12
```

### Step 5 — Taxable Income
```
Taxable income = $30,425.00 − $17,000.00 = $13,425.00   → 1040 Line 15
```

### Step 6 — Income Tax (Bracket Calculation, Single Table)
```
10% on $11,925.00:                          $11,925.00 × 10.00% = $1,192.50
12% on ($13,425.00 − $11,925.00) = $1,500:   $1,500.00 × 12.00% =   $180.00
                                                                    ──────────
Income tax:                                                         $1,372.50
Round to nearest dollar → $1,373.00   → 1040 Line 16
```

### Step 7 — AMT Check
```
Taxable income $13,425 < Single AMT exemption $88,100 → AMT does not apply.
```

### Step 8 — Credits
```
No credits apply.
Total tax liability: $1,373.00   → 1040 Line 24
```

### Step 9 — Payments
```
Federal tax withheld — 1099-R Box 4:   $2,500.00   → 1040 Line 25b
Total payments:                        $2,500.00   → 1040 Line 33
```

### Step 10 — Refund
```
Total payments ($2,500.00) > Total tax ($1,373.00)
REFUND = $2,500.00 − $1,373.00 = $1,127.00   → 1040 Line 35a
```

---

## EXPECTED FINAL SUMMARY OUTPUT

```
FILING STATUS: Single
──────────────────────────────────────────────────
INCOME
  IRA distribution (taxable, Line 4b)  $25,000.00
    [Line 4a gross: $25,000.00]
  Taxable interest                        $500.00
  Social Security (taxable, Line 6b)    $4,925.00
    [Line 6a gross: $18,000.00]
Total income                           $30,425.00

ADJUSTMENTS TO INCOME
  (none)
Adjusted Gross Income (AGI)            $30,425.00

DEDUCTIONS
  Standard deduction (Single base)    −$15,000.00
  Additional (age 68, Single)          −$2,000.00
Total standard deduction              −$17,000.00
Taxable income                         $13,425.00

TAX (bracket calculation)
  10% on $11,925                        $1,192.50
  12% on $1,500                           $180.00
Income tax                              $1,373.00

Total tax liability                     $1,373.00

PAYMENTS
  Federal tax withheld (1099-R)        $2,500.00
Total payments                         $2,500.00
──────────────────────────────────────────────────
REFUND:                                 $1,127.00
```

---

## SS WORKSHEET DISPLAY (agent should show this)

```
Social Security Taxability Worksheet
  Your SS benefits (SSA-1099 Box 5):             $18,000.00
  Other income (IRA + interest):                 $25,500.00
  50% of SS benefits:                             $9,000.00
  Provisional income:                            $34,500.00

  Single threshold — 85% tier: above $34,000
  $34,500 > $34,000 → top tier applies

  (A) 85% × $18,000 =                           $15,300.00
  (B) 85% × ($34,500 − $34,000) + $4,500 =       $4,925.00
  Taxable SS = lesser = $4,925.00

  Of your $18,000 in Social Security, $4,925 is taxable.
  The remaining $13,075 is tax-free.
```

---

## AGENT BEHAVIOR EXPECTATIONS

1. Agent collects SSA-1099 Box 5 early but holds off announcing the taxable amount until worksheet completes.
2. Agent walks through the SS worksheet step by step, explaining provisional income concept naturally: "To figure out how much of your Social Security is taxable, we add up all your other income plus half your Social Security. In your case that's $25,500 + $9,000 = $34,500. That's your 'combined income.'"
3. Agent explains why only $4,925 of $18,000 is taxable: "Even though you're in the top tier, the formula limits it to the lesser of 85% of your total benefits ($15,300) or a calculation based on how far above the threshold you are ($4,925). You're just barely above the $34,000 line, so only $4,925 is taxable."
4. Agent confirms the age-65+ deduction boost: "Since you're 68, your standard deduction gets an extra $2,000 — bringing it from $15,000 to $17,000."
5. Agent confirms 1099-R code 7: no penalty, IRA box checked → Lines 4a/4b.
6. Planning note: "Your withholding of $2,500 is reasonable. If you wanted to fine-tune it, $1,373 in tax on a $30,425 income means roughly 4.5% effective rate — you could adjust your 1099-R withholding for next year to be closer to your actual liability."
