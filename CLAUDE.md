# Moral Evolution Paper — Camera-Ready Revision

## Repository Structure

- `main` branch: Original ACL ARR 2026 January submission version (GPT-4.1-mini, single-run)
- `camera-ready` branch: Camera-ready revision addressing reviewer feedback

The paper directory is `acl-style-files-master/`. The `arxiv_version/` directory contains an older AAAI submission and is not being updated.

## What Changed (main → camera-ready)

### Driven by Reviewer Feedback

All changes have explicit rationale from reviewer comments or Gemini cross-review.

#### New Experiments Added (from rebuttal data)
- **Cross-model robustness table** (Table 2): GPT-5-mini, Qwen-3.5, Kimi-K2.5 × 8 runs each. Shows consistent kin-focused dominance and CM diagonal accuracy 0.86–0.89 across models.
- **Architecture ablation + prompt sensitivity table** (Table 3): Removing memory (-0.11), plan (-0.07), reflection (-0.05), or all modules/ReAct (-0.22). Prompt rewrites show ≤0.03 variation.
- **Updated confusion matrix figure** (Fig 3b): Replaced single-run CM with multi-run averaged version (mean ± std per cell).

#### Mechanism Clarifications (Reviewer 7C8u)
- **Heritability**: Offspring inherit parental moral type deterministically, no mutation (framework.tex)
- **Kinship recognition**: Environment explicitly provides parent/child identities (framework.tex)
- **Social interaction cost**: Defined as number of coordination rounds per step (framework.tex)

#### Conceptual Clarifications (Reviewer ZiGG)
- **Emergence scope**: Clarified that "emergence" refers to population-level dynamics, not individual agent invention of new rules (agent_architecture.tex)
- **"Independent evaluator"** → "separate, more capable model" — more precise language since GPT-5 and GPT-5-mini share training methodology

#### Writing Fixes
- Grammar: "risks being exploited, wins" → "while risking exploitation, gain"
- Grammar: "for avoiding" → "by avoiding"
- Typo: "collborate" → "collaborate" (prompts.tex, flagged by Reviewer ZiGG)
- LaTeX: `\ref {fig}` → `\ref{fig}` (space removal)
- Mode: `\usepackage[preprint]{acl}` → `\usepackage[final]{acl}`

#### Abstract & Introduction
- Abstract: Added sentence about cross-model validation, ablations, and prompt sensitivity
- Introduction contribution 3: Added robustness validation claim

#### Appendix Additions
- Per-model detailed confusion matrices (GPT-5-mini, Qwen-3.5, Kimi-K2.5)
- Population scaling experiment (8 vs 16 agents)
- API cost breakdown (GPT-5-mini pricing)
- Discussion: Why Expanding Circle Theory over MFT/Dyadic Morality/MAC

### Model Name Change
Original submission used GPT-4.1-mini. All rebuttal experiments used GPT-5-mini (with Qwen-3.5 and Kimi-K2.5 for cross-model). Camera-ready version uses GPT-5-mini as primary model throughout. GPT-4.1-mini is not mentioned.

## What Is NOT Yet Done (Pending)

### Figures That Need Updating
The following figures still show OLD data from GPT-4.1-mini single runs, but the text now describes GPT-5-mini results:

1. **Fig 2 (population plots)**: Three population-over-time plots (baseline, high social cost, invisible moral type). These need to be regenerated from GPT-5-mini simulation logs.
2. **Fig 3a (HP trajectories)**: Agent HP curves with action markers. Needs GPT-5-mini run data.

**Why not done yet**: These figures require actual simulation output data (population logs, agent HP trajectories) from GPT-5-mini runs. The data files are not in this repository — they need to be located or regenerated from the simulation codebase.

### Figures That Do NOT Need Updating
- **Fig 3b (confusion matrix)**: ✅ Already updated to multi-run averaged version
- **Fig 4 (mini-game heatmaps)**: No update needed (confirmed by author)
- **Fig 1 (framework overview)**: No change needed

## Build

```bash
cd acl-style-files-master
pdflatex acl_latex.tex
bibtex acl_latex
pdflatex acl_latex.tex
pdflatex acl_latex.tex
```

## Review Process Context

- Venue: ACL ARR 2026 January → ACL Findings
- Meta review: Score 3 (Findings), recommended adding robustness validation and open-source model results
- Three reviewers (u2Du: score 4, ZiGG: score 3, 7C8u: score 3)
- All reviewer concerns addressed in rebuttal; camera-ready integrates rebuttal experiments into paper
