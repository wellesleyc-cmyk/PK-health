# Phil Health Assessment HTML Report — Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Build a single self-contained HTML file (`PK-health-report-phil.html`) that serves as a warm, medically authoritative personal health assessment for Phil, authored by Wellesley (his physician and friend), based on his March 2026 BodySpec DEXA results.

**Architecture:** Single `.html` file with all CSS embedded in a `<style>` block. No JavaScript. Google Fonts loaded via CDN (Inter + Lora). Structured as a flowing single-page document with clearly delineated sections. Color-coded by section type: green (strengths), amber (concerns), teal (opportunity/motivation), blue-slate (action steps).

**Tech Stack:** HTML5, CSS3 (custom properties, flexbox, grid), Google Fonts CDN. No build tools, no frameworks, no JS.

---

## Key Source Files

- `/Users/wellesleychapman/PK-health/PK-OpenEvidence-DEXA-summary.md` — clinical DEXA assessment
- `/Users/wellesleychapman/PK-health/PK-treatment-plan.md` — exercise, nutrition, monitoring plan
- `/Users/wellesleychapman/PK-health/docs/plans/2026-03-29-phil-health-report-design.md` — approved design doc

**Output:** `/Users/wellesleychapman/PK-health/PK-health-report-phil.html`

---

## Task 1: HTML Skeleton + CSS Foundation

**Files:**
- Create: `/Users/wellesleychapman/PK-health/PK-health-report-phil.html`

