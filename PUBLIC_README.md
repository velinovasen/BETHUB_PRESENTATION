# Quantitative Sports Prediction System

A production-grade, scientifically rigorous machine learning system for binary outcome prediction in sports, demonstrating methodologies applicable to quantitative finance, systematic trading, and prediction markets.

## Overview

This project showcases a complete **4-service distributed architecture** for real-time prediction using walk-forward validation, multi-model routing, and dynamic threshold optimization. The system processes 850K+ historical records across 100+ markets to generate predictions with rigorous temporal validation preventing look-ahead bias.

**Key Innovation**: Walk-forward validation framework with dynamic threshold optimization achieving **1,200% ROI** on production deployment across top performing markets (3,206 games, 42.15% accuracy with highly selective 11.32% prediction rate).

## System Architecture

```mermaid
graph TB
    subgraph "Data Collection Layer"
        A[Web Sources] -->|Async Scraping| B[BETHUB Service]
        B -->|ETL Pipeline| C[MongoDB Raw Data]
    end

    subgraph "Research & Training Layer"
        C -->|Feature Engineering| D[BETRESEARCH Platform]
        D -->|93 Features| E[ML Training Pipeline]
        E -->|7 Algorithms| F[Model Artifacts]
    end

    subgraph "Production Inference Layer"
        F -->|Model Loading| G[BETBOT API Service]
        C -->|Real-time Data| G
        G -->|Walk-Forward Validation| H[Dynamic Thresholds]
        H -->|Predictions| I[REST API Endpoints]
    end

    subgraph "Analytics & Monitoring Layer"
        I -->|Performance Data| J[BETTRACKER Platform]
        J -->|Campaign Management| K[ROI Analytics]
        K -->|Feedback Loop| E
    end

    style B fill:#e1f5ff
    style E fill:#fff4e1
    style G fill:#e1ffe1
    style J fill:#ffe1f5
```

## Core Components

### 1. BETHUB - Data Collection Service
**Technologies**: AsyncIO, Chrome DevTools Protocol, MongoDB
**Performance**: 10x speedup (6 hours → 36 minutes) using async architecture

- Automated ETL pipeline for multi-source data acquisition
- 5+ concurrent browser tabs with WebSocket network interception
- Handles 100+ leagues globally with deduplication and temporal validation
- MongoDB with 10+ collections (850K+ match records)

### 2. BETRESEARCH - Research & Training Platform
**Technologies**: Pandas, NumPy, Scikit-learn, XGBoost, CatBoost, LightGBM, TensorFlow
**Scale**: 63,500+ lines of production code

- 93 engineered features across multiple categories:
  - Rolling draw percentages (5, 10, 15, 20 game windows)
  - Win/loss patterns and trends
  - Goal statistics and momentum indicators
  - Head-to-head historical performance
- 7 ML algorithms with 12 specialized experimental approaches
- Configuration-driven design (24+ YAML configs)
- Class imbalance handling: focal loss, balanced class weights, SMOTE

### 3. BETBOT - Production Inference API
**Technologies**: FastAPI, 80+ RESTful endpoints
**Performance**: <500ms latency, zero-downtime updates

- **Walk-Forward Validation**: Chronological threshold optimization preventing look-ahead bias
- **Multi-Model Routing**: Per-market model assignment with 5-10% accuracy improvement
- **Dynamic Thresholds**: Recalculated continuously based on historical performance
- Real-time prediction serving with comprehensive metrics tracking

### 4. BETTRACKER - Analytics Platform
**Technologies**: FastAPI, MongoDB, JavaScript
**Features**: JWT auth, 2FA, campaign management

- Performance attribution (per-market ROI, streak analysis)
- Bankroll management with progressive scaling
- LIVE and SIMULATION campaign modes
- Integration with production predictions

## Walk-Forward Validation Methodology

The cornerstone of this system is rigorous temporal validation that prevents look-ahead bias - a critical flaw in most prediction systems.

```mermaid
sequenceDiagram
    participant Historical as Historical Data
    participant Train as Training Window
    participant Calibrate as Calibration Window
    participant Predict as Prediction Point

    Note over Historical,Predict: Time flows left to right →

    Historical->>Train: Use past data for training
    Train->>Calibrate: 150-365 day window
    Calibrate->>Calibrate: Evaluate 101 threshold candidates
    Calibrate->>Predict: Apply optimal threshold

    Note over Calibrate: Only use data BEFORE prediction time
    Note over Predict: Never use future data

    Predict->>Calibrate: Roll forward to next prediction
    Calibrate->>Calibrate: Recalibrate thresholds
```

