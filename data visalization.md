 ## File: data-visualization-for-ml-syllabus.md

# Data Visualization for ML

## A World-Class, University-Level, Industry-Grade Technical Syllabus & Engineering Learning Roadmap

---

## Table of Contents

1. [Course Overview & Philosophy](#1-course-overview--philosophy)
2. [Target Audience & Prerequisites](#2-target-audience--prerequisites)
3. [Learning Objectives & Outcomes](#3-learning-objectives--outcomes)
4. [Module 0: Mathematical & Computational Foundations](#module-0-mathematical--computational-foundations)
5. [Module 1: The Grammar of Graphics & Visualization Theory](#module-1-the-grammar-of-graphics--visualization-theory)
6. [Module 2: The Browser Rendering Pipeline for Visualization](#module-2-the-browser-rendering-pipeline-for-visualization)
7. [Module 3: D3.js — The Visualization Engine](#module-3-d3js--the-visualization-engine)
8. [Module 4: Observable Plot & Declarative Visualization](#module-4-observable-plot--declarative-visualization)
9. [Module 5: React Integration — Reconciling React with Imperative Visualization](#module-5-react-integration--reconciling-react-with-imperative-visualization)
10. [Module 6: Time-Series & Streaming Visualization](#module-6-time-series--streaming-visualization)
11. [Module 7: High-Dimensional Data Visualization](#module-7-high-dimensional-data-visualization)
12. [Module 8: Model Explainability & Interpretability Visualization](#module-8-model-explainability--interpretability-visualization)
13. [Module 9: Real-Time ML Monitoring Dashboards](#module-9-real-time-ml-monitoring-dashboards)
14. [Module 10: Interactive Data Exploration & Drill-Down](#module-10-interactive-data-exploration--drill-down)
15. [Module 11: Performance Engineering for Visualization](#module-11-performance-engineering-for-visualization)
16. [Module 12: Production Architecture & Embedded Analytics](#module-12-production-architecture--embedded-analytics)
17. [Module 13: Accessibility, Ethics & Design Systems](#module-13-accessibility-ethics--design-systems)
18. [Module 14: AI-Generated Visualization & Natural Language Interfaces](#module-14-ai-generated-visualization--natural-language-interfaces)
19. [Capstone Project](#capstone-project)
20. [Appendix A: Reading List & References](#appendix-a-reading-list--references)
21. [Appendix B: Tooling Matrix](#appendix-b-tooling-matrix)
22. [Appendix C: Interview Preparation](#appendix-c-interview-preparation)

---

## 1. Course Overview & Philosophy

Data visualization for ML is not about making pretty charts. It is a **systems engineering discipline** at the confluence of:

- **Applied Mathematics**: linear algebra, statistics, information theory, topology
- **Computer Graphics**: GPU rendering, canvas APIs, WebGL, shader programming
- **Systems Engineering**: streaming pipelines, real-time rendering, memory management
- **Human-Computer Interaction**: perceptual psychology, cognitive load, affordances
- **Production AI Infrastructure**: serving visualization at scale, embedding in ML platforms, monitoring distributed model behavior

The modern ML visualization stack must handle:
- **High-velocity streaming data** from production model inference
- **High-dimensional latent spaces** from embeddings and attention maps
- **Real-time model monitoring** with sub-second latency requirements
- **Interactive exploration** of billion-row datasets without pre-aggregation
- **Explainable AI interfaces** that translate model internals into human-comprehensible visuals

This course progresses from **foundational theory** → **engine-level implementation** → **production systems** → **ML-specific visualization domains**, with each module building a complete mental model connecting mathematical abstraction to pixel-level rendering to operational infrastructure.

---

## 2. Target Audience & Prerequisites

### Target Audience
- AI Systems Engineers building model monitoring and experiment tracking UIs
- ML Infrastructure Engineers creating distributed training visualization dashboards
- LLM Engineers building attention visualization, token probability displays, and prompt playgrounds
- MLOps Engineers designing real-time model drift and performance dashboards
- Distributed Systems Engineers extending into data-intensive frontend systems
- Backend Engineers transitioning to full-stack with visualization expertise
- Staff-level candidates preparing for visualization and ML systems architecture interviews

### Prerequisites
- **Solid JavaScript/TypeScript**: closures, async/await, generators, type systems
- **Computer Science Fundamentals**: algorithms, data structures, complexity analysis
- **Web Platform**: DOM, Canvas 2D, WebGL basics, browser event loop
- **React**: components, hooks, refs, reconciliation (covered in Frontend Engineering syllabus)
- **Mathematics**: linear algebra (vectors, matrices, eigen decomposition), probability & statistics, calculus
- **ML Basics**: model training, inference, evaluation metrics, feature importance

---

## 3. Learning Objectives & Outcomes

By the end of this course, you will be able to:

1. **Design** visualization grammars from first principles using the Grammar of Graphics
2. **Implement** custom D3.js visualizations with full control over the rendering pipeline
3. **Architect** real-time streaming dashboards handling 10k+ events/second with sub-100ms latency
4. **Visualize** high-dimensional data through dimensionality reduction, projections, and interactive exploration
5. **Build** model explainability interfaces (SHAP, LIME, attention maps, feature importance)
6. **Optimize** rendering performance using Canvas 2D, WebGL, and GPU acceleration
7. **Integrate** visualization into production ML platforms with proper data pipelines and caching
8. **Design** accessible, ethical visualizations that serve diverse audiences without misleading
9. **Implement** natural language interfaces for AI-generated visualizations
10. **Debug** rendering performance bottlenecks using Chrome DevTools, React Profiler, and custom instrumentation

---

## Module 0: Mathematical & Computational Foundations

### 0.1 Linear Algebra for Visualization
- **Vector spaces**: basis, dimension, linear independence
- **Matrix transformations**: scaling, rotation, translation, projection
- **Eigenvalues & eigenvectors**: principal component analysis foundation
- **Singular Value Decomposition (SVD)**: dimensionality reduction, latent semantic analysis
- **Affine transformations**: homogeneous coordinates, transformation matrices
- **Connection to visualization**: coordinate systems, view transforms, data-to-pixel mapping

### 0.2 Probability & Statistics for Data Representation
- **Distributions**: normal, log-normal, exponential, power law
- **Summary statistics**: mean, median, mode, variance, standard deviation, quantiles
- **Correlation & covariance**: Pearson, Spearman, Kendall tau
- **Sampling theory**: random sampling, stratified sampling, reservoir sampling for streaming
- **Statistical significance**: p-values, confidence intervals, effect size
- **Bayesian reasoning**: prior, likelihood, posterior, credible intervals

### 0.3 Information Theory
- **Entropy**: Shannon entropy, cross-entropy, KL divergence
- **Mutual information**: measuring dependence between variables
- **Channel capacity**: compression, efficient encoding
- **Application**: optimal binning, color encoding, information density in visualizations

### 0.4 Computational Geometry
- **Convex hulls**: Graham scan, QuickHull
- **Voronoi diagrams**: nearest-neighbor partitioning
- **Delaunay triangulation**: optimal triangulation for interpolation
- **Point-in-polygon**: ray casting, winding number
- **Spatial indexing**: quadtrees, R-trees, k-d trees for large-scale data

### 0.5 Graph Theory for Network Visualization
- **Graph representations**: adjacency matrix, adjacency list, edge list
- **Layout algorithms**: force-directed (Fruchterman-Reingold), spectral, hierarchical
- **Centrality measures**: degree, betweenness, closeness, eigenvector, PageRank
- **Community detection**: Louvain, label propagation
- **Application**: neural network architecture visualization, attention graph visualization

### 0.6 The Browser Graphics Stack
- **The pixel pipeline**: JavaScript → Style → Layout → Paint → Composite → GPU
- **Rasterization**: vector to pixel conversion, anti-aliasing
- **The compositor thread**: layers, will-change, transform, opacity
- **GPU acceleration**: texture upload, shader execution, framebuffer operations
- **Memory architecture**: CPU RAM vs GPU VRAM, texture memory, buffer objects

### 0.7 Reading
- *Linear Algebra Done Right* — Axler, Ch. 1-5
- *The Elements of Statistical Learning* — Hastie, Tibshirani, Friedman, Ch. 1-3
- *Information Theory and Reliable Communication* — Gallager, Ch. 1-2
- *Computational Geometry: Algorithms and Applications* — de Berg et al., Ch. 1-5

---

## Module 1: The Grammar of Graphics & Visualization Theory

### 1.1 The Grammar of Graphics (Wilkinson)
- **Data**: variables, transformations, statistics
- **Aesthetics**: position, color, size, shape, transparency, texture
- **Geometries**: points, lines, bars, areas, polygons, text
- **Scales**: linear, log, sqrt, ordinal, nominal, temporal
- **Coordinates**: Cartesian, polar, geographic, parallel
- **Facets**: small multiples, trellis plots, conditioning
- **Statistics**: binning, smoothing, aggregation, density estimation

### 1.2 Visual Perception & Cognition
- **Pre-attentive processing**: color, motion, orientation, size — what pops out
- **Gestalt principles**: proximity, similarity, continuity, closure, common fate
- **Color perception**: opponent process theory, CIELAB color space, color blindness
- **Working memory**: chunking, 7±2 rule, cognitive load management
- **Change blindness**: why animations matter, why they can mislead
- **Chart junk vs data-ink ratio**: Tufte's principles, when decoration helps

### 1.3 Color Theory for Data
- **Color spaces**: RGB, HSL, HCL, CIELAB, OKLCH
- **Sequential palettes**: single hue, multi-hue, perceptually uniform
- **Diverging palettes**: two hues with neutral center
- **Qualitative palettes**: distinct hues for categorical data
- **Color blindness simulation**: deuteranopia, protanopia, tritanopia
- **Tools**: ColorBrewer, d3-scale-chromatic, chroma.js

### 1.4 Chart Selection Decision Framework

| Data Type | Question | Recommended Chart |
|-----------|----------|-------------------|
| 1D distribution | What is the shape? | Histogram, KDE plot, box plot, violin |
| 2D relationship | Is there correlation? | Scatter plot, heatmap, contour |
| Time series | What is the trend? | Line chart, area chart, candlestick |
| Composition | What are the parts? | Stacked bar, treemap, pie (sparingly) |
| Comparison | How do groups differ? | Grouped bar, dot plot, radar chart |
| Flow | Where does it go? | Sankey, chord diagram, flow map |
| Hierarchy | What is the structure? | Tree, sunburst, icicle, treemap |
| Network | How are nodes connected? | Force-directed, adjacency matrix, arc diagram |

### 1.5 Statistical Graphics Principles
- **Data density**: maximizing information per pixel
- **Lie factor**: distortion in visual representation
- **Aspect ratio**: banking to 45 degrees for time series
- **Reference lines & annotations**: context, benchmarks, anomalies
- **Uncertainty visualization**: error bars, confidence bands, prediction intervals, hypothetical outcome plots

### 1.6 Lab: Design a Visualization Grammar
- Implement a minimal Grammar of Graphics engine
- Support data transformation, aesthetic mapping, geometry rendering
- Add scale types and coordinate systems
- Evaluate against real datasets

---

## Module 2: The Browser Rendering Pipeline for Visualization

### 2.1 SVG: Scalable Vector Graphics
- **SVG DOM**: elements, attributes, namespaces, the SVG coordinate system
- **Path commands**: M, L, C, Q, A, Z — Bézier curves, arcs
- **Transforms**: translate, scale, rotate, skew, matrix
- **Gradients & patterns**: linear, radial, pattern units
- **Filters**: blur, drop-shadow, color matrix, displacement map
- **Performance**: DOM overhead, reflow cost, when SVG is appropriate

### 2.2 Canvas 2D: Immediate Mode Rendering
- **The 2D rendering context**: `getContext('2d')`
- **Path API**: `beginPath`, `moveTo`, `lineTo`, `arc`, `bezierCurveTo`
- **State stack**: `save()`, `restore()`, transformation matrix
- **Image data**: `getImageData`, `putImageData`, pixel manipulation
- **Performance patterns**: batch drawing, offscreen canvas, dirty rectangle tracking
- **When to use Canvas**: large datasets (>10k elements), animation, games, pixel manipulation

### 2.3 WebGL & WebGPU: GPU-Accelerated Rendering
- **The graphics pipeline**: vertex shader → rasterization → fragment shader
- **WebGL 2.0**: typed arrays, textures, framebuffers, instanced rendering
- **WebGPU**: next-generation API, compute shaders, bind groups
- **Three.js integration**: scene graph, materials, geometries, renderers
- **Custom shaders**: GLSL/GLSL ES, WGSL for WebGPU
- **When to use WebGL**: 3D, massive datasets, particle systems, real-time simulation

### 2.4 The Rendering Decision Matrix

| Dataset Size | Interactivity | Animation | Recommended Renderer |
|-------------|---------------|-----------|---------------------|
| < 1k elements | High | No | SVG |
| 1k - 10k | Medium | Light | Canvas 2D |
| 10k - 100k | Low | Heavy | WebGL (instanced) |
| > 100k | Minimal | Real-time | WebGL/WebGPU compute |
| 3D / Volumetric | High | Real-time | WebGL / WebGPU |

### 2.5 React Integration Strategies
- **SVG in React**: declarative JSX, React manages DOM
- **Canvas in React**: `useRef` + `useEffect`, imperative drawing
- **WebGL in React**: `react-three-fiber`, declarative 3D scene graph
- **The reconciliation problem**: React's virtual DOM vs imperative graphics APIs
- **Performance patterns**: `requestAnimationFrame`, `useLayoutEffect`, `React.memo`

### 2.6 Lab: Implement a Multi-Renderer Chart
- Build the same scatter plot in SVG, Canvas 2D, and WebGL
- Benchmark rendering performance with 1k, 10k, 100k points
- Measure memory usage, frame rate, and interaction latency

---

## Module 3: D3.js — The Visualization Engine

### 3.1 D3 Architecture & Philosophy
- **Data-Driven Documents**: bind data to DOM, apply transformations
- **Modular design**: d3-selection, d3-scale, d3-shape, d3-transition, etc.
- **Functional programming**: method chaining, higher-order functions
- **The enter/update/exit pattern**: data binding lifecycle

### 3.2 D3 Selections & Data Binding
- **Selections**: `d3.select`, `d3.selectAll`, `selection.data()`
- **The data join**: `.enter()`, `.update()`, `.exit()`
- **Key functions**: maintaining object constancy across updates
- **Nested selections**: hierarchical data, recursive patterns
- **Event handling**: `.on('click', ...)`, event delegation, custom events

### 3.3 D3 Scales
- **Continuous scales**: `scaleLinear`, `scaleLog`, `scaleSqrt`, `scaleTime`
- **Sequential scales**: `scaleSequential`, interpolators
- **Quantize & quantile**: `scaleQuantize`, `scaleQuantile`
- **Threshold & ordinal**: `scaleThreshold`, `scaleOrdinal`
- **Band & point**: `scaleBand`, `scalePoint` for categorical positioning
- **Custom scales**: implementing `scale` interface, invert, ticks, tickFormat

### 3.4 D3 Shapes & Layouts
- **Line generators**: `d3.line`, curve interpolation (linear, monotone, basis, catmull-rom)
- **Area generators**: `d3.area`, stacked areas
- **Arc generators**: `d3.arc`, pie layout, donut charts
- **Hierarchy layouts**: `d3.tree`, `d3.cluster`, `d3.pack`, `d3.partition`, `d3.treemap`
- **Force simulation**: `d3.forceSimulation`, force types (link, charge, center, collision)
- **Chord layout**: `d3.chord`, `d3.ribbon` for matrix visualization

### 3.5 D3 Transitions & Animation
- **Transition API**: `selection.transition()`, `duration`, `delay`, `ease`
- **Interpolation**: number, string, color, path, transform
- **Staggering**: per-element delay for sequential reveals
- **Animation scheduling**: `d3.timer`, `d3.timeout`, `d3.interval`
- **Performance**: `transform` and `opacity` for GPU-accelerated transitions

### 3.6 D3 Geo & Projections
- **Geographic projections**: `d3.geoMercator`, `d3.geoAlbersUsa`, `d3.geoNaturalEarth1`
- **Path generators**: `d3.geoPath`, graticules, sphere
- **TopoJSON**: topology encoding, mesh extraction, feature filtering
- **Zoom & pan**: `d3.zoom`, scale extent, translate extent, event transforms

### 3.7 D3 v7+ Modern Patterns
- **ES modules**: importing only needed modules
- **Observable integration**: notebooks, reactive cells
- **TypeScript support**: `@types/d3`, strict typing
- **Web Workers**: offloading heavy computations

### 3.8 Lab: Build a Custom D3 Visualization Library
- Implement reusable chart components with full D3 control
- Add transition animations, tooltips, and brushing
- Support responsive resizing and accessibility
- Benchmark against off-the-shelf libraries

---

## Module 4: Observable Plot & Declarative Visualization

### 4.1 Observable Plot Philosophy
- **Declarative API**: marks, options, transforms — not imperative DOM manipulation
- **Built on D3**: leverages D3 scales, shapes, and projections
- **Observable notebooks**: reactive, literate programming environment
- **The mark abstraction**: `Plot.dot`, `Plot.line`, `Plot.rect`, `Plot.cell`

### 4.2 Plot API Deep Dive
- **Marks**: geometric primitives with data-driven aesthetics
- **Options**: `x`, `y`, `fill`, `stroke`, `r`, `title`, `tip`
- **Transforms**: `groupX`, `binX`, `windowY`, `normalize`, `map`
- **Facets**: `fx`, `fy` for small multiples
- **Scales**: automatic inference, explicit configuration
- **Legends**: automatic legend generation, custom formatting

### 4.3 Observable Notebooks
- **Reactive cells**: dependency graph, automatic re-evaluation
- **Inputs**: sliders, dropdowns, text inputs, file uploads
- **Database clients**: SQL cells, BigQuery, Snowflake
- **Embedding**: exporting notebooks as static sites, iframe embedding
- **Observable Framework**: static site generation from notebooks

### 4.4 Production Integration
- **Static exports**: `Plot.plot()` returns SVG string
- **React integration**: rendering Observable Plot in React components
- **Data pipelines**: connecting Observable to production databases
- **Performance**: server-side rendering, hydration

### 4.5 Lab: Build an Interactive EDA Dashboard
- Use Observable Plot for exploratory data analysis
- Add interactive filters with Observable Inputs
- Export as a static dashboard
- Compare development velocity vs D3 imperative approach

---

## Module 5: React Integration — Reconciling React with Imperative Visualization

### 5.1 The React-D3 Integration Problem
- **Two paradigms**: React's declarative virtual DOM vs D3's imperative DOM manipulation
- **The black box approach**: React mounts a container, D3 manages internals
- **The full React approach**: React renders SVG elements, D3 provides math utilities
- **The hybrid approach**: React for structure, D3 for data processing and scales

### 5.2 The Black Box Pattern
```typescript
// React provides the container, D3 owns the internals
const Chart = ({ data }) => {
  const ref = useRef<SVGSVGElement>(null);
  
  useEffect(() => {
    if (!ref.current) return;
    const svg = d3.select(ref.current);
    // D3 imperative code here
    renderChart(svg, data);
  }, [data]);
  
  return <svg ref={ref} />;
};
```
- **Pros**: full D3 power, direct DOM control
- **Cons**: React doesn't know about D3's DOM changes, reconciliation conflicts
- **Cleanup**: proper teardown on unmount, memory leak prevention

### 5.3 The Full React Pattern
```typescript
// React renders everything, D3 provides scales and path generators
const LineChart = ({ data }) => {
  const xScale = useMemo(() => d3.scaleLinear().domain(...).range(...), [data]);
  const line = useMemo(() => d3.line().x(d => xScale(d.x)).y(d => yScale(d.y)), [xScale, yScale]);
  
  return (
    <svg>
      <path d={line(data)} />
      {data.map(d => <circle cx={xScale(d.x)} cy={yScale(d.y)} />)}
    </svg>
  );
};
```
- **Pros**: React manages lifecycle, props-driven updates
- **Cons**: overhead for large datasets, limited D3 transition support

### 5.4 The Hybrid Pattern (Recommended)
- **D3 for data processing**: scales, layouts, statistics, generators
- **React for rendering**: JSX elements, component lifecycle, state management
- **D3 transitions via React**: `react-spring`, `framer-motion`, or custom `requestAnimationFrame`
- **Ref for D3 selections**: accessing D3 behaviors (zoom, brush, drag) within React

### 5.5 Custom React Hooks for Visualization
- **useD3**: generic hook for D3 initialization and cleanup
- **useResizeObserver**: responsive chart sizing
- **useBrush**: brush selection state management
- **useZoom**: zoom transform state management
- **useTooltip**: tooltip positioning and content

### 5.6 React + Canvas Integration
- **useCanvas**: ref-based canvas drawing with React lifecycle
- **OffscreenCanvas**: web worker rendering for heavy computations
- **React Three Fiber**: declarative Three.js in React

### 5.7 Lab: Build a Reusable React Visualization Library
- Implement 5 chart types (line, bar, scatter, area, pie) as React components
- Support responsive sizing, tooltips, legends, and brushing
- Use the hybrid React-D3 pattern
- Add Storybook documentation and TypeScript types

---

## Module 6: Time-Series & Streaming Visualization

### 6.1 Time-Series Data Structures
- **Temporal data types**: `Date`, `Temporal` API, Unix timestamps, ISO 8601
- **Time scales**: `d3.scaleTime`, `d3.scaleUtc`, time intervals
- **Aggregation windows**: rolling averages, exponential smoothing, resampling
- **Gap handling**: missing data interpolation, null values, discontinuities

### 6.2 Real-Time Streaming Architecture

```
Data Source → Message Queue (Kafka/Pulsar) → 
  Stream Processor (Flink/Spark) → 
    Time-Series DB (TimescaleDB/InfluxDB) → 
      API (WebSocket/SSE) → 
        Frontend (React + D3/Canvas)
```

### 6.3 WebSocket & Server-Sent Events for Visualization
- **WebSocket**: bidirectional, persistent connection, binary frames
- **Server-Sent Events (SSE)**: unidirectional, HTTP-based, automatic reconnection
- **Protocol selection**: when to use which for visualization data
- **Message framing**: JSON, Protocol Buffers, binary formats
- **Backpressure**: handling slow consumers, buffering strategies

### 6.4 Streaming Chart Implementation
- **Data buffer**: circular buffer, fixed window, sliding window
- **Update strategies**: append-only, full redraw, incremental update
- **Animation smoothing**: tweening between data points, easing functions
- **Downsampling**: Largest Triangle Three Buckets (LTTB), min-max decimation
- **Gap detection**: identifying and visualizing data gaps

### 6.5 Canvas-Based Streaming Charts
- **Double buffering**: offscreen canvas for drawing, visible canvas for display
- **Pixel-perfect rendering**: sub-pixel anti-aliasing, crisp lines
- **GPU texture streaming**: uploading data as textures for shader-based rendering
- **WebGL point clouds**: rendering millions of time-series points

### 6.6 Observable Plot for Streaming
- **Reactive data updates**: updating marks with new data
- **Window transforms**: `Plot.windowY` for rolling calculations
- **Animation frames**: `requestAnimationFrame` for smooth updates

### 6.7 Production Patterns for Streaming Dashboards
- **Connection management**: reconnection, heartbeat, timeout handling
- **Data validation**: schema validation, type checking, sanitization
- **Error states**: connection lost, stale data, data gap visualization
- **Multi-tenant isolation**: per-user data streams, access control
- **Rate limiting**: client-side throttling, server-side backpressure

### 6.8 Lab: Build a Real-Time ML Metrics Dashboard
- WebSocket streaming of model inference metrics
- Canvas-based line chart with 10k+ points updating at 60fps
- Downsampling for historical view, full resolution for recent data
- Add anomaly detection visualization (outliers highlighted)
- Implement connection resilience and data gap handling

---

## Module 7: High-Dimensional Data Visualization

### 7.1 Dimensionality Reduction Algorithms
- **Principal Component Analysis (PCA)**: eigendecomposition of covariance matrix
- **t-SNE**: t-distributed stochastic neighbor embedding, perplexity tuning
- **UMAP**: uniform manifold approximation and projection, topological foundations
- **Autoencoders**: neural network-based dimensionality reduction
- **Comparison**: when to use which, computational complexity, interpretability

### 7.2 Scatter Plot Matrices & Parallel Coordinates
- **SPLOM**: pairwise scatter plots for all variable combinations
- **Parallel coordinates**: `d3.line` for each observation across dimensions
- **Brushing & linking**: selecting in one view highlights in others
- **Dimension reordering**: optimizing for pattern discovery

### 7.3 Embedding Visualization
- **Word embeddings**: visualizing word2vec, GloVe, fasttext in 2D/3D
- **Sentence embeddings**: BERT, Sentence-BERT projection
- **Image embeddings**: CNN feature space visualization
- **Cluster visualization**: K-means, DBSCAN, HDBSCAN results

### 7.4 Heatmaps & Matrix Visualization
- **Correlation matrices**: color-encoded correlation coefficients
- **Confusion matrices**: classification performance visualization
- **Attention heatmaps**: transformer attention weight visualization
- **Hierarchical clustering**: dendrograms + heatmap combination

### 7.5 3D Visualization for High-Dimensional Data
- **3D scatter plots**: `three.js`, `react-three-fiber`
- **Volume rendering**: ray marching, transfer functions
- **Interactive rotation**: mouse/touch controls, inertia, snapping
- **Projection to 2D**: perspective, orthographic, isometric

### 7.6 Lab: Visualize a 768-Dimensional Embedding Space
- Apply UMAP to reduce BERT embeddings to 2D/3D
- Build an interactive scatter plot with zoom, pan, and selection
- Add hover tooltips showing original text
- Implement brushing & linking with a parallel coordinates view

---

## Module 8: Model Explainability & Interpretability Visualization

### 8.1 Feature Importance Visualization
- **Permutation importance**: shuffling features, measuring performance drop
- **Built-in importance**: tree-based feature importance, linear coefficients
- **SHAP summary plots**: beeswarm, bar, violin plots for SHAP values
- **Partial dependence plots**: marginal effect of a feature on prediction
- **ICE plots**: individual conditional expectation curves

### 8.2 SHAP (SHapley Additive exPlanations) Visualization
- **SHAP values**: game-theoretic feature attribution
- **Force plots**: pushing prediction from base value to final value
- **Waterfall plots**: sequential feature contributions
- **Decision plots**: cumulative SHAP values across samples
- **Interaction plots**: pairwise feature interactions

### 8.3 LIME (Local Interpretable Model-agnostic Explanations)
- **Local surrogate models**: fitting interpretable models near predictions
- **Feature perturbation**: generating neighborhood samples
- **Visualization**: feature weights, perturbed instances, prediction confidence

### 8.4 Attention Visualization for Transformers
- **Attention matrices**: heatmaps of query-key dot products
- **Attention rollout**: propagating attention through layers
- **Attention flow**: flow-based attention aggregation
- **BertViz**: interactive attention visualization for BERT
- **Token-level visualization**: highlighting attended tokens

### 8.5 Saliency Maps & Grad-CAM
- **Gradient-based saliency**: input gradients for classification
- **Grad-CAM**: gradient-weighted class activation mapping
- **Integrated gradients**: attributing along interpolation path
- **SmoothGrad**: reducing noise in gradient visualization

### 8.6 Model Comparison Visualization
- **ROC curves**: true positive rate vs false positive rate
- **Precision-Recall curves**: trade-off visualization
- **Calibration plots**: predicted probability vs actual frequency
- **Learning curves**: training/validation loss over epochs
- **Model cards**: standardized model documentation visualization

### 8.7 Lab: Build an XAI Dashboard
- SHAP summary plot for a tabular model
- Attention heatmap for a transformer model
- Grad-CAM overlay for an image classification model
- Model comparison with ROC curves and calibration plots
- Interactive feature importance with what-if analysis

---

## Module 9: Real-Time ML Monitoring Dashboards

### 9.1 ML Monitoring Metrics

| Category | Metrics | Visualization |
|----------|---------|---------------|
| **Data Quality** | Null rate, distribution drift, schema changes | Distribution plots, drift scores |
| **Model Performance** | Accuracy, precision, recall, F1, AUC | Time-series line charts, gauges |
| **Prediction Drift** | PSI, KS test, Wasserstein distance | Drift timeline, threshold alerts |
| **Feature Drift** | Feature statistics, correlation changes | Heatmaps, correlation matrices |
| **Latency** | P50, P95, P99 inference time | Histograms, percentile charts |
| **Throughput** | Requests/second, batch size | Line charts, counters |
| **Error Rates** | 4xx, 5xx, timeout rates | Stacked area, alert panels |
| **Resource Usage** | CPU, GPU, memory, disk | Gauge charts, time-series |

### 9.2 Drift Detection Visualization
- **Population Stability Index (PSI)**: threshold-based drift alerts
- **Kolmogorov-Smirnov test**: distribution comparison
- **Wasserstein distance**: optimal transport-based drift
- **Concept drift**: performance degradation over time
- **Visualization**: drift timeline, distribution comparison overlays, alert panels

### 9.3 Alerting & Anomaly Visualization
- **Threshold-based alerts**: static thresholds, dynamic thresholds (EWMA)
- **Anomaly detection**: Isolation Forest, LOF, autoencoder-based
- **Alert visualization**: severity levels, acknowledgment, resolution tracking
- **Incident timeline**: correlating alerts with model deployments

### 9.4 A/B Testing Visualization
- **Experiment design**: control vs treatment, randomization, sample size
- **Metrics visualization**: conversion rates, lift, confidence intervals
- **Sequential testing**: early stopping, peeking correction
- **Cohort analysis**: segmenting by user attributes

### 9.5 Model Registry & Version Visualization
- **Model lineage**: training data → model version → deployment
- **Performance comparison**: version-over-version metrics
- **Deployment status**: staging, production, rollback visualization
- **Artifact visualization**: model architecture, hyperparameters

### 9.6 Production Dashboard Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                    ML Monitoring Dashboard                   │
├────────────────────────────────────────────────────────────────┤
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────────────┐  │
│  │ Model Health │  │ Data Drift  │  │ Performance Metrics │  │
│  │   (Gauge)   │  │  (Timeline) │  │   (Line Charts)     │  │
│  └─────────────┘  └─────────────┘  └─────────────────────┘  │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │              Feature Importance (Bar Chart)              │ │
│  └─────────────────────────────────────────────────────────┘ │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────────────┐  │
│  │   Alerts    │  │  Latency    │  │   Resource Usage    │  │
│  │   (List)    │  │ (Histogram) │  │    (Area Chart)     │  │
│  └─────────────┘  └─────────────┘  └─────────────────────┘  │
└─────────────────────────────────────────────────────────────┘
```

### 9.7 Lab: Build a Production ML Monitoring Dashboard
- Real-time metrics streaming via WebSocket
- Drift detection with visual alerts
- Model version comparison with performance charts
- Alert management with severity levels
- Export to PDF/PNG for reporting

---

## Module 10: Interactive Data Exploration & Drill-Down

### 10.1 Brushing & Linking
- **Brush component**: 1D (axis), 2D (rectangular), multi-brush
- **Linked views**: selecting in one view filters others
- **Crossfilter**: dimensional filtering for large datasets
- **Performance**: indexing, debouncing, incremental updates

### 10.2 Zoom & Pan
- **Geometric zoom**: scale transform on visual elements
- **Semantic zoom**: changing representation detail level
- **D3 zoom behavior**: `d3.zoom`, transform, extent, scale extent
- **Infinite scroll**: virtualized data loading on scroll
- **Minimap**: overview + detail view coordination

### 10.3 Filtering & Querying
- **Dynamic filtering**: slider, dropdown, search, date range
- **Query builders**: visual SQL, filter chips, boolean logic
- **Faceted search**: multi-dimensional filtering with counts
- **Saved views**: bookmarking filter states, sharing

### 10.4 Drill-Down Patterns
- **Hierarchical drill-down**: summary → detail → individual record
- **Temporal drill-down**: year → month → day → hour
- **Geographic drill-down**: country → state → city → zip
- **Transition animations**: smooth morphing between levels

### 10.5 Lab: Build an Interactive ML Experiment Explorer
- Filter experiments by model type, date, metrics
- Drill down from experiment list → run details → step-level metrics
- Linked views: selecting a run highlights it in all charts
- Export filtered data as CSV/JSON

---

## Module 11: Performance Engineering for Visualization

### 11.1 Rendering Performance Metrics
- **Frame rate**: 60fps target, `requestAnimationFrame` timing
- **Frame budget**: 16.67ms per frame at 60fps
- **Jank**: identifying and eliminating frame drops
- **Chrome DevTools**: Performance tab, frame timeline, GPU activity

### 11.2 Data Processing Optimization
- **Web Workers**: offloading data transformation from main thread
- **WASM**: compiled data processing (Rust, C++ → WebAssembly)
- **Streaming computation**: processing data in chunks, not all at once
- **Memoization**: caching expensive computations
- **Virtualization**: rendering only visible elements

### 11.3 Memory Management
- **Object pooling**: reusing objects instead of garbage collection
- **Typed arrays**: `Float32Array`, `Uint8Array` for numeric data
- **Buffer management**: explicit memory allocation/deallocation
- **Memory profiling**: Chrome DevTools Heap snapshots, allocation tracking
- **Memory leaks**: detached DOM nodes, closure captures, event listeners

### 11.4 GPU Optimization
- **Texture atlases**: combining multiple images into one texture
- **Instanced rendering**: drawing many similar objects in one call
- **Shader optimization**: minimizing branching, reducing texture lookups
- **Framebuffer management**: efficient render-to-texture operations

### 11.5 Network Optimization
- **Data compression**: gzip, brotli, Protocol Buffers, Avro
- **Pagination**: loading data in chunks, infinite scroll
- **Prefetching**: loading data before it's needed
- **Caching strategies**: browser cache, service worker, CDN

### 11.6 Lab: Optimize a Slow Dashboard
- Profile rendering performance with Chrome DevTools
- Implement Web Worker for data processing
- Add virtualization for large tables
- Optimize memory usage with typed arrays
- Target 60fps for all interactions

---

## Module 12: Production Architecture & Embedded Analytics

### 12.1 Embedded Analytics Architecture
- **Composable analytics**: chart components embedded in product workflows, not standalone dashboards
- **White-labeling**: deep styling control, brand-native experiences
- **API-first**: chart configuration via JSON/API, not just UI builders
- **Multi-tenant**: row-level security, role-based view access, data scoping

### 12.2 Data Pipeline for Visualization
- **ETL/ELT**: Extract, Transform, Load vs Extract, Load, Transform
- **Data warehouses**: Snowflake, BigQuery, Redshift for analytics
- **OLAP cubes**: pre-aggregated data for fast querying
- **Materialized views**: caching expensive aggregations
- **Real-time pipelines**: Kafka → Flink → Time-series DB → API

### 12.3 API Design for Visualization
- **RESTful endpoints**: `/api/v1/metrics`, `/api/v1/datasets`
- **GraphQL**: flexible querying, reducing over-fetching
- **tRPC**: end-to-end type safety for visualization APIs
- **WebSocket APIs**: real-time data subscriptions
- **Pagination**: cursor-based, offset-based, keyset pagination

### 12.4 Caching Strategy
- **Client-side caching**: React Query, SWR, Apollo Client
- **CDN caching**: static chart images, pre-rendered dashboards
- **Edge caching**: Vercel Edge, Cloudflare Workers
- **Database caching**: query result caching, materialized views

### 12.5 Security & Compliance
- **Data masking**: PII redaction, column-level security
- **Audit logging**: tracking who viewed what data when
- **GDPR/CCPA**: data deletion, right to be forgotten
- **SOC 2 compliance**: access controls, encryption, monitoring

### 12.6 Lab: Architect an Embedded Analytics Platform
- Design API for chart data with pagination and filtering
- Implement row-level security for multi-tenant access
- Add caching layer with cache invalidation
- Create white-labeled chart components
- Deploy with CDN caching and edge functions

---

## Module 13: Accessibility, Ethics & Design Systems

### 13.1 Accessibility (a11y) for Data Visualization
- **WCAG 2.1 AA compliance**: color contrast (4.5:1), text alternatives
- **Screen reader support**: `aria-label`, `role="img"`, data tables for charts
- **Keyboard navigation**: tab order, arrow key navigation, Enter/Space activation
- **Color blindness**: patterns, textures, labels in addition to color
- **Motion sensitivity**: `prefers-reduced-motion`, static alternatives
- **Data sonification**: audio representations of data for blind users

### 13.2 Ethical Visualization
- **Chart junk & distortion**: avoiding misleading scales, truncated axes
- **Cherry-picking**: showing selective data to support a narrative
- **Base rate fallacy**: visualizing rates without denominators
- **Correlation vs causation**: avoiding spurious visual connections
- **Algorithmic bias**: visualizing model bias, fairness metrics
- **Transparency**: showing uncertainty, confidence intervals, data sources

### 13.3 Design Systems for Visualization
- **Token system**: colors, typography, spacing, border radius
- **Chart primitives**: axes, grids, legends, tooltips as reusable components
- **Theme support**: light/dark mode, brand theming
- **Responsive design**: mobile, tablet, desktop breakpoints
- **Documentation**: Storybook, design tokens, usage guidelines

### 13.4 Lab: Build an Accessible Chart Library
- Implement WCAG-compliant color palette
- Add screen reader support with data tables
- Implement keyboard navigation
- Test with color blindness simulators
- Document accessibility features

---

## Module 14: AI-Generated Visualization & Natural Language Interfaces

### 14.1 Natural Language to Visualization
- **NL4Vis**: natural language interfaces for data visualization
- **Intent parsing**: identifying chart type, data source, filters
- **Ambiguity resolution**: clarifying vague queries
- **Context awareness**: conversational state, previous queries
- **Vega-Lite + LLM**: generating Vega-Lite specs from natural language

### 14.2 AI-Powered Data Storytelling
- **Automatic annotation**: generating contextual callouts and insights
- **Anomaly flagging**: AI-identified outliers with explanations
- **Narrative generation**: summarizing trends in natural language
- **Adaptive visualization**: adjusting chart complexity based on user expertise

### 14.3 Multimodal Visualization
- **Text + chart**: LLM-generated summaries alongside visualizations
- **Image + data**: combining visual and tabular data
- **Voice interaction**: speech-to-text queries, text-to-speech summaries
- **Spatial computing**: 3D data environments, AR/VR visualization

### 14.4 LLM Integration Patterns
- **Prompt engineering for visualization**: structured prompts for chart generation
- **Function calling**: LLM calling visualization APIs
- **RAG for data**: retrieving relevant data context for visualization queries
- **Streaming responses**: real-time chart updates from LLM output

### 14.5 Lab: Build an AI-Powered Visualization Assistant
- Natural language query interface for dataset exploration
- Automatic chart type selection based on data and query
- AI-generated annotations and insights
- Conversational refinement of visualizations

---

## Capstone Project

### Project: Production-Grade ML Observability Platform

Build a comprehensive visualization platform for monitoring and exploring ML systems:

**Requirements:**
1. **Real-time model monitoring**: WebSocket streaming of inference metrics with Canvas-based charts
2. **Model explainability dashboard**: SHAP values, attention maps, feature importance
3. **Experiment tracking**: interactive explorer with filtering, drill-down, and comparison
4. **Data drift detection**: visual alerts, distribution comparison, drift timeline
5. **High-dimensional embedding explorer**: UMAP projection with interactive selection
6. **Performance targets**: 60fps for all interactions, <100ms latency for real-time updates
7. **Accessibility**: WCAG 2.1 AA compliant, screen reader support, keyboard navigation
8. **Embedded analytics**: composable chart components for integration into other products
9. **AI assistant**: natural language query interface for chart generation
10. **Documentation**: Architecture Decision Records, API docs, deployment guide

**Architecture:**
- React + TypeScript frontend with D3.js and Observable Plot
- WebSocket streaming with Canvas 2D for high-performance charts
- Web Workers for data processing and dimensionality reduction
- Next.js App Router with server components for data fetching
- Feature-Sliced Design folder structure
- Comprehensive testing (unit, integration, E2E, visual regression)

---

## Appendix A: Reading List & References

### Foundational Mathematics
- *Linear Algebra Done Right* — Sheldon Axler
- *The Elements of Statistical Learning* — Hastie, Tibshirani, Friedman
- *Information Theory and Reliable Communication* — Robert Gallager
- *Computational Geometry: Algorithms and Applications* — de Berg et al.

### Visualization Theory
- *The Grammar of Graphics* — Leland Wilkinson
- *The Visual Display of Quantitative Information* — Edward Tufte
- *Visualization Analysis and Design* — Tamara Munzner
- *Fundamentals of Data Visualization* — Claus O. Wilke

### Technical Implementation
- *Interactive Data Visualization for the Web* — Scott Murray (D3.js)
- *D3.js in Action* — Elijah Meeks
- *Observable Plot Documentation* — Observable
- *WebGL Programming Guide* — Kouichi Matsuda, Rodger Lea

### ML & Explainability
- *Interpretable Machine Learning* — Christoph Molnar
- *Hands-On Machine Learning* — Aurélien Géron
- *Pattern Recognition and Machine Learning* — Christopher Bishop

### Systems & Production
- *Designing Data-Intensive Applications* — Martin Kleppmann
- *High Performance Browser Networking* — Ilya Grigorik
- *Building Microservices* — Sam Newman

---

## Appendix B: Tooling Matrix

### Core Visualization
| Tool | Type | Best For | Complexity |
|------|------|----------|------------|
| **D3.js** | Imperative library | Custom, complex visualizations | High |
| **Observable Plot** | Declarative library | Rapid prototyping, EDA | Medium |
| **Vega-Lite** | Declarative grammar | Specification-based charts | Medium |
| **Apache ECharts** | Chart library | Standard charts, Chinese market | Low |
| **Victory** | React chart library | React-native charts | Low |
| **Recharts** | React chart library | Standard React charts | Low |
| **Nivo** | React chart library | D3-based React charts | Medium |
| **React-Vis** | React chart library | Uber's chart library | Medium |

### High-Performance Rendering
| Tool | Type | Best For |
|------|------|----------|
| **Canvas 2D** | Browser API | Large datasets, custom rendering |
| **WebGL** | Browser API | 3D, massive datasets, shaders |
| **WebGPU** | Browser API | Next-gen GPU compute |
| **Three.js** | 3D library | 3D visualizations, WebGL abstraction |
| **regl** | Functional WebGL | Custom WebGL shaders |
| **deck.gl** | Layered rendering | Geospatial, large-scale data |
| **kepler.gl** | Geospatial | Uber's geospatial visualization |

### ML-Specific
| Tool | Type | Best For |
|------|------|----------|
| **SHAP** | Python library | Model explainability |
| **BertViz** | Python/JS | Transformer attention |
| **TensorBoard** | Dashboard | TensorFlow training |
| **Weights & Biases** | SaaS | Experiment tracking |
| **MLflow** | Platform | ML lifecycle |
| **Evidently AI** | Open source | ML monitoring |

---

## Appendix C: Interview Preparation

### System Design: Visualization Architecture
- Design a real-time dashboard for 1M+ events/second
- Design an interactive embedding explorer for billion-row datasets
- Design a model monitoring system with drift detection
- Design an embedded analytics platform for multi-tenant SaaS

### Visualization Deep Dives
- Explain the Grammar of Graphics and implement a minimal version
- How would you render 100k points in a scatter plot at 60fps?
- Design a color palette that works for color-blind users
- How do you handle streaming data with gaps and backpressure?

### ML Visualization
- How do you visualize attention weights in a transformer?
- Design a SHAP value visualization for non-technical stakeholders
- How do you detect and visualize data drift in production?
- Explain PCA, t-SNE, and UMAP — when to use each for visualization

### Coding Challenges
- Implement a custom D3 line chart with transitions and tooltips
- Build a virtualized table that handles 1M rows
- Create a WebGL particle system for embedding visualization
- Implement LTTB downsampling for time-series data

---

## Course Timeline

| Phase | Duration | Modules | Focus |
|-------|----------|---------|-------|
| **Foundation** | 2 weeks | 0-1 | Math, perception, grammar of graphics |
| **Rendering Engine** | 2 weeks | 2-3 | SVG, Canvas, WebGL, D3.js |
| **React Integration** | 2 weeks | 4-5 | Observable Plot, React patterns |
| **ML Visualization** | 3 weeks | 6-9 | Streaming, embeddings, XAI, monitoring |
| **Production Engineering** | 3 weeks | 10-13 | Performance, architecture, accessibility |
| **Advanced Topics** | 1 week | 14 | AI-generated visualization |
| **Capstone** | 2 weeks | — | Production-grade platform |

**Total Duration: 15 weeks (3.5 months) full-time, or 7 months part-time**

---

*This syllabus treats data visualization as a systems engineering discipline. The tools evolve, but the mathematical foundations, perceptual principles, and architectural patterns remain constant. Master the fundamentals, and you can adapt to any technology stack.*