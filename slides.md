---
theme: apple-basic
title: "CDP 翻译模型训练 — 项目更新"
info: |
  CDP 项目翻译模型微调一期回顾与二期成果
colorSchema: light
drawings:
  persist: false
transition: slide-left
mdc: true
---

<CoverSlide
  title="CDP 翻译模型训练"
  subtitle="一期回顾与二期成果"
  tagline="项目进展 · 优化结果 · 后续计划"
/>

---

# 项目进展与核心发现

<SlideHeading subtitle="一期验证完成 → 二期聚焦翻译自然度" />

<ProcessChevrons
  :steps="[
    { label: '阶段一 ✅', sublabel: '翻译模型微调 PoC', color: '#16a34a' },
    { label: '阶段二 🔄', sublabel: '推理上生产 + 持续微调', color: '#0284c7' },
    { label: '阶段三', sublabel: '扩展到其他业务场景', color: '#94a3b8' }
  ]"
/>

<div class="mt-4 px-8 py-4 bg-gray-50 rounded-lg text-sm">

**一期成果：** Qwen 8B 微调后翻译准确度接近 GPT-4o，技术路线（SFT + GRPO）验证通过，成本优势明确

**业务反馈：** 翻译有明显的机器翻译痕迹 — 专词机械复制、语义重复、句式不自然、用词不符合临床习惯

**根因分析：** 传统指标（BLEU, BERT score）只能衡量词汇匹配，无法衡量翻译自然度；小样本下出现过拟合

<div class="text-blue-600 font-semibold mt-2">→ 二期目标：解决模型拟人化问题，让翻译像人一样自然</div>

</div>

---

# 二期优化结果

<SlideHeading subtitle="Teacher-Student 架构 + LLM as Judge + 生成对抗提示词优化" />

<StatHighlight
  :stats="[
    { value: '+2.1%', label: '翻译评分提升\n8.93 → 9.12', color: '#0284c7' },
    { value: '+164%', label: '优秀翻译增幅\n93-100分：14→37条', color: '#16a34a' },
    { value: '91.1%', label: '业务问题解决率\n56个问题解决51个', color: '#d97706' }
  ]"
/>

<div class="mt-2"></div>

<HorizontalBarChart
  :bars="[
    { label: '优化前', value: '8.93', width: 89.3, color: '#94a3b8' },
    { label: '简洁提示词', value: '9.11', width: 91.1, color: '#0284c7' },
    { label: '详细提示词', value: '9.12', width: 91.2, color: '#2563eb', highlight: true },
    { label: 'GPT-4o', value: '9.77', width: 97.7, color: '#16a34a', highlight: true }
  ]"
  :labelWidth="100"
  :barHeight="24"
/>

<TChart
  leftTitle="优化前"
  rightTitle="优化后"
  leftColor="#ef4444"
  rightColor="#16a34a"
  :leftItems="[
    { text: '专词机械复制（interproximal space allocation）' },
    { text: '语义重复、缺主语、指代不清晰' },
    { text: '用词不符合临床习惯' }
  ]"
  :rightItems="[
    { text: '不再机械使用专词，表达自然' },
    { text: '句式简洁清晰、指代明确' },
    { text: '用词符合临床习惯（heavy occlusion）' }
  ]"
/>

---

# 后续计划 — 时间线

<SlideHeading subtitle="从验证到生产到扩展" />

<CardGrid :columns="3">
  <SummaryCard
    number="1"
    title="近期（1-2 周）"
    description="与业务部门评估训练结果，确认数值提升；模型部署至 LiteLLM 代理 + 压力测试"
    color="#0284c7"
  />
  <SummaryCard
    number="2"
    title="中期（1 个月内）"
    description="评估 Qwen 3.5 替代 Nova 降低评分成本；LiteLLM 代理联合测试，解决国内外访问"
    color="#7c3aed"
  />
  <SummaryCard
    number="3"
    title="CDP 后续"
    description="专词映射灵活性优化；14B 模型效果与成本评估；扩展到其他业务场景（阶段三目标）"
    color="#64748b"
  />
</CardGrid>

---

# 后续计划 — 详细分工

<SlideHeading subtitle="责任矩阵与时间节点" />

| 事项 | 负责方 | 时间 |
|---|---|---|
| 与业务部门评估训练结果 | TAM + 客户 | 2 周内 |
| 评估 Qwen 3.5 替代 Nova | 客户 | 1 月内 |
| 模型部署至代理 + 压力测试 | TAM + 客户 | 评估完成后 |
| LiteLLM 代理联合测试 | TAM + 客户 | 部署完成后 |
| 专词映射灵活性优化 | 待定 | CDP 后 |
| 14B 模型效果与成本评估 | 待定 | CDP 后 |
