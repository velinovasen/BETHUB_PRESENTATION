# Architecture Visualizations

Interactive Mermaid.js diagrams documenting the complete BETUP_SCIENTIFIC system architecture.

## 🚀 Quick Start

**Open the visualization portal:**
```bash
open index.html
```

Or simply double-click `index.html` in your file browser.

---

## 📊 Available Visualizations

### Overview Pages

| Page | File | Diagrams | Description |
|------|------|----------|-------------|
| **Landing Page** | `index.html` | Navigation | Central hub linking to all visualizations |
| **System Architecture** | `system_architecture.html` | 5 diagrams | Complete 4-service architecture overview |
| **Walk-Forward Validation** | `walk_forward_validation.html` | 3 diagrams | Core methodology preventing look-ahead bias |
| **Data Flow** | `data_flow.html` | 7 diagrams | End-to-end prediction and training pipelines |

### Service-Specific Pages

| Service | File | Diagrams | Focus |
|---------|------|----------|-------|
| **BETHUB** | `bethub_architecture.html` | 6 diagrams | Async data collection (10x speedup) |
| **BETRESEARCH** | `betresearch_architecture.html` | 15 diagrams | 93-feature engineering & model training |
| **BETBOT** | `betbot_architecture.html` | 12 diagrams | Production API (<500ms latency) |
| **BETTRACKER** | `bettracker_architecture.html` | 15 diagrams | Analytics & campaign management |

---

## 🎯 What You'll Learn

### BETHUB - Data Collection Service
- Docker containerization with Chrome browser automation
- Async scraping with 5 concurrent tabs
- Chrome DevTools Protocol for JSON interception
- 10x performance improvement (6h → 36min)

### BETRESEARCH - Training Platform
- 93-feature engineering pipeline
- 7 ML algorithms (XGBoost, CatBoost, LightGBM, TensorFlow)
- Data quality validation layer
- Hyperparameter tuning workflows
- Class imbalance handling strategies

### BETBOT - API Service
- Multi-model routing architecture
- Walk-forward threshold optimization
- 80+ RESTful endpoints
- Caching strategies (75% hit rate)
- Hot-swap model updates (zero downtime)

### BETTRACKER - Analytics Platform
- JWT + 2FA authentication
- Real-time WebSocket updates
- ROI calculation and streak detection
- Per-market attribution
- Feedback loops to training

---

## 💡 Viewing Tips

### Best Practices
1. **Use a modern browser** - Chrome, Firefox, Safari, or Edge
2. **Full screen mode** - Press `F11` for immersive viewing
3. **Follow the navigation** - Start with `index.html` and explore systematically
4. **Print to PDF** - Use browser print function to save diagrams

### Navigation
- Each page has a **navigation bar** at the top linking to all services
- Click **← Home** to return to the landing page
- Diagrams are **interactive** - some support zooming and panning

### GitHub Viewing
While these diagrams will render on GitHub, the HTML versions provide:
- ✅ Better styling and formatting
- ✅ Faster loading (no GitHub API calls)
- ✅ Enhanced interactivity
- ✅ Professional presentation

---

## 🛠️ Technical Details

### Technologies Used
- **Mermaid.js** - Diagram rendering engine
- **HTML5 + CSS3** - Modern web standards
- **Responsive Design** - Works on all screen sizes
- **Zero Dependencies** - Self-contained HTML files

### File Structure
```
visualizations/
├── index.html                      # Landing page
├── system_architecture.html        # Overview diagrams
├── walk_forward_validation.html    # Methodology
├── data_flow.html                  # Pipelines
├── bethub_architecture.html        # Service 1
├── betresearch_architecture.html   # Service 2
├── betbot_architecture.html        # Service 3
├── bettracker_architecture.html    # Service 4
├── footer.html                     # Shared footer
└── README.md                       # This file
```

---

## 🎨 Customization

All visualizations use consistent styling:
- **Colors**: Service-specific color coding (BETHUB=blue, BETRESEARCH=orange, etc.)
- **Typography**: System fonts for native OS appearance
- **Layout**: Responsive cards with hover effects
- **Copyright**: Fixed footer on all pages

To customize, edit the `<style>` sections in each HTML file.

---

## 📄 License

© 2026 BETUP_SCIENTIFIC. All Rights Reserved.

These visualizations are proprietary and confidential. See [LICENSE](../LICENSE) for usage terms.

---

## 🤝 Feedback

Found an issue or have suggestions? Open an issue in the main repository.

---

**Last Updated:** March 18, 2026
**Total Diagrams:** 58+ across 7 pages
**Total HTML Files:** 8 files
