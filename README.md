# Dental Knowledge Base v2 — Interactive Demo
## 牙科诊疗知识库 v2 — 交互演示

A **diagnosis-first** dental clinical decision support pilot. Single-file interactive demo, all logic runs locally in the browser, no server required.

以**诊断为入口**的牙科决策支持试点。单文件交互演示，全部逻辑在浏览器本地运行，无需后端服务。

**👉 Live demo: https://ycycycycyc.github.io/dental-cds-v2/**

### What's new / 最近更新

**2026-05-27**
- ✅ All 28 references URL/DOI-verified — see `ATTRIBUTIONS.md`
- ✅ Tiered non-healing rule: 14-day caution + 21-day NICE NG12 urgent (replaces single 14-day rule)
- ✅ Roadmap published — `ROADMAP.md` lists all P1–P5 pending work

**2026-05-26**
- ✅ FDI tooth notation with auto-derivation + canal-count clinician input
- ✅ Anatomical alerts (MB2, C-shape, lower incisor 2-canal etc.)
- ✅ 30 NHSA 立项指南 billing items mapped to treatments

更新摘要：参考文献全部核实 / 两档不愈合规则 / FDI 牙位 / NHSA 立项指南 / 见 ATTRIBUTIONS.md 与 ROADMAP.md。

---

## ⚠ Disclaimer / 免责声明

**This is a pilot / educational demo only.** Use for clinical-review and teaching purposes. **Not a substitute for clinical judgment. Not approved for actual patient care.**

The diagnostic logic, treatment options, and NHSA billing items have **not** been signed off by a licensed clinician for production use. Some referenced data points were extracted by OCR with low confidence and require re-verification against original sources.

**本系统仅供试点与教育演示。** 用于临床审阅与教学。**不可替代临床判断，未经批准用于实际诊疗。**

诊断逻辑、治疗方案及 NHSA 收费项目**均未**经执业医师签字确认。部分 OCR 提取数据置信度较低，需对照原始资料复核。

---

## What it does / 功能概述

- **29 diagnoses** across 5 ICD-10 domains: pulpal, periapical, caries, periodontal, mucosal/oncology
- **65 treatments** gated by clinical answers (auto-selected from clinical state)
- **35 symptoms** with weighted differential mapping
- **11 red flags** including:
  - Two-tier oral-cancer screening (14-day caution → 21-day NICE NG12 urgent referral)
  - MRONJ, ORN, anticoagulant coordination, uncontrolled diabetes, spreading infection
