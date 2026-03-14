# 🔍 skill-mining

> **A Qoder Skill that automatically mines AI-buildable opportunities from process documents.**

[![Live Demo](https://img.shields.io/badge/Live%20Demo-GitHub%20Pages-667eea?style=flat-square&logo=github)](https://james19890801.github.io/skill-mining/)
[![Skill Type](https://img.shields.io/badge/Type-Qoder%20Skill-764ba2?style=flat-square)](https://github.com/James19890801/skill-mining)
[![Language](https://img.shields.io/badge/Language-Python%203-blue?style=flat-square&logo=python)](scripts/)

---

## What It Does

Most organizations have process documents — flowcharts, SOPs, approval workflows — but no clear way to identify **which parts can be turned into reusable AI Skills**.

`skill-mining` solves this. Drop in a process file (Word, PDF, image, or plain text), and it will:

1. **Parse** the document and extract all process nodes
2. **Score** each node on AI feasibility (repetition, clarity, online-executability)
3. **Generate** a visual HTML report with ranked Skill opportunities
4. **Open** the report in your browser automatically
5. **Package** your chosen node into a ready-to-use Qoder Skill file

---

## Live Demo

👉 **[View Sample Report →](https://james19890801.github.io/skill-mining/)**

The demo shows a full analysis of a procurement approval process — 8 nodes scanned, 3 high-priority Skill opportunities identified, scored and ranked.

---

## How to Trigger

Say any of the following inside Qoder:

```
帮我挖掘 skill
这个流程哪里可以做 skill
skill 挖掘
从流程中找 skill 机会
流程里有哪些 skill 可以做
```

---

## Workflow

```
Input (file / text / description)
        ↓
  [parse_doc.py]  ← supports .docx / .pdf / .png / .jpg / .txt
        ↓
   AI Analysis   ← scores each node on 4 dimensions
        ↓
[generate_report.py] ← outputs HTML to D:\, auto-opens browser
        ↓
  Conversation   ← shows Top 3, asks which to build
        ↓
 [build_skill.py] ← packages selected node into SKILL.md
        ↓
  Installed to ~/.qoder/skills/
```

---

## Scoring Model

Each process node is scored out of **100** across four dimensions:

| Dimension | Weight | Description |
|-----------|--------|-------------|
| Repetition Frequency | 30% | How often this task recurs |
| AI Executability | 30% | How fully AI can complete it online |
| Value Release | 25% | Time/quality improvement potential |
| Implementation Difficulty (inverse) | 15% | Lower complexity = higher score |

**Score bands:**
- 🟢 **80–100** — Build now
- 🟡 **60–79** — Needs more context
- 🟠 **40–59** — Pair with other methods
- 🔴 **< 40** — Not ready yet

---

## File Structure

```
skill-mining/
├── SKILL.md                   # Main Qoder Skill instruction file
├── index.html                 # Live demo page (GitHub Pages)
└── scripts/
    ├── parse_doc.py           # Parses Word / PDF / image files
    ├── generate_report.py     # Generates & auto-opens HTML report
    └── build_skill.py         # Packages a node into a Skill file
```

---

## Scripts

### `parse_doc.py`
Extracts plain text from `.docx`, `.pdf`, `.png`, `.jpg`, `.txt`, `.md` files.

```bash
python scripts/parse_doc.py "path/to/process_file.pdf"
```

Dependencies: `pip install python-docx pymupdf pillow pytesseract`

---

### `generate_report.py`
Generates a full visual HTML report from a JSON analysis result.
With no arguments, runs with built-in sample data.

```bash
python scripts/generate_report.py               # demo mode
python scripts/generate_report.py report.json   # custom data
```

Output: `D:\skill_mining_report_YYYYMMDD_HHMMSS.html` (auto-opened in browser)

---

### `build_skill.py`
Packages a process node into a complete Qoder `SKILL.md` file and installs it.

```bash
python scripts/build_skill.py skill_info.json
```

Input JSON format:
```json
{
  "skill_name": "Price Comparison",
  "skill_id": "price-comparison",
  "node_description": "Compare quotes from multiple vendors",
  "trigger_scenes": ["帮我比价", "analyze these quotes"],
  "input_format": "Multiple vendor quote files",
  "output_format": "Comparison matrix + recommendation",
  "key_steps": ["Parse each quote", "Extract key items", "Cross-compare", "Recommend"],
  "install_path": "personal"
}
```

---

## What Makes a Good Skill Candidate?

A process node is a strong Skill candidate if it meets **3 or more** of these:

- ✅ Has a clear Input → Process → Output structure
- ✅ Can be executed fully online without offline human steps
- ✅ Is highly repetitive with a consistent pattern
- ✅ Has a single, well-defined responsibility
- ✅ Can be significantly improved by AI in speed or quality
- ✅ Currently relies on manual effort, is time-consuming or error-prone

---

## Installation

This is a personal Qoder Skill. To install:

1. Clone or download this repo
2. Copy the `skill-mining/` folder to `~/.qoder/skills/`
3. Restart Qoder — the skill is ready

```bash
git clone https://github.com/James19890801/skill-mining.git
cp -r skill-mining ~/.qoder/skills/skill-mining
```

---

## Storage Locations

| Location | Path |
|----------|------|
| Qoder Runtime | `~/.qoder/skills/skill-mining/` |
| Course Materials | `D:\AI赋能流程管理课程\02-课程Skills\skill-mining\` |
| GitHub (this repo) | [James19890801/skill-mining](https://github.com/James19890801/skill-mining) |

---

## Author

**James19890801** · Built with [Qoder](https://qoder.ai)

> This skill was created as part of an AI-powered process management course to demonstrate how AI Skills can be systematically identified and built from real organizational workflows.
