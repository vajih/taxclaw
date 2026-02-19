# Scenario 08 — MFJ High Income, CTC Phase-Out Calculation
# Tax Year 2025 | Expected result: REFUND $4,576
# Tests: CTC phase-out (AGI above $400,000 MFJ threshold), upper brackets (24%), no ACTC

---

## TAXPAYER PROFILE

| Field | Value |
|-------|-------|
| Filing status | Married Filing Jointly |
| Taxpayer age | 42 |
| Spouse age | 40 |
| Dependents | 2 qualifying children: Olivia (age 8, SSN valid) and Noah (age 11, SSN valid) |
| State | California (state return out of scope) |

---

## INPUT DOCUMENTS

### W-2 #1 — Taxpayer, Pacific Capital Partners (EIN 94-1234567)
| Box | Label | Value |
|-----|-------|-------|
| 1 | Wages | $280,000.00 |
| 2 | Federal income tax withheld | $58,000.00 |

### W-2 #2 — Spouse, Bay Area Medical Group (EIN 94-7654321)
| Box | Label | Value |
|-----|-------|-------|
| 1 | Wages | $140,000.00 |
| 2 | Federal income tax withheld | $24,000.00 |

No other income documents.

---

## EXPECTED TRIAGE OUTCOME

All five triage questions clear. In scope. Proceed.

Note: Combined wages $420,000 — agent should check whether Additional Medicare Tax
applies ($420,000 > $250,000 MFJ threshold) and note it. However, AMT check passes
(taxable income below MFJ AMT phase-out start). Additional Medicare Tax flag noted below.

---

## HAND CALCULATION

### Step 1 — Total Income
```
Wages — taxpayer (W-2 #1):    $280,000.00
Wages — spouse (W-2 #2):      $140,000.00
Total wages (1040 Line 1z):   $420,000.00
Total income:                 $420,000.00
```

### Step 2 — Adjustments to Income
```
No adjustments apply.
Total adjustments: $0.00
```

### Step 3 — AGI
```
AGI = $420,000.00   → 1040 Line 11
```

### Step 4 — Standard Deduction
```
Filing status: MFJ → $30,000.00
Neither spouse age 65+ or blind → no additional deduction
Standard deduction: $30,000.00   → 1040 Line 12
```

### Step 5 — Taxable Income
```
Taxable income = $420,000.00 − $30,000.00 = $390,000.00   → 1040 Line 15
```

### Step 6 — Income Tax (Bracket Calculation, MFJ Table)
```
10% on $23,850.00:                                   $23,850.00 × 10.00% =  $2,385.00
12% on ($96,950.00 − $23,850.00) = $73,100.00:       $73,100.00 × 12.00% =  $8,772.00
22% on ($206,700.00 − $96,950.00) = $109,750.00:    $109,750.00 × 22.00% = $24,145.00
24% on ($390,000.00 − $206,700.00) = $183,300.00:   $183,300.00 × 24.00% = $43,992.00
                                                                            ──────────
Income tax:                                                                 $79,294.00   → 1040 Line 16
```

Marginal rate: 24%.

### Step 7 — AMT Check
```
Taxable income $390,000 < MFJ AMT exemption $137,000? No — wait.
AMT exemption for MFJ = $137,000. Phase-out begins at $1,252,700.
$390,000 > $137,000 exemption — but AMT is calculated on AMTI after exemption,
and AMTI ≠ taxable income. For W-2 wage earners with no preferences, AMTI ≈ taxable income.
AMTI ≈ $390,000. After exemption: $390,000 − $137,000 = $253,000.
AMT at 26%: $253,000 × 26% = $65,780.
Regular tax $79,294 > AMT $65,780 → AMT does not apply (regular tax exceeds tentative minimum tax).
Agent note: "AMT doesn't apply here — your regular income tax exceeds what the AMT would be."
```