- **30 NHSA 立项指南 items** mapped to 34 of 65 treatments — real codes from 国家医保局 2024-2025 publications
- **52 FDI tooth lookup** with anatomical alerts (MB2, C-shape, etc.) — auto-derives tooth_type / tooth_position / quadrant
- **28 references** — all URL/DOI-verified (AAE, Cohen's, EFP S3, Tonetti 2018, MASCC, WHO OPMD, NICE NG12, etc.)
- **3 entry points**: by ICD code · by name (EN/CN + synonyms) · by symptom-driven differential
- Bilingual (EN / 中文 / Both)

29 项诊断 · 65 项治疗 · 35 项症状 · 11 项红色警报 · 30 项 NHSA 立项指南 · 52 颗 FDI 牙位 · 28 篇参考文献（全部已核实 URL/DOI）· 3 种入口 · 中英双语

---

## How to use / 使用方法

1. **Open `index.html`** in any modern browser (Chrome, Safari, Firefox, Edge).
2. Pick a **scenario** to instantly load a worked example, OR
3. **Search**: by ICD code (e.g., `K04.01`), by name (e.g., `irreversible pulpitis`, `红斑`), or by symptoms.
4. Fill clinical answers on the right; output updates in real time.
5. (Optional) Select an FDI tooth (e.g., `36`) — `tooth_type` / `tooth_position` / `quadrant` are auto-derived; anatomical alerts surface (MB2, C-shape, etc.).
6. (Optional) Enter `canal_count` for RCT-class billing quantification.

用任意现代浏览器打开 `index.html`。点"场景"一键载入示例，或按编码/名称/症状搜索。右侧填写临床应答，输出实时更新。可选 FDI 自动派生 tooth_type/position/quadrant 并显示解剖学提示。

---

## Architecture / 架构

- **Diagnosis-first**: each diagnosis is the primary node; treatments hang off it, gated by clinical answers
- **`scope` field** on each Dx: `per_tooth` / `per_quadrant` / `per_mouth`
- **Adjunct protocols** for cross-cutting concurrent care (anticoagulant, immunosuppression, diabetes)
- **Concurrent dx hints**: when one Dx is selected, suggest other Dxs commonly co-occurring on the same tooth
- **FDI auto-derivation**: selecting an FDI tooth fills `tooth_type` / `tooth_position` / `quadrant` automatically; canal count remains a clinician-observed input (NOT pre-filled from population averages, to avoid automation complacency)

以诊断为一级节点，治疗作为受门控筛选的子节点；通过 `scope` 字段区分单颗牙/单象限/全口；引入辅助方案作为跨诊断的并行管理；并发诊断提示协助同时记录相关诊断；FDI 自动派生牙位属性但根管数仅由医生术中观察填入。

---

## Data sources / 数据来源

See `ATTRIBUTIONS.md` for full citations. Key sources:

- **NHSA billing items** (`立项指南`): 国家医保局《口腔类医疗服务价格项目立项指南（试行）》2025-03-03 + 《口腔种植类...》2024-11-18
- **Diagnostic criteria**: AAE (American Association of Endodontists), Cohen's Pathways of the Pulp 12th ed., EFP S3 periodontal guidelines, Tonetti 2018 staging
- **Mucosal/oncology safety**: WHO OPMD consensus, NHS NICE 2-week-wait pathway, MASCC/ISOO mucositis
- **Chinese ICD-10 master table**: 651-row K00-K14 catalogue (not yet aligned in v2 — see known debt)

完整引用见 `ATTRIBUTIONS.md`。

---

## Known limitations / 已知缺口

| 项 | 状态 |
|---|---|
| 牙外伤 (S02/S03 + IADT 2020) | 未建模 |
| TMJ/TMD (M26.6) | 未建模 |
| 正畸/错合畸形 (K07.x, 23 NHSA items unmapped) | 未建模 |
| 种植 (15 NHSA items unmapped) | 未建模 |
| K00 / K03 / K09 / K11 / K14 全部章节 | 未建模 |
| References URL/DOI verification | ✓ 全部 28 个 已核实 (2026-05-27) |
| NHSA OCR 低置信度项目 | 口腔类-36, -91, -93 待原文复核 |
| 中国 ICD-10 编码对齐 | 当前用 WHO 5位格式，未对齐中国 6位+x 扩展 |
| 省级价格 | 国家立项指南不含价格，待省级 |
| 临床医师签字 | **未完成 (P1 blocker)** |

---

## License / 许可证

MIT License — see `LICENSE`. You may use, copy, modify, and redistribute this code, with attribution.

MIT 许可证 — 详见 `LICENSE`。允许使用、复制、修改和再发布，需保留版权声明。

**Note**: NHSA 立项指南 data is reproduced from public government publications. AAE / Cohen's / WHO citations are bibliographic references, not redistributed content.

---

## Repository structure / 仓库结构

```
/
├── index.html           # The single-file interactive demo (open this)
├── README.md            # This file
├── LICENSE              # MIT
├── ATTRIBUTIONS.md      # Full citation list
├── DEPLOY.md            # GitHub Pages / Netlify deployment guide
├── .nojekyll            # Disables Jekyll on GitHub Pages
└── data/                # Optional: raw TSV exports of the knowledge base
    ├── diagnoses.tsv
    ├── treatments.tsv
    ├── symptom_differential.tsv
    ├── red_flags_v2.tsv
    ├── adjunct_protocols.tsv
    ├── concurrent_dx_hints.tsv
    ├── tooth_properties.tsv
    ├── billing_nhsa.tsv
    ├── treatment_billing_map.tsv
    └── references.tsv
```

---

## Feedback / 反馈

This is a research-preview pilot. Feedback from clinicians, billing specialists, and developers is welcome — please open a GitHub Issue or contact the maintainer.

本项目为研究预览试点。欢迎临床医师、医保编码专家、开发者的反馈——请在 GitHub Issues 提交，或联系维护者。
