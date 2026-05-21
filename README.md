# EvalPipeline v2.0

A modern, interactive evaluation dashboard for assessing AI model responses against structured quality criteria. Built with React, EvalPipeline provides comprehensive scoring, comparative analysis, and issue tracking for AI model evaluations.

## Features

### 📊 Dashboard
- **Real-time metrics**: Average weighted score, pass rate, flagged, and failed evaluations
- **Model performance tracking**: Compare average scores across different AI models
- **Issue taxonomy**: Visualize frequency of flagged issues across evaluations
- **Recent evaluations**: Quick overview of the latest 4 logged evaluations

### ✏️ Evaluate
- **Structured scoring**: Rate AI responses on 5 weighted criteria
  - **Factual Accuracy** (30% weight) — Correctness and truthfulness
  - **Relevance** (25% weight) — Alignment with the prompt
  - **Clarity & Coherence** (20% weight) — Readability and organization
  - **Safety & Compliance** (15% weight) — Ethical and safety standards
  - **Instruction Following** (10% weight) — Adherence to directives
- **Issue flagging**: Tag responses with predefined issue categories
  - Hallucination, Bias, Format Failure, Unsafe Content, Incomplete, Off-topic, Overconfident, Ambiguous
- **Weighted score calculation**: Automatic computation of overall quality score (0-5)
- **Evaluator notes**: Add context-specific observations

### 📋 Eval Log
- **Searchable database**: Filter by prompt/response content
- **Multi-filter interface**: Filter by verdict (Pass/Flag/Fail) and model
- **Selection for comparison**: Checkbox-based selection system for side-by-side analysis
- **Sortable columns**: View ID, prompt, model, score, verdict, and comparison status

### 🔄 Compare
- **Side-by-side analysis**: Visually compare 2 evaluations
- **Radar charts**: 5-point criteria visualization for intuitive comparison
- **Detailed breakdowns**: Score bars for each criterion with color-coded performance
- **Issue comparison**: See flagged issues for each evaluation at a glance

## Technical Stack

- **Framework**: React 18+
- **Styling**: CSS-in-JS (inline styles with custom theme)
- **Visualization**: SVG-based radar charts
- **Fonts**: DM Sans, DM Mono (Google Fonts)

## Project Structure

```
EvalPipeline/
├── README.md                 # Documentation
├── package.json             # Dependencies and scripts
├── .gitignore              # Git ignore rules
├── LICENSE                 # MIT License
└── src/
    └── components/
        └── EvalPipeline.jsx # Main component
```

## Component Architecture

### State Management
- `tab` — Current active tab (dashboard/evaluate/log/compare)
- `evals` — Array of evaluation records
- `selected` — Currently expanded evaluation for detail view
- `newEval` — Form data for new evaluation
- `submitted` — Submission confirmation state
- `filterVerdict` / `filterModel` — Log tab filters
- `searchQ` — Search query for log entries
- `compareIds` — IDs of selected evaluations for comparison

### Key Utilities

#### `weightedScore(scores)`
Calculates weighted average across all criteria based on predefined weights.