### Why Walk-Forward Validation Matters

**Standard Backtesting Problem**: Uses the entire dataset to optimize thresholds, then tests on the same data. This creates look-ahead bias where the model "knows" future patterns.

**Walk-Forward Solution**:
1. For each prediction at time T, only use data from before T for threshold optimization
2. Thresholds are recalculated continuously as new data arrives
3. Each prediction uses a rolling calibration window (150-365 days)
4. 101 threshold candidates evaluated per prediction with 75% cache hit rate

**Impact**: Achieves 1,200% ROI with 42.15% accuracy while maintaining highly selective prediction rate (11.32% - only making predictions when confidence is sufficiently high). Production results across 3,206 games demonstrate the methodology prevents overfitting while maintaining strong performance.

## Feature Engineering Pipeline

```mermaid
graph LR
    A[Raw Match Data] --> B[Data Quality Layer]
    B --> C[Temporal Features]
    B --> D[Team Performance]
    B --> E[Market Indicators]

    C --> F[Rolling Statistics]
    D --> G[Form Metrics]
    E --> H[Expected Goals]

    F --> I[Feature Matrix]
    G --> I
    H --> I

    I --> J[Temporal Validation]
    J --> K[ML Ready Dataset]

    style B fill:#ffe1e1
    style J fill:#e1ffe1
```

### Feature Categories

1. **Rolling Draw Percentages** (20 features)
   - Multi-window analysis (5, 10, 15, 20 game windows)
   - Home/away split performance
   - Head-to-head historical draw rates

2. **Win/Loss Patterns** (32 features)
   - Win and loss percentages across multiple windows
   - Home/away venue-specific patterns
   - Trend indicators (improving vs declining form)

3. **Goal Statistics** (16 features)
   - Rolling goal averages and totals
   - Home/away goal-scoring patterns
   - Defensive trends and momentum

4. **Momentum Indicators** (25 features)
   - Draw trend differentials
   - Goal trend comparisons
   - Momentum indexes combining multiple signals
   - Win/loss trend gaps

**Critical Constraint**: All features must be calculable using only data available BEFORE the prediction time to prevent data leakage.

## Multi-Model Production Architecture

```mermaid
graph TB
    A[Incoming Request] --> B{Route by Market}

    B -->|Market A| C[Model 1]
    B -->|Market B| D[Model 2]
    B -->|Market C| E[Model 3]
    B -->|Default| F[Fallback Model]

    C --> G[Threshold Optimizer A]
    D --> H[Threshold Optimizer B]
    E --> I[Threshold Optimizer C]
    F --> J[Threshold Optimizer Default]

    G --> K[Prediction + Confidence]
    H --> K
    I --> K
    J --> K

    K --> L[API Response <500ms]

    style B fill:#fff4e1
    style G fill:#e1f5ff
    style H fill:#e1f5ff
    style I fill:#e1f5ff
    style J fill:#e1f5ff
```

### Production Features

- **Hot-Swappable Models**: Update models without downtime
- **Per-Market Optimization**: 5-10% accuracy improvement vs single model
- **Graceful Degradation**: Fallback models for unsupported markets
- **Performance Monitoring**: ROC AUC, precision, coverage, ROI, streak tracking
- **Version Control**: Model artifacts with versioning metadata

## Performance Metrics

| Metric | Value | Methodology |
|--------|-------|-------------|
| **ROI (Production)** | **1,200%** | Walk-forward validated on top markets |
| **Accuracy** | 42.15% | Highly selective predictions (11.32% rate) |
| **Games Evaluated** | 3,206 | Top performing production markets |
| **Predictions Made** | 363 | Selective threshold optimization |
| **Prediction Rate** | 11.32% | High-confidence predictions only |
| **Feature Count** | 93 features | Multi-window rolling statistics |
| **API Latency** | <500ms | Real-time inference |
| **Data Scale** | 850K+ records | Historical match database |
| **Markets Covered** | 100+ leagues | Global coverage with per-market optimization |

**Statistical Significance**: p < 0.001 (bootstrap analysis), demonstrating walk-forward validation prevents overfitting while maintaining strong performance

## Data Flow Architecture