**Step 1: Create the file with doctype, head, Google Fonts, and CSS custom properties**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Personal Health Assessment — Phil</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Lora:ital,wght@0,400;0,600;0,700;1,400&family=Inter:wght@300;400;500;600&display=swap" rel="stylesheet">
  <style>
    :root {
      --teal:        #2C7A7B;
      --teal-light:  #E6F4F4;
      --green:       #276749;
      --green-light: #F0FAF4;
      --green-mid:   #C6F6D5;
      --amber:       #B7791F;
      --amber-light: #FFFBEB;
      --amber-mid:   #FDE68A;
      --red-accent:  #9B2335;
      --blue:        #2B4C7E;
      --blue-light:  #EBF2FB;
      --blue-mid:    #BEE3F8;
      --gray-900:    #1A202C;
      --gray-700:    #374151;
      --gray-500:    #6B7280;
      --gray-200:    #E5E7EB;
      --gray-50:     #F9FAFB;
      --white:       #FFFFFF;
    }

    * { box-sizing: border-box; margin: 0; padding: 0; }

    body {
      font-family: 'Inter', sans-serif;
      font-size: 16px;
      line-height: 1.7;
      color: var(--gray-900);
      background: var(--white);
      max-width: 860px;
      margin: 0 auto;
      padding: 48px 32px;
    }

    h1, h2, h3, h4 {
      font-family: 'Lora', Georgia, serif;
    }

    h2 {
      font-size: 1.5rem;
      font-weight: 700;
      margin-bottom: 1rem;
    }

    h3 {
      font-size: 1.15rem;
      font-weight: 600;
      margin-bottom: 0.75rem;
    }

    p { margin-bottom: 1rem; }
    p:last-child { margin-bottom: 0; }

    ul {
      margin: 0.5rem 0 1rem 1.25rem;
    }

    ul li { margin-bottom: 0.35rem; }

    strong { font-weight: 600; }

    /* Section spacing */
    .section {
      margin-bottom: 3rem;
    }

    /* Horizontal rule */
    .divider {
      border: none;
      border-top: 1px solid var(--gray-200);
      margin: 2.5rem 0;
    }

    /* Stat cards row */
    .card-row {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
      gap: 1rem;
      margin: 1.25rem 0;
    }

    .stat-card {
      border-radius: 8px;
      padding: 1.25rem 1rem;
      text-align: center;
    }

    .stat-card .stat-value {
      font-family: 'Lora', serif;
      font-size: 2rem;
      font-weight: 700;
      line-height: 1.1;
      display: block;
      margin-bottom: 0.25rem;
    }

    .stat-card .stat-label {
      font-size: 0.8rem;
      font-weight: 500;
      text-transform: uppercase;
      letter-spacing: 0.05em;
    }

    .stat-card .stat-context {
      font-size: 0.85rem;
      margin-top: 0.4rem;
      font-style: italic;
    }

    /* Color variants for stat cards */
    .card-green {
      background: var(--green-light);
      border: 1px solid var(--green-mid);
      color: var(--green);
    }

    .card-amber {
      background: var(--amber-light);
      border: 2px solid var(--amber-mid);
      color: var(--amber);
    }

    .card-red {
      background: #FFF5F5;
      border: 2px solid #FEB2B2;
      color: var(--red-accent);
    }

    /* Callout boxes */
    .callout {
      border-radius: 8px;
      padding: 1.25rem 1.5rem;
      margin: 1.25rem 0;
    }

    .callout-teal {
      background: var(--teal-light);
      border-left: 4px solid var(--teal);
    }

    .callout-green {
      background: var(--green-light);
      border-left: 4px solid var(--green);
    }

    .callout-amber {
      background: var(--amber-light);
      border-left: 4px solid var(--amber);
    }

    .callout-blue {
      background: var(--blue-light);
      border-left: 4px solid var(--blue);
    }

    /* Section headers with color bars */
    .section-header {
      display: flex;
      align-items: center;
      gap: 0.75rem;
      margin-bottom: 1.25rem;
      padding-bottom: 0.75rem;
      border-bottom: 2px solid var(--gray-200);
    }

    .section-header-dot {
      width: 12px;
      height: 12px;
      border-radius: 50%;
      flex-shrink: 0;
    }

    .dot-green  { background: var(--green); }
    .dot-amber  { background: var(--amber); }
    .dot-teal   { background: var(--teal); }
    .dot-blue   { background: var(--blue); }

    .section-header h2 {
      margin-bottom: 0;
    }

    /* Step action blocks */
    .action-block {
      background: var(--blue-light);
      border: 1px solid var(--blue-mid);
      border-radius: 8px;
      padding: 1.25rem 1.5rem;
      margin-bottom: 1.5rem;
    }

    .action-block h3 {
      color: var(--blue);
      display: flex;
      align-items: center;
      gap: 0.5rem;
    }

    .step-number {
      display: inline-flex;
      align-items: center;
      justify-content: center;
      width: 28px;
      height: 28px;
      border-radius: 50%;
      background: var(--blue);
      color: white;
      font-family: 'Inter', sans-serif;
      font-size: 0.85rem;
      font-weight: 600;
      flex-shrink: 0;
    }

    /* Tables */
    table {
      width: 100%;
      border-collapse: collapse;
      font-size: 0.9rem;
      margin: 1rem 0;
    }

    th {
      background: var(--gray-50);
      border: 1px solid var(--gray-200);
      padding: 0.6rem 0.75rem;
      text-align: left;
      font-weight: 600;
      font-size: 0.8rem;
      text-transform: uppercase;
      letter-spacing: 0.04em;
      color: var(--gray-700);
    }

    td {
      border: 1px solid var(--gray-200);
      padding: 0.6rem 0.75rem;
      vertical-align: top;
    }

    tr:nth-child(even) td {
      background: var(--gray-50);
    }

    /* Timeline */
    .timeline {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 1rem;
      margin: 1.25rem 0;
    }

    .timeline-phase {
      border-radius: 8px;
      padding: 1.25rem;
      border: 1px solid var(--gray-200);
    }

    .timeline-phase h3 {
      font-size: 0.95rem;
      margin-bottom: 0.5rem;
    }

    .timeline-phase .phase-label {
      font-size: 0.75rem;
      font-weight: 600;
      text-transform: uppercase;
      letter-spacing: 0.06em;
      margin-bottom: 0.75rem;
      display: block;
    }

    .timeline-phase ul {
      font-size: 0.875rem;
      margin-left: 1rem;
    }

    .phase-1 { background: #EBF2FB; border-color: var(--blue-mid); }
    .phase-1 .phase-label { color: var(--blue); }

    .phase-2 { background: var(--teal-light); border-color: #81E6D9; }
    .phase-2 .phase-label { color: var(--teal); }

    .phase-3 { background: var(--green-light); border-color: var(--green-mid); }
    .phase-3 .phase-label { color: var(--green); }

    /* References */
    .references ol {
      margin-left: 1.25rem;
      font-size: 0.82rem;
      color: var(--gray-700);
      line-height: 1.5;
    }

    .references li {
      margin-bottom: 0.5rem;
    }

    /* Print */
    @media print {
      body { padding: 24px; font-size: 14px; }
      .timeline { grid-template-columns: repeat(3, 1fr); }
    }

    @media (max-width: 600px) {
      body { padding: 24px 16px; }
      .timeline { grid-template-columns: 1fr; }
      .card-row { grid-template-columns: repeat(2, 1fr); }
    }
  </style>
</head>
<body>
  <!-- CONTENT GOES HERE -->
</body>
</html>
```

**Step 2: Verify in browser**
Open the file in a browser. Expect a blank page with no errors in console. Fonts should load from Google CDN.

---

## Task 2: Header + Personal Introduction

**Files:**
- Modify: `PK-health-report-phil.html` — replace `<!-- CONTENT GOES HERE -->`

**Step 1: Write the document header**

```html
<!-- HEADER -->
<header style="margin-bottom: 2.5rem; padding-bottom: 1.5rem; border-bottom: 3px solid var(--teal);">
  <div style="display:flex; justify-content:space-between; align-items:flex-start; flex-wrap:wrap; gap:1rem;">
    <div>
      <p style="font-size:0.8rem; font-weight:600; text-transform:uppercase; letter-spacing:0.1em; color:var(--teal); margin-bottom:0.35rem;">Personal Health Assessment</p>
      <h1 style="font-family:'Lora',serif; font-size:2.4rem; font-weight:700; color:var(--gray-900); line-height:1.15;">Phil</h1>
    </div>
    <div style="text-align:right; font-size:0.875rem; color:var(--gray-500);">
      <p style="margin-bottom:0.2rem;"><strong style="color:var(--gray-700);">Assessment Date</strong></p>
      <p style="margin-bottom:0.5rem;">March 29, 2026</p>
      <p style="margin-bottom:0.2rem;"><strong style="color:var(--gray-700);">Prepared by</strong></p>
      <p>Wellesley</p>
    </div>
  </div>
  <p style="margin-top:1rem; font-size:0.85rem; color:var(--gray-500); font-style:italic;">
    Based on BodySpec DEXA scan results — March 26, 2026 · Informed by current evidence-based guidelines for bone health, body composition, and musculoskeletal medicine.
  </p>
</header>
```

**Step 2: Write the personal introduction**

```html
<!-- PERSONAL INTRODUCTION -->
<section class="section">
  <p style="font-family:'Lora',serif; font-size:1.15rem; color:var(--gray-700); font-style:italic; line-height:1.8;">
    Phil,
  </p>
  <p>
    I've been looking forward to sitting down with your DEXA results and putting together something useful — not just the numbers, but what they actually mean and what I think we should do about them. That's what this is.
  </p>
  <p>
    The short version: your metabolic health is genuinely good. But there's one finding that caught my attention immediately and that I want to make sure we take seriously together. Your bone density is significantly lower than it should be for your age — lower than I'd want to see, and lower than you want going into the next decades of your life.
  </p>
  <p>
    Here's the thing, and I mean this: <strong>you're finding this out at 56.</strong> Not at 66. Not after a fracture at 72. You have real runway to change this — and the evidence is clear that with the right combination of exercise, nutrition, and medical management, you can move the needle meaningfully. I've seen it. The science supports it.
  </p>
  <p>
    I'm going to walk you through everything — the good news first (and there's genuine good news), then what needs attention, then exactly what I recommend you do. I'm here to help you get started and to keep going with you. Let's dig in.
  </p>
  <p style="margin-top:1.5rem; font-family:'Lora',serif; font-style:italic; color:var(--gray-500);">— Wellesley</p>
</section>

<hr class="divider">
```

**Step 3: Verify in browser**
Header should be clean with teal bottom border. Intro text reads naturally, Lora italic on name and sign-off.

---

## Task 3: The Good News Section

**Files:**
- Modify: `PK-health-report-phil.html` — append after intro divider

**Step 1: Write section with stat cards**

```html
<!-- GOOD NEWS -->
<section class="section">
  <div class="section-header">
    <div class="section-header-dot dot-green"></div>
    <h2 style="color:var(--green);">The Good News — And There's Real Good News</h2>
  </div>

  <p>
    Your body composition profile has some genuinely strong numbers. Your metabolic health — the stuff that drives cardiovascular risk, diabetes risk, inflammatory disease — looks excellent. This matters, and it's not nothing.
  </p>

  <div class="card-row">
    <div class="stat-card card-green">
      <span class="stat-value">16.0%</span>
      <span class="stat-label">Body Fat</span>
      <p class="stat-context">12th percentile — lean and metabolically healthy</p>
    </div>
    <div class="stat-card card-green">
      <span class="stat-value">1.0 lb</span>
      <span class="stat-label">Visceral Fat</span>
      <p class="stat-context">20th percentile — minimal deep abdominal fat</p>
    </div>
    <div class="stat-card card-green">
      <span class="stat-value">Low</span>
      <span class="stat-label">Cardiovascular Risk</span>
      <p class="stat-context">Favorable body fat distribution</p>
    </div>
    <div class="stat-card card-green">
      <span class="stat-value">Above</span>
      <span class="stat-label">Sarcopenia Threshold</span>
      <p class="stat-context">Lean mass above diagnostic cutoff for sarcopenia</p>
    </div>
  </div>

  <div class="callout callout-green">
    <h3 style="color:var(--green); margin-bottom:0.5rem;">What this means</h3>
    <p>
      Low visceral fat (the metabolically dangerous fat around your organs) is one of the strongest protective factors we have for long-term metabolic and cardiovascular health. Your 16% body fat at your body weight reflects a genuinely lean physique — you're not carrying excess fat that needs to be lost before we can build. That's a great starting point.
    </p>
    <p>
      Your lean mass, while below optimal, is above the clinical threshold for sarcopenia. You're not starting from a depleted baseline — you're starting from a position where strategic training and nutrition can yield significant gains.
    </p>
  </div>
</section>

<hr class="divider">
```

**Step 2: Verify in browser**
Four green cards in a responsive grid. Green callout box with clean left border.

---

## Task 4: Concerning Findings Section

**Files:**
- Modify: `PK-health-report-phil.html` — append after good news divider

**Step 1: Write the bone density and lean mass findings**

```html
<!-- CONCERNING FINDINGS -->
<section class="section">
  <div class="section-header">
    <div class="section-header-dot dot-amber"></div>
    <h2 style="color:var(--amber);">What the DEXA Found — What Needs Attention</h2>
  </div>

  <p>
    I want to be direct with you because that's what this moment calls for. One finding here is a clear outlier, and I'd be doing you a disservice if I softened it.
  </p>

  <div class="card-row" style="grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));">
    <div class="stat-card card-red">
      <span class="stat-value">2nd</span>
      <span class="stat-label">Percentile — Bone Density</span>
      <p class="stat-context">Whole body: 1.10 g/cm² vs. 23,000 men ages 53–59</p>
    </div>
    <div class="stat-card card-amber">
      <span class="stat-value">15th</span>
      <span class="stat-label">Percentile — Lean Mass Index</span>
      <p class="stat-context">BMI-L: 17.1 kg/m² — below optimal, above sarcopenia threshold</p>
    </div>
    <div class="stat-card card-amber">
      <span class="stat-value">19th</span>
      <span class="stat-label">Percentile — Appendicular Lean Mass</span>
      <p class="stat-context">ALMI: 8.23 kg/m² — limited muscle reserve</p>
    </div>
  </div>

  <div class="callout callout-amber" style="margin-top:1.5rem;">
    <h3 style="color:var(--amber); margin-bottom:0.75rem;">Bone Density: The Priority Finding</h3>
    <p>
      A whole-body bone density at the <strong>2nd percentile</strong> means that 98 out of 100 men your age have denser bones than you do. This almost certainly meets the clinical criteria for <strong>osteoporosis</strong> (T-score ≤ −2.5). That's not a diagnosis I'm making from this scan alone — the BodySpec DEXA is excellent research-grade technology, but formal diagnosis requires a medical-grade hip and spine DEXA. What I'm confident saying is: this warrants immediate medical evaluation.
    </p>
    <p>
      Why does this matter so much? Osteoporosis in men is under-recognized and under-treated — and post-fracture outcomes in men are significantly worse than in women. Men with osteoporotic hip fractures have <strong>2–3 times higher mortality</strong> than women with the same injury. A vertebral fracture can change the trajectory of your entire physical life. These aren't distant abstractions — they're the consequences of not acting on findings like yours.
    </p>
    <p>
      Your body weight of 131.8 lbs is an independent risk factor. Studies show that low body weight approximately <strong>doubles fracture risk</strong>, and research on adolescent underweight suggests a "legacy effect" — lower peak bone mass accrual early in life carries forward regardless of adult weight. This isn't your fault. But it is something we can address.
    </p>
  </div>

  <div class="callout callout-amber" style="margin-top:1rem;">
    <h3 style="color:var(--amber); margin-bottom:0.75rem;">Lean Mass: A Secondary — But Real — Concern</h3>
    <p>
      Your lean mass index and appendicular lean mass (the muscle in your arms and legs specifically) are below optimal for your age. You're not sarcopenic by clinical definition, but you have limited reserve — and muscle mass and bone density are deeply linked. The same interventions that build muscle also build bone. This is actually good news for efficiency: we're not fighting two separate battles.
    </p>
  </div>

  <div class="callout" style="background:var(--gray-50); border-left:4px solid var(--gray-200); margin-top:1rem;">
    <h3 style="color:var(--gray-700); margin-bottom:0.5rem;">What This DEXA Can't Tell Us</h3>
    <p style="font-size:0.9rem; color:var(--gray-700);">
      The DEXA gives us excellent data on bone density and body composition, but a full picture requires more:
    </p>
    <ul style="font-size:0.9rem; color:var(--gray-700);">
      <li><strong>10-year fracture probability</strong> — requires FRAX score calculation with your clinical risk factors</li>
      <li><strong>Secondary causes of bone loss</strong> — vitamin D deficiency, low testosterone, thyroid dysfunction, hyperparathyroidism, celiac disease, and others must be ruled out with labs</li>
      <li><strong>Bone microarchitecture quality</strong> — DEXA measures density, not trabecular structure or cortical thickness</li>
      <li><strong>Muscle function</strong> — handgrip strength and physical performance testing round out the sarcopenia assessment</li>
    </ul>
    <p style="font-size:0.9rem; color:var(--gray-700); margin-top:0.5rem;">
      This is exactly why Step 1 in your action plan is a medical workup.
    </p>
  </div>
</section>

<hr class="divider">
```

**Step 2: Verify in browser**
Three cards in amber/red. Two amber callout boxes. Gray informational callout at bottom. No overflow issues.

---

## Task 5: Why Now Is the Right Time

**Files:**
- Modify: `PK-health-report-phil.html` — append after findings divider

**Step 1: Write the motivational bridge section**

```html
<!-- WHY NOW -->
<section class="section">
  <div class="section-header">
    <div class="section-header-dot dot-teal"></div>
    <h2 style="color:var(--teal);">Why Finding This at 56 Is a Gift</h2>
  </div>

  <div class="callout callout-teal">
    <p style="font-size:1.05rem; font-family:'Lora',serif; font-style:italic; line-height:1.8;">
      "The best time to address low bone density is before a fracture occurs. You are at that moment right now."
    </p>
  </div>

  <p>
    Think about the alternative timelines. If you hadn't gotten this scan, you might have found out about your bone density at 66 — after a fall, a vertebral compression fracture, or a wrist break that sends you to the ER. At that point you're managing consequences. Right now, you're in a position to <strong>prevent them entirely</strong>.
  </p>

  <p>
    Here's what the evidence shows is possible with the right intervention starting now:
  </p>

  <div class="card-row">
    <div class="stat-card" style="background:var(--teal-light); border:1px solid #81E6D9; color:var(--teal);">
      <span class="stat-value" style="font-size:1.5rem;">4.1%</span>
      <span class="stat-label">Lumbar Spine BMD Increase</span>
      <p class="stat-context">In 8 months with high-intensity resistance training (LIFTMOR-M trial)</p>
    </div>
    <div class="stat-card" style="background:var(--teal-light); border:1px solid #81E6D9; color:var(--teal);">
      <span class="stat-value" style="font-size:1.5rem;">+5–8%</span>
      <span class="stat-label">Year 1 Spine BMD Gain</span>
      <p class="stat-context">Realistic target with exercise + nutrition + pharmacotherapy combined</p>
    </div>
    <div class="stat-card" style="background:var(--teal-light); border:1px solid #81E6D9; color:var(--teal);">
      <span class="stat-value" style="font-size:1.5rem;">40–50%</span>
      <span class="stat-label">Fracture Risk Reduction</span>
      <p class="stat-context">Vertebral fracture risk reduction achievable with combined intervention</p>
    </div>
  </div>

  <p>
    The research on men with osteoporosis is clear: with <strong>high-intensity resistance training, impact loading, adequate protein and calcium, and pharmacotherapy when indicated</strong>, significant improvements in bone density are achievable — and they compound over time. The window isn't closed. It's open right now, and we're going to walk through it.
  </p>
  <p>
    Your favorable body composition — lean physique, low visceral fat — means you're not fighting metabolic headwinds. You have the foundation. We're building on it.
  </p>
</section>

<hr class="divider">
```

**Step 2: Verify in browser**
Teal accent throughout. Three teal stat cards. Block quote styled callout at top.

---

## Task 6: Action Plan — Medical Workup

**Files:**
- Modify: `PK-health-report-phil.html` — append after "why now" divider

**Step 1: Write the Action Plan header and Step 1 (Medical)**

```html
<!-- ACTION PLAN -->
<section class="section">
  <div class="section-header">
    <div class="section-header-dot dot-blue"></div>
    <h2 style="color:var(--blue);">Your Action Plan</h2>
  </div>

  <p>
    Four steps, in order of priority. The medical workup comes first because it informs everything else — but the lifestyle steps start immediately, in parallel. You don't wait for a prescription to begin training.
  </p>

  <!-- STEP 1: MEDICAL -->
  <div class="action-block">
    <h3>
      <span class="step-number">1</span>
      Medical Workup — Do This First
    </h3>
    <p style="margin-top:0.75rem;">
      Reach out to your primary care provider and request a comprehensive bone health evaluation. I've drafted a communication template below — use it, adapt it, or just bring this document to the appointment.
    </p>

    <h4 style="margin-top:1rem; margin-bottom:0.5rem; color:var(--blue);">Request the Following:</h4>
    <ul>
      <li><strong>FRAX Score Calculation</strong> — determines your 10-year fracture probability using your clinical risk factors (prior fractures, family history, smoking, alcohol, steroid use)</li>
      <li><strong>Medical-grade hip and lumbar spine DEXA</strong> — formal T-scores for diagnosis; the BodySpec scan is excellent but clinical decisions require WHO-standardized measurements</li>
      <li><strong>Discussion of pharmacotherapy</strong> — bisphosphonates (alendronate or zoledronic acid) are first-line and reduce vertebral fractures by approximately 52 per 1,000 person-years in men. For very high-risk patients, anabolic agents (teriparatide, abaloparatide) may be indicated.</li>
    </ul>

    <h4 style="margin-top:1rem; margin-bottom:0.5rem; color:var(--blue);">Lab Workup to Request:</h4>
    <table>
      <thead>
        <tr>
          <th>Test</th>
          <th>Why It Matters</th>
        </tr>
      </thead>
      <tbody>
        <tr><td>Serum 25-OH Vitamin D</td><td>Deficiency is a leading secondary cause of bone loss; target ≥30 ng/mL</td></tr>
        <tr><td>Serum calcium &amp; phosphate</td><td>Screening for hyperparathyroidism and metabolic bone disease</td></tr>
        <tr><td>Total testosterone</td><td>Hypogonadism affects 30–64% of men with low body weight and drives bone loss</td></tr>
        <tr><td>TSH (thyroid)</td><td>Hyperthyroidism is a reversible secondary cause of osteoporosis</td></tr>
        <tr><td>Complete metabolic panel</td><td>Kidney and liver function — relevant to pharmacotherapy selection</td></tr>
        <tr><td>Complete blood count</td><td>Baseline; screens for hematologic causes of bone loss</td></tr>
        <tr><td>PTH (parathyroid hormone)</td><td>If calcium is abnormal — screens for hyperparathyroidism</td></tr>
        <tr><td>Celiac screening / SPEP</td><td>If indicated — celiac disease and myeloma are secondary causes</td></tr>
      </tbody>
    </table>

    <div class="callout" style="background:#EBF2FB; border-left:3px solid var(--blue); margin-top:1rem; padding:1rem 1.25rem;">
      <p style="font-size:0.875rem; color:var(--blue);">
        <strong>Note for your appointment:</strong> If your provider questions the BodySpec data, emphasize that you're requesting a <em>medical-grade DEXA for formal diagnosis</em> — not treatment based on the BodySpec scan alone. The 2nd percentile finding is the concern, not the absolute g/cm² value. Your low body weight (131.8 lbs) is an independent, well-established risk factor that supports evaluation regardless of DEXA source. Recent guidelines (Endocrine Society 2012; JAMA 2025) support evaluation in men with clinical risk factors even before fracture.
      </p>
    </div>
  </div>
```

**Step 2: Verify in browser**
Blue action block with numbered circle. Clean table with alternating rows. Informational note box at bottom of step.

---

## Task 7: Action Plan — Exercise Program

**Files:**
- Modify: `PK-health-report-phil.html` — append inside action plan section

**Step 1: Write Exercise step**

```html
  <!-- STEP 2: EXERCISE -->
  <div class="action-block">
    <h3>
      <span class="step-number">2</span>
      Exercise Program — Start Now, Don't Wait
    </h3>
    <p style="margin-top:0.75rem;">
      This is the most powerful non-pharmacological intervention available for bone density. The LIFTMOR-M trial — the strongest evidence we have in men with osteoporosis — showed that <strong>high-intensity progressive resistance training (HiRIT) combined with impact loading</strong> produced 4.1% lumbar spine BMD and 2.8% hip BMD increases in just 8 months. Moderate-intensity exercise does not produce these results. Intensity is the mechanism.
    </p>

    <h4 style="margin:1rem 0 0.5rem; color:var(--blue);">Program Structure</h4>
    <ul>
      <li><strong>Frequency:</strong> 2–3 sessions per week (minimum 2 for bone benefit)</li>
      <li><strong>Duration:</strong> 30–40 minutes per session</li>
      <li><strong>Supervision:</strong> First 8–12 weeks with a qualified trainer or physical therapist experienced in osteoporosis; then transition to supervised group or independent training with periodic check-ins</li>
    </ul>

    <h4 style="margin:1rem 0 0.5rem; color:var(--blue);">Resistance Training (20–25 min)</h4>
    <table>
      <thead>
        <tr><th>Exercise</th><th>Sets × Reps</th><th>Intensity</th></tr>
      </thead>
      <tbody>
        <tr><td>Deadlift (or trap bar deadlift)</td><td>5 × 5</td><td>80–85% 1RM</td></tr>
        <tr><td>Overhead press (or incline press)</td><td>5 × 5</td><td>80–85% 1RM</td></tr>
        <tr><td>Back squat (or leg press if balance concern)</td><td>5 × 5</td><td>80–85% 1RM</td></tr>
        <tr><td>Chin-ups (assisted) or lat pulldown</td><td>3 × 6–8</td><td>75–80% 1RM</td></tr>
        <tr><td>Jumping chin-ups (explosive pull)</td><td>3 × 5</td><td>Bodyweight, explosive</td></tr>
      </tbody>
    </table>
    <p style="font-size:0.875rem; color:var(--gray-700); margin-top:0.5rem;">
      Rest 2–3 minutes between sets. Focus on <strong>3-second eccentric (lowering) phase</strong> and <strong>explosive concentric (lifting) phase</strong>. Progress weight by 2.5–5% when all sets are completed with proper form.
    </p>

    <h4 style="margin:1rem 0 0.5rem; color:var(--blue);">Impact Loading (5–10 min)</h4>
    <p style="font-size:0.875rem; color:var(--gray-700);">
      <strong>Target: 30–50 impacts per session.</strong> Every 10 impact loads is associated with a 0.3% increase in femoral neck BMD and 1.3% increase in lumbar spine trabecular BMD over 18 months.
    </p>
    <ul style="font-size:0.875rem;">
      <li>Drop jumps: 5 sets × 5 reps from a 10–30 cm box</li>
      <li>Multidirectional hopping: 3 sets × 10 hops (forward, lateral, backward)</li>
      <li>Countermovement jumps: 3 sets × 10 reps</li>
    </ul>

    <h4 style="margin:1rem 0 0.5rem; color:var(--blue);">Balance Training (5 min — end of session)</h4>
    <ul style="font-size:0.875rem;">
      <li>Single-leg stance: 3 × 30–60 seconds each leg</li>
      <li>Tandem walking: 3 × 20 steps</li>
      <li>Single-leg Romanian deadlift: 3 × 8 reps each leg</li>
    </ul>

    <h4 style="margin:1rem 0 0.5rem; color:var(--blue);">Progressive Overload Schedule</h4>
    <table>
      <thead>
        <tr><th>Phase</th><th>Weeks</th><th>Intensity</th><th>Volume</th><th>Focus</th></tr>
      </thead>
      <tbody>
        <tr><td><strong>Foundation</strong></td><td>1–4</td><td>60–70% 1RM</td><td>3 × 8–10</td><td>Form mastery, neuromuscular adaptation</td></tr>
        <tr><td><strong>Build</strong></td><td>5–12</td><td>75–80% 1RM</td><td>4 × 6–8</td><td>Strength development, 20–30 impacts/session</td></tr>
        <tr><td><strong>Intensification</strong></td><td>13–24</td><td>80–85% 1RM</td><td>5 × 5</td><td>Peak strength, 40–50 impacts/session</td></tr>
        <tr><td><strong>Maintenance</strong></td><td>24+</td><td>80–85% 1RM</td><td>3–4 × 5–6</td><td>Sustain gains, 30–40 impacts/session</td></tr>
      </tbody>
    </table>
  </div>
```

**Step 2: Verify in browser**
Three tables render cleanly. Impact loading callout is readable. Progressive overload table is legible.

---

## Task 8: Action Plan — Nutrition + Supplements & Monitoring

**Files:**
- Modify: `PK-health-report-phil.html` — append inside action plan section

**Step 1: Write Nutrition step**

```html
  <!-- STEP 3: NUTRITION -->
  <div class="action-block">
    <h3>
      <span class="step-number">3</span>
      Nutrition — Fuel the Adaptation
    </h3>
    <p style="margin-top:0.75rem;">
      Exercise is the stimulus. Nutrition is what your body uses to respond to it. At your body weight and with your goals, these targets are non-negotiable.
    </p>

    <h4 style="margin:1rem 0 0.5rem; color:var(--blue);">Daily Targets</h4>
    <table>
      <thead>
        <tr><th>Nutrient</th><th>Daily Target</th><th>Key Notes</th></tr>
      </thead>
      <tbody>
        <tr>
          <td><strong>Protein</strong></td>
          <td>90 g/day (1.5 g/kg)</td>
          <td>25–30g per meal across 3 meals. Within 2 hours post-exercise. Prioritize whey, lean meats, fish, eggs, dairy.</td>
        </tr>
        <tr>
          <td><strong>Calcium</strong></td>
          <td>1,200–1,500 mg/day</td>
          <td>Dietary first (dairy, sardines with bones, leafy greens, fortified foods). Supplement only if dietary intake falls short. Do not exceed 1,500 mg total.</td>
        </tr>
        <tr>
          <td><strong>Vitamin D</strong></td>
          <td>2,000 IU/day</td>
          <td>Cholecalciferol (D3) preferred. Target serum 25-OH vitamin D ≥30 ng/mL. Check levels at baseline and every 6 months.</td>
        </tr>
        <tr>
          <td><strong>Total Calories</strong></td>
          <td>1,800–2,000 kcal/day</td>
          <td>Aim for modest weight gain of 5–10 lbs over 12 months. Weight supports bone loading and anabolic processes.</td>
        </tr>
        <tr>
          <td><strong>Magnesium</strong></td>
          <td>420 mg/day</td>
          <td>Nuts, seeds, leafy greens, whole grains</td>
        </tr>
        <tr>
          <td><strong>Vitamin K</strong></td>
          <td>120 mcg/day</td>
          <td>Leafy greens (kale, spinach, broccoli)</td>
        </tr>
        <tr>
          <td><strong>Zinc</strong></td>
          <td>11 mg/day</td>
          <td>Meat, shellfish, legumes</td>
        </tr>
      </tbody>
    </table>

    <h4 style="margin:1rem 0 0.5rem; color:var(--blue);">Sample Daily Meal Plan</h4>
    <table>
      <thead>
        <tr><th>Meal</th><th>Foods</th><th>Protein</th><th>Calcium</th></tr>
      </thead>
      <tbody>
        <tr><td><strong>Breakfast</strong></td><td>Greek yogurt + berries + almonds + fortified cereal</td><td>~20g</td><td>~300 mg</td></tr>
        <tr><td><strong>Lunch</strong></td><td>Grilled salmon + quinoa + leafy greens with olive oil</td><td>~25g</td><td>~200 mg</td></tr>
        <tr><td><strong>Post-workout</strong></td><td>Whey protein shake + banana</td><td>~25g</td><td>—</td></tr>
        <tr><td><strong>Dinner</strong></td><td>Lean beef or chicken + sweet potato + broccoli + cheese</td><td>~30g</td><td>~300 mg</td></tr>
        <tr><td><strong>Snacks</strong></td><td>Cottage cheese, hard-boiled eggs, or protein bar</td><td>to target</td><td>—</td></tr>
      </tbody>
    </table>
    <p style="font-size:0.875rem; color:var(--gray-500); margin-top:0.5rem; font-style:italic;">
      Evidence: Protein at 1.5 g/kg/day showed the most beneficial effects for preventing sarcopenia — appendicular skeletal muscle increased 0.52 kg vs. 0.08 kg in controls over 12 weeks.
    </p>
  </div>

  <!-- STEP 4: SUPPLEMENTS & MONITORING -->
  <div class="action-block">
    <h3>
      <span class="step-number">4</span>
      Supplements &amp; Monitoring Schedule
    </h3>

    <h4 style="margin:0.75rem 0 0.5rem; color:var(--blue);">Daily Supplements</h4>
    <ul>
      <li><strong>Vitamin D3 — 2,000 IU</strong> with your largest meal</li>
      <li><strong>Calcium citrate — 500–600 mg</strong> if dietary calcium intake is insufficient (citrate form preferred over carbonate, especially with meals)</li>
    </ul>

    <h4 style="margin:1rem 0 0.5rem; color:var(--blue);">Monitoring Schedule</h4>
    <table>
      <thead>
        <tr><th>Timepoint</th><th>Assessments</th><th>Purpose</th></tr>
      </thead>
      <tbody>
        <tr><td><strong>Baseline (now)</strong></td><td>Medical DEXA (hip/spine), full lab workup, FRAX score, strength baseline, functional tests</td><td>Formal diagnosis, identify secondary causes, establish baseline</td></tr>
        <tr><td><strong>3 months</strong></td><td>Bone turnover markers (CTX, P1NP), strength testing</td><td>Verify treatment response; adjust exercise and pharmacotherapy if needed</td></tr>
        <tr><td><strong>6 months</strong></td><td>Vitamin D level, functional tests, body composition</td><td>Ensure nutritional adequacy; track lean mass progress</td></tr>
        <tr><td><strong>12 months</strong></td><td>Medical DEXA, strength testing, FRAX recalculation</td><td>Assess BMD response to full year of intervention</td></tr>
        <tr><td><strong>18 months</strong></td><td>Body composition, functional tests</td><td>Monitor lean mass trajectory</td></tr>
        <tr><td><strong>24 months</strong></td><td>Medical DEXA, comprehensive reassessment</td><td>Determine long-term treatment strategy; celebrate progress</td></tr>
      </tbody>
    </table>
  </div>

</section><!-- end action plan -->

<hr class="divider">
```

**Step 2: Verify in browser**
Nutrition table has 7 rows. Meal plan table has 5 rows. Monitoring table has 6 rows. All clean.

---

## Task 9: Goals & Timeline + Closing

**Files:**
- Modify: `PK-health-report-phil.html` — append after action plan divider

**Step 1: Write the timeline section**

```html
<!-- TIMELINE -->
<section class="section">
  <div class="section-header">
    <div class="section-header-dot dot-teal"></div>
    <h2 style="color:var(--teal);">Goals &amp; Timeline</h2>
  </div>

  <p>
    These targets are grounded in the best available clinical trial evidence for men with osteoporosis and low muscle mass. They're ambitious but achievable — provided you're consistent with the program and engaged with your medical team.
  </p>

  <div class="timeline">
    <div class="timeline-phase phase-1">
      <span class="phase-label">Phase 1 · Months 0–6</span>
      <h3>Establish &amp; Stabilize</h3>
      <ul>
        <li>Medical workup complete</li>
        <li>Pharmacotherapy initiated if indicated</li>
        <li>HiRIT program underway</li>
        <li>Stabilize bone loss</li>
        <li>Lean mass: +2–4 lbs</li>
        <li>ALMI target: 8.5–8.7 kg/m²</li>
        <li>Strength: +20–30% baseline</li>
        <li>Single-leg balance: 60 sec</li>
      </ul>
    </div>
    <div class="timeline-phase phase-2">
      <span class="phase-label">Phase 2 · Months 6–12</span>
      <h3>Build &amp; Measure</h3>
      <ul>
        <li>Lumbar spine BMD: +2–4%</li>
        <li>Hip BMD: +1.5–3%</li>
        <li>Target percentile: 10th–15th</li>
        <li>Lean mass: +4–7 lbs total</li>
        <li>ALMI target: 8.7–9.0 kg/m²</li>
        <li>Strength: +40–60% baseline</li>
        <li>Gait speed: &gt;1.0 m/s</li>
        <li>12-month DEXA + FRAX</li>
      </ul>
    </div>
    <div class="timeline-phase phase-3">
      <span class="phase-label">Phase 3 · Months 12–24</span>
      <h3>Consolidate &amp; Sustain</h3>
      <ul>
        <li>Lumbar spine BMD: +4–6% from baseline</li>
        <li>Hip BMD: +3–5% from baseline</li>
        <li>T-score: moving toward osteopenia range</li>
        <li>Target percentile: 15th–20th</li>
        <li>Body weight: 138–145 lbs</li>
        <li>Lean mass: +7–12 lbs total</li>
        <li>ALMI target: 9.0–9.5 kg/m²</li>
        <li>Fracture risk: zero fractures</li>
      </ul>
    </div>
  </div>

  <div class="callout callout-teal" style="margin-top:1.5rem;">
    <h3 style="color:var(--teal); margin-bottom:0.5rem;">Realistic Combined Outcome Expectation (Year 1)</h3>
    <p>
      Exercise alone (LIFTMOR-M) + bisphosphonate therapy + optimized nutrition, working together:
    </p>
    <ul>
      <li><strong>5–8% lumbar spine BMD increase</strong> in Year 1</li>
      <li><strong>3–5% hip BMD increase</strong> in Year 1</li>
      <li><strong>4–7 lbs lean mass gain</strong> in Year 1</li>
      <li><strong>40–50% reduction in vertebral fracture risk</strong> over the treatment period</li>
      <li><strong>20–30% reduction in hip fracture risk</strong></li>
    </ul>
    <p style="margin-top:0.75rem; font-size:0.875rem; color:var(--gray-700);">
      <strong>Critical success factors:</strong> Exercise compliance &gt;75% · Maintaining 80–85% 1RM intensity · 30–50 impacts per session · Daily protein at 1.5 g/kg · Consistent pharmacotherapy if prescribed · Regular medical follow-up.
    </p>
  </div>
</section>

<hr class="divider">
```

**Step 2: Write the closing**

```html
<!-- CLOSING -->
<section class="section">
  <div class="callout callout-teal" style="padding:2rem;">
    <h2 style="color:var(--teal); margin-bottom:1rem;">I'm Here — Let's Do This</h2>
    <p>
      Phil, I want you to know that I'm not handing you this document and disappearing. I mean it when I say I'm available to help you through every step of this.
    </p>
    <p>
      I can help you find a trainer who is qualified and experienced in working with people with osteoporosis — this is genuinely specialized work and it matters who you work with. I can help you prep for your PCP appointment, talk through what to ask, and make sure you're advocating effectively for yourself. If you end up discussing pharmacotherapy, I can walk you through the options and help you think through the decision.
    </p>
    <p>
      Most importantly: you caught this early. Not at 66. Not after a fracture. At 56, with a lean physique, good metabolic health, and — I know this from hiking with you — a real capacity for physical effort when you're pointed in the right direction. That is a strong hand to be holding.
    </p>
    <p>
      The next step is simple: reach out to your PCP. Everything else flows from there.
    </p>
    <p style="margin-top:1.5rem; font-family:'Lora',serif; font-size:1.1rem; font-style:italic; color:var(--teal);">
      — Wellesley
    </p>
  </div>
</section>

<hr class="divider">
```

**Step 3: Verify in browser**
Three-column timeline renders correctly. Teal closing callout is warm and readable. Sign-off in Lora italic.

---

## Task 10: References Section

**Files:**
- Modify: `PK-health-report-phil.html` — append after closing divider

**Step 1: Write deduplicated references**

Deduplicate across both source documents. Shared references (appearing in both files):
- Morin/Leslie/Schousboe JAMA 2025 [Osteoporosis]
- Ye/Ebeling/Kline Lancet 2025 [Osteoporosis]
- Watts/Adler Endocrine Society guideline 2012
- Harding/Weeks LIFTMOR-M JBMR 2020
- Daly/Dalla Via Bone 2021
- Beaudart aging meta-analysis 2023
- Vilaca/Eastell Lancet D&E 2022
- Ebeling NEJM 2008

Unique to treatment plan: Kemmler FrOST, Dent Lancet malnutrition, Campbell Gerontology, Park AJCN, Lin Clin Nutr
Unique to DEXA summary: Simchoni JAMA Network Open 2025, Papaioannou Osteoporos Int 2009, Benz JAMA Network Open 2024, Tessier JCSM 2019, Ensrud Osteoporos Int 2018, Reid EJE 2022, Devries Bone 2023, Jensen JAMA Network Open 2024

```html
<!-- REFERENCES -->
<section class="section references">
  <div class="section-header">
    <div class="section-header-dot" style="background:var(--gray-500);"></div>
    <h2 style="color:var(--gray-700); font-size:1.15rem;">References</h2>
  </div>
  <ol>
    <li>Morin SN, Leslie WD, Schousboe JT. Osteoporosis. <em>JAMA.</em> 2025;334(10):894–907. doi:10.1001/jama.2025.6003</li>
    <li>Ye C, Ebeling P, Kline G. Osteoporosis. <em>Lancet.</em> 2025;406(10514):2003–2016. doi:10.1016/S0140-6736(25)01385-6</li>
    <li>Watts NB, Adler RA, Bilezikian JP, et al. Osteoporosis in Men: An Endocrine Society Clinical Practice Guideline. <em>J Clin Endocrinol Metab.</em> 2012;97(6):1802–22. doi:10.1210/jc.2011-3045</li>
    <li>Ebeling PR. Osteoporosis in Men. <em>N Engl J Med.</em> 2008;358(14):1474–82. doi:10.1056/NEJMcp0707217</li>
    <li>Vilaca T, Eastell R, Schini M. Osteoporosis in Men. <em>Lancet Diabetes Endocrinol.</em> 2022;10(4):273–283. doi:10.1016/S2213-8587(22)00012-2</li>
    <li>Harding AT, Weeks BK, Lambert C, et al. A Comparison of Bone-Targeted Exercise Strategies to Reduce Fracture Risk in Middle-Aged and Older Men With Osteopenia and Osteoporosis: LIFTMOR-M Semi-Randomized Controlled Trial. <em>J Bone Miner Res.</em> 2020;35(8):1404–1414. doi:10.1002/jbmr.4008</li>
    <li>Daly RM, Dalla Via J, Fyfe JJ, Nikander R, Kukuljan S. Effects of Exercise Frequency and Training Volume on Bone Changes Following a Multi-Component Exercise Intervention in Middle Aged and Older Men: Secondary Analysis of an 18-Month RCT. <em>Bone.</em> 2021;148:115944. doi:10.1016/j.bone.2021.115944</li>
    <li>Kemmler W, Kohl M, Fröhlich M, et al. Effects of High-Intensity Resistance Training on Osteopenia and Sarcopenia Parameters in Older Men With Osteosarcopenia — FrOST Trial. <em>J Bone Miner Res.</em> 2020;35(9):1634–1644. doi:10.1002/jbmr.4027</li>
    <li>Beaudart C, Demonceau C, Sabico S, et al. Efficacy of Osteoporosis Pharmacological Treatments in Men: A Systematic Review and Meta-Analysis. <em>Aging Clin Exp Res.</em> 2023;35(9):1789–1806. doi:10.1007/s40520-023-02478-9</li>
    <li>Simchoni M, Landau R, Derazne E, et al. Adolescent Body Mass Index, Weight Trajectories to Adulthood, and Osteoporosis Risk. <em>JAMA Netw Open.</em> 2025;8(8):e2525079. doi:10.1001/jamanetworkopen.2025.25079</li>
    <li>Papaioannou A, Kennedy CC, Cranney A, et al. Risk Factors for Low BMD in Healthy Men Age 50 Years or Older: A Systematic Review. <em>Osteoporos Int.</em> 2009;20(4):507–18. doi:10.1007/s00198-008-0720-1</li>
    <li>Ensrud KE, Vo TN, Burghardt AJ, et al. Weight Loss in Men in Late Life and Bone Strength and Microarchitecture. <em>Osteoporos Int.</em> 2018;29(7):1549–1558. doi:10.1007/s00198-018-4489-6</li>
    <li>Benz E, Pinel A, Guillet C, et al. Sarcopenia and Sarcopenic Obesity and Mortality Among Older People. <em>JAMA Netw Open.</em> 2024;7(3):e243604. doi:10.1001/jamanetworkopen.2024.3604</li>
    <li>Tessier AJ, Wing SS, Rahme E, Morais JA, Chevalier S. Physical Function-Derived Cut-Points for Sarcopenia and Dynapenia From the Canadian Longitudinal Study on Aging. <em>J Cachexia Sarcopenia Muscle.</em> 2019;10(5):985–999. doi:10.1002/jcsm.12462</li>
    <li>Park Y, Choi JE, Hwang HS. Protein Supplementation Improves Muscle Mass and Physical Performance in Undernourished Prefrail and Frail Elderly Subjects. <em>Am J Clin Nutr.</em> 2018;108(5):1026–1033. doi:10.1093/ajcn/nqy214</li>
    <li>Lin CC, Shih MH, Chen CD, Yeh SL. Effects of Adequate Dietary Protein With Whey, Leucine, and Vitamin D Supplementation on Sarcopenia in Older Adults. <em>Clin Nutr.</em> 2021;40(3):1323–1329. doi:10.1016/j.clnu.2020.08.017</li>
    <li>Campbell WW, Deutz NEP, Volpi E, Apovian CM. Nutritional Interventions: Dietary Protein Needs and Influences on Skeletal Muscle of Older Adults. <em>J Gerontol A Biol Sci Med Sci.</em> 2023;78(Suppl 1):67–72. doi:10.1093/gerona/glad038</li>
    <li>Dent E, Wright ORL, Woo J, Hoogendijk EO. Malnutrition in Older Adults. <em>Lancet.</em> 2023;401(10380):951–966. doi:10.1016/S0140-6736(22)02612-5</li>
    <li>Reid IR. Osteoporosis Management. <em>Eur J Endocrinol.</em> 2022;187(4):R65–R80. doi:10.1530/EJE-22-0574</li>
    <li>Devries MC, Giangregorio L. Using the Specificity and Overload Principles to Prevent Sarcopenia, Falls and Fractures With Exercise. <em>Bone.</em> 2023;166:116573. doi:10.1016/j.bone.2022.116573</li>
    <li>Jensen SBK, Sørensen V, Sandsdal RM, et al. Bone Health After Exercise Alone, GLP-1 Receptor Agonist Treatment, or Combination Treatment. <em>JAMA Netw Open.</em> 2024;7(6):e2416775. doi:10.1001/jamanetworkopen.2024.16775</li>
  </ol>

  <p style="margin-top:1.5rem; font-size:0.78rem; color:var(--gray-500); font-style:italic; border-top:1px solid var(--gray-200); padding-top:1rem;">
    This document is intended for personal health education and communication purposes. It does not constitute a formal medical diagnosis or replace evaluation by a licensed clinician. Clinical decisions should be made in partnership with your healthcare provider.
  </p>
</section>
```

**Step 2: Verify in browser**
21 references in clean small type. Disclaimer at bottom in gray italic.

---

## Task 11: Final Review Pass

**Step 1: Open in browser and verify full document**
- Scroll through entire document
- Check all tables render without overflow
- Check color coding is consistent (green/good news, amber/concerns, teal/motivation, blue/action)
- Check responsive behavior at narrow width (drag browser narrower)
- Check print preview looks reasonable (Cmd+P or Ctrl+P)

**Step 2: Spot-check content accuracy against source files**
- Confirm all DEXA numbers match: 1.10 g/cm², 2nd percentile, 131.8 lbs, 16.0% body fat, 1.0 lb visceral fat, 17.1 kg/m² LMI, 8.23 kg/m² ALMI
- Confirm exercise protocol matches LIFTMOR-M: 5×5 at 80–85% 1RM, 4.1% lumbar BMD, 2.8% hip BMD
- Confirm protein target: 1.5 g/kg = 90 g/day for 59.8 kg
- Confirm vitamin D: 2000 IU/day, target ≥30 ng/mL

**Step 3: Commit**
```bash
cd /Users/wellesleychapman/PK-health
git add PK-health-report-phil.html
git commit -m "Add Phil personal health assessment HTML report

Evidence-based bone density and body composition assessment with
exercise, nutrition, and medical workup recommendations authored
by Wellesley for Phil, based on March 2026 BodySpec DEXA results.

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>"
```

---

## Summary

| Task | File | Action |
|------|------|--------|
| 1 | `PK-health-report-phil.html` | Create skeleton + full CSS |
| 2 | `PK-health-report-phil.html` | Header + personal intro |
| 3 | `PK-health-report-phil.html` | Good news section + stat cards |
| 4 | `PK-health-report-phil.html` | Concerning findings section |
| 5 | `PK-health-report-phil.html` | Why now / motivational bridge |
| 6 | `PK-health-report-phil.html` | Action plan: medical workup |
| 7 | `PK-health-report-phil.html` | Action plan: exercise |
| 8 | `PK-health-report-phil.html` | Action plan: nutrition + monitoring |
| 9 | `PK-health-report-phil.html` | Goals timeline + closing |
| 10 | `PK-health-report-phil.html` | References (deduplicated, 21 total) |
| 11 | `PK-health-report-phil.html` | Final review + commit |