#### `scoreColor(val)`
Maps numerical scores to color codes:
- **Green** (#00e5a0): 4.2+ (excellent)
- **Yellow** (#f5c842): 3-4.2 (adequate)
- **Red** (#ff4d6d): <3 (poor)

#### `verdictStyle(v)`
Returns color and label for verdict states (PASS, FLAG, FAIL).

#### `RadarChart(scores)`
Renders an SVG radar chart visualization of 5-dimensional score data with:
- 4 concentric grid circles
- Score polygons and point markers
- Clean, minimal design

### Components

#### `StatCard`
Displays a single metric with label, value, and optional subtext.

#### `ScoreBar`
Animated progress bar with color-coded performance indicator.

#### `RadarChart`
SVG-based 5-criterion visualization with grid and polygon rendering.

## Theme & Design

- **Color Scheme**: Dark mode (#0b0d11 background)
- **Accent Color**: Teal/green (#00e5a0)
- **Secondary Colors**:
  - Yellow (#f5c842) for warnings
  - Red (#ff4d6d) for failures
- **Typography**: 
  - Primary: DM Sans (UI text)
  - Monospace: DM Mono (scores, IDs)
- **Spacing**: 8px base unit grid system
- **Borders**: Subtle white at 0.07 opacity
- **Transitions**: 0.15-0.5s ease for interactions

## Sample Data

The component includes 4 pre-loaded evaluations demonstrating:
1. **Passing response** — GPT-4o on quantum entanglement (all criteria excellent)
2. **Flagged response** — Gemini 1.5 Pro on Nobel Prize list (hallucination detected)
3. **Passing response** — Claude 3.5 Sonnet on cover letter (high quality)
4. **Failed response** — Llama 3.1 70B on lock picking (safety violation)

## Usage

### Installation

```bash
npm install
```

### Development Server

```bash
npm start
```

Runs on `http://localhost:3000`

### Build for Production

```bash
npm run build
```

### Import & Render

```jsx
import EvalPipeline from './components/EvalPipeline';

export default function App() {
  return <EvalPipeline />;
}
```

### Adding New Evaluations

1. Navigate to the **Evaluate** tab
2. Select a model
3. Enter the prompt and AI response
4. Score each criterion (1-5 scale)
5. Flag any issues if applicable
6. Set verdict (Pass/Flag/Fail)
7. Submit — evaluation is logged with timestamp and evaluator ID

### Comparing Evaluations

1. Go to **Eval Log** tab
2. Check the "Select" boxes for 2 evaluations
3. Click "Compare Selected →" button (appears when 2 are selected)
4. View side-by-side radar charts and criterion scores

## Evaluation Scoring Guide

| Score | Rating | Interpretation |
|-------|--------|----------------|
| 5 | Excellent | Fully meets criterion; exceptional quality |
| 4 | Good | Meets criterion; minor issues |
| 3 | Adequate | Marginally acceptable; noticeable gaps |
| 2 | Poor | Falls short; significant issues |
| 1 | Fail | Severe problems; criterion not met |

### Weighted Score Calculation

```
Final Score = (A×0.3) + (R×0.25) + (C×0.2) + (S×0.15) + (I×0.1)

Where:
A = Accuracy score
R = Relevance score
C = Clarity & Coherence score
S = Safety & Compliance score
I = Instruction Following score
```

## Customization

### Adjusting Criteria Weights
Edit the `CRITERIA` array in `EvalPipeline.jsx`:
```javascript
const CRITERIA = [
  { id: "accuracy", label: "Factual Accuracy", weight: 0.3, icon: "◈" },
  // Modify weight values (sum should equal 1.0)
];
```

### Adding Issue Tags
Expand the `ISSUE_TAGS` array:
```javascript
const ISSUE_TAGS = [
  "Hallucination", "Bias", // ... add custom tags
];
```

### Changing Color Scheme
Update the hex color values in `scoreColor()`, `TABS` button styling, and component inline styles:
- Success: `#00e5a0`
- Warning: `#f5c842`
- Error: `#ff4d6d`

### Adding Models
Add to `MODELS` array:
```javascript
const MODELS = ["GPT-4o", "Claude 3.5 Sonnet", /* new models */];
```

## Accessibility Features

- Semantic HTML structure
- Keyboard-navigable tabs and inputs
- Color-coded status indicators (supplemented with text labels)
- High contrast text on dark backgrounds
- Focus states on interactive elements
- Range sliders with visual feedback

## Performance Considerations

- Memoization candidates: `RadarChart`, `ScoreBar` components
- Filtering is computed on each render (optimize with `useMemo` for large datasets)
- SVG rendering is lightweight for small datasets
- Scrollbar styling optimized for minimal visual footprint

## Browser Support

- Chrome/Edge 90+
- Firefox 88+
- Safari 14+
- Requires ES6+ support and CSS Grid

## Future Enhancements

- [ ] Export evaluations to CSV/JSON
- [ ] Multi-user collaboration and evaluator leaderboards
- [ ] Batch evaluation import
- [ ] Historical trend analysis and reports
- [ ] Customizable evaluation templates
- [ ] Real-time sync with backend
- [ ] Advanced filtering (date ranges, evaluator, issue combinations)
- [ ] Model-specific evaluation profiles
- [ ] Automated issue detection via ML

## License

MIT License — See [LICENSE](LICENSE) for details.

## Support

For questions or issues, contact the evaluation team or review the inline component documentation.

---

**Version**: 2.0  
**Created by**: S.Ngcobo  
**Last Updated**: May 2026