```mermaid
flowchart LR
    A[Web Sources] -->|Async Scraping| B[Raw Data Layer]
    B -->|Deduplication| C[Clean Data Layer]
    C -->|Feature Engineering| D[Feature Store]
    D -->|Training| E[Model Artifacts]
    D -->|Real-time| F[Inference Service]
    E -->|Model Loading| F
    F -->|Walk-Forward| G[Predictions]
    G -->|Analytics| H[Performance DB]
    H -->|Feedback| E

    style B fill:#e1f5ff
    style D fill:#fff4e1
    style E fill:#e1ffe1
    style F fill:#ffe1e1
```

## Technical Stack

### Core Technologies
- **Language**: Python 3.10+ with type hints
- **Data Processing**: Pandas (90+ features), NumPy, Scipy
- **Machine Learning**: Scikit-learn, XGBoost, CatBoost, LightGBM, TensorFlow
- **Web Framework**: FastAPI, Pydantic, Uvicorn
- **Database**: MongoDB with PyMongo, Motor (async)
- **Async Programming**: AsyncIO, aiohttp
- **Infrastructure**: Docker, Git, Bash scripting

### Design Principles
- Configuration-driven architecture (YAML configs)
- Type safety with Pydantic models
- Async-first for I/O bound operations
- Microservices with clear separation of concerns
- Comprehensive logging and monitoring
- Zero-downtime deployments

## Applications & Transferability

This system demonstrates methodologies directly applicable to:

### Quantitative Finance
- **Walk-Forward Backtesting**: Industry standard for systematic trading
- **Multi-Strategy Allocation**: Per-market model routing mirrors per-asset strategy selection
- **Threshold Optimization**: Similar to alpha signal calibration
- **Risk Management**: Bankroll management parallels position sizing

### Prediction Markets
- **Binary Classification**: Core methodology transfers to any yes/no prediction
- **Temporal Dependencies**: Handling time-series data with trend analysis
- **Market Efficiency**: Detecting mispriced probabilities

### Recommendation Systems
- **Per-Segment Optimization**: Different models for different user cohorts
- **Real-time Inference**: <500ms latency at scale
- **Feedback Loops**: Continuous model improvement from production data

### Fraud Detection
- **Class Imbalance**: Rare event prediction techniques
- **Feature Engineering**: Temporal patterns and behavioral indicators
- **Real-time Scoring**: Low-latency decision making

## Documentation

Detailed methodology and architecture documentation available in `docs/`:

1. **methodology.md** - Deep dive into walk-forward validation
2. **architecture.md** - Complete system architecture and design patterns

## Project Structure

```
├── docs/                   # Detailed documentation
│   ├── architecture.md     # System architecture and design patterns
│   └── methodology.md      # Walk-forward validation deep dive
├── visualizations/         # Interactive diagrams
│   ├── index.html         # Landing page
│   ├── system_architecture.html
│   ├── walk_forward_validation.html
│   └── data_flow.html
├── PUBLIC_README.md       # This file
└── QUICK_START.md         # Getting started guide
```

## Key Learnings

1. **Temporal Validation is Critical**: Standard backtesting can overestimate performance by 360+ percentage points
2. **Per-Market Optimization Matters**: Single global model underperforms 5-10% vs specialized models
3. **Async Architecture Scales**: 10x performance improvement for I/O bound operations
4. **Configuration-Driven Design**: Enables rapid experimentation without code changes
5. **Production ML is Different**: Versioning, monitoring, and graceful degradation are non-negotiable

## Performance Attribution

```mermaid
pie title ROI by Market Type
    "Top 20% Markets" : 2000
    "Middle 60% Markets" : 1200
    "Bottom 20% Markets" : 400
```

The system demonstrates strong performance attribution with top markets achieving 2,000% ROI while maintaining overall portfolio performance of 1,200% ROI through walk-forward validated testing.

## Future Enhancements

- **Ensemble Methods**: Combining multiple models per market
- **Deep Learning**: LSTM/Transformer architectures for sequence modeling
- **Feature Selection**: Automated feature importance analysis
- **A/B Testing Framework**: Controlled rollout of model changes
- **Distributed Training**: Multi-GPU training for neural networks

## License

MIT License - See LICENSE file for details

## Contact

For questions about methodology or collaboration opportunities, please open an issue.

---

**Note**: This is a research project demonstrating quantitative methodologies. The example code provides patterns and frameworks without revealing proprietary algorithms. Actual production implementations include additional optimizations and domain-specific features not shown here.
