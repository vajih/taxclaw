# Scenario 05 — MFJ with American Opportunity Tax Credit (AOTC)
# Tax Year 2025 | Expected result: REFUND $5,377
# Tests: AOTC calculation, non-refundable portion, refundable 40% portion, 1098-T

---

## TAXPAYER PROFILE

| Field | Value |
|-------|-------|
| Filing status | Married Filing Jointly |
| Taxpayer age | 45 |
| Spouse age | 44 |
| Dependents | 1 dependent — Jordan (age 19, full-time sophomore, SSN valid) |
| State | Michigan |

---

## INPUT DOCUMENTS

### W-2 #1 — Taxpayer, Meridian Tech Inc (EIN 38-1122334)
| Box | Label | Value |
|-----|-------|-------|
| 1 | Wages | $80,000.00 |
| 2 | Federal income tax withheld | $9,000.00 |

### W-2 #2 — Spouse, Meridian Public Schools (EIN 38-5566778)
| Box | Label | Value |
|-----|-------|-------|
| 1 | Wages | $40,000.00 |
| 2 | Federal income tax withheld | $4,200.00 |

### 1098-T — State University (EIN 38-6543210)
| Box | Label | Value |
|-----|-------|-------|
| 1 | Payments received for qualified tuition | $8,000.00 |
| 5 | Scholarships or grants | $2,000.00 |

Additional context (agent must ask):
- Jordan is a second-year (sophomore) student — within first 4 years ✓
- Enrolled at least half-time ✓
- No felony drug conviction ✓
- AOTC not claimed for Jordan for more than 3 prior years (first use: year 1, year 2 is current) ✓

---

## EXPECTED TRIAGE OUTCOME

All five triage questions clear. In scope. Proceed.

---

## HAND CALCULATION

### Step 1 — Total Income
```
Wages — taxpayer (W-2 #1):   $80,000.00
Wages — spouse (W-2 #2):     $40,000.00
Total wages (1040 Line 1z):  $120,000.00
Total income:                $120,000.00
```

### Step 2 — Adjustments to Income
```
No adjustments apply.
Total adjustments: $0.00
```

### Step 3 — AGI
```
AGI = $120,000.00   → 1040 Line 11
MAGI = $120,000.00 (no foreign income exclusion)
```

### Step 4 — Standard Deduction
```
Filing status: MFJ → $30,000.00
No age 65+ or blindness → no additional deduction
Standard deduction: $30,000.00   → 1040 Line 12
```

### Step 5 — Taxable Income
```
Taxable income = $120,000.00 − $30,000.00 = $90,000.00   → 1040 Line 15
```

### Step 6 — Income Tax (Bracket Calculation, MFJ Table)
```
10% on $23,850.00:                            $23,850.00 × 10.00% = $2,385.00
12% on ($90,000.00 − $23,850.00) = $66,150:   $66,150.00 × 12.00% = $7,938.00
                                                                     ──────────
Income tax:                                                         $10,323.00   → 1040 Line 16
```

### Step 7 — AMT Check
```
Taxable income $90,000 < MFJ AMT exemption $137,000 → AMT does not apply.
```

### Step 8 — American Opportunity Tax Credit (AOTC)

```
Qualifying expenses:
  1098-T Box 1 (payments):          $8,000.00
  1098-T Box 5 (scholarships):     −$2,000.00
  Net qualifying expenses:          $6,000.00

AOTC calculation:
  100% of first $2,000:             $2,000.00 × 100% = $2,000.00
  25% of next $2,000:               $2,000.00 × 25%  =   $500.00
  (Remaining $2,000 of $6,000 expenses beyond the first $4,000 — not eligible)
  Total AOTC:                                          $2,500.00

MAGI phase-out check:
  MAGI = $120,000
  MFJ phase-out range: $160,000 − $180,000
  $120,000 < $160,000 → NO phase-out → full $2,500 credit

Split into refundable / non-refundable:
  Non-refundable (60%): $2,500.00 × 60% = $1,500.00
  Refundable (40%):     $2,500.00 × 40% = $1,000.00   → 1040 Line 29
```

Apply non-refundable AOTC:
```
Tax before credits:         $10,323.00
Non-refundable AOTC:        −$1,500.00
                            ──────────
Total tax liability:         $8,823.00   → 1040 Line 24
```

### Step 9 — Payments and Refundable Credits
```
Federal tax withheld — W-2 #1:   $9,000.00
Federal tax withheld — W-2 #2:   $4,200.00
Total withholding (Line 25a):   $13,200.00

Refundable AOTC (Line 29):      +$1,000.00

Total payments + credits:       $14,200.00   → 1040 Line 33
```

### Step 10 — Refund
```
Total payments ($14,200.00) > Total tax ($8,823.00)
REFUND = $14,200.00 − $8,823.00 = $5,377.00   → 1040 Line 35a
```

---

## EXPECTED FINAL SUMMARY OUTPUT

```
FILING STATUS: Married Filing Jointly
──────────────────────────────────────────────────
INCOME
  Wages (taxpayer)                     $80,000.00
  Wages (spouse)                       $40,000.00
Total income                          $120,000.00

ADJUSTMENTS TO INCOME
  (none)
Adjusted Gross Income (AGI)           $120,000.00

DEDUCTIONS
  Standard deduction (MFJ)            −$30,000.00
Taxable income                         $90,000.00

TAX (bracket calculation)
  10% on $23,850                        $2,385.00
  12% on $66,150                        $7,938.00
Income tax                             $10,323.00

NON-REFUNDABLE CREDITS
  AOTC — non-refundable (60%)          −$1,500.00
Total tax liability                     $8,823.00

PAYMENTS & REFUNDABLE CREDITS
  Federal tax withheld (W-2s)         $13,200.00
  AOTC — refundable portion (40%)     +$1,000.00
Total payments + credits              $14,200.00
──────────────────────────────────────────────────
REFUND:                                 $5,377.00
```

---

## AGENT BEHAVIOR EXPECTATIONS

1. Agent confirms AOTC eligibility criteria for Jordan before calculating.
2. Agent reads back 1098-T: "I'm reading your 1098-T as $8,000 in qualified payments and $2,000 in scholarships. Net qualifying expenses are $6,000 — does that look right?"
3. Agent explains the AOTC formula: "The AOTC covers 100% of the first $2,000 in expenses ($2,000) plus 25% of the next $2,000 ($500) — total $2,500."
4. Agent confirms no phase-out: "Your income of $120,000 is below the $160,000 threshold, so you get the full $2,500 credit."
5. Agent explains the refundable split: "Of the $2,500 credit, $1,500 is non-refundable (reduces your tax bill) and $1,000 is refundable (paid to you even if your tax is already zero)."
