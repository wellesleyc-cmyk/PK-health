# Design Doc: Phil Personal Health Assessment HTML Report
**Date:** 2026-03-29
**Author:** Wellesley (Primary Care physician, friend)
**Patient:** Phil (first name only)
**Output file:** `/Users/wellesleychapman/PK-health/PK-health-report-phil.html`

---

## Purpose

A single-page, self-contained HTML health assessment report written by Wellesley (Phil's physician and close friend/hiking partner) to communicate Phil's BodySpec DEXA results (March 26, 2026), what they mean, and a clear evidence-based action plan. Tone: warm, personal, medically authoritative. Not a clinical form — a document from a friend who happens to be a doctor.

---

## Source Material

- `/Users/wellesleychapman/PK-health/PK-OpenEvidence-DEXA-summary.md` — clinical assessment of DEXA findings
- `/Users/wellesleychapman/PK-health/PK-treatment-plan.md` — comprehensive exercise, nutrition, and monitoring plan

---

## Visual Design

- **Style:** Personal Health Report (Option A)
- **Color palette:**
  - Teal/slate primary (`#2C7A7B` or similar) for headers and accents
  - Green (`#276749` / light green bg) for "good news" callouts
  - Amber (`#B7791F` / light amber bg) for "concerning findings"
  - Red-adjacent (`#9B2335`) for critical stat callouts (2nd percentile)
  - Blue-slate (`#2B4C7E` / light blue bg) for action/recommendation items
  - Clean white background, generous whitespace
- **Typography:**
  - Headers: Georgia or similar serif (via Google Fonts: Lora)
  - Body: Inter or similar sans-serif (via Google Fonts: Inter)
- **No external JS dependencies.** Pure HTML + CSS only. Self-contained.
- **Print-friendly:** Reasonable behavior if Phil prints or saves as PDF.

---

## Page Structure (Top to Bottom)

### 1. Header
- "Personal Health Assessment" label (small caps, subdued)
- Phil's name large
- Date: March 29, 2026
- Prepared by: Wellesley
- Thin teal rule beneath

### 2. Personal Introduction
- 2–3 short paragraphs from Wellesley
- Warm, friend-to-friend voice
- Key message: "I reviewed your DEXA results and I want to walk you through what I see — the good, the concerning, and most importantly, the opportunity. The timing here is genuinely fortunate."
- Sets up the positive framing: learning this at 56 vs. 66 or 76

### 3. The Good News
- Section header in green
- 3–4 stat cards (green-accented):
  - Body fat: 16.0% — favorable metabolic profile
  - Visceral fat: 1.0 lbs (20th percentile) — low cardiovascular risk
  - Lean mass index: above sarcopenia threshold
  - Overall body composition strengths
- Brief explanatory prose under the cards

### 4. What the DEXA Found — The Findings That Need Attention
- Section header in amber
- Large bold callout card: **Bone Density: 2nd Percentile**
- Secondary callout: Lean Mass Index 15th percentile / ALMI 19th percentile
- Explanation of what these numbers mean in plain language
- Fracture risk context (without being alarmist)
- The "legacy effect" of low body weight on bone health
- What we cannot determine from DEXA alone (FRAX, secondary causes, bone quality)

### 5. Why Now Is the Right Time
- Motivational bridge section — teal accented
- The 56 vs. 66 vs. 76 framing: bone density is modifiable, especially with early intervention
- Window of opportunity: HiRIT studies show 2–4% BMD improvement in 8–18 months
- Pharmacotherapy + exercise + nutrition together = compounding gains
- Tone: hopeful, energizing, not scary

### 6. Your Action Plan
Four subsections, each with a distinct blue-slate callout header:

**a) Step 1 — Medical Workup (Do This First)**
- Reach out to PCP
- FRAX score calculation
- Lab workup list (vitamin D, calcium, testosterone, TSH, CMP, CBC, PTH if indicated)
- Medical-grade DEXA (hip/spine T-scores)
- Discussion of pharmacotherapy (bisphosphonates first-line)
- Include the key talking points from the PCP communication template

**b) Step 2 — Exercise Program**
- HiRIT protocol from LIFTMOR-M
- Progressive overload table (Foundation → Build → Intensification → Maintenance)
- Impact loading targets (30–50 impacts/session)
- Balance training
- Key principle callouts (80–85% 1RM, eccentric control, explosive concentric)

**c) Step 3 — Nutrition**
- Protein target: 90g/day (1.5g/kg), distribution across meals
- Calcium: 1200–1500 mg/day
- Vitamin D: 2000 IU/day
- Total calories: 1800–2000 kcal/day
- Sample daily meal plan (as a clean table)
- Micronutrients (magnesium, vitamin K, zinc)

**d) Step 4 — Supplements & Monitoring**
- Vitamin D3 2000 IU
- Calcium citrate if dietary insufficient
- Monitoring schedule table (Baseline → 3mo → 6mo → 12mo → 18mo → 24mo)
- Bone turnover markers, repeat DEXA timeline

### 7. Goals & Timeline
- Visual 3-phase horizontal timeline or table
- Phase 1 (0–6 months): stabilize, establish baseline, begin HiRIT
- Phase 2 (6–12 months): +2–4% lumbar BMD, +4–7 lbs lean mass
- Phase 3 (12–24 months): +4–6% BMD from baseline, T-score toward osteopenia range
- Key outcome expectations with evidence citations inline

### 8. Closing — I'm Here
- Short warm closing from Wellesley
- Offer to help Phil find a qualified trainer, prep for PCP appointment, talk through pharmacotherapy options
- "You caught this at the right time. Let's use it."
- Wellesley's sign-off (first name only)

### 9. References
- Clean numbered list
- All 16 references from PK-OpenEvidence-DEXA-summary.md + all 13 from PK-treatment-plan.md
- Deduplicated (several overlap)
- Standard citation format: Authors. Title. Journal. Year;vol(issue):pages. doi.

---

## Tone Guidelines

- **Never alarmist.** Honest about severity but always paired with what can be done.
- **Personal throughout.** This is from Wellesley to Phil — use "you" and "I" freely.
- **Evidence-grounded.** Specific trial names (LIFTMOR-M, FrOST), specific numbers (4.1% BMD increase, 52 fractures per 1000 person-years reduced) lend credibility.
- **Actionable.** Every concerning finding is followed by what to do about it.
- **Optimistic but not dismissive.** The 2nd percentile finding is serious. The response to it is energizing.

---

## Technical Constraints

- Single `.html` file, fully self-contained
- Google Fonts via CDN (acceptable offline limitation)
- No JavaScript required
- Mobile-readable (responsive CSS)
- Saves cleanly as PDF from browser print dialog
