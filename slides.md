---
theme: apple-basic
title: "CDP 翻译模型训练 — 项目更新"
info: |
  CDP 项目翻译模型微调优化成果更新
colorSchema: light
drawings:
  persist: false
transition: slide-left
mdc: true
---

<CoverSlide
  title="CDP 翻译模型训练"
  subtitle="项目优化成果更新"
  tagline="问题分析 · 优化方案 · 效果验证 · 下一步"
/>

---

# CDP 翻译模型优化 — 问题分析与技术方案

<ProcessChevrons
  :steps="[
    { label: '一期 ✅', sublabel: 'Qwen 8B 微调 PoC\n准确度接近 GPT-4o', color: '#16a34a' },
    { label: '优化阶段 🔄', sublabel: '翻译自然度优化\n+ 推理上生产', color: '#0284c7' },
    { label: '下一阶段', sublabel: '扩展到更多场景', color: '#94a3b8' }
  ]"
/>

<div class="grid grid-cols-[3fr_2fr] gap-4 mt-1">
<div class="text-xs leading-relaxed">

**一期完成情况：** 完成 Qwen 8B SFT+GRPO 微调，验证了自有模型替代商业 API 的可行性与成本优势。但业务使用中发现**翻译有明显机器痕迹** — 专词机械复制、语义重复、句式不自然

**根因：** 传统指标（BLEU/BERT score）只衡量词汇匹配，不衡量自然度；小样本下过拟合

**优化方案 — Teacher-Student + LLM as Judge：**
- **大模型（Teacher）** 作为评委，按精细化标准给翻译打分
- **小模型（Student）** 根据评分反馈迭代学习
- **评分标准自动生成：** 生成器 vs 评分器对抗迭代，自动发现最具区分度的评分提示词（避免人工编写不够精细）
- **评分模型：** Nova 2 Lite（vs Claude 4.5 Sonnet 效果无差异，成本更低）
- **训练配置：** Qwen 8B / GRPO / 2×g6e.48xlarge / ~14h
- **AWS** 团队主导方案设计与训练平台搭建

</div>
<div class="flex flex-col items-center justify-center">

<div class="text-xs font-semibold mb-0">迭代优化闭环</div>

<Flywheel
  :items="[
    { label: '生成器\n生成翻译', color: '#0284c7' },
    { label: '评分器\nLLM 评分', color: '#16a34a' },
    { label: '优化器\n调整提示词', color: '#d97706' },
    { label: '小模型\n迭代学习', color: '#7c3aed' }
  ]"
  :size="220"
  centerIcon="⟳"
/>

<div class="text-xs text-gray-500 text-center">生成器与评分器对抗迭代<br/>自动发现最优评分标准</div>

</div>
</div>

---

# 效果验证与下一步

<div class="grid grid-cols-[1fr_1fr] gap-6 text-sm">
<div>

### 优化效果

小规模测试集（200 条）显示翻译质量**显著提升**，业务标记的翻译问题**绝大部分已解决**：

<TChart
  leftTitle="优化前"
  rightTitle="优化后"
  leftColor="#ef4444"
  rightColor="#16a34a"
  :leftItems="[
    { text: '专词机械复制、缺主语' },
    { text: '语义重复、用词不符合临床习惯' }
  ]"
  :rightItems="[
    { text: '自然表达，专词不再机械复制' },
    { text: '句式简洁清晰，用词符合临床惯例' }
  ]"
/>

<div class="text-xs text-gray-400 mt-1">* 评分基于小规模测试集，仍需业务侧进一步验证</div>

</div>
<div>

### 模型代理部署（LiteLLM）

客户主要服务在美洲（可用 Claude），国内需 VPN — 已完成 LiteLLM 代理部署：测试账号部署完成、Admin access 已开通、AWS Key 配置测试通过，待联合测试

### 下一步

<CardGrid :columns="1">
  <SummaryCard number="1" title="业务验证" description="与业务部门联合评估，确认翻译质量提升" color="#0284c7" />
  <SummaryCard number="2" title="模型上线" description="LiteLLM 代理联合测试 + 压力测试" color="#7c3aed" />
  <SummaryCard number="3" title="持续优化" description="更低成本评分模型；14B 模型；更多场景" color="#64748b" />
</CardGrid>

</div>
</div>