### Step 8 — Additional Medicare Tax (informational flag)
```
Combined wages: $420,000
MFJ threshold: $250,000
Excess: $420,000 − $250,000 = $170,000
Additional Medicare Tax: $170,000 × 0.9% = $1,530

Note: Employer withholds at $200,000 per employee. With two W-2s, neither may have
triggered employer withholding (depends on each employer). This amount reconciles on
Form 8959 → Schedule 2 → 1040 Line 17.

For this scenario: flag the Additional Medicare Tax but note it is separate from income
tax. This scenario focuses on CTC phase-out; AMT calculation confirms no AMT.
Additional Medicare Tax amount: $1,530 → added to total tax.
```

### Step 9 — Child Tax Credit Phase-Out

```
Tentative CTC = 2 children × $2,200 = $4,400.00

Phase-out calculation:
  Modified AGI = $420,000
  MFJ threshold = $400,000
  Excess = $420,000 − $400,000 = $20,000.00

  Number of $1,000 increments (round up):
    ceil($20,000 / $1,000) = 20 increments

  Reduction = 20 × $50.00 = $1,000.00

CTC after phase-out = $4,400.00 − $1,000.00 = $3,400.00

Apply against tax:
  min($3,400.00, $79,294.00) = $3,400.00   [CTC fully absorbed by tax]
  Tax after CTC = $79,294.00 − $3,400.00 = $75,894.00

Unused CTC = $0.00 → ACTC = $0 (no unused CTC to refund)
```

### Step 10 — Total Tax
```
Income tax:                 $79,294.00
Additional Medicare Tax:    +$1,530.00
Non-refundable CTC:         −$3,400.00
                            ──────────
Total tax liability:        $77,424.00   → 1040 Line 24
```

### Step 11 — Payments
```
Federal tax withheld — W-2 #1:   $58,000.00
Federal tax withheld — W-2 #2:   $24,000.00
Total withholding (Line 25a):    $82,000.00   → 1040 Line 33
```

### Step 12 — Refund
```
Total payments ($82,000.00) > Total tax ($77,424.00)
REFUND = $82,000.00 − $77,424.00 = $4,576.00   → 1040 Line 35a
```

---

## EXPECTED FINAL SUMMARY OUTPUT

```
FILING STATUS: Married Filing Jointly
──────────────────────────────────────────────────
INCOME
  Wages (taxpayer)                    $280,000.00
  Wages (spouse)                      $140,000.00
Total income                          $420,000.00

ADJUSTMENTS TO INCOME
  (none)
Adjusted Gross Income (AGI)           $420,000.00

DEDUCTIONS
  Standard deduction (MFJ)            −$30,000.00
Taxable income                        $390,000.00

TAX (bracket calculation)
  10% on $23,850                        $2,385.00
  12% on $73,100                        $8,772.00
  22% on $109,750                      $24,145.00
  24% on $183,300                      $43,992.00
Income tax                             $79,294.00
Additional Medicare Tax (0.9%)         +$1,530.00

NON-REFUNDABLE CREDITS
  Child Tax Credit (after phase-out)   −$3,400.00
Total tax liability                    $77,424.00

PAYMENTS
  Federal tax withheld (W-2s)         $82,000.00
Total payments                        $82,000.00
──────────────────────────────────────────────────
REFUND:                                 $4,576.00
```

---

## AGENT BEHAVIOR EXPECTATIONS

1. Agent explains CTC phase-out: "Your Child Tax Credit starts at $4,400, but because your income of $420,000 is $20,000 above the $400,000 threshold, the credit is reduced by $50 for each $1,000 over the limit — that's 20 increments × $50 = $1,000 reduction — leaving you with $3,400."
2. Agent flags Additional Medicare Tax: "Your combined wages of $420,000 exceed the $250,000 MFJ threshold for the Additional Medicare Tax. The 0.9% applies to $170,000, adding $1,530 to your tax bill. This may not have been fully withheld by your employers — they each withhold based on your individual wages."
3. Agent confirms AMT does not result in additional tax (regular tax > tentative minimum tax).
4. Agent confirms no ACTC: "The CTC was fully absorbed by your tax — there's no leftover credit to be refunded as ACTC."
