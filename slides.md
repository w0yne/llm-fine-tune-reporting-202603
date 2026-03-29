---
theme: apple-basic
title: "LLM Translation Fine-Tuning — CDP Project Update"
info: |
  CDP project update on LLM translation model fine-tuning
  Phase 1 review and Phase 2 results
colorSchema: light
drawings:
  persist: false
transition: slide-left
mdc: true
---

<CoverSlide
  title="LLM Translation Fine-Tuning"
  subtitle="CDP Project Update — 2026.03"
  tagline="Phase 1 Review · Phase 2 Results · Next Steps"
/>

---

# Phase 1 Review & Phase 2 Focus

<SlideHeading subtitle="From accuracy validation to natural fluency" />

<ProcessChevrons
  :steps="[
    { label: 'Phase 1 ✅', description: 'Translation model\nfine-tune PoC', color: '#16a34a' },
    { label: 'Phase 2 🔄', description: 'Production deployment\n+ continuous tuning', color: '#0284c7' },
    { label: 'Phase 3', description: 'Expand to other\nbusiness scenarios', color: '#94a3b8' }
  ]"
/>

<div class="grid grid-cols-2 gap-8 mt-6">
<div>

### Phase 1 Results

- **Qwen 8B** fine-tuned, accuracy approaching GPT-4o
- Technical validation: **SFT + GRPO** training pipeline
- Cost advantage: self-hosted model vs GPT-4o API

</div>
<div>

### Business Feedback: Machine Translation Artifacts

<div class="text-red-600 font-semibold mb-2">Translation lacks natural fluency</div>

- Mechanical term copying — clinical terminology not idiomatic
- Semantic redundancy, unnatural syntax, imprecise word choice

**Root cause:** Traditional metrics (BLEU, BERT score) only measure lexical matching, not naturalness; overfitting on small sample

<div class="text-blue-600 font-semibold mt-3">→ Phase 2 goal: Solve humanization problem</div>

</div>
</div>

---

# Phase 2 Solution & Key Results

<SlideHeading subtitle="Teacher-Student architecture with adversarial prompt optimization" />

<div class="grid grid-cols-2 gap-8">
<div>

### Technical Approach

- **Teacher-Student** architecture + **LLM as Judge**
- TAM innovation: **Adversarial prompt optimization**
  - Auto-discovers optimal scoring criteria
  - Novel approach — no similar method found in literature
- Scoring model: **Nova 2 Lite**
  - No significant difference vs Claude 4.5 Sonnet
  - Lower cost selected
- Training: Qwen 8B / GRPO / 2×g6e.48x / ~14h
- Training platform migrated us-west-2 → us-east-2 (GPU capacity)

</div>
<div>

### Key Results (200 test samples)

<div class="space-y-4">

<div class="bg-blue-50 rounded-lg p-3">
  <div class="text-blue-700 font-bold text-lg">Translation Score +2.1%</div>
  <div class="text-sm">8.93 → 9.11-9.12 (+0.18-0.19)</div>
  <div class="text-sm">Approaching GPT-4o level (9.77)</div>
</div>

<div class="bg-green-50 rounded-lg p-3">
  <div class="text-green-700 font-bold text-lg">Excellent Translations +129-164%</div>
  <div class="text-sm">93-100 score range: 14 → 32-37 samples</div>
</div>

<div class="bg-amber-50 rounded-lg p-3">
  <div class="text-amber-700 font-bold text-lg">Business Issue Resolution 87.5-91.1%</div>
  <div class="text-sm">56 tagged issues → 49-51 resolved</div>
  <div class="text-sm">Concise prompt: 91.1% | Detailed prompt: 87.5%</div>
</div>

<div class="bg-gray-50 rounded-lg p-3">
  <div class="text-gray-700 font-bold">Score Reliability ✓</div>
  <div class="text-sm">LLM Judge vs human scoring: consistent trend</div>
</div>

</div>

</div>
</div>

---

# Next Steps

<SlideHeading subtitle="Phased plan from validation to production to expansion" />

<div class="grid grid-cols-3 gap-6 mt-4">

<div class="border-l-4 border-blue-500 pl-4">

### Near-term (1-2 weeks)

- Evaluate current results with business team — confirm score improvements
- Deploy model to **LiteLLM proxy** + stress test

</div>

<div class="border-l-4 border-indigo-500 pl-4">

### Mid-term (1 month)

- Evaluate **Qwen 3.5** to replace Nova — reduce scoring cost
- **LiteLLM** proxy joint testing (solve domestic/international access)

</div>

<div class="border-l-4 border-gray-400 pl-4">

### Post-CDP

- Specialized term mapping flexibility optimization
- **14B model** evaluation — performance vs cost
- Expand to other business scenarios (Phase 3 target)

</div>

</div>

<div class="mt-8 text-center text-gray-500 text-sm">

AWS Enterprise Support Team · CDP Project · 2026-03

</div>
