 ## File: web-scraping-data-collection-syllabus.md

# Web Scraping & Data Collection

## A World-Class, University-Level, Industry-Grade Technical Syllabus & Engineering Learning Roadmap

---

## Table of Contents

1. [Course Overview & Philosophy](#1-course-overview--philosophy)
2. [Target Audience & Prerequisites](#2-target-audience--prerequisites)
3. [Learning Objectives & Outcomes](#3-learning-objectives--outcomes)
4. [Module 0: Mathematical & Computational Foundations](#module-0-mathematical--computational-foundations)
5. [Module 1: The Web as a Data Source — HTTP, DOM, and the Modern Web Platform](#module-1-the-web-as-a-data-source)
6. [Module 2: Scrapy Architecture — The Production Crawling Engine](#module-2-scrapy-architecture--the-production-crawling-engine)
7. [Module 3: HTML Parsing & Data Extraction](#module-3-html-parsing--data-extraction)
8. [Module 4: Dynamic Content & JavaScript-Rendered Pages](#module-4-dynamic-content--javascript-rendered-pages)
9. [Module 5: Anti-Bot Evasion & Browser Fingerprinting](#module-5-anti-bot-evasion--browser-fingerprinting)
10. [Module 6: Distributed Crawling Architecture](#module-6-distributed-crawling-architecture)
11. [Module 7: Data Quality, Validation & Schema Enforcement](#module-7-data-quality-validation--schema-enforcement)
12. [Module 8: Data Pipelines & ETL for Scraped Data](#module-8-data-pipelines--etl-for-scraped-data)
13. [Module 9: Legal, Ethical & Compliance Framework](#module-9-legal-ethical--compliance-framework)
14. [Module 10: Real-Time Streaming Data Collection](#module-10-real-time-streaming-data-collection)
15. [Module 11: API-First Data Collection & Reverse Engineering](#module-11-api-first-data-collection--reverse-engineering)
16. [Module 12: AI-Powered Data Extraction & Adaptive Scraping](#module-12-ai-powered-data-extraction--adaptive-scraping)
17. [Module 13: Production Operations — Monitoring, Alerting & Debugging](#module-13-production-operations)
18. [Module 14: Performance Engineering & Cost Optimization](#module-14-performance-engineering--cost-optimization)
19. [Capstone Project](#capstone-project)
20. [Appendix A: Reading List & References](#appendix-a-reading-list--references)
21. [Appendix B: Tooling Matrix](#appendix-b-tooling-matrix)
22. [Appendix C: Interview Preparation](#appendix-c-interview-preparation)

---

## 1. Course Overview & Philosophy

Web scraping and data collection are not about writing quick scripts to grab HTML. They constitute a **systems engineering discipline** at the intersection of:

- **Computer Networks**: HTTP/1.1, HTTP/2, HTTP/3, TLS handshakes, TCP congestion control, DNS resolution
- **Distributed Systems**: message queues, worker coordination, consensus, partitioning, fault tolerance
- **Reverse Engineering**: DOM analysis, JavaScript deobfuscation, API endpoint discovery, mobile app traffic interception
- **Data Engineering**: schema validation, ETL pipelines, data quality, lineage tracking
- **Security Engineering**: TLS fingerprinting, browser fingerprint evasion, CAPTCHA solving, bot detection bypass
- **Legal & Ethics**: robots.txt, CFAA, GDPR, CCPA, terms of service, fair use

The modern data collection stack must handle:
- **Millions of pages per day** across distributed worker fleets
- **JavaScript-rendered SPAs** that require full browser execution
- **Sophisticated anti-bot systems** using ML-based behavioral analysis, TLS fingerprinting, and multi-layer detection
- **Real-time data streams** from WebSockets, SSE, and live APIs
- **Strict compliance requirements** for PII, copyright, and jurisdictional law
- **Schema drift** from websites that change structure without notice

This course progresses from **foundational networking** → **single-machine scraping** → **distributed crawling** → **production data pipelines** → **AI-powered adaptive extraction**, with each module building a complete mental model connecting protocol-level details to fleet-level architecture.

---

## 2. Target Audience & Prerequisites

### Target Audience
- AI Systems Engineers building training data pipelines for LLMs
- ML Infrastructure Engineers collecting evaluation datasets and benchmark data
- MLOps Engineers creating data ingestion pipelines for model monitoring
- Distributed Systems Engineers designing large-scale crawling infrastructure
- Backend Engineers transitioning to data engineering and web data systems
- Staff-level candidates preparing for data infrastructure and scraping architecture interviews

### Prerequisites
- **Solid Python**: async/await, generators, decorators, context managers, type hints
- **Computer Networks**: TCP/IP, HTTP, DNS, TLS basics
- **Data Structures**: queues, hash tables, bloom filters, tries
- **Linux**: process management, networking tools (curl, tcpdump, wireshark basics)
- **Databases**: SQL, NoSQL basics, Redis fundamentals
- **Docker & Kubernetes**: containerization, orchestration basics

---

## 3. Learning Objectives & Outcomes

By the end of this course, you will be able to:

1. **Architect** distributed crawling systems handling 1M+ requests/day with fault tolerance and politeness
2. **Reverse-engineer** JavaScript-rendered sites and hidden APIs to extract structured data
3. **Bypass** modern anti-bot systems using TLS fingerprint spoofing, browser stealth, and behavioral simulation
4. **Design** data validation pipelines with Pydantic/Cerberus that catch schema drift and data quality issues
5. **Build** production ETL pipelines that transform raw HTML into ML-ready datasets
6. **Navigate** the legal landscape of web scraping: CFAA, GDPR, robots.txt, terms of service
7. **Implement** real-time data collection from WebSockets, SSE, and streaming APIs
8. **Optimize** crawling infrastructure for cost, latency, and throughput using proxy rotation and caching
9. **Monitor** distributed crawling fleets with metrics, logging, and alerting
10. **Leverage** AI/LLM tools for adaptive extraction, selector generation, and schema inference

---

## Module 0: Mathematical & Computational Foundations

### 0.1 Graph Theory for Web Crawling
- **Directed graphs**: the web as a graph, pages as nodes, links as edges
- **Breadth-First Search (BFS)**: level-order crawling, frontier management
- **Depth-First Search (DFS)**: deep-link exploration, recursion limits
- **PageRank**: eigenvector centrality, iterative computation, damping factor
- **Crawl prioritization**: OPIC (Online Page Importance Computation), link-based ranking
- **Graph traversal complexity**: O(V + E) for BFS/DFS, space complexity of frontier

### 0.2 Set Theory & Probabilistic Data Structures
- **Bloom filters**: false positive probability, optimal hash count, bit array sizing
  - `m = -n * ln(p) / (ln(2)^2)`, `k = m/n * ln(2)`
  - Application: URL deduplication at scale without storing all URLs
- **Count-Min Sketch**: frequency estimation, heavy hitter detection
- **HyperLogLog**: cardinality estimation, unique URL counting
- **Cuckoo filters**: deletion support, better cache locality than bloom filters

### 0.3 Probability & Queueing Theory
- **Poisson processes**: request arrival modeling
- **Exponential distributions**: inter-arrival times, service times
- **M/M/1 queues**: single-server queue, utilization, average wait time
- **Little's Law**: `L = λW` — relating queue length, arrival rate, and wait time
- **Backpressure**: when downstream can't keep up, propagating pressure upstream
- **Application**: crawl rate limiting, politeness scheduling, worker pool sizing

### 0.4 Information Theory for Data Deduplication
- **Shannon entropy**: measuring information content of web pages
- **SimHash**: locality-sensitive hashing for near-duplicate detection
  - Hamming distance threshold for similarity
  - Application: detecting duplicate content, boilerplate removal
- **MinHash**: Jaccard similarity estimation for document comparison
- **TF-IDF**: term frequency-inverse document frequency for content relevance

### 0.5 Complexity Analysis for Crawling
- **Time complexity**: O(n) for n pages, O(d) for depth-limited crawling
- **Space complexity**: frontier storage, visited set, page content cache
- **Amortized analysis**: batch processing, incremental deduplication
- **Network latency dominates**: I/O-bound, not CPU-bound, async architecture necessity

### 0.6 Reading
- *Introduction to Algorithms* — Cormen et al., Ch. 22 (Graphs), Ch. 11 (Hash Tables)
- *Probability and Computing* — Mitzenmacher & Upfal, Ch. 4 (Probabilistic Data Structures)
- *Mining of Massive Datasets* — Leskovec, Rajaraman, Ullman, Ch. 3 (Similarity), Ch. 5 (PageRank)

---

## Module 1: The Web as a Data Source — HTTP, DOM, and the Modern Web Platform

### 1.1 HTTP Deep Dive
- **HTTP/1.1**: persistent connections, pipelining, chunked transfer encoding
- **HTTP/2**: multiplexing, server push, header compression (HPACK), stream prioritization
- **HTTP/3**: QUIC over UDP, 0-RTT, connection migration, no head-of-line blocking
- **Request/response anatomy**: methods, headers, status codes, content negotiation
- **Cookies & sessions**: `Set-Cookie`, `Cookie`, `SameSite`, `Secure`, `HttpOnly`
- **Caching**: `Cache-Control`, `ETag`, `Last-Modified`, conditional requests
- **Compression**: `gzip`, `brotli`, `deflate` — negotiation and decompression

### 1.2 TLS/SSL & HTTPS
- **TLS handshake**: ClientHello → ServerHello → Certificate → Key Exchange → Finished
- **TLS 1.3**: 1-RTT handshake, 0-RTT resumption, forward secrecy
- **Certificate validation**: chain of trust, OCSP stapling, SNI (Server Name Indication)
- **Cipher suites**: key exchange, authentication, encryption, MAC algorithms
- **Application-Layer Protocol Negotiation (ALPN)**: HTTP/2 vs HTTP/1.1 negotiation

### 1.3 The Document Object Model (DOM)
- **DOM tree structure**: nodes, elements, attributes, text nodes
- **HTML parsing**: tokenization, tree construction, error handling (HTML5 spec)
- **CSS selectors**: element, class, ID, descendant, child, sibling, attribute, pseudo-class
- **XPath**: axes (ancestor, descendant, following, preceding), predicates, functions
- **Shadow DOM**: encapsulated DOM trees, piercing shadow roots
- **Dynamic DOM**: JavaScript mutations, MutationObserver, DOM diffing

### 1.4 The Modern Web Platform
- **Single Page Applications (SPAs)**: client-side routing, virtual DOM, hydration
- **Progressive Web Apps (PWAs)**: service workers, offline capability, manifest
- **Web APIs**: Fetch API, WebSocket, Server-Sent Events, WebRTC, Web Workers
- **Authentication**: OAuth 2.0, JWT, session cookies, API keys
- **Rate limiting**: `X-RateLimit-*` headers, 429 responses, retry-after

### 1.5 robots.txt & Crawl Politeness
- **Robots Exclusion Protocol**: `User-agent`, `Disallow`, `Allow`, `Crawl-delay`, `Sitemap`
- **Parsing robots.txt**: `robotparser` module, caching, TTL
- **Politeness policies**: request rate, crawl delay, respecting `Disallow`
- **Sitemap.xml**: URL discovery, `lastmod`, `changefreq`, `priority`
- **Ethical considerations**: bandwidth consumption, server load, legal boundaries

### 1.6 Lab: Build a Protocol Analyzer
- Use `curl` with verbose mode to inspect full HTTP/2 request/response cycles
- Capture TLS handshakes with `openssl s_client` and Wireshark
- Parse robots.txt and sitemap.xml for major websites
- Measure TTFB, TLS handshake time, and content download time

---

## Module 2: Scrapy Architecture — The Production Crawling Engine

### 2.1 Scrapy Component Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                         Scrapy Engine                            │
│  ┌─────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐  │
│  │ Spider  │───▶│ Scheduler│───▶│Downloader│───▶│  Spider  │  │
│  │         │    │ (Queue)  │    │ (HTTP)   │    │ (Parse)  │  │
│  └─────────┘    └──────────┘    └──────────┘    └──────────┘  │
│       ▲              ▲               ▲               ▲         │
│       │              │               │               │         │
│  ┌────┴────┐    ┌───┴────┐     ┌────┴────┐     ┌───┴────┐    │
│  │Spider   │    │Dupe    │     │Downloader│     │Spider  │    │
│  │Middleware│    │Filter  │     │Middleware│     │Middleware│   │
│  └─────────┘    └────────┘     └─────────┘     └─────────┘   │
│                                                                │
│  ┌──────────────────────────────────────────────────────────┐ │
│  │              Item Pipeline (Process & Store)              │ │
│  └──────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────────┘
```

### 2.2 The Scrapy Engine
- **Execution engine**: coordinates all components, manages data flow
- **Twisted reactor**: async event loop, deferreds, callbacks, errbacks
- **Crawler API**: `CrawlerProcess`, `CrawlerRunner`, signals (`engine_started`, `spider_opened`)
- **Settings system**: priority levels, overrides, project settings, command-line options

### 2.3 The Scheduler
- **Request queue**: priority queue implementation, disk-based vs memory-based
- **Duplication filter**: `RFPDupeFilter`, fingerprinting requests, bloom filter integration
- **Priority management**: `priority` field, negative priorities for depth-first
- **Middleware integration**: `process_request`, `process_response`, `process_exception`

### 2.4 The Downloader
- **Async HTTP client**: Twisted `Agent`, connection pooling, persistent connections
- **DNS caching**: `CACHED_DNS_TIMEOUT`, TTL-based caching
- **Retry middleware**: `RETRY_TIMES`, `RETRY_HTTP_CODES`, exponential backoff
- **Timeout handling**: `DOWNLOAD_TIMEOUT`, connect timeout, read timeout
- **Concurrent requests**: `CONCURRENT_REQUESTS`, per-domain limits

### 2.5 Spiders
- **Spider base class**: `start_requests`, `parse`, `closed`
- **CrawlSpider**: `Rule`, `LinkExtractor`, callback chaining
- **SitemapSpider**: sitemap-based crawling, `sitemap_urls`, `sitemap_rules`
- **XMLFeedSpider / CSVFeedSpider**: structured feed parsing
- **Custom spiders**: overriding `__init__`, dynamic start URLs, parameterized crawling

### 2.6 Item Pipelines
- **Pipeline architecture**: sequential processing, `process_item`, `open_spider`, `close_spider`
- **Built-in pipelines**: `FilesPipeline`, `ImagesPipeline`, media download
- **Custom pipelines**: validation, cleaning, deduplication, storage
- **Pipeline ordering**: `ITEM_PIPELINES` setting, priority values

### 2.7 Middleware Deep Dive
- **Downloader middlewares**: `process_request`, `process_response`, `process_exception`
  - Built-in: `UserAgentMiddleware`, `RetryMiddleware`, `RedirectMiddleware`, `HttpAuthMiddleware`
  - Custom: proxy rotation, header injection, response modification
- **Spider middlewares**: `process_spider_input`, `process_spider_output`, `process_spider_exception`
  - Built-in: `DepthMiddleware`, `RefererMiddleware`, `UrlLengthMiddleware`
  - Custom: item enrichment, request filtering

### 2.8 Signals & Extensions
- **Signal system**: `engine_started`, `spider_opened`, `item_scraped`, `request_dropped`
- **Extension API**: `from_crawler`, `spider_opened`, `spider_closed`
- **Built-in extensions**: `CoreStats`, `TelnetConsole`, `MemoryUsage`, `LogStats`
- **Custom extensions**: metrics collection, monitoring, alerting

### 2.9 Lab: Build a Production Scrapy Project
- Create a spider with custom middleware for proxy rotation
- Implement an item pipeline with Pydantic validation
- Add custom extensions for metrics collection
- Configure logging, stats, and telnet console
- Deploy with `scrapyd` or Docker

---

## Module 3: HTML Parsing & Data Extraction

### 3.1 Parsing Libraries Comparison

| Library | Speed | Memory | CSS Selectors | XPath | JavaScript | Best For |
|---------|-------|--------|---------------|-------|------------|----------|
| **BeautifulSoup** | Slow | High | Limited | No | No | Quick prototypes, small scale |
| **lxml** | Fast | Medium | Yes | Yes | No | Production parsing, large docs |
| **parsel** | Fast | Low | Yes | Yes | No | Scrapy integration, streaming |
| **html5lib** | Slow | High | No | No | No | Standards-compliant parsing |
| **selectolax** | Very Fast | Low | Limited | No | No | High-performance extraction |
| **Playwright** | Slow | Very High | Yes | Yes | Yes | Dynamic content, full browser |

### 3.2 CSS Selectors
- **Basic selectors**: `tag`, `.class`, `#id`, `[attr]`, `[attr=value]`
- **Combinators**: `descendant`, `> child`, `+ adjacent`, `~ general sibling`
- **Pseudo-classes**: `:nth-child()`, `:first-child`, `:last-child`, `:not()`, `:contains()`
- **Pseudo-elements**: `::text`, `::attr(href)` (Scrapy-specific)
- **Selector specificity**: calculating priority, avoiding conflicts

### 3.3 XPath
- **Axes**: `ancestor`, `descendant`, `following`, `preceding`, `self`, `parent`, `child`
- **Predicates**: `[position()=1]`, `[contains(@class, 'foo')]`, `[text()='bar']`
- **Functions**: `text()`, `normalize-space()`, `string()`, `count()`, `sum()`
- **Namespaces**: handling XML namespaces, prefix registration
- **Scrapy extensions**: `extract()`, `extract_first()`, `get()`, `getall()`, `re()`, `re_first()`

### 3.4 Advanced Extraction Patterns
- **Nested data**: extracting hierarchical structures, recursive parsing
- **Table extraction**: row/column iteration, header mapping, colspan/rowspan handling
- **JSON-LD**: structured data extraction, schema.org parsing
- **Microdata**: itemscope, itemtype, itemprop extraction
- **Open Graph**: `og:title`, `og:description`, `og:image` meta tags
- **Schema.org**: rich snippets, structured data validation

### 3.5 Data Cleaning & Normalization
- **Text normalization**: whitespace stripping, Unicode normalization (NFC, NFD)
- **HTML entity decoding**: `&amp;`, `&lt;`, `&gt;`, numeric entities
- **URL normalization**: resolving relative URLs, canonicalization, query parameter sorting
- **Date parsing**: `dateutil`, `arrow`, ISO 8601, locale-specific formats
- **Number parsing**: locale-aware decimal separators, currency symbols, unit conversion

### 3.6 Lab: Build an Extraction Engine
- Parse 1000 pages from a complex e-commerce site
- Extract product data (name, price, description, images, reviews)
- Handle pagination, variants, and out-of-stock states
- Compare BeautifulSoup vs lxml vs parsel performance
- Implement fallback selectors for robustness

---

## Module 4: Dynamic Content & JavaScript-Rendered Pages

### 4.1 When Static Scraping Fails
- **Client-side rendering**: React, Vue, Angular — empty initial HTML
- **Lazy loading**: infinite scroll, pagination via AJAX
- **Authentication gates**: login-required content, session management
- **Anti-scraping**: JavaScript challenges, dynamic content generation

### 4.2 Headless Browser Architecture
- **Browser automation**: CDP (Chrome DevTools Protocol), WebDriver, Playwright protocol
- **Process model**: browser process, renderer process, GPU process, network service
- **Resource overhead**: memory per page, CPU for rendering, startup latency
- **Lifecycle management**: launching, context creation, page navigation, cleanup

### 4.3 Playwright for Scraping
- **Browser types**: Chromium, Firefox, WebKit
- **Context isolation**: incognito contexts, persistent contexts, state separation
- **Page operations**: `goto`, `wait_for_selector`, `evaluate`, `screenshot`, `pdf`
- **Network interception**: `route`, `fulfill`, `abort`, `continue`
- **Authentication**: `http_credentials`, `storage_state`, cookie management
- **Mobile emulation**: viewport, user agent, device scale factor, touch events

### 4.4 Scrapy + Playwright Integration
- **scrapy-playwright**: download handler, page creation, response handling
- **Configuration**: `PLAYWRIGHT_BROWSER_TYPE`, `PLAYWRIGHT_LAUNCH_OPTIONS`, `PLAYWRIGHT_CONTEXTS`
- **Page methods**: `page_method` meta key for custom Playwright actions
- **Screenshot capture**: `page.screenshot()` for debugging and verification
- **JavaScript execution**: `page.evaluate()` for custom extraction logic

### 4.5 API Reverse Engineering
- **Network tab analysis**: XHR/Fetch requests, WebSocket traffic, GraphQL queries
- **Mobile app interception**: HTTP Toolkit, mitmproxy, Frida for SSL pinning bypass
- **Authentication token extraction**: JWT parsing, session cookie analysis
- **GraphQL introspection**: schema discovery, query construction
- **HMAC/API signature reverse engineering**: parameter ordering, secret extraction

### 4.6 Lab: Scrape a Modern SPA
- Use Playwright to render a React-based e-commerce site
- Intercept and reverse-engineer the site's internal API
- Extract data both via DOM parsing and API calls
- Compare performance: static HTTP vs headless browser vs API direct
- Implement session management and authentication

---

## Module 5: Anti-Bot Evasion & Browser Fingerprinting

### 5.1 The Five Layers of Modern Bot Detection

Modern anti-bot systems operate across five stacked detection layers. Missing any layer results in detection and blocking.

| Layer | What It Checks | Key Signals | Bypass Strategy |
|-------|---------------|-------------|-----------------|
| **1. IP Reputation** | ASN type, abuse history, datacenter range | IP geolocation, ASN, proxy detection | Residential/mobile proxies, IP rotation |
| **2. TLS Fingerprinting** | JA3/JA4 hash, cipher suites, extensions | ClientHello parameters, HTTP/2 SETTINGS | `curl_cffi`, `tls-client`, real browsers |
| **3. Browser Fingerprint** | Canvas, WebGL, AudioContext, fonts | GPU renderer, canvas hash, audio fingerprint | Camoufox, stealth patches, real hardware |
| **4. Behavioral Analysis** | Mouse curves, scroll entropy, timing | Trajectory physics, click distributions, cadence | Gaussian jitter, human-like delays, Botasaurus |
| **5. Active Challenges** | CAPTCHA, JavaScript puzzles, Turnstile | Challenge completion, proof-of-work | Solving services, challenge bypass |

### 5.2 TLS Fingerprinting (JA3/JA4)
- **JA3**: MD5 hash of TLS version, cipher suites, extensions, elliptic curves, EC point formats
- **JA4**: Next-generation fingerprint, sorts extensions to defeat randomization, includes ALPN and signature algorithms
- **JA4+ suite**: JA4 (client), JA4S (server), JA4H (HTTP), JA4X (X509), JA4SSH (SSH)
- **Detection**: Cloudflare, Akamai, AWS WAF, VirusTotal, NetWitness all use JA4+ in 2026
- **Bypass tools**: `curl_cffi` (impersonate Chrome/Firefox), `tls-client` (Go), `uTLS` (custom ClientHello)

```python
# curl_cffi — TLS impersonation
from curl_cffi import requests

response = requests.get(
    "https://target-site.com",
    impersonate="chrome131"  # Exact Chrome 131 TLS fingerprint
)
```

### 5.3 Browser Fingerprint Evasion
- **Headless detection**: `navigator.webdriver`, `HeadlessChrome` in UA, missing plugins
- **Canvas fingerprinting**: noise injection, consistent hashing, GPU renderer spoofing
- **WebGL fingerprinting**: renderer string, vendor, parameter consistency
- **AudioContext fingerprinting**: compressor node output, hardware-dependent timing
- **Font enumeration**: installed font list, OS-specific fonts
- **Screen properties**: resolution, color depth, pixel ratio, touch support

### 5.4 Behavioral Analysis Evasion
- **Mouse movement**: Gaussian curves, Bezier paths, jitter, micro-corrections
- **Scroll behavior**: variable velocity, inertia simulation, random pauses
- **Typing cadence**: variable inter-keystroke delays, typo simulation, backspacing
- **Interaction timing**: human reaction times (200-400ms), random delays between actions
- **Session warming**: homepage visit → dwell → scroll → navigate to target

### 5.5 Proxy Architecture
- **Proxy types**: datacenter, residential, ISP, mobile (4G/5G)
- **Rotation strategies**: per-request, per-session, per-domain, adaptive
- **IP quality metrics**: reputation score, blacklist status, ASN diversity
- **Geolocation alignment**: matching IP timezone, locale, WebRTC to proxy location
- **Session persistence**: sticky sessions for trust accumulation (Akamai, DataDome)

### 5.6 CAPTCHA & Challenge Handling
- **reCAPTCHA v2/v3**: score-based, invisible challenges, enterprise version
- **hCaptcha**: image labeling, checkbox, invisible
- **Cloudflare Turnstile**: invisible challenge, managed challenge
- **Akamai sensor.js**: 512KB obfuscated fingerprinting script, 60+ extension probes
- **Solving services**: 2captcha, Anti-Captcha, CapSolver — API integration, cost analysis

### 5.7 Lab: Bypass a Protected Site
- Identify the anti-bot vendor (Wappalyzer, cookie names, response headers)
- Implement TLS fingerprint spoofing with curl_cffi
- Add browser stealth with Playwright + stealth patches
- Simulate human behavior with Gaussian mouse curves
- Use residential proxies with session persistence
- Measure success rate and cost per successful request

---

## Module 6: Distributed Crawling Architecture

### 6.1 The RESILIENT Scraping Model

For production-scale scraping (1M+ requests/day), follow the RESILIENT framework:

1. **R**otate Everything: IPs, User-Agents, headers, request patterns, fingerprints
2. **E**rror Budgeting: Accept 1-3% failure rate, build retry with exponential backoff
3. **S**tateless Workers: Crash → no data loss, worker is disposable
4. **I**solate Parsing: Fetch raw HTML first, parse later — don't let regex errors stop network requests
5. **L**atency Monitoring: Auto-slowdown if target responds slowly
6. **I**ntelligent Throttling: Respect robots.txt, watch for 429, react instantly
7. **E**ncapsulate Session Logic: Cookies/session state localized per worker
8. **N**ormalize Early: Convert to structured schema immediately after parsing
9. **T**elemetry: Dashboard for success/failure rates, or you're flying blind

### 6.2 Decoupled Micro-Worker Architecture

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│  URL Frontier   │────▶│  Message Queue  │────▶│  Worker Pool    │
│  (Seed URLs)    │     │  (Redis/RabbitMQ│     │  (Celery/K8s)   │
└─────────────────┘     └─────────────────┘     └─────────────────┘
                                                        │
                                                        ▼
                                              ┌─────────────────┐
                                              │  Raw Storage    │
                                              │  (S3/MinIO)     │
                                              └─────────────────┘
                                                        │
                                                        ▼
                                              ┌─────────────────┐
                                              │  Parser Workers │
                                              │  (ETL Pipeline) │
                                              └─────────────────┘
                                                        │
                                                        ▼
                                              ┌─────────────────┐
                                              │  Data Warehouse │
                                              │  (Postgres/CH)  │
                                              └─────────────────┘
```

### 6.3 Message Queue Design
- **Redis**: simple, fast, in-memory, pub/sub, lists for queues
- **RabbitMQ**: AMQP, routing, exchanges, durable queues, priority support
- **Apache Kafka**: distributed log, high throughput, replay capability, consumer groups
- **Queue routing**: segregate by priority, domain, or job type to prevent noisy neighbors
- **Backpressure**: monitor queue depth, scale workers, or throttle producers

### 6.4 Scrapy-Redis for Distributed Crawling
- **Shared scheduler**: Redis-backed request queue, all workers pull from same queue
- **Duplication filter**: Redis-backed bloom filter or set for URL deduplication
- **Item pipeline**: Redis queue for scraped items, separate processing workers
- **Crawl resumption**: queue persists across restarts, resume from last state
- **Scaling**: add workers dynamically, auto-scaling based on queue depth

### 6.5 Celery + Redis Architecture
- **Task definition**: `@app.task`, `delay()`, `apply_async()`
- **Worker pools**: prefork, eventlet, gevent, solo — choose based on workload
- **Task routing**: `task_routes` for queue segregation, priority queues
- **Rate limiting**: `rate_limit` per task, distributed token bucket with Redis
- **Result backend**: avoid storing large payloads in Redis, stream to S3 instead
- **Monitoring**: Flower for real-time worker monitoring, queue depths, retry rates

### 6.6 Kubernetes Deployment
- **Containerization**: Docker images for scrapers, minimal base images
- **Deployment patterns**: Deployment for long-running, CronJob for scheduled, Job for one-off
- **Resource management**: CPU/memory limits, HPA for auto-scaling
- **Config management**: ConfigMaps for settings, Secrets for API keys and proxies
- **Service mesh**: Istio/Linkerd for traffic management, observability

### 6.7 Lab: Build a Million-Request Crawler
- Deploy Scrapy-Redis with 3+ worker nodes
- Implement Celery task routing for priority jobs
- Add distributed rate limiting with Redis token bucket
- Monitor with Flower, Prometheus, and Grafana
- Measure throughput, success rate, and cost per 1M requests

---

## Module 7: Data Quality, Validation & Schema Enforcement

### 7.1 The Data Quality Problem

Web data is inherently messy:
- Missing fields due to dynamic loading or site changes
- Inconsistent formats (dates, numbers, currencies)
- HTML entities and encoding issues
- Duplicate records from pagination overlap
- Silent failures where scrapers return empty but don't crash
- Schema drift when websites redesign

### 7.2 Pydantic for Schema Validation

```python
from pydantic import BaseModel, field_validator, HttpUrl
from typing import Optional
import re

class Product(BaseModel):
    title: str
    price: float
    currency: str = "USD"
    in_stock: bool
    url: HttpUrl
    
    @field_validator('price', mode='before')
    @classmethod
    def clean_price(cls, v):
        if isinstance(v, (float, int)):
            return v
        cleaned = re.sub(r'[^\d.]', '', str(v))
        return float(cleaned)
    
    @field_validator('in_stock', mode='before')
    @classmethod
    def parse_availability(cls, v):
        if isinstance(v, bool):
            return v
        return v.lower() in ['in stock', 'available', 'buy now']
```

- **Type enforcement**: automatic coercion, strict mode
- **Custom validators**: `@field_validator`, `@model_validator`
- **Nested models**: complex hierarchical data structures
- **Serialization**: `model_dump()`, `model_dump_json()`, ORM mode
- **Error handling**: `ValidationError`, detailed error messages

### 7.3 Cerberus for Flexible Validation
- **Schema definition**: type, required, allowed, min/max, regex
- **Normalization**: coercion, default values, renaming
- **Custom validators**: Python functions for complex rules
- **Validation levels**: soft (warnings) vs hard (errors)

### 7.4 Data Quality Metrics

| Metric | Definition | Target |
|--------|-----------|--------|
| **Completeness** | % of required fields present | > 99% |
| **Accuracy** | % of values matching ground truth | > 95% |
| **Consistency** | % of records with valid cross-field relationships | > 98% |
| **Timeliness** | Age of data at ingestion | < 24 hours |
| **Uniqueness** | % of non-duplicate records | > 99.5% |
| **Validity** | % of records passing schema validation | > 99% |

### 7.5 Anomaly Detection
- **Statistical methods**: Z-score, IQR, moving averages for numeric fields
- **Rule-based**: threshold checks, range validation, pattern matching
- **ML-based**: Isolation Forest, LOF for detecting unusual records
- **Time-series monitoring**: tracking data volume, success rates, field distributions over time

### 7.6 Schema Drift Detection
- **Baseline establishment**: historical schema fingerprint
- **Change detection**: new fields, missing fields, type changes
- **Alerting**: notify when schema drift exceeds threshold
- **Adaptive parsing**: fallback selectors, multiple extraction strategies

### 7.7 Lab: Build a Data Quality Pipeline
- Define Pydantic schemas for e-commerce product data
- Implement validation in Scrapy item pipeline
- Add anomaly detection for price outliers and missing images
- Create schema drift monitoring with alerting
- Generate data quality dashboard

---

## Module 8: Data Pipelines & ETL for Scraped Data

### 8.1 ETL Architecture for Web Data

```
Raw HTML ──▶ Extract ──▶ Transform ──▶ Validate ──▶ Load ──▶ Warehouse
   │            │            │           │          │
   │            │            │           │          ▼
   │            │            │           │     ┌─────────────┐
   │            │            │           │     │ Data Lake   │
   │            │            │           │     │ (S3/MinIO)  │
   │            │            │           │     └─────────────┘
   │            │            │           │
   ▼            ▼            ▼           ▼          ▼
┌──────┐   ┌────────┐   ┌────────┐  ┌────────┐  ┌──────────┐
│Queue │   │Parser  │   │Cleaner │  │Validator│  │Database  │
│(Kafka│   │(Scrapy│   │(Pandas│  │(Pydantic│  │(Postgres/ │
│/Redis│   │/Celery│   │/Polars)│  │/Cerberus)│  │ClickHouse│
└──────┘   └────────┘   └────────┘  └────────┘  └──────────┘
```

### 8.2 Extract Phase
- **Raw storage**: S3/MinIO for HTML archives, versioning, lifecycle policies
- **Metadata tracking**: crawl timestamp, URL, proxy used, success/failure
- **Incremental extraction**: checkpointing, resume capability, change detection
- **Parallel extraction**: chunked processing, worker pools

### 8.3 Transform Phase
- **HTML parsing**: selector-based extraction, template matching
- **Data cleaning**: null handling, outlier removal, format normalization
- **Enrichment**: geocoding, category mapping, sentiment analysis
- **Aggregation**: rolling windows, grouping, summarization
- **Deduplication**: SimHash, MinHash, exact matching

### 8.4 Validation Phase
- **Schema validation**: Pydantic/Cerberus enforcement
- **Business rules**: cross-field validation, referential integrity
- **Statistical validation**: distribution checks, anomaly flagging
- **Sampling**: random spot checks, manual verification

### 8.5 Load Phase
- **Batch loading**: COPY commands, bulk inserts, transaction management
- **Streaming loading**: Kafka Connect, Debezium, CDC
- **Data formats**: Parquet, Avro, JSONL, CSV
- **Partitioning**: time-based, hash-based, range-based
- **Indexing**: primary keys, foreign keys, search indexes

### 8.6 Apache Kafka + Flink for Streaming ETL
- **Kafka topics**: raw-pages, parsed-items, validated-items, errors
- **Flink jobs**: stream processing, windowing, stateful computations
- **Exactly-once semantics**: checkpointing, transactional writes
- **Schema registry**: Avro/Protobuf schema evolution, compatibility

### 8.7 Lab: Build an End-to-End ETL Pipeline
- Scrape 10k product pages, store raw HTML in S3
- Parse with Scrapy, transform with Pydantic
- Load into ClickHouse for analytics
- Add Kafka streaming for real-time updates
- Monitor data quality metrics

---

## Module 9: Legal, Ethical & Compliance Framework

### 9.1 Legal Landscape
- **CFAA (Computer Fraud and Abuse Act)**: unauthorized access, bypassing barriers
- **Copyright law**: facts vs creative works, transformative use, fair use
- **Contract law**: terms of service, clickwrap vs browsewrap agreements
- **Trespass to chattels**: server resource consumption, economic harm
- **Key cases**: hiQ v. LinkedIn (2019), Craigslist v. 3Taps, Facebook v. Power Ventures

### 9.2 Privacy Regulations
- **GDPR (EU)**: lawful basis, legitimate interest, data minimization, right to erasure
- **CCPA/CPRA (California)**: consumer rights, opt-out, sale of personal information
- **PII handling**: detection, redaction, anonymization, pseudonymization
- **Consent management**: explicit consent for personal data collection

### 9.3 robots.txt & Technical Compliance
- **Robots Exclusion Protocol**: voluntary standard, not legally binding
- **Crawl-delay**: respecting rate limits, avoiding server strain
- **Disallow directives**: honoring restricted paths
- **Sitemap compliance**: using provided sitemaps for discovery

### 9.4 Ethical Scraping Principles
- **Transparency**: clear user-agent, contact information, purpose disclosure
- **Minimal impact**: rate limiting, off-peak crawling, bandwidth consideration
- **Data minimization**: collect only what's needed, delete when done
- **Attribution**: crediting sources, respecting intellectual property
- **No harm**: avoiding DDoS-like behavior, respecting business models

### 9.5 Compliance Checklist

| Checklist Item | Assessment Question | Action/Mitigation |
|---------------|---------------------|-------------------|
| Authentication Gate | Data behind login? | Stop — CFAA risk |
| PII Content | Names, emails, photos? | Avoid or consult privacy expert |
| Copyright | Creative works or facts? | Focus on facts, transformative use |
| Terms of Service | Explicit scraping ban? | Assess breach of contract risk |
| robots.txt | Disallow on target URLs? | Honor all Disallow rules |
| Scraping Rate | Aggressive or polite? | Rate limits, random delays |
| Data Usage | Internal or republication? | Internal = lowest risk |
| Data Value | Worth the legal risk? | Document business case |

### 9.6 Lab: Conduct a Legal Risk Assessment
- Analyze a target website's robots.txt, ToS, and technical barriers
- Document legal risk factors and mitigation strategies
- Create a compliance policy document
- Implement technical controls (rate limiting, PII detection)

---

## Module 10: Real-Time Streaming Data Collection

### 10.1 Streaming Protocols
- **WebSocket**: full-duplex, persistent connection, binary frames
- **Server-Sent Events (SSE)**: unidirectional, HTTP-based, auto-reconnect
- **HTTP/2 Server Push**: server-initiated streams
- **gRPC Streaming**: bidirectional streaming, Protocol Buffers
- **MQTT**: lightweight pub/sub for IoT, QoS levels

### 10.2 WebSocket Scraping
- **Connection lifecycle**: handshake, frame exchange, close
- **Message framing**: text, binary, ping/pong, close frames
- **Authentication**: token in query param, cookie-based, custom headers
- **Reconnection**: exponential backoff, heartbeat, state recovery
- **Libraries**: `websockets` (Python), `ws` (Node.js), `aiohttp`

### 10.3 SSE Scraping
- **Event format**: `id:`, `event:`, `data:`, `retry:` fields
- **Auto-reconnect**: browser-native, `EventSource` API
- **Last-Event-ID**: resuming from disconnect
- **Libraries**: `sseclient`, `aiohttp-sse-client`

### 10.4 Real-Time Data Processing
- **Stream parsing**: JSON Lines, Protocol Buffers, Avro
- **Windowing**: tumbling, sliding, session windows
- **State management**: keyed state, operator state, checkpointing
- **Backpressure**: reactive streams, buffer sizing, dropping policies

### 10.5 Lab: Build a Real-Time Price Monitor
- Connect to a WebSocket API for live price updates
- Process and validate incoming data with Pydantic
- Store in time-series database (TimescaleDB, InfluxDB)
- Detect price anomalies and trigger alerts
- Implement reconnection and error recovery

---

## Module 11: API-First Data Collection & Reverse Engineering

### 11.1 API Discovery Techniques
- **Network tab analysis**: Chrome DevTools, Firefox Developer Tools
- **Mobile app interception**: HTTP Toolkit, mitmproxy, Charles Proxy
- **JavaScript deobfuscation**: beautification, debugging, breakpoint analysis
- **Documentation scraping**: OpenAPI/Swagger discovery, README parsing

### 11.2 Authentication Patterns
- **API Keys**: header-based, query param, custom header
- **OAuth 2.0**: authorization code, client credentials, implicit, PKCE
- **JWT**: structure (header.payload.signature), validation, refresh
- **Session Cookies**: `Set-Cookie`, `Cookie`, CSRF tokens
- **HMAC Signatures**: parameter ordering, timestamp, nonce, secret key

### 11.3 Rate Limit Handling
- **Strategies**: exponential backoff, token bucket, leaky bucket
- **Headers**: `X-RateLimit-Limit`, `X-RateLimit-Remaining`, `X-RateLimit-Reset`
- **429 handling**: retry-after parsing, jitter, circuit breaker
- **Distributed rate limiting**: Redis-based token bucket across workers

### 11.4 GraphQL Scraping
- **Introspection**: `__schema`, `__type` queries for schema discovery
- **Query construction**: fields, arguments, fragments, variables
- **Pagination**: cursor-based, offset-based, connection patterns
- **Batching**: multiple queries in single request, DataLoader pattern

### 11.5 Lab: Reverse-Engineer a Mobile App API
- Intercept mobile app traffic with mitmproxy
- Identify authentication mechanism and token refresh
- Map API endpoints and request/response schemas
- Build a Python client with rate limiting and error handling
- Compare API data vs HTML scraping for same content

---

## Module 12: AI-Powered Data Extraction & Adaptive Scraping

### 12.1 LLM-Based Extraction
- **Zero-shot extraction**: prompting LLMs with HTML to extract structured data
- **Few-shot learning**: providing examples for better accuracy
- **Schema-guided extraction**: enforcing output format with JSON schema
- **Cost analysis**: token pricing, cost per page, vs traditional scraping

### 12.2 AI-Generated Selectors
- **Selector generation**: LLM suggests CSS/XPath selectors from HTML sample
- **Self-healing scrapers**: auto-generating new selectors when old ones fail
- **Visual grounding**: identifying elements by description, not just selectors
- **Maintenance reduction**: AI adapts to site changes without manual intervention

### 12.3 Adaptive Crawling
- **Reinforcement learning**: RL agents for crawl policy optimization
- **Bandit algorithms**: multi-armed bandit for URL prioritization
- **Content classification**: ML models for page type detection (product, listing, detail)
- **Crawl budget optimization**: maximizing valuable pages within resource constraints

### 12.4 Computer Vision for Scraping
- **OCR**: Tesseract, EasyOCR for text in images
- **Object detection**: identifying UI elements, buttons, forms
- **Visual similarity**: detecting layout changes, template matching
- **CAPTCHA solving**: image classification, text recognition

### 12.5 Lab: Build an AI-Adaptive Scraper
- Use LLM to generate selectors from HTML samples
- Implement self-healing: detect selector failure, generate alternatives
- Compare accuracy and cost: AI extraction vs traditional scraping
- Add visual element detection for complex layouts

---

## Module 13: Production Operations — Monitoring, Alerting & Debugging

### 13.1 Metrics & Observability
- **Success rate**: 200 OK / total requests
- **Error rate**: 4xx, 5xx, timeout, DNS failure, SSL errors
- **Throughput**: requests/second, pages/minute
- **Latency**: TTFB, total response time, parsing time
- **Queue depth**: pending URLs, processing lag
- **Data quality**: validation pass rate, anomaly count

### 13.2 Logging Strategy
- **Structured logging**: JSON format, correlation IDs, context fields
- **Log levels**: DEBUG (selectors), INFO (requests), WARNING (retries), ERROR (failures)
- **Log aggregation**: ELK stack, Datadog, Splunk, CloudWatch
- **Sampling**: high-volume logging with representative sampling

### 13.3 Alerting
- **Threshold alerts**: success rate < 95%, queue depth > 10k, error rate > 5%
- **Anomaly alerts**: sudden drop in data volume, schema drift detected
- **Escalation**: PagerDuty, Opsgenie, Slack integration
- **Runbooks**: documented procedures for common alerts

### 13.4 Debugging Techniques
- **Request replay**: capturing and replaying failed requests
- **Screenshot capture**: Playwright screenshots on failure
- **HAR analysis**: HTTP Archive format for request/response inspection
- **Selector testing**: Scrapy shell, SelectorGadget, browser DevTools
- **Distributed tracing**: Jaeger, Zipkin for cross-service debugging

### 13.5 Lab: Build a Monitoring Dashboard
- Deploy Prometheus + Grafana for metrics collection
- Configure alerts for critical thresholds
- Implement structured logging with correlation IDs
- Add distributed tracing across crawl pipeline
- Create runbooks for common failure modes

---

## Module 14: Performance Engineering & Cost Optimization

### 14.1 Throughput Optimization
- **Connection pooling**: reuse TCP connections, HTTP/2 multiplexing
- **DNS caching**: reduce DNS lookup overhead
- **Parallelism**: async I/O, worker pools, concurrent requests
- **Batching**: bulk operations, batch inserts, batch API calls
- **Caching**: HTTP cache, CDN, local cache for repeated requests

### 14.2 Memory Optimization
- **Streaming parsing**: SAX-style parsing for large documents
- **Generator patterns**: yield items instead of building lists
- **Object pooling**: reuse browser instances, connection objects
- **Garbage collection tuning**: generation thresholds, manual collection

### 14.3 Cost Optimization
- **Proxy cost**: residential vs datacenter, usage-based vs subscription
- **Compute cost**: spot instances, auto-scaling, right-sizing
- **Storage cost**: tiered storage, lifecycle policies, compression
- **API cost**: rate limit optimization, caching, batching
- **Headless browser cost**: resource sharing, pool management, cleanup

### 14.4 Benchmarking
- **Load testing**: k6, Locust, JMeter for crawl endpoint testing
- **Profiling**: cProfile, py-spy, memory_profiler for bottleneck identification
- **A/B testing**: comparing extraction strategies, proxy providers
- **Cost per successful request**: total cost / successful extractions

### 14.5 Lab: Optimize a Crawler for Cost
- Profile current crawler for CPU/memory bottlenecks
- Implement connection pooling and DNS caching
- Compare proxy providers on cost/success rate
- Optimize storage with compression and lifecycle policies
- Target: reduce cost per 1M requests by 50%

---

## Capstone Project

### Project: Production-Scale AI Training Data Pipeline

Build a comprehensive data collection platform for gathering, validating, and preparing web data for LLM training:

**Requirements:**
1. **Multi-source crawling**: 5+ different website types (news, e-commerce, forums, documentation, social)
2. **Distributed architecture**: Scrapy-Redis with 10+ workers, Celery task queue
3. **Anti-bot evasion**: TLS fingerprint spoofing, browser stealth, proxy rotation
4. **Data quality**: Pydantic validation, anomaly detection, schema drift monitoring
5. **Real-time streaming**: Kafka + Flink for processing high-velocity data
6. **ETL pipeline**: Raw HTML → parsed → validated → normalized → Parquet in S3
7. **Compliance**: robots.txt respect, rate limiting, PII detection and redaction
8. **Monitoring**: Prometheus + Grafana dashboard, structured logging, alerting
9. **AI integration**: LLM-based selector generation, adaptive extraction
10. **Cost optimization**: < $0.001 per successful page extraction

**Architecture:**
- Scrapy + Playwright for crawling
- Redis for queue management and deduplication
- Celery for task distribution
- Kafka for streaming data
- Flink for real-time processing
- S3 for raw storage
- ClickHouse for analytics
- Pydantic for validation
- Prometheus/Grafana for monitoring

---

## Appendix A: Reading List & References

### Networking & Protocols
- *HTTP: The Definitive Guide* — David Gourley, Brian Totty
- *High Performance Browser Networking* — Ilya Grigorik
- *TLS Mastery* — Michael W. Lucas

### Web Scraping & Crawling
- *Web Scraping with Python* — Ryan Mitchell
- *Scrapy Documentation* — scrapy.org
- *Playwright Documentation* — playwright.dev

### Distributed Systems
- *Designing Data-Intensive Applications* — Martin Kleppmann
- *Building Microservices* — Sam Newman
- *Site Reliability Engineering* — Google

### Data Engineering
- *Fundamentals of Data Engineering* — Joe Reis, Matt Housley
- *Data Pipelines with Apache Airflow* — Bas Harenslak, Julian de Ruiter
- *Streaming Systems* — Tyler Akidau, Slava Chernyak, Reuven Lax

### Security & Evasion
- *The Art of Deception* — Kevin Mitnick
- *Browser Fingerprinting Research Papers* — various academic sources
- *JA4+ Specification* — FoxIO

---

## Appendix B: Tooling Matrix

### Core Scraping
| Tool | Type | Best For | Scale |
|------|------|----------|-------|
| **Scrapy** | Framework | Production crawling, large scale | 1M+ pages/day |
| **Requests** | Library | Simple HTTP, API calls | < 10k pages/day |
| **httpx** | Library | Async HTTP, HTTP/2 | < 100k pages/day |
| **aiohttp** | Library | Async scraping, WebSocket | < 100k pages/day |
| **Playwright** | Browser | Dynamic content, JS rendering | < 10k pages/day |
| **Selenium** | Browser | Legacy support, complex interactions | < 5k pages/day |

### Parsing
| Tool | Speed | CSS | XPath | Best For |
|------|-------|-----|-------|----------|
| **lxml** | Fast | Yes | Yes | Production parsing |
| **parsel** | Fast | Yes | Yes | Scrapy integration |
| **BeautifulSoup** | Slow | Limited | No | Quick prototypes |
| **selectolax** | Very Fast | Limited | No | High-performance |

### Distributed Systems
| Tool | Role | Best For |
|------|------|----------|
| **Redis** | Queue/Cache | Simple, fast, in-memory |
| **RabbitMQ** | Message Broker | Complex routing, AMQP |
| **Kafka** | Event Streaming | High throughput, replay |
| **Celery** | Task Queue | Async job distribution |
| **Kubernetes** | Orchestration | Container management |

### Data Quality
| Tool | Type | Best For |
|------|------|----------|
| **Pydantic** | Type-based | Strict validation, IDE support |
| **Cerberus** | Schema-based | Flexible, lightweight |
| **Great Expectations** | Data testing | Data pipeline validation |
| **Deequ** | Data quality | Spark-based, large scale |

### Anti-Bot
| Tool | Type | Best For |
|------|------|----------|
| **curl_cffi** | TLS spoofing | HTTP requests, API calls |
| **Camoufox** | Stealth browser | Maximum stealth |
| **scrapy-stealth** | Middleware | Scrapy integration |
| **Botasaurus** | Behavior | Mouse simulation |

---

## Appendix C: Interview Preparation

### System Design: Crawling Infrastructure
- Design a web crawler that handles 10M pages/day
- Design a real-time price monitoring system
- Design a distributed anti-bot evasion system
- Design a data quality pipeline for web data

### Deep Dives
- Explain Scrapy's architecture and data flow
- How does TLS fingerprinting work? How do you bypass it?
- Design a bloom filter for URL deduplication at scale
- How do you handle schema drift in production scrapers?
- Compare BFS vs DFS for web crawling with examples

### Coding Challenges
- Implement a bloom filter from scratch
- Build a rate limiter with token bucket algorithm
- Write a recursive web crawler with politeness
- Implement SimHash for near-duplicate detection
- Build a proxy rotation middleware for Scrapy

### Legal & Ethics
- When is web scraping legal vs illegal?
- How do you handle PII in scraped data under GDPR?
- What are the ethical considerations of training AI on scraped data?

---

## Course Timeline

| Phase | Duration | Modules | Focus |
|-------|----------|---------|-------|
| **Foundation** | 1 week | 0-1 | Networking, DOM, HTTP deep dive |
| **Core Scraping** | 2 weeks | 2-3 | Scrapy architecture, parsing, extraction |
| **Dynamic Content** | 1 week | 4-5 | Playwright, anti-bot, fingerprinting |
| **Distributed Systems** | 2 weeks | 6-7 | Scaling, data quality, validation |
| **Data Pipelines** | 2 weeks | 8-9 | ETL, compliance, legal framework |
| **Advanced Topics** | 2 weeks | 10-12 | Streaming, APIs, AI-powered extraction |
| **Production** | 1 week | 13-14 | Monitoring, performance, cost optimization |
| **Capstone** | 2 weeks | — | Production-scale pipeline |

**Total Duration: 13 weeks (3 months) full-time, or 6 months part-time**

---

*This syllabus treats web scraping as a systems engineering discipline. The tools evolve rapidly — anti-bot systems, browser technologies, and legal frameworks change constantly. Master the fundamentals of networking, distributed systems, and data engineering, and you can adapt to any technology stack or regulatory environment.*

---

Download this file: [web-scraping-data-collection-syllabus.md](sandbox:///mnt/agents/output/web-scraping-data-collection-syllabus.md)