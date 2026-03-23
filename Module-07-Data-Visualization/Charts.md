# Visualization & Presentation Notes

## Table of Contents
- [Reveal.js](#revealjs)
- [Marp (Markdown Presentations)](#marp-markdown-presentations)
- [Marimo (Reactive Python Notebooks)](#marimo-reactive-python-notebooks)
- [Excel Data Analysis](#excel-data-analysis)
- [RAWGraphs](#rawgraphs)
- [Seaborn Guide](#seaborn-guide)
- [PowerPoint Animation (Bar Chart Race)](#powerpoint-animation-bar-chart-race)
- [Network Visualization](#network-visualization)
- [AI Data Visualization Workflow](#ai-data-visualization-workflow)

---

## Reveal.js

Reveal.js is a JavaScript framework to create interactive HTML presentations using Markdown or HTML.

### Uses
- Data presentations (charts, dashboards)
- Technical talks (code highlighting)
- Portfolios and demos
- Educational slides
- Documentation

### Setup
`bash
git clone https://github.com/hakimel/reveal.js.git
cd reveal.js

## Open
http://localhost:8000

---

## Basics
- --- → New slide (Markdown)
- <section> → Slide (HTML)

### Example
`md
# Slide 1
- Hello

---
## Slide 2

npm install
npm start

## Features
- Keyboard navigation
- Code highlighting
- Nested slides
- Animations and media support
- PDF export

---

## Marp (Markdown Presentations)

### Setup
- Install Marp VS Code Extension

Add this at the top:
``md
---
marp: true
---

## Features
- Markdown-based slides
- Fragmented lists (*)
- Code blocks with syntax highlighting
- Math support (KaTeX/MathJax)
- Themes: default, gaia, uncover

### Styling
- Dark mode → class: invert
- Custom HTML supported
- Slide-specific styling

### Export
- HTML (recommended)
- PDF (limited features)
- PPT (static slides)

---

## Marimo (Reactive Python Notebooks)

### Core Idea
- Reactive execution (similar to Excel)
- No hidden state
- Based on DAG (data flow)

### Features
- Auto-updating cells
- Python-based markdown (mo.md())
- Built-in UI (sliders, inputs)
- Interactive charts

### Benefits
- Saved as .py (Git-friendly)

Run as script:
``bash
python notebook.py

## RAWGraphs

### Chart Types
- Flow: Sankey, Alluvial
- Hierarchy: Treemap, Sunburst
- Distribution: Beeswarm
- Trends: Streamgraph
- Spatial: Hexbin, Voronoi

### Workflow
1. Load data  
2. Choose chart  
3. Map fields  
4. Customize  
5. Export (SVG/PNG)

---

## Seaborn Guide

### Setup
``python
import seaborn as sns
sns.set_style('whitegrid')


## Plots
- Distribution → displot, jointplot
- Categorical → barplot, boxplot, violinplot
- Matrix → heatmap, clustermap
- Regression → lmplot

---

## PowerPoint Animation (Bar Chart Race)

### Steps
1. Create bars using shapes  
2. Set exact width (scaled values)  
3. Rename shapes (use clear names)  
4. Duplicate slides and adjust values  
5. Apply Morph transition  

### Extras
- Add voiceover  
- Add background music  
- Export as video  

---

## Network Visualization

### Process
1. Filter IMDb datasets (actors, movies)  
2. Create matrix (Movies × Actors)  
3. Compute co-occurrence (Aᵀ × A)  
4. Remove self-loops  
5. Export processed data  

### Tool
- Upload data to Kumu for visualization  

---

## AI Data Visualization Workflow

### Steps
1. Find dataset (Kaggle, etc.)  
2. Generate ideas using LLM  
3. Analyze using code interpreter  
4. Build visualization (HTML/JS)  
5. Deploy (GitHub Pages)  

### Debugging
- Use browser DevTools (F12)  
- Copy errors and analyze  
- Use LLMs for debugging help  

### Key Ideas
- Avoid manual repetitive work  
- Use multiple outputs for exploration  
- Focus on context, not syntax  
- Validate results to avoid bias
