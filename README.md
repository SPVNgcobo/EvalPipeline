# EvalPipeline v2.0 README

## Overview
A modern, interactive evaluation dashboard for assessing AI model responses against structured quality criteria. Built with React, EvalPipeline provides comprehensive scoring, comparative analysis, and issue tracking for AI model evaluations.

## Key Features

### 📊 Dashboard
- Real-time metrics (pass rate, average score, flagged/failed counts)
- Model performance comparison with weighted scores
- Issue frequency heatmap across all evaluations
- Recent evaluations quick-view

### ✏️ Evaluate Tab
- **5 Weighted Criteria**:
  - Factual Accuracy (30%)
  - Relevance (25%)
  - Clarity & Coherence (20%)
  - Safety & Compliance (15%)
  - Instruction Following (10%)
- Issue tagging (Hallucination, Bias, Format Failure, Unsafe Content, Incomplete, Off-topic, Overconfident, Ambiguous)
- Real-time weighted score calculation
- Evaluator notes field

### 📋 Eval Log Tab
- Searchable, filterable evaluation history
- Multi-criteria filtering (verdict, model, search query)
- Checkbox selection for side-by-side comparison
- Sortable data table

### 🔄 Compare Tab
- Side-by-side evaluation analysis
- SVG radar charts for visual criterion comparison
- Detailed score breakdowns
- Issue comparison

## Technical Stack
- **React** 18+ with Hooks
- **CSS-in-JS** with inline styles
- **SVG Radar Charts** for visualization
- **Google Fonts** (DM Sans, DM Mono)

## Component Structure

### Core Utilities
```javascript
weightedScore(scores)        // Calculates weighted average
scoreColor(val)              // Maps score to color (#00e5a0, #f5c842, #ff4d6d)
verdictStyle(verdict)        // Returns color + label for Pass/Flag/Fail
```

### Visualization Components
- **RadarChart** — 5-dimensional score visualization with grid and polygon
- **ScoreBar** — Animated progress indicator with color coding
- **StatCard** — Metric display with label and value

### State Variables
| Variable | Purpose |
|----------|---------|
| `tab` | Current active tab |
| `evals` | Array of evaluation records |
| `selected` | Expanded evaluation detail |
| `newEval` | Form state for new evaluation |
| `compareIds` | IDs of 2 selected evaluations |
| `filterVerdict` / `filterModel` | Log filtering |
| `searchQ` | Search query |

## Score Interpretation

| Score | Status | Meaning |
|-------|--------|---------|
| 4.2-5.0 | **Pass** (Green) | Excellent, meets criterion fully |
| 3.0-4.2 | **Flag** (Yellow) | Acceptable but needs review |
| <3.0 | **Fail** (Red) | Poor, significant issues |

### Weighted Score Formula
```
Final = (Accuracy × 0.3) + (Relevance × 0.25) + (Clarity × 0.2) 
        + (Safety × 0.15) + (Instruction × 0.1)
```

## Theme & Design

**Color Palette**:
- Background: `#0b0d11` (dark)
- Accent: `#00e5a0` (teal)
- Warning: `#f5c842` (yellow)
- Error: `#ff4d6d` (red)
- Text: `#e8eaf0` (light gray)

**Fonts**:
- UI: DM Sans (300-700)
- Data: DM Mono (400-500)

## Sample Data

4 pre-loaded evaluations demonstrate:
1. **GPT-4o** — Quantum entanglement (PASS, all criteria 4-5)
2. **Gemini 1.5 Pro** — Nobel Prize list (FLAG, hallucination detected)
3. **Claude 3.5 Sonnet** — Cover letter (PASS, high quality)
4. **Llama 3.1 70B** — Lock picking (FAIL, safety violation)

## Customization Guide

### Modify Criteria
```javascript
const CRITERIA = [
  { id: "accuracy", label: "Factual Accuracy", weight: 0.3, icon: "◈" },
  // Edit weight values (sum = 1.0)
];
```

### Add Issue Tags
```javascript
const ISSUE_TAGS = [
  "Hallucination", "Bias", /* custom tags */
];
```

### Change Color Scheme
Update in `scoreColor()` function and inline styles:
- Green: `#00e5a0`
- Yellow: `#f5c842`
- Red: `#ff4d6d`

### Add Models
```javascript
const MODELS = ["GPT-4o", "Claude 3.5 Sonnet", /* new models */];
```

## Usage Workflow

### Creating an Evaluation
1. Go to **Evaluate** tab
2. Select model and verdict
3. Enter prompt and response
4. Score each criterion (1-5 sliders)
5. Flag any issues (toggle tags)
6. Submit → automatically logged with timestamp

### Comparing Two Evaluations
1. Go to **Eval Log** tab
2. Check "Select" on 2 evaluations
3. Click "Compare Selected →"
4. View side-by-side radar charts and scores

## Future Enhancements

- [ ] CSV/JSON export
- [ ] Multi-user collaboration
- [ ] Batch import
- [ ] Trend analysis & reports
- [ ] Custom evaluation templates
- [ ] Backend sync
- [ ] Date range filtering
- [ ] Automated issue detection

## Browser Support

- Chrome/Edge 90+
- Firefox 88+
- Safari 14+
- Requires ES6+ and CSS Grid

---

**Version**: 2.0 | **Created by**: S.Ngcobo | **Last Updated**: May 2026
